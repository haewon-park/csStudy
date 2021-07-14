# UDP
*데이터를 보내기 위해  Transport 계층에서 사용하는 프로토콜인 TCP, UDP 중 하나*

![img](https://t1.daumcdn.net/cfile/tistory/99F6363359FDDC9E1F)

## 1. UDP  vs TCP
**UDP (User Datagram Protocol)**
> 정의: 데이터를 데이터 그램 단위로 처리하는 프로토콜

**UDP의 특징**
* 비연결형 서비스로 *데이터 그램 방식* 을 제공한다.
* 정보를 주고 받을 때, 정보를 보내거나 받는다는 신호 절차를 거치지 않는다.
* 연결 자체가 없기에 서버 소켓과 클라이언트 소켓의 구분이 없다.
* UDP 헤더의 CheckSum 필드를 통해 최소한의 *오류만 검출한다.
* 낮은 신뢰성
* TCP 보다 빠른 속도
* *따라서, 신뢰성보다도 연속성이 중요한 서비스에서 주로 사용된다.*
* ex) 스트리밍 서비스(유튜브...)

## 
**TCP (Transmission Control Protocol)**
> 정의: 인터넷 상에서 데이터를 메세지 형태로 보내기 위해 IP와 함께 사용하는 프로토콜.

**TCP의 특징**
* *가상 회선 방식* 을 제공한다.
* 서버 소켓은 연결만을 담당한다.
* [3 - way handshaking 과정을 통해 연결을 설정하고, 4 - way handshaking 과정을 통해 해제한다.](https://github.com/haewon-park/csStudy/blob/main/Network/TCP%203-way%20%26%204-way%20Handshake.md) 
* 높은 신뢰성을 보장한다.
* UDP 보다 느린 속도.
* 전 이중(Full - Duplex), 점대점(Point to Point) 방식
* *따라서, 연속성보다 신뢰성있는 전송이 중요할 때 주로 사용한다.*
* ex) 파일 전송 

## 
**UDP와 TCP의 탄생 배경**
1. IP의 역할은 host to host 만을 지원하는데 host 에서 host 이동은 IP 로 가능하지만 하나의 장비 안에서 수많은 프로그램들이 통신하는 것은 IP 만으로 한계가 있었다. (*같은 IP 주소를 사용하니까!*)
2. IP에서 오류가 발생한다면 ICMP에서 알려주기만 할 뿐 대처를 못하기 떄문에 IP보다 윗단에서 처리해줘야 했다.
<pre><code>*ICMP: 인터넷 제어 메시지 프로토콜, 네트워크 컴퓨터 위에서 돌아가는 운영체제에서 오류 메세지를 전송받는데 주요 쓰임</code></pre>
3. 따라서, 1번을 해결하기 위해 port 번호, 2번을 해결하기 위해 TCP / UDP가 탄생하였다.
<br>

## 2. UDP Header
**UDP Header 구조**

![img](https://t1.daumcdn.net/cfile/tistory/99B12B385BD6DC0F03)
* Source Port: 출발지 포트 번호
* Destination Port: 도착지 포트 번호
* Total Length: Header + Data ⇒ 사용자 데이터그램의 전체 길이
* *CheckSum*: 오류 검출
<pre><code>*CheckSum: 중복 검사의 한 형태, 오류 정정을 통해 공간이나 시간 속에서 송신된 자료의 무결성을 보호하는 단순한 방법</code></pre>
<br>

## 3. DNS에서 UDP를 주로 사용하는 이유?
**DNS(Domain Name System)**
> 정의: 호스트의 도메인 이름을 호스트의 네트워크 주소로 바꾸거나 그 반대의 변환을 수행.
*ex) www.naver.com --> 192.168.1.0*

**DNS에서 UDP를 주로 사용하는 이유**
* 연결의 시작과 끝이 없다. ⇒ 연결 설정에 드는 비용이 없다.
	- 반면, TCP는 데이터 전송 시작 전 3 - way handshaking 사용
* 연결 설정을 유지할 필요가 없다. ⇒ 더 많은 클라이언트 수용 가능
	- 반면, TCP는 수신버퍼, 송신버퍼, congestion control parameter, sequence number, ACK number
* UDP Request는 UDP segement에 들어갈 정도로 작다.
* Request에 대한 손실은 Application Layer에서 제어가 가능하다.
	- Timeout 추가, Resend 작업을 통해

**DNS에서 TCP를 사용하는 경우**
* Zone transfer를 사용할 때
* 응답을 못받았을 때
* 데이터의 크기가 512 bytes를 넘었을 때
<pre><code>*Zone transfer: DNS 서버 간의 요청을 주고 받을 때 사용하는 transfer</code></pre>

*UDP, TCP 모두 사용 가능함으로 DNS는 UDP 53번, TCP 53번 포트를 사용한다.*
<br>
<br>

## 4. 오류 해결 방법
* UDP: TCP와 달리 오류가 날 수도 있고, 재전송이나 순서가 뒤바뀔 수 있어 어플리케이션에서 재처리해야 한다.
* TCP: 데이터의 분실, 중복, 순서 등을 자동으로 보정하기 때문에 송수신 데이터의 정확한 전달을 할 수 있도록 해준다.
