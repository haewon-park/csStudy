## 기수 정렬(Radix Sort)이란?
- 낮은 자리수부터 비교하여 정렬하는 알고리즘

<br>

### 과정
ex) ```200, 152, 2, 0, 32, 45, 99, 87``` 있다고 할 때,

#### 1. 일의 자리를 기준으로 정렬
![](https://images.velog.io/images/hammii/post/b2329d56-07ab-48ef-a6da-b6a81a12fbd5/image.png)

Queue이기 때문에 선입선출이다. ```200, 0, 152, 2, 32, 45, 87, 99``` 로 정렬된다.

#### 2. 십의 자리를 기준으로 정렬
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FclPLBd%2FbtqEq7mrVe3%2F4D8canLJtZwQW88KfjLsjk%2Fimg.png)

십의 자리가 없는 것은 0으로 간주한다. ```200, 0, 2, 32, 45, 152, 87, 99``` 로 정렬된다.

#### 3. 백의 자리를 기준으로 정렬
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F0how1%2FbtqEsrq1Ohh%2FhCQ3HOFbVUeFpCcBVjKgZ0%2Fimg.png)

최종적으로 ```0, 2, 32, 45, 87, 99, 152, 200``` 로 정렬된다.

<br>

### 시간복잡도
- O(d*(n+k))

n: 입력 데이터의 개수 <br>
d: 정수 중 가장 큰 자릿수

<br>

### 장단점
- 장점: 비교 연산을 하지 않아 정렬 속도가 빠르다.
- 단점
  - 중간 결과를 저장할 bucket 공간이 필요하다.
  - 자릿수가 없는 것은 정렬할 수 없다.

<br>

### 💡 왜 낮은 자리수부터 정렬할까?
MSD(Most-Significant-Digit): 가장 큰 자리수부터 정렬 <br>
LSD(List-Significant-Digit): 가장 낮은 자리수부터 정렬

![](https://media.vlpt.us/images/seochan99/post/0ca42ecc-8ae9-4d16-a0f7-b13e12c82bad/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-15%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.59.49.png)

LSD는 마지막에 가서 정렬 순서를 판단하는 반면, MSD는 점진적으로 정렬을 완성해내간다. 따라서 MSD는 중간에 정렬이 완료될 수도 있다.

그러나 중간에 데이터를 점검하지 않으면 224, 232와 같이 두번째 단계에서 이미 대소가 결정됐는데도 자리를 바꾸는 경우가 발생한다.

따라서 **MSD는 정렬이 되었는지 확인하는 과정이 필요하다.**
구현의 난이도가 LSD에 비해 높고, 이 때문에 메모리를 더 사용한다.

<br>

#### 참고 자료
https://kosaf04pyh.tistory.com/262 <br>
https://velog.io/@seochan99/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EB%B3%B5%EC%9E%A1%ED%95%98%EC%A7%80%EB%A7%8C-%ED%9A%A8%EC%9C%A8%EC%A0%81%EC%9D%B8-%EC%A0%95%EB%A0%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-10-2%EA%B8%B0%EC%88%98-%EC%A0%95%EB%A0%AC-2
