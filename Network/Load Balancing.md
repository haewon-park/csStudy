# Load Balancing(로드 밸런싱)
## 로드 밸런싱이란?
- 네트워크 또는 서버에 가해지는 **로드를 분산** 해주는 기술
- 중앙처리장치 혹은 저장장치와 같은 컴퓨터 자원들에게 **작업을 나누는 것**을 의미 

<br>

## Load Balancer(로드 밸런서)
- 로드밸런싱 기술을 제공하는 **서비스 또는 장치**
- 클라이언트와 네트워크 트래픽이 집중되는 서버들 또는 네트워크 허브 사이에 위치

<br>

## Load Balancer 종류
### **(1) L4 로드 밸런싱**
![l4](https://user-images.githubusercontent.com/63101648/125741001-501ec659-dbde-4cd5-8bec-bbe131fb5030.png)

- **전송 계층**에서 로드를 분산한다.
- **IP주소나 포트번호, MAC주소** 등에 따라 트래픽을 나누고 분산처리 하는 것이 가능 
- CLB(Connection Load Balancer) 혹은 SLB(Session Load Balancer)라고 부르기도 한다.

<br>

### **(2) L7 로드 밸런싱**
![l7](https://user-images.githubusercontent.com/63101648/125741034-5ca914f9-27cc-42ed-ac14-7b38a3c6c3c8.png)

- **애플리케이션 계층**에서 로드를 분산한다. 
- OSI 7계층의 프로토콜(HTTP, SMTP, FTP 등)을 바탕으로도 분산 처리 가능 

<br>

## **특징 한 눈에 비교하기**
![로드밸런서](https://user-images.githubusercontent.com/63101648/125739575-c334b8c0-ddfb-497c-97cd-165a07f14098.png)


<br>

## Load Balancing Algorithm
### **1. 라운드 로빈**
서버에 들어온 요청을 **순서대로** 돌아가며 배정하는 방식

### **2. 가중 라운드로빈 방식**
각 서버에 가중치를 매기고 **가중치가 높은 서버에 요청을 우선적으로** 배정하는 방식

### **3. 최소 연결 방식**
**가장 적은 연결 상태**를 보이는 서버에 트래픽을 배정하는 방식

### **4. IP 해시 방식**
클라이언트의 **IP주소를 hashing**하여 분배하는 방식 
