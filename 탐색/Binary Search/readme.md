## Binary Search (이진 탐색)
- 정렬되어 있는 배열 속에서 원하는 값을 효율적으로 찾기 위한 탐색 알고리즘
- 처음과 끝을 정한 뒤, 두 값을 더하여 나눈 값과 찾는 값을 비교하여 크거나 작다면 처음이나 끝 값을 변경.
- 배열의 값이 많은 경우 훨씬 효율적으로 찾을 수 있다.

### 알고리즘 구조
- left와 right, mid 변수를 선언한다.
- left는 찾는 배열의 가장 앞 배열 번호, right는 찾는 배열의 가장 끝 배열 번호.
- mid는 left와 right를 더한 뒤 나눈 값.
- mid와 찾는 값을 비교 후, left가 right보다 커지거나 mid와 같을때 까지 아래 코드 반복.
  - mid보다 작다면 right를 mid - 1로 변경
  - mid보다 크다면 left를 mid + 1로 변경
  - mid와 같다면 break;

아래는 [백준 1764](https://www.acmicpc.net/problem/1764) 문제에서 사용한 이진 탐색이다. 
```C
for (int i = 0; i < m; i++) {
		cin >> s;
		int left = 0, right = n; //left를 배열의 첫값인 0으로, right를 끝값인 n으로 선언
		while (left <= right) { //left가 right보다 커질 때 까지 반복
			int mid = (left + right) / 2; //mid 선언
			if (s == v1[mid]) { //mid와 같다면 종료
				v2.push_back(s);
				break;
			}
			else if (s.compare(v1[mid]) < 0) //mid보다 작다면
				right = mid - 1; //right를 mid - 1로
			else if (s.compare(v1[mid]) > 0) //mid보다 크다면
				left = mid + 1; //left를 mid + 1로
		}
	}
```

## 정리
해당 탐색 구조를 사용할 수 있는 경우
- 크기가 큰 배열에서 특정 값을 찾을 때. (선형 탐색보다 훨씬 효율적이다.)

시간 복잡도 && 공간 복잡도
- 실행된 탐색의 횟수가 시간 복잡도(K) 라고 한다면, 2^K = N => K = log2N
- 시간 복잡도는 O(logN)
