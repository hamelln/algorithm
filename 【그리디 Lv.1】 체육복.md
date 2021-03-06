## 체육복 (프로그래머스 문제 Lv 1)

### 문제 설명

![image](https://user-images.githubusercontent.com/39308313/144626552-cd1173fb-67cf-4561-9f7e-90dbc7e01145.png)

### 풀이 과정

```txt
예를 하나 보자.

체육복이 없는 학생 : [2,4]
여벌이 있는 학생 : [1,3]

'뒷번호'한테 먼저 체육복을 빌리려고 하면?
2번 학생은 3한테서 체육복을 빌릴 것이다.
그러면 4번 학생은 체육복을 못 빌린다.

그러니 차라리 '앞번호'한테 먼저 체육복을 빌리려고 시도하자.
```

### 코드 구현

```javascript
function solution(n, lost, reserve) {
<!-- lost와 reserve를 오름차순 정렬 & 중복하는 숫자를 제거한다.-->

	let _lost = lost
		.sort((a, b) => a - b)
		.filter(s => !reserve.includes(s));
	let _reserve = reserve
		.sort((a, b) => a - b)
		.filter(s => !lost.includes(s));

<!-- 
1. 앞자리 학생에게 빌릴 수 있는지 먼저 확인하고
2. 안 되면 뒷자리 학생에게 빌릴 수 있는지 확인한다.
3. 둘 다 안 되면 못 빌리는 것으로 처리.
-->

	_lost = _lost.filter((s) => {
		if (_reserve.includes(s-1)) {
			const front = _reserve.indexOf(s - 1);
			_reserve.splice(front, 1);
			return false;
		} else if (_reserve.includes(s+1)) {
			const back = _reserve.indexOf(s + 1);
			_reserve.splice(back, 1);
			return false;
		} 
        	return true;
	});
	return n - _lost.length;
}
```

[출처 : 프로그래머스 체육복](https://programmers.co.kr/learn/courses/30/lessons/42862?)
