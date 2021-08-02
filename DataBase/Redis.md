![](https://images.velog.io/images/hammii/post/54d9ca76-8a97-4223-aba9-07ebef51d71a/banner-1544x500.png)

### Redis
- **Re**mote **Di**ctionary **S**erver의 약자
- "키-값" 구조의 비정형 데이터를 저장하고 관리하기 위한 오픈 소스 기반의 비관계형 데이터베이스 관리 시스템

<br>

### Redis 특징
- 오픈소스 소프트웨어
- 디스크가 아닌 메모리 기반 데이터 저장소
- NoSQL & Cache 솔루션

보통 데이터베이스는 보조기억장치(SSD, 하드디스크)에 저장하지만 Redis는 메모리(RAM)에 저장해서 디스크 스캐닝이 필요 없어 매우 빠르다.

<br>

### 데이터 타입
- String
- Set
- Sorted Set
- Hash
- List

<br>

### 데이터 저장 방법
- snapshotting (RDB): 순간적으로 메모리에 있는 내용을 DISK에 전체를 옮겨 담는 방식
- AOF(Append Only File): redis의 모든 write/update 연산 자체를 모두 log 파일에 기록하는 형태. 서버가 재시작될때 기록된 write/update 연산을 순차적으로 재실행하여 데이터를 복구한다.

<br>

#### 참고 링크
https://codingmania.tistory.com/18

https://bcho.tistory.com/654
