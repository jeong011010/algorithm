## Hash Table (해시 테이블) - Hash search algorithm (해시 탐색 알고리즘)
- key, value 두가지 값을 한 쌍으로 묶어 사용하는 탐색 방법
- 특정 값을 넣었을 때 특정 연산을 통해 해당 value에 해당하는 key가 도출되어 빠른 탐색이 가능한 알고리즘
- key의 값만 겹치지 않으면 이분, 선형 탐색보다 훨씬 빠르고 효율적으로 사용이 가능하다.

### 알고리즘 구조
- 임의의 길이를 갖는 임의의 데이터에 대해 고정된 길이의 데이터로 매핑하는 알고리즘

- 즉 문자열을 받아서 숫자(key)를 반환하여 해당 key에 해당하는 값(value)를 도출해내는 알고리즘이다.

아래는 [백준 1620](https://www.acmicpc.net/problem/1620) 문제에서 구현한 해시 알고리즘이다. 
```C
map<string, int> pokemon; //map STL을 이용해 해시 구현 (string이 들어왔을 때 번호(key)를 도출하기 위함)
string pokemon_s[100001]; 
int n, q;

int main() {
	cin >> n >> q;
	for (int i = 1; i <= n; i++) {
		string s;
		cin >> s;
		pokemon.insert(make_pair(s, i)); // string(key), int(value) map에 삽입
		pokemon_s[i] = s;
	}
	
	for (int i = 0; i < q; i++) {
		string tmp;
		cin >> tmp;
		if (tmp[0] > 64 && tmp[0] < 91) {
			cout<<pokemon[string(tmp)]<<'\n'; // map[key] - 해당 key에 해당하는 value 호출
		}
		else {
			int num = tmp[0]-48;
			for (int j = 1; j < tmp.size(); j++) {
				num *= 10;
				num += tmp[j] - 48;
			}
			cout << pokemon_s[num] << '\n';
		}
	}
}
```

## 정리
해시 알고리즘을 사용하는 경우
- 탐색이 필요할 때, string을 통해 int를 도출해야 하는 경우
- 방대한 값이 저장되어 있을 때 빠른 탐색 시간이 필요한 경우

시간 복잡도
- 해시 알고리즘은 해당 string(key)를 넣고 바로 auto(value)가 도출 가능하므로 시간복잡도는 O(1)이다.
