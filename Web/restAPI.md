# REST API
## 1. REST란? 
### 정의 🌟🌟🌟
> Representational State Transfer의 약자
> 즉, **HTTP URI**를 통해 자원을 명시하고, **HTTP Method**(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 **CRUD 연산**을 적용하는 것을 의미
> 
_어플리케이션 사이에 결합도를 낮추게끔 설계하는 아키텍처 스타일. 결합도를 낮춰 **서버, 클라이언트가 별도로 구축되고 결합**될 수 있게 하는 것._

<br>

### 필요성
* 애플리케이션 분리 및 통합
* 다양한 클라이언트의 등장
<br>

### 구성요소 🌟🌟🌟
1. **자원(Resource)**: `URI`
	* 지원을 구별하는 ID: URI
	* 모든 자원에 대한 ID가 존재하고, 이 자원은 서버에 존재
	* 클라이언트는 URI를 이용하여 자원을 지정하고, 해당 자원의 상태(정보)에 대한 조작을 서버에 요청
	
2. **행위(Verb, 동사)**: `HTTP Method`
    | Method | 의미   | Idempotent |
    | ------ | ------ | ---------- |
    | POST   | Create | No         |
    | GET    | Select | Yes        |
    | PUT    | Update | Yes        |
    | PATCH | Update | No        |
    | DELETE | Delete | Yes        |
    
    > Idempotent(멱등법칙) 이란? 연산을 여러 번 적용하더라도 결과가 달라지지 않는 성질
    
3. **표현(Representation of Resource)**
	* 클라이언트가 자원의 상태(정보)에 대한 조작을 요청하면 서버는 이에 적절한 응답을 보낸다.
	* REST에서 하나의 자원은 *JSON, XML, TEXT, RSS* 등 여러 형태 표현 가능
<br>

### 조건 🌟
1. `서버-클라이언트 구조`
	* 클라이언트와 서버가 서로 의존하지 않아도 된다.
⇒ 클라이언트는 서버의 리소스 URI만 알고 있으면 되기 때문에

2. `Stateless(무상태)` 
	* **클라이언트에서 서버로의 각 요청에는 그 요청을 이해하는데 필요한 모든 정보가 포함**되어야 한다.
	⇒ 따라서, 세션의 정보는 클라이언트가 가지고 있어야 한다.

3. `캐시 처리 가능` 
	* **요청에 대한 응답 내의 데이터에 해당 요청은 캐시가 가능한지 불가능한지 명시**해야한다.
	* 응답을 캐시할 수 있다면 클라이언트에서 동일한 요청이 왔을 때 응답 데이터를 재사용할 수 있어야 한다.
	* REST의 가장 큰 특징 중 하나는 HTTP라는 기존 웹표준을 그대로 사용하기 때문에, 웹에서 사용하는 기존 인프라를 그대로 활용이 가능하다. 따라서 HTTP가 가진 캐싱 기능이 적용 가능하다.

4. `계층화`
	* 계층화된 시스템 아키텍처를 사용하여 **각 구성들 간의 계층을 마음대로 상호작용할 수 없도록 제한함**으로서 인터페이스를 일원화할 수 있다.

5. `Uniform Interface(인터페이스 일관성)`
	* 전체적인 시스템 아키텍처를 간단하고 잘 파악할 수 있도록 하기 위한 약속된 인터페이스를 사용

6. `Code-On-Demand(optional)`
	* 서버가 클라이언트에 프로그램을 전달하면 클라이언트에서 실행될 수 있어야 한다.
<br>

### 장단점 🌟🌟
* *장점*
	* HTTP 프로토콜의 인프라를 그대로 사용하므로 REST API 사용을 위한 별도의 인프라 구축 필요 X
	* HTTP표준 프로토콜에 따르는 모든 플랫폼에서 사용 O
	* REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악 가능
	* 서버와 클라이언트의 역할을 명확하게 분리한다.
* *단점*
	* 표준 존재 X
	* 사용할 수 있는 메소드가 4가지 밖에 없다. (POST, GET, PUT, DELETE)
<br>

## 2. REST API란?
### 정의 🌟🌟🌟
> REST 기반으로 서비스 API를 구현한 것.
> 즉, HTTP 요청을 보낼 때, 어떤 URI에 어떤 메소드를 사용할지 개발자들 사이에 널리 지켜지는 약속

![img](https://www.altexsoft.com/media/2021/03/word-image.png)

*REST API를 사용한다고 해서 성능이 향상되지는 않는다. 일관적인 컨벤션과 API의 이해도 및 호환성을 높이는 것이 REST API의 목적*

<br>

### 특징
* 사내 시스템들도 REST 기반으로 시스템을 분산해 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 할 수 있다.
* REST는 HTTP 표준을 기반으로 구현하므로, HTTP를 지원하는 프로그램 언어로 클라이언트, 서버를 구현할 수 있다.
* 즉, REST API를 제작하면 델파이 클라이언트 뿐 아니라, 자바, C#, 웹 등을 이용해 클라이언트를 제작할 수 있다.
<br>

### 설계 기본 규칙
1. Resources
2. HTTP Methods
3. HTTP headers
4. Query parameters
5. Status Code
<br>

## 3. RESTful이란?
### 정의 🌟🌟🌟
> REST의 원리를 따르는 시스템을 의미
> 
<br>

### 목적
* 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것(API의 이해도 및 호환성 향샹)
* 성능이 중요한 상황에서는 굳이 RESTful한 API를 구현할 필요는 없다.
<br>

## 4. 참고 질문
**Q. REST vs SOAP**
| REST | Ajax |
| -------------------- | --------------- |
| - REST는 네트워크 기반의 소프트웨어 아키텍처를 위한 서비스 아키텍처 디자인 <br> - 다양한 데이터 형식 지원 <br> - REST 읽기는 캐싱 가능 <br> - REST 클라이언트는 방법을 표준화하는 방법을 알고 있어야 하며 응용 프로그램이 그 안에 들어있어야 함. <br> - SOAP보다 빠름 <br> - HTTP 헤더를 사용하여 메타 정보를 저장 | - SOAP은 두 컴퓨터가 XML 문서를 공유하여 통신하는 프로토콜 <br> - XML만 허용 <br> - SOAP 기반 읽기는 캐시 불가 <br> - SOAP 서버에 밀접하게 연결된 사용자 정의 데스크톰은 응용 프로그램과 같음 | 
<br>

**Q. REST vs Ajax**
| REST | Ajax |
| -------------------- | --------------- |
| - URL 구조와 요청 / 응답 패턴이 있어 자원 사용을 중심으로 함. <br> - REST는 사용자가 서버에서 데이터 또는 정보를 요청할 수 있는 소프트웨어 아키텍처 및 방법 유형 <br> - REST는 고객과 서버 간의 상호 작용을 필요로 한다. | - 요청을 XMLHttpRequest 객체를 사용하여 서버로 전송된다. 응답은 자바스크립트 코드에서 현재 페이지를 동적으로 변경하는데 사용된다. <br> - Ajax는 페이지를 다시 로드할 필요 없이 UI 일부분을 동적으로 업데이트 하는 기술이다. <br> - 클라이언트와 서버 간의 상호 작용을 비동기적으로 제거 한다. | 
<br>

**Q. JAX-WS / JAX-RS 란?**
* `JAX-WS`: JAVA에서 *SOAP 통신*을 수행하는데 사용할 수 있는 라이브러리
* `JAX-RS`: JAVA에서 *REST 통신*을 수행하는데 사용할 수 있는 라이브러리
<br>

**Q. PUT vs PATCH**
PUT은 통째로, PATCH는 부분 update할 때 사용

---

**참고 자료**
* **[응답 상태 코드](https://github.com/haewon-park/csStudy/blob/f482c3fc7668f143241d2b6ff5318115c91e6300/Web/HTTP%20Status%20Code.md)**
* https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html
* https://sabarada.tistory.com/26
* [RESTful 웹서비스 질문 목록](https://ko.myservername.com/top-20-restful-web-services-interview-question)
* [REST 디자인 가이드](https://gunju-ko.github.io/spring/2020/09/15/Rest-API-%EB%94%94%EC%9E%90%EC%9D%B8-%EA%B0%80%EC%9D%B4%EB%93%9C.html)
* https://velog.io/@ellyheetov/REST-API

