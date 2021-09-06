## Count Sort
### Count Sort란?
>**(값의) 크기를 기준으로** 세는 알고리즘

`범위 조건`이 있는 경우에 한해서 굉장히 빠른 알고리즘이다. _Ex) 모든 데이터가 1부터 5 사이에 속한다_

- 시간복잡도 : `O(N)`

<br>

### 과정

1. 최댓값의 값만큼 count배열을 선언한다. (데이터의 값의 최댓값이 5라면 `int count[5]`)
2. counting 배열로 각 숫자가 몇번 등장하는지 센다.
3. counting 배열을 누적합으로 만든다.
4. 뒤에서부터 counting 배열을 돌면서, 해당하는 값의 인덱스에 값을 넣어준다.

<br>

#### 애니메이션으로 이해하기

![](https://images.velog.io/images/yanghl98/post/f389cf08-c72e-40d3-9993-d417867c1253/image.png)
![](https://images.velog.io/images/yanghl98/post/1c342cf2-2d82-4c47-ad7e-da81d6c5a96a/image.png)
![](https://images.velog.io/images/yanghl98/post/ca0db5f2-c1ee-4369-b0b2-209287405a29/image.png)

[링크](https://www.cs.miami.edu/home/burt/learning/Csc517.091/workbook/countingsort.html)

<br>

### 코드
```java
int arr[5]; 		// [5, 4, 3, 2, 1]
int sorted_arr[5];
// 과정 1 - counting 배열의 사이즈를 최대값 5가 담기도록 크게 잡기
int counting[6];	// 단점 : counting 배열의 사이즈의 범위를 가능한 값의 범위만큼 크게 잡아야 하므로, 비효율적이 됨.

// 과정 2 - counting 배열의 값을 증가해주기.
for (int i = 0; i < arr.length; i++) {
    counting[arr[i]]++;
}
// 과정 3 - counting 배열을 누적합으로 만들어주기.
for (int i = 1; i < arr.length; i++) {
    counting[i] += counting[i - 1];
}
// 과정 4 - 뒤에서부터 배열을 돌면서, 해당하는 값의 인덱스에 값을 넣어주기.
for (int i = arr.length - 1; i >= 0; i--) {
    sorted_arr[counting[arr[i]]] = arr[i];
    counting[arr[i]]--;
}
```

<br>

## 출처
https://bowbowbow.tistory.com/8<br>
https://github.com/gyoogle/tech-interview-for-developer/blob/master/Algorithm/Sort_Counting.md
