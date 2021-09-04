# **Quick Sort** 


<br>

## **Quick Sort** 

![quick](https://user-images.githubusercontent.com/63101648/132096582-4f6bf29b-98c6-48e1-91ad-60470d08680f.png)

1. 리스트 중 하나의 원소를 고른다 (= **pivot 지정**)
2. pivot 기준 **앞에는 작은 값**을 가진 원소들이, **뒤에는 큰 값**을 가진 원소들이 오도록 pivot을 기준으로 리스트를 둘로 나눈다.
    - 리스트가 둘로 나뉘는 것을 **분할**이라 함
    - 분할을 마치면 pivot은 움직이지 않는다.
3. 분할된 두 리스트에 대해 **재귀적으로 반복**한다.


<br>

## **Quick Sort 특징**
### - **장점**
- 속도가 빠름
- 추가 메모리 공간을 필요로 하지 않는다.

### - **단점** 
- 정렬된 리스트에 대해서는 퀵 정렬의 불균형 분할에 의해 오히려 수행시간이 더 오래걸린다.
- pivot을 선택할 때 불균형 분할을 방지하기 위해 리스트를 균등하게 분할할 수 있는 데이터를 선택해야한다.
    Ex) 리스트 내의 몇 개의 데이터 중 크기순으로 중간 값을 pivot으로 선택한다. 

<br>

## **Quick Sort의 시간복잡도**
- **Best** : nlog2n
- **Avg** : nlog2n
- **Worst** : n^2

<br>


### 출처
- https://gmlwjd9405.github.io/2018/05/10/algorithm-quick-sort.html
- https://velog.io/@roro/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%ED%80%B5%EC%A0%95%EB%A0%AC-%ED%9E%99%EC%A0%95%EB%A0%AC-%EC%9C%84%EC%83%81-%EC%A0%95%EB%A0%AC
- https://coding-factory.tistory.com/137