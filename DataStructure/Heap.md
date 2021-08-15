## Heap(힙)
### 개념

우선순위 큐를 위해 만들어진 자료구조

> **우선순위 큐(Priority Queue)?**
>
>`우선순위`의 개념을 큐에 도입한 자료구조
>데이터들이 우선순위를 가지고 있어 **우선순위가 높은 데이터가 먼저 나간다!**

<br>

- 완전 이진 트리의 일종이다.
- 여러 값 중, 최대값과 최소값을 빠르게 찾아내도록 만들어진 자료구조로 **반정렬 상태**이다.
- 힙 트리는 중복된 값을 허용한다. (이진 탐색 트리는 중복값 허용X)


<br><br>


### 힙의 종류

1. **최대 힙(max heap)**
부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전 이진 트리

2. **최소 힙(min heap)**
부모 노드의 키 값이 자식 노드의 키 값보다 작거나 같은 완전 이진 트리

![](https://images.velog.io/images/yanghl98/post/8ddbc281-c845-45c0-81d6-8ce0d49b25d9/image.png)<br>
(이미지 출처 : https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html)

<br>


### 힙의 활용 예시

- 시뮬레이션 시스템
- 네트워크 트래픽 제어
- 운영 체제에서의 작업 스케쥴링
- 수치 해석적인 계산

<br>

### Tip!
우선순위 큐는 배열, 연결리스트, 힙 으로 구현이 가능하다. 이 중에서 **힙(heap)으로 구현하는 것이 가장 효율적**이다.
![](https://images.velog.io/images/yanghl98/post/c64db4c9-6151-4c26-9f06-bb2b9193168a/image.png)<br>
(이미지 출처 : https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html)


<br><br>


## 힙의 구현

- 힙을 저장하는 표준적인 자료구조는 `배열`이다.
- 구현을 쉽게 하기 위해 배열의 첫번째 인덱스인 0은 사용되지 않는다.
- 특정 위치의 노드 번호는 새로운 노드가 추가되어도 변하지 않는다. (`ex` 루트 노드(1)의 오른쪽 노드 번호는 항상 3)

<br>

### 부모 노드와 자식 노드 관계
![](https://images.velog.io/images/yanghl98/post/b898faf5-7394-4dcd-96ee-d043d6f8c139/image.png)<br>
(이미지 출처 : https://ipwag.tistory.com/86)

```
왼쪽 자식 index = (부모 index) * 2
오른쪽 자식 index = (부모 index) * 2 + 1
부모 index = (자식 index) / 2
```

<br>

### 힙의 삽입
1. 힙에 새로운 요소가 들어오면, 일단 새로운 노드를 **힙의 마지막 노드에 삽입**한다.
2. 새로운 노드를 부모 노드들과 교환한다.

![](https://images.velog.io/images/yanghl98/post/73220cd3-a136-4ada-8234-91c26f9199ee/image.png)<br>
(이미지 출처 : https://velog.io/@emplam27/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-%ED%9E%99Heap)

<br><br>

```java
// 최대 힙 삽입
void insert_max_heap(int x) {
    
    maxHeap[++heapSize] = x; // 힙 크기를 하나 증가하고, 마지막 노드에 x를 넣음
    
    for( int i = heapSize; i > 1; i /= 2) {
        
        // 마지막 노드가 자신의 부모 노드보다 크면 swap
        if(maxHeap[i/2] < maxHeap[i]) {
            swap(i/2, i);
        } else {
            break;
        }
        
    }
}
```
부모 노드는 자신의 인덱스의 /2 이므로, 비교하고 자신이 더 크면 swap하는 방식이다.


<br>

### 힙의 삭제
1. 최대 힙에서 최대값은 루트 노드이므로 **루트 노드**가 삭제된다. (최대 힙에서 삭제 연산은 최대값 요소를 삭제하는 것)
2. 삭제된 루트 노드에는 **힙의 마지막 노드를 가져옴**
3. 힙을 재구성

![](https://images.velog.io/images/yanghl98/post/f33d8046-50c6-4684-8c6c-0ccd687b4211/image.png)<br>
(이미지 출처 : https://velog.io/@emplam27/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-%ED%9E%99Heap)

<br><br>

```java
// 최대 힙 삭제
int delete_max_heap() {
    
    if(heapSize == 0) // 배열이 비어있으면 리턴
        return 0;
    
    int item = maxHeap[1]; 		// 루트 노드의 값을 저장
    maxHeap[1] = maxHeap[heapSize]; 	// 마지막 노드 값을 루트로 이동
    maxHeap[heapSize--] = 0; 		// 힙 크기를 하나 줄이고 마지막 노드 0 초기화
    
    for(int i = 1; i*2 <= heapSize;) {
        
        // 마지막 노드가 왼쪽 노드와 오른쪽 노드보다 크면 끝
        if(maxHeap[i] > maxHeap[i*2] && maxHeap[i] > maxHeap[i*2+1]) {
            break;
        }
        // 왼쪽 노드가 더 큰 경우, swap
        else if (maxHeap[i*2] > maxHeap[i*2+1]) {
            swap(i, i*2);
            i = i*2;
        }
        // 오른쪽 노드가 더 큰 경우, swap
        else {
            swap(i, i*2+1);
            i = i*2+1;
        }
    }
    
    return item;
    
}

```


<br><br>

## 출처
https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/Heap.md<br>
https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html<br>
