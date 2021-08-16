# Trie
## 들어가며
_**Q. 수많은 문자열을 저장하고, 입력으로 어떤 문자열이 주어졌을 때, 그 문자열이 내가 저장한 구조에 포함된 문제열인지 어떻게 알 수 있을까?**_

① 단순 비교
-   전체 문자열의 맨 처음부터 끝까지 개별 문자를 비교하는 방식
-   최대 문자열 길이 m, 전체 문자 개수 n개 시 시간복잡도 : 최악의 경우 O(nm)

② 이진 탐색 기법
-   전체 문자열을 사전 순으로 배열 저장 후, 중간 값과 비교해 사전적으로 이전이면 좌측의 반 / 이후면 우측의 반으로 비교하는 방식을 반복
-   최대 문자열 길이 m, 전체 문자 개수 n개 시 시간복잡도 : 정렬 O(nmlogn) / 탐색 O(mlogn) ⇒  즉, O(nmlogn)

③ 트라이(Trie)

<br>

## 1. Trie
### Trie란?
> 문자열을 저장하고, 효율적으로 탐색하기 위한 트리 형태의 자료구조
> Digital Tree, Radix Tree, Prefix Tree라고도 불림.

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/b/be/Trie_example.svg/375px-Trie_example.svg.png)

* 트리의 루트에서부터 자식들을 따라가면서 생성된 문자열들이 트라이 자료구조에 저장
* 저장된 단어는 끝을 표시하는 변수를 추가해서 저장된 단어의 끝을 구분할 수 있음
* **DFS**로 검색하면 `to, tea, ted, ten, A, i, in, inn` 라는 단어들이 위의 트라이에 들어가 있음.
<br>

### 장단점
**장점**
* 문자열 검색이 빠름
* 문자열을 탐색할 때, 하나하나씩 전부 비교하면서 탐색을 하는 것보다 시간 복잡도 측면에서 훨씬 더 효율적

**단점**
* 각 노드에서 자식들에 대한 포인터들을 배열로 모두 저장하고 있다는 점에서 저장 공간의 크기가 크다는 단점도 있다. (메모리 측면에서 비효율적일 수 있음!)
* **최종 메모리의 크기 = O(포인터 크기 * 포인터 배열 개수 * 트라이에 존재하는 총 노드의 개수) ** 

**시간 복잡도**
-   최대 문자열 길이 m 일 때 문자의 개수와 무관하게 시간복잡도는 `O(m)`
    -   각 문자 하나를 배열의 위치로 지정하여 문자열 하나 찾을 때 `O(1)`이므로 길이만큼의 시간만 소요함
    -   만약, 문자열 길이가 너무 너무 커서 Map 등을 이용해 동적할당을 해야 하는 경우 `O(mlogn)` 만큼 소요할 수 있다.
<br>

_**Q. map을 이용하면 충분히 트라이와 같은 효과를 낼 수 있지 않을까?**_
A. 충분히 비슷한 효과를 낼 수 있지만 맵의 특성상 이진 검색 트리에서 `O(lgN)`만큼의 시간이 들 것.
또한, 그 문자열을 확인하는데 `O(MlgN)`만큼의 시간이 들 것이기에 map을 이용하는 것과 Trie를 이용하는 것은 엄연히 다른 시간 복잡도를 나타냄.

<br>

## 2. Trie 구현
### using JAVA
```java
public class Trie {
    private TrieNode root = new TrieNode();
 
    private void insert(String key) {
        root.insert(key + '\0');
    }
 
    private void find(String key) {
        Boolean result = root.find(key + '\0');
 
        if (result == null)
            System.out.println("값이 없음");
        else if (result)
            System.out.println("값이 있음");
        else
            System.out.println("값이 있으나 끝이 아님");
    }
 
    public static void main(String[] args) {
        Trie trie = new Trie();
        trie.insert("Hello");
        trie.insert("House");
 
        trie.find("House"); // 값이 있음
        trie.find("Hell"); // 값이 있으나 끝이 아님
        trie.find("Horse"); // 값이 없음
    }
}
 
class TrieNode {
    private TrieNode[] next = new TrieNode[26];
    private boolean leaf;
 
    void insert(String string) {
        char[] s = string.toCharArray();
        char curr = s[0];
 
        if (curr == '\0')
            leaf = true;
 
        else {
            int idx = char2idx(curr);
 
            if (next[idx] == null) 
                next[idx] = new TrieNode();
 
            if (string.length() > 1) 
                string = string.substring(1);
 
            next[idx].insert(string);
        }
    }
 
    Boolean find(String string) {
        char[] s = string.toCharArray();
        char curr = s[0];
 
        if (curr == '\0')
            return leaf;
 
        else {
            int idx = char2idx(curr);
 
            if (next[idx] == null)
                return null;
 
            if (string.length() > 1)
                string = string.substring(1);
 
            return next[idx].find(string);
        }
    }
 
    private int char2idx(char c) {
        // make lowercase
        if (c < 'a') {
            c += ('a' - 'A');
        }
 
        return c - 'a';
    }
}
```
<br>

### using Python
```python
class Node():
	def __init__(self, key = None, data = None):
		self.key = key
		self.data = data
		self.child_node = {}
class Trie():
	def __init__(self):
		self.head = Node()
	def insert(self, string):
		cur_node = self.head
		for chr in string:
			if chr not in cur_node.child_node.keys():
		# 노드 순차적 검색하며 없으면 노드등록		
				cur_node.child_node[chr] = Node(chr)
			cur_node = cur_node.child_node[chr]
		# 현재노드를 다음 문자의 노드로 변경
		cur_node.data = string
		# 마지막 노드에는 문자열 전체 저장
		
	def search(self, string):
		cur_node = self.head
		for chr in string:
			if chr not in cur_node.child_node.keys():
	# 문자가 노드에 없으면 찾지못함
				print("Not in char")
				return False
			cur_node = cur_node.child_node[chr]
	# 현재노드를 다음문자로 변경하며 탐색
			
		if cur_node.data != None:
			print ("search result : " ,string)
	# 마지막 노드인 경우. Data는 문자열을 가진다
			return True
		else:
			print("exist : ", string)
	# 문자가 다 저장되어있으나 마지막이 아닌경우, data는 None이기 때문에 한번더 체크

t = Trie() 
t.insert("hello") 
t.insert("bye") 
t.search("qweqwe") 
t.search("hell") 
t.search("bye")

```
<br>

---
**참고 자료**
* https://the-dev.tistory.com/3(구현 - java)
* https://kangprog.tistory.com/92(구현 - python)
* https://www.crocus.co.kr/1053(시간, 공간 복잡도)
