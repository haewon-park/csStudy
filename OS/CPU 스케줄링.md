### 스케줄링이란?
> CPU를 잘 사용하기 위해 프로세스를 잘 배정하는 것

<br>

#### - 어떻게 스케줄링 해야 하는가?
처리율과 CPU 이용률 ↑

오버헤드, 응답시간, 반환시간, 대기시간, 기아 현상 ↓

<br>

### 프로세스 상태
![](https://images.velog.io/images/hammii/post/479c5903-1975-4255-a9b4-79beffc74e3c/image.png)

- `New`: **프로세스 생성 중**

프로세스를 생성하고 있는 단계로 커널 공간에 PCB가 만들어진 상태이다.

- `Ready`: **프로세스가 CPU를 기다리는 상태**

프로세스가 메모리에 적재된 상태로, 실행하는데 필요한 자원을 모두 얻은 상태이다.

- `Running`: **프로세스가 CPU를 할당받아 명령어를 수행 중인 상태**

일반적으로 CPU가 하나이기 때문에 여러 프로세스가 동시에 실행되어도 실제로 실행 중인 프로세스는 매 시점 하나뿐이다.

- `Waiting`: **프로세스가 어떤 사건(event)이 일어나기를 기다리는 상태**

프로세스가 실행하다가 할당받은 CPU를 반납하고 특별한 사건을 기다린다. (ex. I/O 작업)

- `Terminated`: **프로세스의 실행 종료**

프로세스의 실행이 완료되고 할당된 CPU를 반납한다.

<br>

### 프로세스의 상태 전이
- `승인 (Admitted)` : 프로세스 생성이 가능하여 승인받는 것
- `스케줄러 디스패치 (Scheduler Dispatch)` : 준비 상태에 있는 프로세스 중 하나를 선택하여 실행시키는 것
- `인터럽트 (Interrupt)` : 예외, 입출력, 이벤트 등이 발생하여 현재 실행 중인 프로세스를 Ready 상태로 바꾸고, 해당 작업을 먼저 처리하는 것
- `입출력 또는 이벤트 대기 (I/O or Event wait)` : 실행 중인 프로세스가 입출력이나 이벤트를 처리해야 하는 경우, 입출력/이벤트가 모두 끝날 때까지 Waiting 상태로 만드는 것
- `입출력 또는 이벤트 완료 (I/O or Event Completion)` : 입출력/이벤트가 끝난 프로세스를 준비 상태로 전환하여 스케줄러에 의해 선택될 수 있도록 만드는 것

<br>

### 선점 / 비선점 스케줄링
- **선점 스케줄링**: 하나의 프로세스가 CPU를 차지하고 있을 때, 우선순위가 높은 다른 프로세스가 현재 프로세스를 중단시키고 CPU를 점유하는 스케줄링 방식 (`I/O or Event wait`)
- **비선점 스케줄링**: 한 프로세스가 CPU를 할당받으면 작업 종료 후 CPU 반환 시까지 다른 프로세스는 CPU 점유가 불가능한 스케줄링 방식 (`Interrupt`, `Scheduler Dispatch`)

### CPU 스케줄링의 종류
- 선점 스케줄링
  - RR (Round Robin)
    - 비선점인 FCFS 알고리즘을 선점 형태로 변형한 기법
    - 할당된 시간 동안만 실행한 후, 실행이 완료되지 않으면 다음 프로세스에게 CPU를 넘겨주고 큐의 가장 뒤로 배치됨
    - 할당 시간이 크면 FCFS와 같게 되고, 작으면 문맥 교환(Context Switching) 잦아져서 오버헤드 증가
  - SRT (Shortest Remaining Time)
    - 비선점인 SJF 알고리즘을 선점 형태로 변경한 기법
    - 남은 실행 시간이 가장 짧은 프로세스가 먼저 수행
  - 다단계 큐 (Multi Level Queue)
    - 프로세스들을 여러 종류의 그룹으로 나누어 여러 개의 큐를 이용하는 기법
    ![](https://images.velog.io/images/hammii/post/bd9e00db-d18e-416c-812b-292faa79bf89/multilevelfeedbackqueue.png)
  - 다단계 피드백 큐 (Multi Level Feedback Queue)
    - 다단계 큐의 단점을 보완한 것으로, 큐마다 time out을 설정하여 시간 초과 시 우선순위가 낮은 다음 단계 큐로 이동하는 기법
    ![](https://images.velog.io/images/hammii/post/a6e955de-edea-4a7a-bd65-3110b2c4ab8c/multilevel-feedback-queue-scheduling.png)

- 비선점 스케줄링
  - FCFS (First Come First Served)
    - 큐에 도착한 순서대로 CPU 할당
    - 실행 시간이 짧은 게 뒤로 가면 평균 대기 시간이 길어짐
  - SJF (Shortest Job First)
    - 도착하는 시점에 따라 수행 시간이 가장 짧은 프로세스가 먼저 수행
    - FCFS 보다 평균 대기 시간 감소, 짧은 작업에 유리 
    - But, 기아 현상 발생 가능
  - HRN (Hightest Response-ratio Next)
    - 우선순위를 계산하여 기아 현상을 보완한 방법 (SJF의 단점 보완)
    - 우선순위 = (대기시간 + 실행 시간) / (실행 시간)

<br>

우선순위 스케줄링은 선점, 비선점 둘 다 가능하다. 우선순위가 낮은 프로세스가 무한정 기다리는 기아 현상이 발생 가능하지만, 에이징 방법으로 기아 현상 문제를 해결할 수 있다.

`에이징(Aging)`: 기다린 시간에 비례하여 일정 시간이 지나면 우선순위를 한 단계씩 높여 가까운 시간 안에 자원을 할당받도록 하는 기법


<br>


> 💡 현재 컴퓨터 시스템이 사용하는 방법은 '우선순위 + 라운드 로빈' 방식이다.

<br>

#### 참고 링크
https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/CPU%20Scheduling.md

https://kosaf04pyh.tistory.com/190

https://esoongan.tistory.com/81

https://jhnyang.tistory.com/132

https://colomy.tistory.com/120
