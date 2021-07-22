### Process Management
> 프로세스가 여러 개일 때, CPU 스케줄링을 통해 프로세스들을 관리하는 것

이때, CPU는 각 프로세스들이 누군지 알아야 관리가 가능하다.
이러한 프로세스들의 특징을 갖고 있는 것이 바로 _**Process Metadata**_ 이다.

#### Process Metadata 구성 요소
- Process ID (PID)
- Process State (프로세스 상태)
- Process Priority (스케줄링 정보)
- CPU Registers
- Owner (계정 정보)
- CPU Usage
- Memeory Usage

이 메타데이터는 프로세스가 생성되면 PCB에 저장된다.

<br>

## PCB
> 프로세스 메타데이터들을 저장해 놓는 곳

![image](https://user-images.githubusercontent.com/44565524/126703560-6d390c3a-d76c-410d-a24d-6aa05aeaabeb.png)

#### 진행 과정
1. 프로그램 실행
2. 프로세스 생성
3. 프로세스 주소 공간에 코드, 데이터, 스택 생성
4. 이 프로세스의 메타데이터들이 PCB에 저장

![image](https://user-images.githubusercontent.com/44565524/126705396-dcf1ecee-bdd0-40f6-96e8-3d9ed05c20f4.png)

- Process State: 프로세스 상태 (Create, Ready, Running, Waiting, Terminated)
- Program Counter: 다음 실행할 명령어 주소
- CPU registers: 여러 범용 목적의 레지스터들 (accumulator, index register, stack pointers, general purpose registers)

<br>

### PCB는 어떻게 관리되나?
**Linked List 방식**으로 관리한다. PCB List Head에 PCB들이 생성될 때마다 붙게 된다.

`PCB List Head` -> `PCB1` -> `PCB2` -> `PCB3`

주소값으로 연결이 이루어져 있는 연결리스트이기 때문에 삽입 삭제가 용이하다.
즉, 프로세스가 생성되면 해당 PCB가 생성되고 프로세스 완료시 제거된다.

<br>

## Context Switching
> CPU가 이전의 프로세스 상태를 PCB에 보관하고, 또 다른 프로세스의 정보를 PCB에서 읽어서 레지스터에 적재하는 과정

보통 인터럽트가 발생하거나, 실행 중인 CPU 사용 허가시간을 모두 소모하거나, 입출력을 위해 대기해야 하는 경우에 Context Switching이 발생한다.

### Context Switching이 왜 필요한가?
- 컴퓨터가 매번 하나의 Task만 처리할 수 있다면 반응 속도가 매우 느리고 불편하기 때문에
- 빠른 속도로 Task를 바꿔가며 실행하면 사람들에겐 실시간으로 보이게 할 수 있기 때문에

![image](https://user-images.githubusercontent.com/44565524/126708805-c9659884-5fff-4186-897e-34aded1614e5.png)

### Context Switching의 Overhead
Context Switching에 걸린 시간과 메모리를 말한다.

I/O 이벤트가 발생했을 때 디스크에 명령을 내렸는데 끝날 때까지 기다리면서 CPU가 가만히 있으면 CPU가 낭비된다. 때문에 다른 프로세스로 바꾸면서까지 CPU를 더 사용하는게 이익이다.

**overhead를 감수하면서 기존 프로세스를 새 프로세스로 바꾸는 것이 더 낫다.**

<br>

### 스레드 vs 프로세스
스레드는 Context Switching 될 때 text, data, heap 영역은 프로세스 것이기 때문에 자신의 PCB에는 stack 및 간단한 정보만 저장하기에 프로세스 컨텍스트 스위칭보다 빠르다.

<br>

#### 참고 링크
https://m.blog.naver.com/adamdoha/222019884898
https://jhnyang.tistory.com/33
