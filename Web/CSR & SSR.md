# CSR & SSR
**페이지를 렌더링하는 방법**에 따라 SPA와 SSR로 나눌 수 있다. 

<br>

## CSR(Client Side Rendering)

![CSR](https://user-images.githubusercontent.com/63101648/129189015-da4059aa-944e-4e12-b5fa-eb13a1574f82.png)

## CSR이란
- JS를 사용하여 브라우저에서 **페이지를 직접 렌더링 하는 것**
- 최초에 1번 서버에서 전체 페이지를 로딩하여 보여주고 이후에는 사용자의 요청이 올 때마다, 리소스를 서버에서 제공한 후 클라이언트가 해석하고 렌더링을 하는 방식
- 클라이언트 측에서 HTML을 반환한 후 Script가 동작하면서 데이터만을 주고 받아 클라이언트에서 렌더링을 하는 것 

<br>

### 장점
- 렌더링 속도가 빠르다(필요한 부분만 가져오면 되기 때문)
- 모바일 앱에서도 **속도가 빠름**
- 서버에 요청하는 횟수가 훨씬 적기 때문에 **서버 부담이 덜함**

<br>

### 단점
- **맨 처음 화면의 렌더링 속도가 느림**(JS를 읽고 화면에 그려야하므로!)
- 모든 HTML과 Static 파일이 **로드될 때까지 기다려야 함** 
- 검색엔진 최적화 **(SEO) 문제가 발생할 수 있음**

<br>

## SSR(Server Side Rendering)

![SSR](https://user-images.githubusercontent.com/63101648/129189004-c76fe30f-2e2b-4269-bf15-e155ee10fd14.png)

## SSR이란
- **서버에서 렌더링 작업**을 하는 것
- **완전하게 만들어진 HTML 파일을 받아와서** 렌더링 하게 된다.
- 사용자가 웹페이지에 접근할 때 서버에서 페이지에 대한 요청을 하며 서버에서는 HTML, VIEW와 같은 리소스들을 해석하고 렌더링하여 사용자에게 반환하는 것
- 웹서버에 요청할 때마다 브라우저 새로고침이 일어나고 서버에 새로운 페이지에 대한 요청을 하는 방식 
 

<br>


### 장점
- **맨 처음 화면의 로드 시간이 짧다**(렌더링 속도가 빠르다)
- 검색 엔진 최적화 **(SEO)에 적합**하다(완성된 HTML 파일을 받아 데이터를 갖고 있기 때문)

<br>


### 단점
- 이후의 렌더링은 서버를 거쳐야 하므로 **속도가 느릴 수 있음**
- 서버에 매번 요청을 하기 때문에 **트래픽, 서버 부하가 커짐**

<br>


### ⭐한 눈에 비교⭐

![ssr_and_csr_3](https://user-images.githubusercontent.com/63101648/129215790-c9922ac9-dda5-4989-bbc2-0ba8929c0617.png)

![CSRSSR](https://user-images.githubusercontent.com/63101648/129216432-b53f0739-e1cb-48d8-a3dc-176e90999e26.png)


<br>


### 출처
- https://velog.io/@solmii/How-the-Web-Works-SPA-MPA-CSR-SSR
- https://velog.io/@qkrdudgh052/SSR-CSR-%EC%B0%A8%EC%9D%B4
- https://pyolog.tistory.com/8
- https://velog.io/@namezin/CSR-SSR
