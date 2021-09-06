# Bubble Sort & Selection Sort & Insertion Sort
## 1. Bubble Sort  
### Bubble Sort란?  
> 서로 인접된 두 원소의 대소를 비교하고, 조건에 맞지 않다면 자리를 교환하며 정렬하는 알고리즘

![img](https://github.com/GimunLee/tech-refrigerator/raw/master/Algorithm/resources/bubble-sort-001.gif)
<br>
<br>  

**시간 & 공간 복잡도**  
|  | Bubble Sort |  
|---------| -------------------- |  
| 시간복잡도 | O(n^2) |  
| 공간복잡도 |O(n) |   
<br>  

### 장단점  
**장점**  
- 구현이 매우 간단
- 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 X ⇒  `제자리 정렬(in-place sorting)`
- **안정 정렬(Stable Sort)** 
 
**단점**  
-   시간복잡도가 최악, 최선, 평균 모두 O(n^2)으로, 굉장히 비효율적
-  정렬 돼있지 않은 원소가 정렬 됐을때의 자리로 가기 위해서, 교환 연산(swap)이 많이 일어남.
<br>

**Code**  
```Java
void bubbleSort(int[] arr) {
    int temp = 0;
	for(int i = 0; i < arr.length; i++) {       // 1.
		for(int j= 1 ; j < arr.length-i; j++) { // 2.
			if(arr[j-1] > arr[j]) {             // 3.
                // swap(arr[j-1], arr[j])
				temp = arr[j-1];
				arr[j-1] = arr[j];
				arr[j] = temp;
			}
		}
	}
	System.out.println(Arrays.toString(arr));
}
```
<br>  

## 2. Selection Sort  
### Selection Sort란?  
> 해당 순서에 원소를 넣을 위치는 이미 정해져 있고, 어떤 원소를 넣을지 선택하는 알고리즘

![img](https://github.com/GimunLee/tech-refrigerator/raw/master/Algorithm/resources/selection-sort-001.gif)
<br>
<br>  

**시간 & 공간 복잡도**  
|  | Selection Sort |  
|---------| -------------------- |  
| 시간복잡도 | O(n^2) |  
| 공간복잡도 |O(n) |   
<br>  

### 장단점  
**장점**  
- Bubble sort와 마찬가지로 알고리즘이 단순
-  정렬을 위한 비교 횟수는 많지만, Bubble Sort에 비해 실제로 교환하는 횟수는 적기 때문에 많은 교환이 일어나야 하는 자료상태에서 비교적 효율적
-   Bubble Sort와 마찬가지로 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 X ⇒ `제자리 정렬(in-place sorting)`
 
**단점**  
-   시간복잡도가 `O(n^2)`으로, 비효율적
-   **불안정 정렬(Unstable Sort)** 
<br>

**Code**  
```Java
void selectionSort(int[] arr) {
    int indexMin, temp;
    for (int i = 0; i < arr.length-1; i++) {        // 1.
        indexMin = i;
        for (int j = i + 1; j < arr.length; j++) {  // 2.
            if (arr[j] < arr[indexMin]) {           // 3.
                indexMin = j;
            }
        }
        // 4. swap(arr[indexMin], arr[i])
        temp = arr[indexMin];
        arr[indexMin] = arr[i];
        arr[i] = temp;
  }
  System.out.println(Arrays.toString(arr));
}
```
<br>  
 
## 3. Insertion Sort  
### Insertion Sort란?  
> 2번째 원소부터 시작하여 그 앞(왼쪽)의 원소들과 비교하여 삽입할 위치를 지정한 후, 원소를 뒤로 옮기고 지정된 자리에 자료를 삽입하여 정렬하는 알고리즘

![img](https://github.com/GimunLee/tech-refrigerator/raw/master/Algorithm/resources/insertion-sort-001.gif)
<br>
<br>  

**시간 & 공간 복잡도**  
|  | Insertion Sort |  
|---------| -------------------- |  
| 시간복잡도 | O(n^2) |  
| 공간복잡도 |O(n) |   
<br>  

### 장단점  
**장점**  
-   알고리즘이 단순
-   대부분의 원소가 이미 정렬되어 있는 경우, 매우 효율적
-   정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 X ⇒ `제자리 정렬(in-place sorting)`
-   **안정 정렬(Stable Sort)** 
-   Selection Sort나 Bubble Sort과 같은 `O(n^2)` 알고리즘에 비교하여 상대적으로 빠름
    
**단점**  
-  평균과 최악의 시간복잡도가 `O(n^2)`으로 비효율적
-   Bubble Sort와 Selection Sort와 마찬가지로, 배열의 길이가 길어질수록 비효율적
<br>

**Code**  
```Java
void insertionSort(int[] arr)
{
   for(int index = 1 ; index < arr.length ; index++){ // 1.
      int temp = arr[index];
      int prev = index - 1;
      while( (prev >= 0) && (arr[prev] > temp) ) {    // 2.
         arr[prev+1] = arr[prev];
         prev--;
      }
      arr[prev + 1] = temp;                           // 3.
   }
   System.out.println(Arrays.toString(arr));
}
```
<br>  

---
**참고 자료**
* https://gyoogle.dev/blog/algorithm/Bubble%20Sort.html
* https://gyoogle.dev/blog/algorithm/Selection%20Sort.html
* https://gyoogle.dev/blog/algorithm/Insertion%20Sort.html
