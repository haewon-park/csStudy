
# Graph
## 1. Graph
### 1-1. Graph란?
> 단순히 node와 그 node를 연결하는 edge를 하나로 모아 놓은 자료 구조
> 즉, 연결되어 있는 객체 간의 관계를 표현할 수 있는 자료 구조

`무방향 그래프`, `방향 그래프`, `가중치 그래프`, `연결 그래프`, `비연결 그래프`, `사이클`, `비순환 그래프`, `완전 그래프`

<br>

### 1-2. Graph vs Tree
|         | Graph | Tree |
|---------| -------------------- | --------------- |
| 정의     | - node와 그 node를 연결하는 edge를 하나로 모아 놓은 자료 구조 | - 그래프의 한 종류, 방향성이 있는 비순환 그래프 | 
| 방향성     | - 방향 그래프, 무방향 그래프 둘다 O | - 방향 그래프만 O | 
| 사이클     | - 사이클 가능<br> - 순환, 비순환 그래프 둘다 O | - 비순환 그래프로 사이클 X | 
| 루트 노드     | - 루트 노드 X | - 루트 노드 O | 
| 부모/자식 관계     | - 부모 자식 개념 X | - 부모 자식 관계 O | 
| 간선의 수     | - 자유<br> - 없을 수도 있음 | - N개의 노드를 가진 트리는 항상 N - 1 개의 간선 O | 
| 순회     | - DFS, BFS | - DFS, BFS 방식의 preorder, inorder, postorder  | 

<br>

## 2. Graph 구현
###  2-1. 인접 리스트(Adjacency List)
![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbujUPG%2FbtqARXBaXPp%2FFbmfDM9POfGbsncsYjuzlK%2Fimg.png)
* 모든 정점을 인접 리스트에 저장 ⇒ 각 정점에 인접한 정점들을 리스트로 표현.
* **array**, **ArrayList**, **LinkedList**를 이용해서 인접 리스트 표현.
* 트리 구조라면 루트 노드에서 다른 노드 한번에 접근 가능(?사이클 X)
* 그래프라면 루트 노드에서 한번에 접근이 불가능함.

<br>

**_장점_**
* 메모리 효율이 좋음. ⇒ 메모리 사용량이 노드의 개수가 아닌 간선의 개수에 따라 달라짐.
* 특정 노드에 직접 접근할 수 있어 인접한 노드를 찾기 쉬움.
* 노드의 추가 삭제가 빠름. ⇒  `O(1)`
* 새로운 간선 추가가 빠름. ⇒  `O(1)`
* 그래프의 모든 간선의 수를 찾는데 빠름. ⇒  `O(M + E)`

**_단점_**
* 두 노드의 간선 정보를 확인하는데 오래 걸림.

<br>

### 2-2. 인접 행렬(Adjacency Matrix)
![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FOQ6rH%2FbtqAQNzuxw5%2FbMRXxEIOUNYTobjG8k8pWk%2Fimg.png)
* 노드의 개수가 N인 그래프를 인접 행렬로 표현

<br>

**_장점_**
* 두 노드의 간선 정보 확인이 빠름 ⇒ `O(1)`
* 새로운 간선 추가 제거 빠름 ⇒ `O(1)`

**_단점_**
* 간선의 개수와 상관없이 배열의 크기는 항상 `M * M` ⇒ O(M^2)의 메모리 사용
* 특정한 노드에 인접한 노드를 찾기 위해서 모든 노드를 순회해야함.
* 노드를 추가하거나 제거하는데 오래 걸림 ⇒  `O(M^2)`
* 그래프의 모든 간선의 수를 찾는데 오래 걸림 ⇒ `O(M^2)`

<br>

### 2-3. 인접 리스트 vs 인접 행렬
**시간 복잡도**
|         | 인접 리스트 | 인접 행렬 | 
|---------| ------ | ------ | 
| node 추가 | O(1)|O(M^2) | 
| node 삭제 | O(M + E)| O(M^2)| 
| edge 추가 | O(1)|O(1) | 
| edge 삭제 | O(E)|O(1) | 

<br>

**선택 방법**
* 인접 리스트
	> **노드의 개수가 많고, 간선의 개수가 상대적으로 적을 때 사용!**
	> 따라서, 간선이 적은 희소 그래프(Sparse Graph)에 적합!
* 인접 행렬
	> **상대적으로 노드의 개수가 적고, 간선의 수가 많을 때 사용!**
	> 따라서, 간선이 많은 밀집 그래프(Dense Graph)에 적합!

<br>

## 3. Graph 탐색
### 3-1. 깊이 우선 탐색(DFS, Depth-First Search)
![img](https://gmlwjd9405.github.io/images/algorithm-dfs-vs-bfs/dfs-example.png)
> 루트 노드에서 시작해서 다음 분기로 넘어가기 전에 해당 분기를 완벽하게 탐색하는 방법
* **모든 노드를 방문하고자 하는 경우**, **경로의 특징을 저장해둬야 하는 문제**에 사용
* 검색 속도 자체는 BFS에 비해서 느림

<br>

### 3-2. 너비 우선 탐색(BFS, Breadth-First Search)
![img](https://gmlwjd9405.github.io/images/algorithm-dfs-vs-bfs/bfs-example.png)
> 루트 노드에서 시작해서 인접한 노드를 먼저 탐색하는 방법
* 시작 정점으로부터 가까운 정점을 먼저 방문하고, 멀리 떨어져 있는 정점을 나중에 방문하는 순회 방법
* **두 노드 사이의 최단 경로** or **임의의 경로**를 찾고 싶을 때 사용

<br>

## 4. Graph 알고리즘
### 4-1. 다익스트라 알고리즘
> 첫 정점을 기준으로 연결되어 있는 정점들을 추가해가며 최단 거리를 갱신하는 기법

**특징**
* `음의 간선`이 없을 때만 정상적으로 동작
* 매번 가장 비용이 적게 드는 노드를 선택하는 것임으로 Greedy Algorithm

<br>

### 4-2. 벨만 포드 알고리즘
> 한 노드에서 다른 노드까지의 최단 거리를 구하는 기법

**특징**
* 가중치가 `음수`여도 동작 가능
* 모든 간선 확인

<br>

### 4-3. 플로이드 워셜 알고리즘
> 모든 정점에서 모든 정점으로의 최단 경로를 구하는 기법

**특징**
* `거쳐가는 정점`을 기준으로 최단거리를 구하는 것
* 가중치가 `음수`여도 동작 가능
* DP

<br>

### 4-4. 다익스트라 vs 벨만 포드 vs 플로이드 워셜 비교
**시간 복잡도 /  공간복잡도**
|         | 다익스트라 | 벨만 포드 | 플로이드 워셜 | 
|---------| ------ | ------ | --------- | 
| 시간 복잡도 | - priorityQueue 사용X: O(V^2)<br>- priorityQueue 사용O: O(ElogV) |O(VE) | O(V^3) | 
| 공간 복잡도 |  - priorityQueue 사용X: O(V+E)<br>- priorityQueue 사용O: O(V+E)| O(V)| O(V^2) | 

<br>

--- 

**참고자료**
* https://gmlwjd9405.github.io/2018/08/13/data-structure-graph.html
* https://hsc-tech.tistory.com/12 (구현 차이)
* https://gmlwjd9405.github.io/2018/08/15/algorithm-bfs.html (BFS)
* https://gmlwjd9405.github.io/2018/08/14/algorithm-dfs.html (DFS)
