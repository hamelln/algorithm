## 올바른 괄호의 갯수 (프로그래머스 문제 Lv 4)


### 문제 설명

![image](https://user-images.githubusercontent.com/39308313/142751499-6bc8826a-c782-48a6-9cc8-09579ff74fd7.png)

### 자료 구조

- **Molecular**
    - 타입 : 정수
    - 저장 데이터 : 분자로 쓸 변수
- **denominator**
    - 타입 : 정수
    - 저장 데이터 : 분모로 쓸 변수

### 풀이 과정
```txt
※ 3 x n 타일링 문제하고 비슷한 논리다.

1. 일반항의 규칙을 구해야 하니 초반 몇 가지 항을 구해본다.
f(1) = 1, f(2) = 2 , f(3) = 5, f(4) = 14...  

2. f(2)는 '()(), (())' 두 가지로 이뤄진다.
()()는 () + ()이므로 f(1)에서 괄호 한 쌍을 추가하면 만들 수 있다.
하지만 (())는 f(1)의 괄호 뒤에 추가하는 걸로는 만들 수 없는 경우다.
f(1) 옆에 추가하는 방식으로는 못 만드는, 괄호 2쌍을 순전히 채우는 경우를 g(2)라고 칭하겠다.

3. f(3) = f(1)에서 2쌍을 채우는 경우 + f(2)에서 1쌍을 채우는 경우 + g(3).
   f(4) = f(1)에서 3쌍을 채우는 경우 + f(2)에서 2쌍을 채우는 경우 + f(3)에서 한 쌍을 채우는 경우 + g(4)
   ...
   
   이를 다시 정리하면,
   f(3) = f(1)*g(2) + f(2)*g(1) + g(3)
   f(4) = f(1)*g(3) + f(2)*g(2) + f(3)*g(1) + g(4)
   f(5) = f(1)*g(4) + f(2)*g(3) + f(3)*g(2) + f(4)*g(1) + g(5)
   ...

5. 이제 g(n)의 규칙성을 찾자.
g(1) = 1, g(2) = 1, g(3) = 2, g(4) = 5, g(5) = 14...

∵예를 들어 g(3)는 ((())), (()())이고 g(4) = (()(())), (()()()), ((())()), (((()))), ((()()))이다.
공통점은 ( ) 안에 n-1쌍의 괄호를 정렬했다는 점이다. n-1쌍의 괄호를 만드는 방법의 가지 수는 f(n-1)이다. 
따라서 g(n) = f(n-1)이다.

6. 3의 식을 다시 정리하면 
f(n) = f(n-1)*f(1) + f(n-2)+f(2) + ... +  f(1)*f(n-1)
이는 아래 그림과 같이 정리된다.
```
![image](https://user-images.githubusercontent.com/39308313/142752168-ea7ba9b5-08e2-45c9-8585-96b67c3d251f.png)
![image](https://user-images.githubusercontent.com/39308313/142752208-0f7a990c-85fc-4f49-b0e0-142ad6794caa.png)

```txt

∴ 위 그림과 같이 코드를 구현하면 끝난다.

```

### 코드 구현

```javascript
function solution(n) {
	let Molecular = n + 1, denominator = n;
        
	for (let i = 1; i < n; i++) {
        Molecular *= n + 1 + i; 
        denominator *= n - i;
   }
	return Number(Molecular / denominator) / (n + 1);
}

```

[출처]<https://programmers.co.kr/learn/courses/30/lessons/12929>
