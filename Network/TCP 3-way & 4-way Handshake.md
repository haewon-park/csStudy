## TCP 3-way Handshake & 4-way Handshake

### 🤝 **3-way Handshake**

- Why? 장치들 사이에 논리적인 접속을 성립(establish)하기 위해

![image](https://user-images.githubusercontent.com/44565524/125661341-86cf1929-3293-4730-a092-55496a4aa5cf.png)

1. 클라이언트가 서버에게 SYN 패킷을 보냄 (sequence : x)
2. 서버가 SYN(x)을 받고, 클라이언트로 받았다는 신호인 ACK와 SYN 패킷을 보냄 (sequence : y, ACK : x + 1)
3. 클라이언트가 ACK(y+1)를 서버로 보내고 연결이 이루어짐

<br>

- SYN: synchronize sequence numbers
- ACK: acknowledgment

<hr>

### 🤝 **4-way Handshake**

- Why? 세션을 종료하기 위해

![image](https://user-images.githubusercontent.com/44565524/125661616-04417fd9-e2ea-4dfa-8dbf-55f33a4f80af.png)

1. 클라이언트가 서버에게 연결을 종료한다는 FIN 플래그를 보냄
2. 서버는 FIN을 받고, 확인했다는 ACK를 클라이언트에게 보냄 (이때 모든 데이터를 보내기 위해 CLOSE_WAIT 상태가 된다)
3. 데이터를 모두 보냈다면, 연결이 종료되었다는 FIN 플래그를 클라이언트에게 보냄
4. 클라이언트는 FIN을 받고, 확인했다는 ACK를 서버에게 보냄 (아직 서버로부터 받지 못한 데이터가 있을 수 있으므로 TIME_WAIT을 통해 기다린다)

- 서버는 ACK를 받은 이후 소켓을 닫는다 (Closed)
- TIME_WAIT 시간이 끝나면 클라이언트도 닫는다 (Closed)

<br>

**TIME_WAIT**: Client가 Server로부터 FIN을 수신하더라도 일정시간(디폴트 240초)동안 세션을 남겨놓고 잉여 패킷을 기다리는 과정
