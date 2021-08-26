# **Map & Set**

![listmapset](https://user-images.githubusercontent.com/63101648/130954584-f34c9007-e22e-493c-9adf-698b0c7977a8.jpeg)


## **Map**
- Key Value의 한 쌍으로 이루어지는 데이터의 집합
- Key에 대한 중복이 없고 순서를 보장하지 않는다.
- 뛰어난 검색 속도
- 따로 인덱스가 존재하지 않기에 iterator 사용

<br>

## **Map의 종류와 특징**
### - **HaxhMap**
    - key에 대한 중복이 없으며 순서를 보장하지 않는다.
    - Key와 Value값으로 null을 허용
    - 검색에 가장 뛰어난 성능을 가진다.
### - **HashTable**
    - Key와 Value값으로 null 허용하지 않는다.
### - **LinkedHashMap**
    - 입력된 순서를 보장
### - **TreeMap**
    - Red-Black Tree를 기반으로 키와 값을 저장함
    - key값을 기준으로 오름차순 정렬되고 빠른 검색 가능
    - 저장시 정렬을 하기에 시간이 오래 걸린다.
    
 
<br>

## **Set**
- 데이터의 집합
- 순서가 없고 중복된 데이터를 허용하지 않는 자료구조
- 빠른 검색 속도를 가진다.
- 인덱스가 따로 존재하지 않기에 iterator를 사용
- Ex) ABBCCCDDD 입력이라도 ABCD만 남아있다!

<br>

## **Set의 종류와 특징**
### - **HashSet**

![hashset](https://user-images.githubusercontent.com/63101648/130954488-403e091e-f0d5-44fe-8c37-01fc4e5b8dd4.png)

    - null 값 허용
    - 순서가 보장되지 않고, 중복된 값이 없는 자료구조
    - add, remove, oontains와 같은 메소드 제공
### - **LinkedHashSet**

![linkedhashset](https://user-images.githubusercontent.com/63101648/130954505-53fab494-9917-4484-a3ac-c80f44f7b556.png)

    - 들어오는 데이터의 순서를 보장하고 있는 자료구조
    - add, remove, contains와 같은 메소드 제공
### - **TreeSet**

![treeset](https://user-images.githubusercontent.com/63101648/130954555-fe8fc809-44eb-43bc-889a-28aa0203ea0e.png)

    - 데이터들이 오름차순으로 정렬됨
    - 데이터의 삽입, 삭제 시간은 좀 걸리지만 검색, 정렬은 빠르다.(BinarySearch Tree의 구조로 이뤄져있기 때문에!)
    - Red-Black Tree를 기반으로 함
    - add, remove, contains와 같은 메소드 제공

<br>

### 출처
- https://gamjatwigim.tistory.com/73
- https://lelumiere.tistory.com/3
- https://cocoon1787.tistory.com/527
