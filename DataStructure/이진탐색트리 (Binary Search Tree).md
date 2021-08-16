### 이진탐색트리란?
- 이진탐색 : 탐색에 소요되는 시간복잡도는 **O(logN)**, but 삽입,삭제가 불가능
- 연결리스트 : 삽입, 삭제의 시간복잡도는 **O(1)**, but 탐색하는 시간복잡도가 O(N)

위 두가지를 합하여 장점을 모두 얻는 것
즉, 효율적인 탐색 능력을 가지고, 자료의 삽입 삭제도 가능하게 만들자

![](https://images.velog.io/images/hammii/post/79007ee9-db76-4bf1-8412-d532eef6acd0/image.png)

<br>
  
### 이진탐색트리 특징
- 각 노드의 자식이 2개 이하
- 각 노드의 왼쪽 자식은 부모보다 작고, 오른쪽 자식은 부모보다 큼
- 중복된 노드가 없어야 함
- 중위순회(inorder) 방식 (left - root - right)

<br>

### 시간 복잡도
- 균등 트리 : 노드 개수가 N개일 때 O(logN)
- 편향 트리 : 노드 개수가 N개일 때 O(N)

✅ 삽입, 검색, 삭제 시간복잡도는 트리의 Depth에 비례하다.

편향트리는 시간복잡도가 O(N)이므로 트리를 사용할 이유가 사라진다.<br>
=> 이를 바로 잡도록 도와주는 개선된 트리가 `AVL Tree`, `RedBlack Tree`

<br>

### 삭제의 3가지 Case
1. 자식이 없는 leaf 노드일 때 → 그냥 삭제
2. 자식이 1개인 노드일 때 → 지워진 노드에 자식을 올리기
3. 자식이 2개인 노드일 때 → 오른쪽 자식 노드에서 가장 작은 값 or 왼쪽 자식 노드에서 가장 큰 값 올리기

<br>

#### 참고 링크
https://gyoogle.dev/blog/computer-science/data-structure/Binary%20Search%20Tree.html
