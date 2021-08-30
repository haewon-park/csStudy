![](https://user-images.githubusercontent.com/63101648/130954584-f34c9007-e22e-493c-9adf-698b0c7977a8.jpeg)


## Set
- 데이터의 집합
- **순서 X, 중복 X**
- 빠른 검색 속도를 가진다.
- 인덱스가 따로 존재하지 않기에 iterator를 사용
- `add`, `remove`, `contains`와 같은 메소드 제공 (java)

ex) ABBCCCDDD 입력이라도 ABCD만 남아있다!

<br>

### HashSet
![](https://user-images.githubusercontent.com/63101648/130954488-403e091e-f0d5-44fe-8c37-01fc4e5b8dd4.png)
- 인스턴스의 **해시값**을 기준으로 저장하기 때문에 순서를 보장하지 않는다.
- 가장 빠른 임의 접근 속도: O(1)
- null 값 허용

### LinkedHashSet
![](https://user-images.githubusercontent.com/63101648/130954505-53fab494-9917-4484-a3ac-c80f44f7b556.png)
- Set 인터페이스를 구현하고 HashSet 클래스를 상속받은 LinkedList
- 순회시 인스턴스가 입력된 순서를 보장한다.

### TreeSet
![](https://user-images.githubusercontent.com/63101648/130954555-fe8fc809-44eb-43bc-889a-28aa0203ea0e.png)
- 데이터 하나하나 저장할때 정렬한다. (이진탐색트리 기반으로 저장하기때문)
  - 정렬 방법 지정 가능: Comparable 인터페이스를 구현하거나, 생성자의 인자로 Comparator을 구현한 인스턴스 전달해주면 된다.
- Red-Black Tree를 기반으로 함

<br>

## Map
- Key, Value의 한 쌍으로 이루어지는 데이터의 집합
- Key에 대한 중복이 없고 순서를 보장하지 않는다.
- 뛰어난 검색 속도
- 따로 인덱스가 존재하지 않기에 iterator 사용

### HashMap
- Key에 대한 중복이 없으며 순서를 보장하지 않는다.
- 키와 값으로 null을 허용
- 검색에 가장 뛰어난 성능을 가진다.

### HashTable
- 키와 값으로 null 허용하지 않는다.

### LinkedHashMap
- 입력된 순서를 보장
- HashMap을 상속받아 HashMap과 매우 흡사

### TreeMap
- Red-Black Tree를 기반으로 키와 값을 저장함
- Key 값을 기준으로 오름차순 정렬되고 빠른 검색 가능
- 저장시 정렬을 하기에 시간이 오래 걸린다.

<br>

### 💡 HashMap과 HashTable의 차이?
- Null 값 여부
  - HashMap은 Null을 허용하지만, HashTable은 허용하지 않는다.
- 동기화 보장 유무
  - 동기화가 필요없다면 HashMap을, 동기화가 필요하다면 HashTable을 사용한다.
  (HashTable은 Thread-safe하다)
  - 동기화는 속도를 굉장히 느리게 해주기 때문에, 동기화가 보장되는 HashMap이 등장하기도 하였다. (ConcurrentHashMap)

<br>

#### 출처
- https://gamjatwigim.tistory.com/73
- https://lelumiere.tistory.com/3
- https://cocoon1787.tistory.com/527
- https://velog.io/@syleemk/%EB%A9%B4%EC%A0%91-%EB%8C%80%EB%B9%84-Java#set
