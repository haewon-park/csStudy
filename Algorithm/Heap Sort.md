## 힙 정렬(Heap Sort)이란?
- 힙(Heap) 자료구조를 기반으로한 정렬 방식
- 내림차순 정렬을 하고 싶을 땐 최대 힙을, 오름차순 정렬을 하고 싶을 땐 최소 힙을 구성하면 된다.

<br>

## 과정 (최소 힙)
### - 삽입
![](https://images.velog.io/images/hammii/post/e4bffb9d-467f-4306-b4be-302204168c22/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-09-06%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.22.08.png)

### - 삭제
![](https://images.velog.io/images/hammii/post/ecd3ee21-4429-48cb-a5a1-2659784d537d/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-09-06%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.22.38.png)

### 코드
```java
public static void swap(int[] arr, int x, int y) {
    int temp = arr[x];
    arr[x] = arr[y];
    arr[y] = temp;
}

public static void heapify(int[] arr, int parent, int size) {
    int temp_parent = parent;
    int left_child = parent * 2 + 1;
    int right_child = parent * 2 + 2;

    if (left_child < size && arr[temp_parent] > arr[left_child])
        temp_parent = left_child;

    if (right_child < size && arr[temp_parent] > arr[right_child])
        temp_parent = right_child;

    if (parent != temp_parent) {
        swap(arr, parent, temp_parent);
        heapify(arr, temp_parent, size);
    }
}

public static void main(String[] args) {
    int[] arr = new int[]{7, 3, 22, 6, 2, 14, 1};
    int len = arr.length;

    // heapify를 통해 초기 배열을 min heap으로 만듦
    for (int i = len / 2 - 1; i >= 0; --i)
        heapify(arr, i, len);

    // 루트노드를 뒤로 넘기고(삭제) 나머지 원소들을 heap으로 만듦
    for (int i = len - 1; i > 0; --i) {
        swap(arr, 0, i);    
        heapify(arr, 0, i); 
    }
}
```

### 시간복잡도
heapify 알고리즘: O(logN)

|   평균   |   최선   |   최악   |
| :------: | :------: | :------: |
| Θ(nlogn) | Ω(nlogn) | O(nlogn) |

<br>

### 장단점
- 장점
  - 추가적인 메모리를 필요로하지 않는다.
  - 최악의 경우에도 O(nlogn)으로 유지된다.
- 단점
  - 퀵정렬과 비교했을 때 시간복잡도는 O(nlogn)으로 똑같으나, 실제 시간을 측정하면 퀵정렬보다 느리다.

<br>

#### 참고 자료
https://github.com/gyoogle/tech-interview-for-developer/blob/master/Algorithm/HeapSort.md <br>
https://soobarkbar.tistory.com/212 <br>
https://st-lab.tistory.com/225 <br>
