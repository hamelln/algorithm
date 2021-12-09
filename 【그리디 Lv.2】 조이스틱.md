## 조이스틱 (프로그래머스 문제 Lv 2)

### 문제 설명

![image](https://user-images.githubusercontent.com/39308313/145410074-c79c5eec-a46b-46a5-a5cb-79cf384b10d3.png)

### 풀이 과정

```txt

```

### 코드 구현

```javascript
function solution(name) {
	// "JAZ" => ['J','A','Z'] => [74, 65, 90] => [9,0,25] => [9,0,1]로 만듭니다.
	const parse = n => (n <= 78 ? n - 65 : 91 - n);
	name = name.split("").map(s => parse(s.charCodeAt(0)));
	const sum = name.reduce((a, b) => a + b + 1);

	let min = 0, count = 0, temp = 0;
	for (let i = 1; i < name.length; i++) {
		if (name[i] !== 0) {
			temp = (i-1) - count * 2;
			min = min > temp ? temp : min;
			count = 0;
		} else {
			count++;
		}
	}
	return min > 0 ? sum : sum + min;
}
```

[출처 : 프로그래머스 체육복](https://programmers.co.kr/learn/courses/30/lessons/42862?)
