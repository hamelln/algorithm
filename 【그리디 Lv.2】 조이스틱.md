# 조이스틱 (프로그래머스 문제 Lv 2)

![image](https://user-images.githubusercontent.com/39308313/145410074-c79c5eec-a46b-46a5-a5cb-79cf384b10d3.png)

## 풀이 과정

### 알파벳을 입력할 때 처리할 계산은 두 가지이다.
 - 위, 아래로 스틱을 몇 번 움직여야 하는가?
 - 어떻게 해야 옆으로 적게 움직이는가?

```txt
1. 
위 아래로 몇 번 움직여야하는지 먼저 구하자.

2. 
JAZ가 입력됐을 때 A는 움직일 필요가 없으니 0이다.
J는 A에서 9번 위로 움직여야 한다. A + 9다.
Z는 A에서 1번 아래로 움직여야 한다. A - 1이다.

2-1. 
알파벳은 총 26개다. 13번 이상 위로 올릴 거면 아래로 내리는 게 빠르다.
알파벳을 charCode로 바꾼다. 그냥 바꾸면 74, 65, 90같은 숫자가 나온다.
알파벳 대문자는 65~90까지다. 모든 charCode에서 65를 빼면 된다.
2-1의 조건을 만족하기 위해 가운데 숫자 78을 넘는 알파벳은 91 - charCode를 한다.

3. 
모든 숫자들의 합 sum을 구한다.

4.
111011처럼 0이 4번에 있으면 3번까지 이동한 거리만큼은 이득을 얻어야 한다.
이 거리를 min이라는 변수에 저장한다.

5.
1110111100000011111이라는 숫자가 있을 때에도 마찬가지다.
0이 6개 있으므로 count 변수로 0을 다 센 다음,
이동한 거리에서 count * 2만큼 뺀다.
(count * 2를 하는 이유는 0을 세는 동안에도 거리는 계속 늘어나고 있기 때문.)
결과값이 min보다 더 작으면 min에 저장한다.
기존에 있는 min이 더 작으면, 그곳에서 후진하는 게 더 이득이란 얘기다.

6. 마지막 인덱스까지 진행하고 min값이 음수이면 sum과 계산한다.

7. 만약 min값이 음수가 아니면, 어떤 경우에도 후진하지 않고 그냥 전진하는 게 더 낫다는 얘기다.
그럴 땐 그냥 sum만 return한다.
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

[출처 : 프로그래머스 조이스틱](https://programmers.co.kr/learn/courses/30/lessons/42860)
