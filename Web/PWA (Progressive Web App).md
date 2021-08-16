## PWA란?
> 웹의 장점과 앱의 장점을 결합한 환경

- 구글 개발자 컨퍼런스인 I/O 2016 에 발표된 기술
- 앱 수준과 같은 사용자 경험을 웹에서 제공하는 것
- 확장성이 좋고, 깊이 있는 앱같은 웹을 만드는 것을 지향

<br>

### 채택 기술
- **웹 메니페스트** (Web App Manifest): 브라우저가 웹 앱을 설치할 때 그리고 홈 화면에서 웹 앱을 적절히 표현하는 데 필요한 정보

- **서비스 워커** (Service Worker): 브라우저가 백그라운드에서 실행하는 스크립트 (푸쉬 알람, 백그라운드 동기화 등)

- **반응형 웹** (Responsive Web): 현재 사용되는 대부분의 반응형 웹 기술

<br>

### PWA 장점
- 반응형 : 데스크톱, 모바일, 테블릿 등 모든 폼 factor에 맞음
- 연결 독립적 : 로컬 기기의 캐시를 활용하여 오프라인이나 불안한 네트워크에서도 실행 가능
- 재참여 가능 : 브라우저가 닫혀 있더라도 푸쉬 알람을 보낼 수 있어서 재방문율을 높여줌
- 안전성 : HTTPS 통신으로 제공되므로 기존 웹 대비 안전함
- 설치 가능한 경험 제공 : 앱스토어를 찾지 않아도 간단히 홈스크린에 앱 등록 가능
- 검색 가능 : 구글, 네이버 등 포털 검색 결과에 노출

<br>

### PWA 단점
- 로딩 속도, 성능이 다소 떨어짐
- 오래된 브라우저들은 PWA를 지원하지 않음
- iOS에서는 성능이 약하고 애플의 장치에 대한 지원이 적음
- 앱 스토어에서는 사용할 수 없으므로 마케팅 효과 떨어짐

<br>

### 모바일 앱 개발 시 어떤 걸 선택해야할까?
- 앱의 성능이나 실행될 장치의 하드웨어 방면 기능이 매우 필요한 경우: **네이티브 앱(Native App) 선택**
- 쇼핑몰 같이 사용자의 방문이 많을 수 있고 웹과 모바일 둘 다 되는 앱을 구상 중인 경우: **프로그레시브 웹 앱(PWA)을 선택**
- 웹 개발에 익숙하고 빠른 기간 내에 앱을 구축하고 싶은 경우: **하이브리드 앱(Hybrid App) 선택**


<br>

#### 참고 링크
https://www.insilicogen.com/blog/350

https://www.hanl.tech/blog/native-vs-hybrid-vs-pwa/

https://www.simicart.com/blog/progressive-web-apps-examples/ (PWA 모범 사례)