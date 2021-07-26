## Race condition

### 1. Race condition 이란? 🌟
**정의**
> 두 개 이상의 프로세스가 공유 자원에 동시에 접근할 때, 결과값에 영향을 줄 수 있는 상황

*동시 접근 시 자료의 일관성을 해치는 결과가 나타날 수 있음*

##

### 2. Race condition 이 발생하는 경우
**1) 커널 작업을 수행하는 중 인터럽트가 발생하는 경우**
  * 문제점: 커널모드에서 데이터를 로드하여 작업을 수행하다가 인터럽트가 발생하여 같은 데이터를 조작하는 경우 ⇒ 사용자 프로세스는 해당 프로세스에 할당 받은 메모리에만 존재할 수 있지만 커널은 서로 다른 프로세스가 공유하기 때문에 발생
  * 해결법: 커널모드에서 작업을 수행하는 동안 **인터럽트를 disable** 시켜 CPU 제어권을 가져가지 못하도록  한다.
<br>

**2) 프로세스가 시스템 콜(System Call)을 호출하여 커널 모드로 수행하는 도중 Context Switch가 발생하는 경우**
  * 문제점: 프로세스1이 커널모드에서 데이터를 조작하는 도중, 시간이 초과되어 CPU 제어권이 프로세스2로 넘어가 같은 데이터를 조작하는 경우
  * 해결법: 프로세스가 커널모드에서 작업을 하는 경우 시간이 초과되어도 CPU 제어권이 다른 프로세스에게 넘어가지 않도록 한다.
<br>

**3) 멀티 프로세서 환경에서 여러 프로세스가 공유 메모리 내 커널 안 변수에 접근하는 경우**
  * 문제점: 멀티 프로세서 환경에서 2개의 CPU가 동시에 커널 내부의 공유 데이터에 접근하여 조작하는 경우
  * 해결법: 커널 내부에 있는 각 공유 데이터에 접근할 때마다, 그 데이터에 대한 **lock/unlock**을 한다. ⇒ 매 순간 그 데이터에 접근하는 프로세스는 1개

##

### 3. Race condition 을 예방할 수 있는 방법🌟
* **[세마포어 (Semaphore)](https://github.com/haewon-park/csStudy/blob/ddf7b70602a194eee7444d738ea23b850e10615a/OS/%EC%84%B8%EB%A7%88%ED%8F%AC%EC%96%B4(Semaphore)%20&%20%EB%AE%A4%ED%85%8D%EC%8A%A4(Mutex).md)**
* **[뮤텍스 (Mutex)](https://github.com/haewon-park/csStudy/blob/ddf7b70602a194eee7444d738ea23b850e10615a/OS/%EC%84%B8%EB%A7%88%ED%8F%AC%EC%96%B4(Semaphore)%20&%20%EB%AE%A4%ED%85%8D%EC%8A%A4(Mutex).md)**

---

**참고 자료**
* https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/Race%20Condition.md
* https://javairus.tistory.com/44
