## 3진법 뒤집기(프로그래머스 문제 Lv 1)


### 문제 설명

![image](https://user-images.githubusercontent.com/39308313/142717596-c9404214-32cb-4c5b-9479-8b953f502dfe.png)

### 자료 구조

- **judge**
    - 타입 : 정수
    - 저장 데이터 : n을 나눌 3의 제곱수 중 가장 큰 수
- **answer**
    - 타입 : 정수
    - 저장 데이터 : 변환이 끝난 정수
- **gop**
    - 타입 : 정수
    - 저장 데이터 : n을 3으로 나눴을 때 발생하는 나머지 값


### 풀이 1

```txt

n = 45일 때의 예시

45 / 3 = 15...0
15 / 3 = 5...0
5 / 3 = 1...2
1 / 3 = 0...1

1. 45를 3진법으로 표현하면 1200
2. 문제에서 요구하는 건 1200을 거꾸로 해야하므로 0021
3. 3진법의 1200을 10진법으로 표현하면 7
4. 즉, n을 끝까지 나눴을 때의 나머지값만 구해서 계산하면 된다.
```

### 코드 구현

```javascript
function solution(n) {
    if (n<3) return n;
  let judge = 3;
  while (judge <= n) judge *= 3;
  judge /= 3;

  let answer = (judge == n)? 1 : (judge*2 ==n)? 2 : 0;
  if (answer != 0 ) return answer;
  
  let gop = n%3;
  while (n>2) {
    answer += gop*judge;
    judge /= 3;
    n = parseInt(n/3);
    gop = n%3;      
  }
  answer += n;
  return answer;
}
```

### 풀이 2

```txt
num.toString(x)는 숫자 num을 x진법으로 변환하는 기능이 있다.
parseInt(str,x)는 숫자형 문자열 str을 x진법으로 변환하는 기능이 있다.

1. n.toString(3)으로 n을 3진법화 및 문자열화한다. // 45 => "1200"
2. split("")으로 한 글자씩 분리시켜 배열화한다. // "1200" => ['1','2','0','0']
3. reverse()를 써서 거꾸로 정렬한다. // ['1','2','0','0'] => ['0','0','2','1']
4. join으로 배열 내용들을 다 합친다. // ['0','0','2','1'] => "0021"
5. parseInt(str,3)으로 다시 3진법화한다. "0021" => 7
```

```javascript
function solution(n) {
	return parseInt(n.toString(3).split("").reverse().join(""), 3);
}
```

[출처]<https://programmers.co.kr/learn/courses/30/lessons/68935>
