### OSI 7계층이란?
<br>

#### 정의
>컴퓨터 네트워크 프로토콜 디자인과 통신을 계층으로 나누어 설명한 것
<br>

#### 계층을 나누는 이유
처음 네트워크에 대한 표준이 없을 땐, 장비 간 호환이 잘 되지 않는 문제점이 있었다. <br>

*즉, LG 장비랑 Samsung 장비랑 같이 못쓰는거 ㅋ* 

그래서 네트워크를 7계층으로 분리하면서 **표준**을 만들게 됐는데, 이게 바로 `OSI 7 계층`이다.
간략하게 말하면 서로 통신할 수 있게 규칙을 만든 것!

보내는 쪽에서는 데이터를 안전하고, 정확하고, 신속하게 규격화 즉 **포장하는 방법**이 필요하고, 받는 쪽에서는 그 데이터를 안전하고 정확하고 신속하게 **해석하는 방법**이 필요한 것.

<br><br>

### OSI 7계층 구조
#### 전체적인 흐름
![](https://images.velog.io/images/yanghl98/post/5d3ce03a-249a-4c31-9682-ed8f2042e0b4/image.png)

`~H는 header, ~T는 tail`


위 그림을 보면, 응용계층에서 내려온 데이터부터 시작해서 계속 헤더가 붙는 것을 알 수 있다.
헤더에는 <span style="color:#FF8224">해당 계층의 기능과 관련된 제어 정보가 포함</span> 되어 있다.

제어 정보들을 모두 운영체제가 제공하는 프로토콜에 의해 송신 측에서는 계층을 지날 때마다 덧붙여서 추가되고(`Encapsulation`), 수신 측에서는 계층을 지날 때마다 제거된다(`Decapsulation`).
<br><br>

#### PDU(Protocol Data Unit)란?

_데이터 통신에서 상위 계층이 전달한 데이터에 붙이는 제어정보_

데이터에 어떤 헤더를 붙혔느냐에 따라 이름이 달라진다. 
즉, 데이터 자체는 동일하지만 각 레이어를 거치면서 헤더 정보가 추가되면서 이름이 달라진다.<br>
`2계층-프레임(Frame)` `3계층-패킷(Packet)` `4계층-세그먼트(Segment)` 
<br><br>

<img src="https://images.velog.io/images/yanghl98/post/038657f9-cbe0-42c5-83e8-26fe4d3600bc/image.png" width='500px'>



#### 1) 물리계층 (Phisical Layer)

- 실제 장치들을 연결하기 위해 필요한 전기적, 물리적 세부 사항들을 정의하는 계층
- 단지 데이터를 전기적인 신호(0, 1)로 변환해서 전달만 함
- 데이터의 종류나 오류를 제어하지 않음
- 즉, **데이터를 전송하는 역할만 진행**
- 장비 : 케이블, 허브(Hub), 리피터(Repeater)
<br>

#### 2) 데이터 링크 계층 (Data Link Layer)

- 링크의 설정과 유지 및 종료를 담당
- 물리 계층으로 송수신되는 정보를 관리하여 안전하게 전달되도록 도와주는 역할
- Mac 주소를 통해 통신, 프레임에 Mac 주소를 부여하고 **에러검출, 재전송, 흐름제어**를 진행함
- 장비 : 스위치(Switch), 브리지(Bridge) -> 여기서 MAC 주소 사용함
<br>


#### 3) 네트워크 계층 (Network Layer)

- **라우팅 알고리즘을 사용하여 최적의 경로를 선택**
- 이때, 전송되는 데이터는 패킷 단위로 분할하여 전송한 후 다시 합쳐진다. 
- 데이터를 **목적지까지 가장 안전하고 빠르게** 전달하는 기능을 담당함
(2계층이 노드 대 노드 전달을 감독한다면, 3계층은 각 패킷이 목적지까지)
- 라우팅, 패킷 포워딩, 인터네트워킹 등을 수행
- 프로토콜 : IP, ARP, RARP, ICMP, IGMP, 라우팅 프로토콜
- 장비 : 라우터(Router), L3 스위치
<br>

#### 4) 전송 계층 (Transport Layer)

- 양종단 호스트 내 프로세스 상호 간에 **신뢰적인 연결지향성** 서비스를 제공
- End-to-End 간 제어와 에러를 관리
- 패킷의 전송이 유효한지 확인하고 전송에 실패된 패킷을 다시 보내는 것과 같은 신뢰성있는 통신을 보장
- 주소 설정, 오류 및 흐름 제어, 다중화를 수행
- 프로토콜 : TCP, UDP
- 장비 : 게이트웨이, L4 스위치
<br>

#### 5) 세션 계층 (Session Layer)

- **TCP/IP 세션 설정, 유지, 종료, 전송 중단시 복구**하는 역할
- 통신 중 연결이 끊어지지 않도록 유지시켜줌
- 프로토콜 : NetBIOS, SSH, TLS

<br>

#### 6) 표현 계층 (Presentation Layer)

- 받은 데이터를 코드 변환, 구문 검색, 암호화, 압축의 과정을 통해 올바른 **표준방식으로 변환**하는 역할
- 예를 들면, EBCDIC로 인코딩된 문서 파일을 ASCII로 인코딩된 파일로 바꿔 주는 것, 
해당 데이터가 TEXT인지, 그림인지, GIF인지 JPG인지의 구분하는 것
- 프로토콜 : SSL, SSH, IMAP, FTP, MPEG, JPEG

<br>

#### 7) 응용 계층 (Application Layer)
- 사용자와 바로 연결되어 있으며 응용 SW를 도와주는 계층
- 파일 전송, 메일 전송 등 여러가지 **응용 서비스를 네트워크에 연결해주는 역할**
- 사용자 인터페이스, 전자우편, 데이터베이스 관리 등의 서비스를 제공
- 프로토콜 : HTTP, FTP, SMTP, POP3, IMAP, Telnet, DNS
<br><br>


### 암기해야 할 것 !!
- 물데네전세표응
<br>


### 출처
https://ko.wikipedia.org/wiki/OSI_%EB%AA%A8%ED%98%95

https://velog.io/@poiuyy0420/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-OSI-7-%EA%B3%84%EC%B8%B5-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC

https://velog.io/@hidaehyunlee/%EB%8D%B0%EC%9D%B4%ED%84%B0%EA%B0%80-%EC%A0%84%EB%8B%AC%EB%90%98%EB%8A%94-%EC%9B%90%EB%A6%AC-OSI-7%EA%B3%84%EC%B8%B5-%EB%AA%A8%EB%8D%B8%EA%B3%BC-TCPIP-%EB%AA%A8%EB%8D%B8

https://velog.io/@hidaehyunlee/%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%84%B8%EA%B7%B8%EB%A8%BC%ED%8A%B8-%ED%8C%A8%ED%82%B7-%ED%97%B7%EA%B0%88%EB%A6%B4-%EB%95%90-PDU%EB%A5%BC-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90

https://shlee0882.tistory.com/110
