# OAuth
## 1. OAuth란? 🌟🌟🌟
### 정의 
> Open Authentication의 약자로 인터넷 사용자들이 비밀번호를 제공하지 않고, 다른 웹사이트 상의 자신들의 정보에 대해 웹사이트나 애플리케이션의 접근 권한을 부여할 수있는 개방형 표준 방법

<br>

_**왜 사용할까?**_

네이버 로그인, 카카오 로그인, 구글 로그인을 우리가 편리해서 사용하지만 기술적으로 네이버 로그인을 시도한 사람이 네이버 회원임을 어떻게 알 수 있을까?

간단한 방법으로 고객한테 네이버 회원 정보를 받아서 네이버에 로그인을 해보면 되지만 이는 너무 불편하기 때문에 `OAuth`가 생겼다.

`OAuth`는 고객이 자신의 네이버 회원 정보를 로그인 하고자 하는 서비스에 알려주지 않아도, **네이버에 있는 고객의 회원 정보**를 로그인하고자 하는 서비스에서 **안전하게** 사용하기 위한 방법

<br>

## 2. OAuth 2.0 
### 구성 🌟🌟🌟
* **Resource Owner**: User
* **Client**: Resource Server에 대한 액세스를 요청하는 프로그램(Resource Owner가 가입하고자 하는 사이트)
* **Resource Server(API Server)**: 자원을 호스팅하는 서버(ex. 카카오, 네이버 등)
* **Authorization Server**: 사용자의 동의를 받아서 권한을 부여하는 서버
<br>

### 토큰(Token) 🌟🌟
**1. 접근 토큰(Access Token)**
* 사용자의 데이터에 접근하기 위해 필요한 자격 증명으로서 사용자가 특정 앱에 부여한 권한에 대한 정보가 담긴 문자열
* 누구든지 유효한 접근 토큰을 보유하면 통제된 데이터에 접근 가능함 ⇒ 따라서, 일반적으로 접근 토큰의 유효기간을 짧게함. 
* `접근할 수 있는 특정 scope` `접근 가능 기간` 등이 담겨 있음.
<br>

**2. 재생 토큰(Refresh Token)** 
* 접근 토큰의 유효 기간이 만료되었을 경우를 대비하여 앱 개발자는 재생 토큰을 사용하여 인증을 반복하게 하지 않고, 새로 접근 토큰을 받을 수 있게 함.
<br>

### 흐름(flow) 🌟🌟🌟
**Access Token 인증 과정**
![img](https://media.vlpt.us/images/denmark-choco/post/265bf6a1-e4e9-4b91-a8ab-d08570e553e3/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-08-03%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%206.30.14.png)

**(A) (앱→사용자)** 사용자 데이터에 접근하기 위한  **권한을 요청**한다. 

**(B) (사용자→앱)**  접근에 동의함을 증명하는  **권한 부여 동의서(Authorization Grant)를 발급**한다. RFC 6749에서는 4가지 유형의 권한 부여 동의서를 정의하고 있다. 앱의 유형 및 권한 제공기관의 지원 여부에 따라 사용할 권한 부여 동의서의 유형이 결정된다.

**(C) (앱→권한 제공기관)**  **권한 부여 동의서를 제출**하여 접근 토큰을 요청한다. 

**(D) (권한 제공기관→앱)** 권한 부여 동의서를 확인하여 사용자가 동의한 데이터 항목, 범위 및 기간 등에 대한 정보가 담긴  **접근 토큰을 제공**한다. 

**(E) (앱→데이터 제공기관)**  **접근 토큰을 제출**하여 사용자 데이터를 요청한다.

**(F) (데이터 제공기관→앱) 사용자 데이터를 제공**한다. 이때 앱이 제출한 접근 토큰이 유효함을 확인하고, 접근 토큰의 정보를 확인하여 제공할 데이터 항목, 범위 및 유효기간이 정해진다.

<br>

**Access Token & Refresh Token 인증 과정**
![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99DB8C475B5CA1C936)

* `장점`
	* 기존 접근 토큰만 이용하는 것보다 안전함.
* `단점`
	* 구현이 복잡함.
	* 접근 토큰이 만료될 때마다 새롭게 발급하는 과정에서 생기는 HTTP 요청 횟수가 많아짐. ⇒ 서버의 자원의 낭비
<br>

### 인증 종류 
1. Authorization Code(승인 코드) 유형
2. Implicit(암묵적) 유형
3. Password Credentials(사용자 비밀번호 인증) 유형
4. Client Credentials(앱 인증) 유형

_**자세하게 알고싶다면 참고 자료 참고**_

<br>

## 3. 추가 질문
**Q. OAuth vs JWT** 🌟🌟🌟

A. 이건 나도 모르겠어 ! 히히

**Q. OAuth 1.0 vs OAuth 2.0**
* 간단해졌다! 
* 인증 방법이 다양해졌다!
* 대형 서비스로의 확장성이 열려있다!
	* 대형 서비스를 위해서는 인증서버 분리, 인증 서버 다중화가 되어야 함! 
	⇒ 인증부분을 다른 부분으로 분리함으로써 인증 서버 다중화 가능해짐!


---
**참고 자료**
* [OAuth1.0 vs OAuth2.0 I](https://velog.io/@devsh/OAuth-2.0-%EC%97%90-%EB%8C%80%ED%95%98%EC%97%AC)
* [OAuth1.0 vs OAuth2.0 II](https://berrrrr.github.io/programming/2019/11/03/oauth1-vs-oauth2/)
* [Acess Token & Refresh Token 인증 과정](https://velog.io/@daybreak/Access-Token-Refresh-Token)
* [OAuth && Redirect](https://velog.io/@undefcat/OAuth-2.0-%EA%B0%84%EB%8B%A8%EC%A0%95%EB%A6%AC)
* [인증 유형](http://www.2e.co.kr/news/articleView.html?idxno=208594)
