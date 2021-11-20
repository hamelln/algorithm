## 2 x n 타일링 (프로그래머스 문제 Lv 3)


### 문제 설명

![image](https://user-images.githubusercontent.com/39308313/142726498-5976a420-7040-4b95-92c0-49b8bbcce578.png)

### 자료 구조

- **arr**
    - 타입 : 배열
    - 저장 데이터 : 피보나치 수열을 만들기 위한 변수
- **i**
    - 타입 : 정수
    - 저장 데이터 : arr 배열에 사용할 인덱스

### 풀이 과정

> 가로가 n인 바닥을 채우는 방법의 가지 수를 f(n)이라고 하자.  
> > f(1) = 1  
> > f(2) = 2  
> > >그런데, f(3)은 f(1)에서 두 칸을 채우는 방법 f(2)에서 한 칸을 채우는 방법이 전부다.  
> > >마찬가지로 f(4)는 f(2)에서 두 칸을 채우는 방법, f(3)에서 한 칸을 채우는 방법이 전부다. 타일의 길이가 2이기 때문이다.
> > >따라서 f(n) = f(n-2) + f(n-1)이다. 이는 피보나치 수다.


### 코드 구현

```javascript
function solution(n) {
    let arr = [1,2], i = 2;
    for (; i<n; i++) arr.push((arr[i-2] + arr[i-1])%1000000007);
    return arr[n-1];
}
```

[출처]<https://programmers.co.kr/learn/courses/30/lessons/12900>
