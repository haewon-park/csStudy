## 1. 서버 기반 인증 vs 토큰 기반 인증

_기존의 권한 인증 인가는 대부분 서버 기반으로 이루어져 있었다. 하지만 서버 기반의 권한 인증 인가는 MSA(MicroService Architecture)에 적합하지 않아 그의 대안으로 JWT가 등장하였다._

<br>

### ✔ 서버 기반 인증

#### 리마인드

HTTP의 특징 : `connectionless`, `stateless`

따라서 로그인 후 다시 웹페이지에 접근하면 로그인 상태가 유지되지 않는다는 문제점이 있다. 
-> HTTP 프로토콜의 인증 문제를 해결하기 위해 `세션`과 `쿠키`를 사용한다.

<br>

#### 흐름

![](https://images.velog.io/images/yanghl98/post/abc3066d-8ded-4e6e-8622-f0821bc22307/image.png)

1) 사용자가 로그인 한다. (로그인 정보(id, pw)를 서버로 request)

2) 서버는 request가 들어오면 DB를 쿼리 하여 사용자를 검증하고 유효할 경우 **사용자의 고유한 ID값을 부여하여 세션 저장소에 저장**한 후, 이와 연결되는 세션 ID를 생성하여 response header에 포함시켜 반환한다.

3) 사용자는 서버에서 해당 세션ID를 받아 쿠키에 저장을 한 후, 제한된 end point(인증이 필요한 요청)에 접근할 때 마다 쿠키를 request header에 포함시켜 보낸다.

4) 서버에서는 쿠키를 받아 `세션 저장소`에서 검증한 후 요청에 해당하는 데이터를 반환한다.

<br>

#### 특징

- 쿠키(서버에 저장된 세션에 접근하기 위한 세션 ID)가 HTTP 요청 중 노출되어도 **쿠키 자체에 중요한 정보는 담겨있지 않다**. 
  - 하지만 쿠키 자체를 훔쳐 세션에 접근하여 중요한 정보를 빼낼 수 있는데, 이를 막기 위해 세션에 유효시간을 넣거나 HTTPS를 사용해 요청을 훔쳐도 그 안의 정보를 보기 힘들게 한다.

- 쿠키를 통해 세션에 접근하면 세션 ID로 사용자를 구분할 수 있으므로 일일이 사용자 정보를 확인할 필요가 없다.

- 서버(메모리 or DB)에 세션을 저장하기 때문에 사용자 수가 많아지면 서버의 부담이 늘어난다. 

- 서버 확장성(scalability)이 나빠진다. 서버 사양 업그레이드뿐만 아니라 늘어나는 트래픽을 감당하기 위해 여러 프로세스를 돌리거나, 여러 대의 서버 컴퓨터를 추가하는 것이 어려워진다.

- CORS(Cross-Origin Resource Sharing)  
쿠키는 단일 도메인 및 서브 도메인에서만 작동하도록 설계되어 여러 도메인에서 관리하기 번거롭다. 

<br>

### ✔ 토큰 기반 인증

#### 기본

세션 기반 인증과는 다르게 **서버가 사인한 토큰을 이용**하여 인증을 수행하는 방식이다.

`세션 기반 인증`의 서버는 클라이언트로부터의 요청이 있을 때마다 클라이언트의 상태를 유지한다. 사용자가 로그인을 하여 인증을 요청하면 stateful 서버는 인증에 성공하였을 때의 결과(세션)를 메모리 또는 데이터베이스에 유지하기 때문에 서버에 부하가 발생할 수 있다. 

하지만 `토큰 기반 인증`은 stateful 서버와 반대적 개념인 stateless 서버를 사용하며 상태 정보를 유지하지 않는다. 

서버가 전달받은 토큰을 검증만 하면 되기 때문에 서버의 부담을 줄이고 서비스의 확장성을 높일 수 있다.

<br>

#### 흐름

![](https://images.velog.io/images/yanghl98/post/985298e5-28da-4de2-b972-837480bc5244/image.png)

1) 로그인 한다. (로그인 정보를 서버로 request)

