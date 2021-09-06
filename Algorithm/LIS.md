## LIS (Longest Increasing Sequence)

### 정의
>최장 증가 수열 : 가장 긴 증가하는 부분 수열

<br>

#### 예시
다음과 같은 수열이 있다면, 가장 긴 증가하는 부분 수열(LIS)는 `10, 20, 50, 90` 또는 `10, 20, 40, 60` 이다.
![](https://images.velog.io/images/yanghl98/post/b74d92b5-3823-45d3-8409-bc8f2d10709b/image.png)

- 주의할 점 : 항상 이전에 선택한 원소보다 커야하기 때문에 같은원소 역시 연속으로 선택할수 없다.

<br>

### 구현


#### 1. DP
- `dp[i]` = i보다 앞에 있는 작은 수(`j`=`i-1`~`0`) 중 가장 큰 값을 가지는 `dp[j]` + `1`
- 시간복잡도 : `O(N^2)`

```java
int arr[] = {7, 2, 3, 8, 4, 5};
int dp[] = new int[arr.length]; 


for(int i = 1; i < dp.length; i++) {
    for(int j = i-1; j>=0; j--) {
        if(arr[i] > arr[j]) {
            dp[i] = (dp[i] < dp[j]+1) ? dp[j]+1 : dp[i];
        }
    }
}

for (int i = 0; i < dp.length; i++) {
	if(max < dp[i]) max = dp[i];
}

// 저장된 dp 배열 값 : [0, 0, 1, 2, 2, 3]
// LIS : dp배열에 저장된 값 중 최대 값 + 1

```

<br>

#### 2. Lower Bound

Lower Bound란 정렬된 배열에서 찾고자 하는 값 이상이 처음으로 나타나는 위치를 말한다.
![](https://images.velog.io/images/yanghl98/post/d7c37eee-07d4-4a4b-a3ff-70d677e3e530/image.png)
- 즉, `처음으로 나타나는 자신보다 큰값` or `자신보다 큰 값들중 가장 작은 값`
- 이분탐색으로 lower bound를 찾아 리스트에 저장하며 LIS를 찾는 방법
  - 1. 현재 만든 시퀀스에서 lower bound를 찾아 그 위치에 해당 수로 바꿔준다.
  - 2. 만약 그러한 수가 없다면 가장 뒤에 추가를 해준다.

![](https://images.velog.io/images/yanghl98/post/5c9c9b94-a2ff-44af-ab9c-3848a3e91c29/image.png)
![](https://images.velog.io/images/yanghl98/post/a13431c0-4933-4260-b842-ae7c201582d8/image.png)

- 시간복잡도 : `O(NlogN)`


<br>
<br>

## 출처
https://source-sc.tistory.com/15?category=882382 (lower bound 방식) <br>
https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=jh20s&logNo=221310955726 (dp + lower bound)
