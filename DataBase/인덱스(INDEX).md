![image](https://user-images.githubusercontent.com/44565524/127948541-b88030b7-90a9-4628-84f0-d0d092ebbc24.png)

### 인덱스 (INDEX)
> 테이블에 대한 동작의 속도를 높여주는 자료 구조

<br>

### 인덱스 사용 이유
- RDBMS에서 검색 속도를 높이기 위해
- 데이터베이스 안의 레코드를 처음부터 풀스캔하지 않고, `B+ Tree`로 구성된 구조에서 Index 파일 검색으로 속도를 향상시킨다.

<br>

### 인덱스 사용 시 단점
- Index 생성시, .mdb 파일 크기가 증가한다.
- 한 페이지를 동시에 수정할 수 있는 **병행성**이 줄어든다.
- 인덱스 된 필드에서 데이터를 업데이트하거나, 레코드를 추가 또는 삭제시 성능이 떨어진다.
- 인덱스가 데이터베이스 공간을 차지해 추가적인 공간이 필요해진다. (DB의 10퍼센트 내외의 공간이 추가로 필요)

<br>

### 언제 사용해야 할까?
- 사용하면 좋은 경우
   - Where 절에서 자주 사용되는 Column
   - 외래키가 사용되는 Column
   - Join에 자주 사용되는 Column
   
- 사용을 피해야 하는 경우
   - Data 중복도가 높은 Column
   - DML이 자주 일어나는 Column

<br>

### DML이 일어났을 때 상황
- INSERT
   - 기존 Block에 여유가 없을 때, 새로운 Data가 입력된다.<br>
   → 새로운 Block을 할당 받은 후, Key를 옮기는 작업을 수행한다.<br>
   → Index split 작업 동안, 해당 Block의 Key 값에 대해서 DML이 블로킹 된다. (대기 이벤트 발생)
- DELETE
   - 테이블: 데이터가 지워지고, 다른 데이터가 그 공간을 사용 가능하다.
   - 인덱스: 데이터가 지워지지 않고, 사용 안 됨 표시만 해둔다.
- UPDATE
   - 테이블: update 수행
   - 인덱스: delete가 발생한 후, 새로운 작업의 insert 수행 (2배의 작업이 소요됨)

<br>

#### 참고 링크
https://ko.wikipedia.org/wiki/%EC%9D%B8%EB%8D%B1%EC%8A%A4_(%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4)

https://lalwr.blogspot.com/2016/02/db-index.html