2) 서버는 request가 들어오면 사용자를 검증하고 유효할 경우 정상적으로 발급된 토큰임을 증명하는 signature를 갖는 토큰을 클라이언트에 반환한다. 

3) 클라이언트는 토큰을 저장하고 서버 요청 시 해당 토큰을 Request header에 담아 서버에 전달한다. 

4) 서버는 토큰을 검증한 후, 요청에 응답한다.

<br>

#### 특징

- `Stateless 서버`로 확장성(Scalability) 높음
  - Stateful 서버는 클라이언트에게서 요청을 받을 때마다 클라이언트의 상태를 계속해서 유지하고 이 정보를 서비스 제공에 이용한다.
    - `ex`) 세션을 유지하는 웹서버가 있다. 로그인을 하면 세션에 로그인이 되었다고 저장을 해 두고 서비스를 제공할 때에 그 데이터를 사용한다. 세션은 `서버의 메모리`나 `데이터베이스`에 저장한다. 
  - Stateless 서버는 **상태를 유지하지 않는다**. 서버는 클라이언트 측에서 들어오는 요청만으로만 작업을 처리한다. 클라이언트와 서버의 연결고리가 없기 때문에 서버의 확장성(Scalability)이 높아진다. 

- 플랫폼 간 권한 공유 : 대표적인 예로 OAuth가 있다. 페이스북/구글 같은 소셜 계정들을 이용하여 다른 웹서비스에서도 로그인할 수 있다. 

<br><br>

## 2. JWT란?
### 정의
> JSON Web Tokens are an open, industry standard RFC 7519 method for representing claims securely between two parties.
= 개방형 표준 (RFC 7519)으로 당사자간에 정보를 JSON 객체로 안전하게 전송하기 위한 간결하고 독립적인 방법

- Json 포맷을 이용하여 사용자에 대한 속성을 저장하는 Claim 기반의 Web Token이다. JWT는 토큰 자체를 정보로 사용하는 Self-Contained 방식으로 정보를 안전하게 전달한다. 주로 회원 인증이나 정보 전달에 사용되는 JWT는 아래의 로직을 따라서 처리된다.

