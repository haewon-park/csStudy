# Apps
## 1. Native App
### Native App이란?
> 우리가 흔히 알고 있는 어플리케이션으로 **각 플랫폼에 맞는 언어로 개발한 앱**을 의미
* Android 모바일 앱 개발의 경우는 Kotlin 또는 Java로 네이티브 앱을 제작
* iOS의 경우 Swift 또는 Objective C로 네이티브 앱을 제작
<br>

### 장단점
**장점**
* 사용자에게 가장 빠르고 안정적이며 반응이 빠른 환경을 제공
* 다양한 네이티브 기능을 쉽게 활용
 `카메라`, `마이크(microphone)`, `GPS 및 스와이프 제스처(swipe gesture)`

**단점**
* Android와 IOS의 호환이 되지 않기 때문에 별도로 제작
* 더 많은 비용이 들고 빌드 시 시간이 더 오래 걸림

<br>

## 2. Web App
### Web App이란?
<img src = "https://user-images.githubusercontent.com/65820741/128849623-e1a96bdd-89d1-4edb-9be5-59a09b4e29cb.png" width="50%" height="50%">
> 모바일 웹 + 네이티브 앱
*사파리로 네이버 들어간 느낌!*

<br>

### 장단점
**장점**
-   웹 사이트를 보는 것이므로 따로 설치할 필요X
-   모든 기기와 브라우저에서 접근 가능
-   별도 설치 및 승인 과정이 필요치 않아 유지보수에 용이

**단점**
-   플랫폼 API 사용 불가능. 오로지 브라우저 API만 사용가능
-   친화적 터치 앱을 개발하기 약간 번거로움
-   네이티브, 하이브리드 앱보다 실행 까다로움 (브라우저 열거 검색해서 들어가야함)

<br>

## 3. Hybrid App
### Hybrid App이란? 
![img](https://miro.medium.com/max/4800/0*xUKspCczfvfOORjY)
> 네이티브 앱 + 웹 앱
* 기본적인 기능은 HTML 등의 PC로 작업이 가능한 웹문서로 구현
* 디자인과 같은 패키징은 모바일 운영체제로 구현
* *ex) 네이버, 구글 어플*
<br>

### 장단점
**장점**
* 네이티브 API, 브라우저 API를 모두 활용한 다양한 개발 가능
* 웹 개발 기술로 앱 개발 가능
* 한번의 개발로 다수 플랫폼에서 사용 가능

**단점**
* 네이티브 기능 접근 위해 개발 지식 필요
* UI 프레임도구 사용안하면 개발자가 직접 UI 제작

<br>

### Mobile Web vs Hybrid Web
![img](https://user-images.githubusercontent.com/65820741/128850242-8c707687-7572-4c0a-b9e5-83fe8dc395b6.png)
<br>

### 추가 질문
**Q. 하이브리드  앱에서  세션  관리를  위해  필요한  처리는  무엇인가요?**
A. 

<br>

## 4. Cross-platform App
### Cross-platform App이란? 
> 네이티브 코드가 아닌 언어로 코딩을 한 후, 나중에 ios/android가 이해할 수 있는 코드로 변환
**크로스 플랫폼 프레임 워크(Cross-platform frameworks)**

-   Google이 만든  *Flutter*  - Dart -> C, C++로 컴파일
-   Facebook이 만든  *React Native*
<br>

### 장단점
**장점**
-   코드를 한 번만 작성하면 2개의 플랫폼에서 사용 가능
-   시간 절약
-   다양한 배경의 개발자 유입 (백엔드 개발자, Java 개발자)
-   다양한 형태의 라이브러리, 튜토리얼, 커뮤니티 발전

**단점**
-   네이티브가 아님
-   퍼포먼스 이슈 발생 (속도 저하)
-   지원하는 플러그인 부족
-   정보 부족

<br>

---
**참고 자료**
* https://velog.io/@nezhitsya/%EA%B8%B0%EC%88%A0%EB%A9%B4%EC%A0%91-03
