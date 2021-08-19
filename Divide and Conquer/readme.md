## Divide and Conquer (분할 정복)
- 문제를 나눌 수 없을 때 까지 나누어서 각각 해결한 후, 다시 병합하여 해를 구하는 알고리즘
- 보통 재귀 함수로 구현됨.

### 알고리즘 구조
- 해결해야할 문제를 dac 함수로 호출
- 전체 문제를 문제를 해결하기에 적합한 특정 크기(size)로 분할(Divide).
- 분할하여 분할된 부분을 다시 dac 함수로 호출
- 호출 후 해결이 되지 않는다면 해결될 때 까지 분할(Divide)후 다시 호출(Conquer).
- 모든 문제가 분할되어 해결되었을 시 해결된 모든 문제의 정답을 병합(Combine).

아래는 [백준 1074](https://www.acmicpc.net/problem/1074) 문제에서 구현한 분할 정복 함수이다. 
```C
void f(int y, int x, int s) {
	if (y == r && x == c) { //y와 r(행), x와 c(열)이 같다면
		cout << sum << '\n'; //정답 출력 후 함수 return
		return;
	}
	if (r < y + s && r >= y && c < x + s && c >= x) { //분할해야 하는 경우, 조건에 충족하다면
		f(y, x, s / 2); // 총 4개의 문제로 분할하여 재귀 함수 호출
		f(y, x + s / 2, s / 2);
		f(y + s / 2, x, s / 2);
		f(y + s / 2, x + s / 2, s / 2);
	}
	else {
		sum += s * s;
	}
}
```

## 정리
분할 정복을 사용하는 경우
- 주어진 전체 문제를 해결해야 하는데, 나누어서 해결하면 더 효율적인 경우

시간 복잡도
- 각 단계에서 드는 총합 연산량: O(N) 매 단계마다 각 문제의 크기가 지수적으로 줄어들기 때문
- 단계는 총 O(logN)개 있으므로, 시간 복잡도는 O(NlogN)