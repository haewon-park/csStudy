## 시스템 콜(System Call)
### 🌟 알고 가기! 🌟
**커널 모드란?**
> 프로세서의 특권 레벨로 프로세서의 모든 명령을 처리하며 시스템의 자원이나 하드웨어를 직접적으로 엑세스하여 컨트롤할 수 있는 모드. 
> 실제 장치 드라이버나 운영체제 프로그램이 구동하는 모드

**사용자 모드란?**
> 일반 응용 프로그램이 동작하는 비특권 모드.
> 시스템의 자원이나 하드웨어를 직접적으로 컨트롤 할 수 없으며 이를 하기 위해서는 **시스템 콜**을 사용해야 한다.

##

### 1. 시스템 콜(System Call) 이란? 🌟
**정의**
> 커널 영역의 기능을 사용자 모드가 사용 가능하도록! 
> ⇒ 즉, 프로세스가 하드웨어에 직접 접근해서 필요한 기능을 사용할 수 있게 해주는 것. 

![img](https://t1.daumcdn.net/cfile/tistory/23791D3B55CC38683A)

##

### 2. 시스템 콜(System Call)과 인터럽트(Interrupt)
* 시스템 콜은 소프트웨어가 발생시키는 [**동기적 인터럽트인 trap**](https://github.com/haewon-park/csStudy/blob/main/OS/%EC%9D%B8%ED%84%B0%EB%9F%BD%ED%8A%B8%20.md)의 한 종류로 볼 수 있다. 

##
### 3. 시스템 콜(System Call)의 유형
1. 프로세스 제어: 프로세스 특권 모드를 사용하여 직접적으로 프로세스 제어가 가능
2. 파일 조작 : 파일을 생성하거나 삭제, 관리 등
3. 장치 관리 : 장치 요구 및 장치 해제, 읽기, 쓰기, 재배치 등
4. 정보 유지: 시간과 날짜의 설정과 획득, 시스템 자료의 설정과 획득
5. 통신 : 통신 연결의 생성 및 제거, 메시지의 송수신, 상태 정보 전달 등

##
### 4. 대표적인 시스템 콜(System Call)
**1) Fork()**
> 새로운 프로세스를 생성할 때 사용. 
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(int argc, char *argv[]) {
    printf("pid : %d", (int) getpid()); // pid : 29146
    
    int rc = fork();					// 주목
    
    if (rc < 0) {
        exit(1);
    }									// (1) fork 실패
    else if (rc == 0) {					// (2) child 인 경우 (fork 값이 0)
        printf("child (pid : %d)", (int) getpid());
    }
    else {								// (3) parent case
        printf("parent of %d (pid : %d)", rc, (int)getpid());
    }
}
```
[output]
```
pid : 29146
parent of 29147
child (pid : 29147)
```

* fork()가 실행되는 순간. 프로세스가 하나 더 생기는데, 이 때 생긴 자식(child) 프로세스는 fork를 만든 부모(parent) 프로세스와 (거의) 동일한 복사본을 갖게 됨.
* **이 때, 운영체제는 위와 똑같은 2개의 프로그램이 동작한다고 생각하고, fork()가 return될 차례라고 생각한다. ⇒  따라서, 자식(child) 프로세스는 main이 아닌 if문부터 시작하게 되는 것.**
* 자식(child) 부모(parent) 프로세스의 fork() 값이 다르다는 점 ⇒ 따라서, 완전한 동일한 복사본이라고 할 수 없음.
* **둘 중 누가 먼저 실행될지는 알 수 없음. 스케줄러가 결정하는 것**

```
Parent의 fork()값 ⇒ child의 pid 값

Child의 fork()값 ⇒ 0
```
<br>

**2) wait()**
> 자식(child) 프로세스가 종료될 때까지 기다리는 작업
위의 예시에 int wc = wait(NULL)만 추가함.

```C
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main(int argc, char *argv[]) {
    printf("pid : %d", (int) getpid()); // pid : 29146
    
    int rc = fork();					// 주목
    
    if (rc < 0) {
        exit(1);
    }									// (1) fork 실패
    else if (rc == 0) {					// (2) child 인 경우 (fork 값이 0)
        printf("child (pid : %d)", (int) getpid());
    }
    else {								// (3) parent case
        int wc = wait(NULL)				// 추가된 부분
        printf("parent of %d (wc : %d / pid : %d)", wc, rc, (int)getpid());
    }
}
```
```
pid : 29146

child (pid : 29147)

parent of 29147 (wc : 29147 / pid : 29146)
```
* wait를 통해서 자식(child)의 실행이 끝날 때까지 기다림.
* 부모(parent)가 먼저 실행되더라도, wait()는 자식(child)가 끝나기 전에는 return 하지 않으므로, 반드시 자식(child)가 먼저 실행됨.
<br>

**3) exec()**
>  단순 fork()는 동일한 프로세스의 내용을 여러번 동작할 때 사용.
>  자식(child)에서는 부모(parent)와 다른 동작을 하고 싶을 때는 exec를 사용!
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main(int argc, char *argv[]) {
    printf("pid : %d", (int) getpid()); // pid : 29146
    
    int rc = fork();					// 주목
    
    if (rc < 0) {
        exit(1);
    }									// (1) fork 실패
    else if (rc == 0) {					// (2) child 인 경우 (fork 값이 0)
        printf("child (pid : %d)", (int) getpid());
        char *myargs[3];
        myargs[0] = strdup("wc");		// 내가 실행할 파일 이름
        myargs[1] = strdup("p3.c");		// 실행할 파일에 넘겨줄 argument
        myargs[2] = NULL;				// end of array
        execvp(myarges[0], myargs);		// wc 파일 실행.
        printf("this shouldn't print out") // 실행되지 않음.
    }
    else {								// (3) parent case
        int wc = wait(NULL)				// 추가된 부분
        printf("parent of %d (wc : %d / pid : %d)", wc, rc, (int)getpid());
    }
}
```
* exec()가 실행되면 execvp( 실행 파일, 전달 인자 ) 함수는 code segment 영역에 실행 파일의 코드를 읽어와서 덮어 씌움.
* 이후, heap, stack, 다른 메모리 영역이 초기화되고, OS는 그냥 실행
⇒ **즉, 새로운 프로세스를 생성하지 않고, 현재 프로그램에 wc라는 파일을 실행**
⇒ execvp() 이후의 부분은 실행X

---

**참고 자료**
* https://gyoogle.dev/blog/computer-science/operating-system/System%20Call.html
* https://velog.io/@woo00oo/%EC%8B%9C%EC%8A%A4%ED%85%9C-%EC%BD%9CSystem-Call
