# Authentication and Authorization

## Authentication(인증)
- 클라이언트가 자신이 주장하는 사용자와 같은 사용자인지를 확인하는 과정
- 유저가 누구인지 확인하는 절차
- Ex) 회원가입을 하고 로그인 하는 것


⭐**필요한 이유**
- 누가, 언제, 어떻게 쓰고 있는가를 파악하기 위해 어떤 사이트에서나 인증, 인가가 존재
- 서비스를 누가 사용하며, 추적이 가능하도록 하기 위함
- 타인에게 사용자의 정보를 보호하기 위함

<br>

## Authorization(인가)
- 접근 제어라고도 할 수 있음
- 권한을 부여하는 것으로 클라이언트가 하고자 하는 작업이 해당 클라이언트에게 허가된 작업인지를 확인
- 특정 자원에 대한 접근 권한이 있는지 확인
- 유저에 대한 권한 허락

  <br>

## Authorization 절차
- 인가 절차를 통해 access token을 생성
- access token에는 유저 정보를 확인할 수 있는 정보가 들어있어야 함(Ex. user id)
- 유저가 request 보낼 때 access token을 첨부해서 보냄
- 서버에서는 유저가 보낸 access token을 복호화 한다.
- user id를 사용해 DB에 해당 유저의 권한을 확인
- 유저가 충분한 권한을 가지고 있으면 해당 요청을 처리
- 유저가 권한을 가지고 있지 않으면 401에러(Unauthorized Response) 혹은 다른 에러 코드를 보냄
🥕정리
- 유저의 목표는 리소스(웹페이지, 텍스트, 이미지 등)에 접근하는 것
- 리소스에 접근하기 위해서는 인증과 권한이 필요
- Authentication(인증)은 본인의 신분을 증명하는 것
- Authorization(인가)는 인증하고 나면 그 다음 절차를 할 수 있게 되는 것 

<br>

## 출처
- https://velog.io/@sdc337dc/%EC%9B%B9-%EC%9D%B8%EC%A6%9DAuthentication-%EC%9D%B8%EA%B0%80Authorization
- https://velog.io/@aaronddy/%EC%9D%B8%EC%A6%9DAuthentication%EA%B3%BC-%EC%9D%B8%EA%B0%80Authorization