![](https://images.velog.io/images/yanghl98/post/473b31b1-3e97-48dc-9402-76d7fbf603e0/image.png)<br>
(이미지 출처 : https://mangkyu.tistory.com/56)

```
애플리케이션이 실행될 때, JWT를 static 변수와 로컬 스토리지에 저장하게 된다. 
static 변수에 저장되는 이유는 HTTP 통신을 할 때마다 JWT를 HTTP 헤더에 담아서 보내야 하는데, 
이를 로컬 스토리지에서 계속 불러오면 오버헤드가 발생하기 때문이다. 
클라이언트에서 JWT를 포함해 요청을 보내면 서버는 허가된 JWT인지를 검사한다. 

또한 로그아웃을 할 경우 로컬 스토리지에 저장된 JWT 데이터를 제거한다. 
(실제 서비스의 경우에는 로그아웃 시, 사용했던 토큰을 blacklist라는 DB 테이블에 넣어 
해당 토큰의 접근을 막는 작업을 해주어야 한다.)
```

<br>

#### 로그인 할 때 토큰이란?
인터넷에 사이트를 올리면 전 세계에서 접근 할 수 있기 때문에 사용자뿐만 아니라 해커도 이 사이트에 접근을 할 수 있다. 결제 서비스를 생각한다면, 사용자들의 돈을 보호 하기 위해 **본인만** 주문을 넣고 결제를 할 수 있게 만들어야 하는데, 이 토큰은 **본인 확인 수단**이다. 

로그인을 할 때 id와 pw를 넣고 로그인 버튼을 클릭하여 서버로 보내면, 서버는 id와 pw를 확인하여 맞으면 `이 사용자가 유효한 사용자라`는 토큰을 발행 해준다. 그러면 사용자들은 이 토큰을 가지고 해당 사이트의 서비스들을 이용 할 수 있는 것!

<br><br>

## 3. JWT 구조
JWT는 `Header`, `Payload`, `Signature`의 세 부분으로 이루어지며, Json 형태인 각 부분은 Base64로 인코딩 되어 표현된다. 또한 각각의 부분을 이어 주기 위해 `.` 구분자를 사용하여 구분한다.

![](https://images.velog.io/images/yanghl98/post/9f0dcbb0-672b-4014-8390-e36ebf5b56a0/image.png)<br>
(이미지 출처 : https://mangkyu.tistory.com/56)

<br>

### ✔ Header(헤더)

토큰의 헤더는 `typ(토큰 타입)`과 `alg(암호화 방법)` 두 가지 정보로 구성되며, Base-64로 인코딩 된다. alg는 헤더(Header)를 암호화 하는 것이 아니고, Signature를 해싱하기 위한 알고리즘을 지정하는 것이다.

- `typ`: 토큰의 타입을 지정 
  - ex) JWT
- `alg`: 알고리즘 방식을 지정하며, 서명(Signature) 및 토큰 검증에 사용한다.
  - ex) HS256(SHA256) 또는 RSA


<br>

### ✔ Payload(페이로드)

`Payload`에는 유저 정보, 상품 정보 등의 다양한 종류의 정보를 넣을 수 있다. Base-64로 인코딩 된다. 

토큰의 페이로드에는 토큰에서 사용할 정보의 조각들인 클레임(Claim)이 담겨 있다. 클레임은 총 3가지로 나누어지며, Json(Key/Value) 형태로 다수의 정보를 넣을 수 있다.

#### 1) 등록된 클레임(Registered Claim)

등록된 클레임은 토큰 정보를 표현하기 위해 **이미 정해진 종류의 데이터**들로, 등록된 클레임의 사용은 모두 선택적(optional)이다. 또한 JWT를 간결하게 하기 위해 key는 모두 길이 3의 String이다. (여기서 subject로는 unique한 값을 사용하는데, 사용자 이메일을 주로 사용한다.)

- `iss`: 토큰 발급자(issuer)
- `sub`: 토큰 제목(subject)
- `aud`: 토큰 대상자(audience)
- `exp`: 토큰 만료 시간(expiration), NumericDate 형식으로 되어 있어야 함 ex) 1480849147370
- `nbf`: 토큰 활성 날짜(not before), 이 날이 지나기 전의 토큰은 활성화되지 않음
- `iat`: 토큰 발급 시간(issued at), 토큰 발급 이후의 경과 시간을 알 수 있음
- `jti`: JWT 토큰 식별자(JWT ID), 중복 방지를 위해 사용하며, 일회용 토큰(Access Token) 등에 사용

#### 2) 공개 클레임(Public Claim)

공개 클레임은 사용자 정의 클레임으로, 공개용 정보를 위해 사용된다. 충돌 방지를 위해 URI 포맷을 이용하며, 예시는 아래와 같다.
```
{ 
    "https://mangkyu.tistory.com": true
}
```

#### 3) 비공개 클레임(Private Claim)

비공개 클레임은 사용자 정의 클레임으로, 서버와 클라이언트 사이에 임의로 지정한 정보를 저장한다. 아래의 예시와 같다.
```
{ 
    "token_type": access 
}
```

<br>

### ✔ Signature(서명) 

- `Signature`는 Header, Payload, Secret key의 조합으로, 토큰을 인코딩하거나 유효성 검증을 할 때 사용하는 고유한 암호화 코드이다. Secret key는 반드시 서버에 안전하게 보관되어야 한다. 

- 서명(Signature)은 위에서 만든 헤더(Header)와 페이로드(Payload)의 값을 각각 BASE64로 인코딩하고, 인코딩한 값을 비밀 키를 이용해 헤더(Header)에서 정의한 알고리즘으로 해싱을 하고, 이 값을 다시 BASE64로 인코딩하여 생성한다.

<br>

### 알아두기

- 생성된 토큰은 HTTP 통신을 할 때 Authorization이라는 key의 value로 사용된다. 일반적으로 value에는 Bearer이 앞에 붙여진다.
```
{ 
    "Authorization": "Bearer {생성된 토큰 값}",
 }
```

- Base64는 암호화된 문자열이 아니고, 같은 문자열에 대해 항상 같은 인코딩 문자열을 반환한다. 

- 토큰의 페이로드(Payload)에 3종류의 클레임을 저장하기 때문에, 정보가 많아질수록 토큰의 길이가 늘어나 네트워크에 부하를 줄 수 있다. 

- 페이로드(Payload) 자체는 암호화 된 것이 아니라, BASE64로 인코딩 된 것이다. 중간에 Payload를 탈취하여 디코딩하면 데이터를 볼 수 있으므로, JWE로 암호화하거나 Payload에 중요 데이터를 넣지 않아야 한다. 

- 별도의 인증 저장소가 필요가 없다. 그래서 인증 서버와 DB에 의존하지 않아도 된다. 

<br><br>

## 4. Access Token + Refresh Token ⭐
만약 `유효기간이 짧은 Token`을 발급하게되면 사용자 입장에서 자주 로그인을 해야하기 때문에 번거롭고 반대로 `유효기간이 긴 Token`을 발급하게되면 제 3자에게 토큰을 탈취당할 경우 보안에 취약하다는 약점이 있다.

사용자 편의성을 위하여 JWT의 만료시간을 엄청 길게 가져간 상황에서, JWT가 탈취당한다면 해당 토큰이 만료되기 전까지는 해당 유저인 척하며 여러 정보를 접근해갈 수 있다.

>이를 보완하기 위해 `AccessToken`, `RefreshToken`을 활용한다.
액세스 토큰이 만료 될 경우 따로 저장했던 `RefreshToken`을 이용하여 `AccessToken` 재발급을 요청한다.

![](https://images.velog.io/images/yanghl98/post/3f175df3-7e9c-4770-ab9d-22b6ddf0ce87/image.png)

Refresh Token은 Access Token과 똑같은 형태의 JWT이다. 처음에 로그인을 완료했을 때 Access Token과 동시에 발급되는 Refresh Token은 긴 유효기간을 가지면서, Access Token이 만료됐을 때 새로 발급해주는 열쇠가 된다. (만료==유효기간이 지났다는 의미) 

- `ex` : Refresh Token의 유효기간은 `2주`, Access Token의 유효기간은 `1시간`이라고 정한다. 사용자는 API 요청을 신나게 하다가 1시간이 지나게 되면, 가지고 있는 Access Token은 만료된다. 그러면 Refresh Token의 유효기간 전까지는 Access Token을 새롭게 발급받을 수 있다. 

- Access Token은 탈취당하면 정보가 유출되는건 동일하다. 다만 짧은 유효기간 안에만 사용이 가능하기에 더 안전하다는 의미임.
- Refresh Token의 유효기간이 만료됐다면, 사용자는 새로 로그인해야 한다. Refresh Token도 탈취될 가능성이 있기 때문에 적절한 유효기간 설정이 필요하다. (주로 2주)

<br><br>

## 5. 면접 질문?

#### # JWT의 구성 요소 3가지?

#### # 토큰 인증 방식의 흐름?

#### # facebook이나 Instagram의 경우는 장기간 로그인이 유지된다. 만약 JWT를 유효기간을 설정하지 않을 경우, 보안에 취약할 것으로 보이는데 어떻게 구현되어 있을지 설명할수 있겠는가?




<br><br>

## 출처
https://dooopark.tistory.com/6 (서버 인증 방식과 토큰 인증 방식)<br>
https://meetup.toast.com/posts/239<br>
https://mangkyu.tistory.com/56<br>
https://node-js.tistory.com/entry/JWT-%EC%84%9C%EB%B2%84-%EC%9D%B8%EC%A6%9D-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-JWT%EB%9E%80-%EC%84%9C%EB%B2%84-%EC%9D%B8%EC%A6%9D-%ED%86%A0%ED%81%B0-%EC%9D%B8%EC%A6%9D<br>
https://joomn11.tistory.com/25<br>
https://tech.toktokhan.dev/2021/04/30/JWT/<br>
https://thgus13.tistory.com/4<br>
https://tansfil.tistory.com/59
