## depth-First Search (깊이 우선 탐색)
- 그래프 탐색 알고리즘.

### 알고리즘 구조
- 하나의 정점에서 최대한 깊이 내려간 뒤, 더 이상 내려갈 곳이 없다면 옆으로 이동.
- 임의의 노드에서 시작하여 다음 분기로 넘어가기 전에 해당 분기를 완벽하게 탐색
- stack을 이용하여 정점마다 push 후, 더 이상 연결된 정점이 없다면 pop 이후, 다음 정점을 push 하는 방식

아래는 [백준 1260](https://www.acmicpc.net/problem/1260) 문제에서 구현한 dfs 함수이다. 
```C
stack<int> s;
vector<pair<int, int>> vec;
int arr[1001];

void dfs() {
	while(!s.empty()) { //stack이 비어있을 때 까지 반복
		int c=0;
		for (int i = 0; i < vec.size(); i++) { //vector의 크기만큼 반복
			if (vec[i].first == s.top()) { //vector의 첫번째 인수와 stack의 top이 같을 경우.
				if (arr[vec[i].second] == 0) { //해당 배열이 비어있다면
					arr[vec[i].second] = 1; //배열 채워주고
					s.push(vec[i].second); //stack에 해당 배열을 push
					vec.erase(vec.begin() + i); //해당 vector 삭제
					cout << ' ' << s.top(); // top 출력
					c = 1;
					break;
				}
			}
			else if (vec[i].second == s.top()) {//vector의 두번째 인수와 stack의 top이 같을 경우.
				if (arr[vec[i].first] == 0) { // 위와 동일
					arr[vec[i].first] = 1;
					s.push(vec[i].first);
					vec.erase(vec.begin() + i);
					cout << ' ' << s.top();
					c = 1;
					break;
				}
			}
		}
		if (c == 0) { s.pop(); }
	}
}
```

## 정리
해당 알고리즘을 활용할 수 있는 경우는
- 모든 노드를 방문하고자 하는 경우.

장단점
- bfs보다 간단하다. bfs는 queue를 이용해 구현하는 것에 비해 stack을 사용한다.
- 탐색 속도가 bfs보다 느리다.

시간 복잡도
- dfs(x)는 x에 방문하는 함수이므로 정점의 개수, 즉 차수인 V번만큼 dfs(x)가 호출된다. 
- dfs(x) 시간복잡도 * V (인접행렬: O(V), 인접리스트: O(V+E))
