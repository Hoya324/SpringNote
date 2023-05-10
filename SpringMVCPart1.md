2023.02.09 ~ 

# springMVCStudy
스프링 MVC 1편- 백엔드 웹 개발 핵심 기술

## 웹 애플리케이션 이해

### 웹 서버, 웹 애플리케이션 서버

#### 웹 서버
<img width="685" alt="스크린샷 2023-02-09 오후 8 32 02" src="https://user-images.githubusercontent.com/96857599/217801299-79e6f7f7-8142-4a29-91f4-e0ce96010678.png">

#### 웹 애플리케이션 서버
<img width="686" alt="스크린샷 2023-02-09 오후 8 49 45" src="https://user-images.githubusercontent.com/96857599/217804970-54d30801-699d-4aa7-87ab-2371ae4ea660.png">


#### 웹 서버, 웹 애플리케이션 서버(WAS) 차이
- 웹 서버는 정적 리소스(파일), WAS는 애플리케이션 로직 
- 사실은 둘의 용어도 경계도 모호함
    - 웹 서버도 프로그램을 실행하는 기능을 포함하기도 함
    - 웹 애플리케이션 서버도 웹 서버의 기능을 제공함 
- 자바는 서블릿 컨테이너 기능을 제공하면 WAS
    - 서블릿 없이 자바코드를 실행하는 서버 프레임워크도 있음 
- ⭐️WAS는 애플리케이션 코드를 실행하는데 더 특화

#### 웹 시스템 구성 - WAS, DB
<img width="683" alt="스크린샷 2023-02-09 오후 8 52 33" src="https://user-images.githubusercontent.com/96857599/217805505-222018e9-feaa-4db4-8f07-3a3f259adb3c.png">


<img width="689" alt="스크린샷 2023-02-09 오후 8 53 30" src="https://user-images.githubusercontent.com/96857599/217805713-6e9bd172-4e94-441d-bdfa-be63fd8edeec.png">


#### 웹 시스템 구성 - WEB, WAS, DB
<img width="689" alt="스크린샷 2023-02-09 오후 8 54 08" src="https://user-images.githubusercontent.com/96857599/217805840-9069953f-9379-4490-832f-30d271f41d95.png">

<img width="688" alt="스크린샷 2023-02-09 오후 8 54 59" src="https://user-images.githubusercontent.com/96857599/217806018-4e177271-4017-4dae-a70c-3224a823081d.png">

<img width="686" alt="스크린샷 2023-02-09 오후 8 56 30" src="https://user-images.githubusercontent.com/96857599/217806306-94bbc8ca-05b1-4b8d-9f1e-5946edea303a.png">

### 서블릿

<img width="682" alt="스크린샷 2023-02-09 오후 8 58 29" src="https://user-images.githubusercontent.com/96857599/217806713-f3749fb0-115a-4971-a670-89caf26c82ab.png">


#### 서버에서 처리해야하는 업무
- 웹 애플리케이션 서버 직접 구현

<img width="676" alt="스크린샷 2023-02-09 오후 9 00 04" src="https://user-images.githubusercontent.com/96857599/217807022-8feaf384-c24e-40c4-9804-324c7725a221.png">

- 서블릿을 지원하는 WAS 사용
<img width="648" alt="스크린샷 2023-02-09 오후 9 02 43" src="https://user-images.githubusercontent.com/96857599/217807489-cf0c4c4a-8f8a-4069-80af-99d5faf079d4.png">

#### 서블릿 특징
<img width="673" alt="스크린샷 2023-02-09 오후 9 03 57" src="https://user-images.githubusercontent.com/96857599/217807739-ed9a8962-da6c-43ce-81ce-d1e314c25305.png">

- localhost:8080/hello 요청
- WAS 서버에서 response 객체를 생성함.
- 서블릿 컨테이너에서 실행함
- HTTP 응답 정보 
<img width="684" alt="스크린샷 2023-02-09 오후 9 05 01" src="https://user-images.githubusercontent.com/96857599/217807958-e0bffba0-afd6-4aa5-a373-f447e59a095a.png">
<img width="674" alt="스크린샷 2023-02-09 오후 9 07 30" src="https://user-images.githubusercontent.com/96857599/217808771-6cc09c13-2018-4855-b001-bb34a370b31a.png">

#### 서블릿 컨테이너

<img width="675" alt="스크린샷 2023-02-09 오후 9 08 09" src="https://user-images.githubusercontent.com/96857599/217808884-75cdc6a5-f833-4099-bc4c-10a106613dd2.png">

- 톰캣처럼 서블릿을 지원하는 WAS를 서블릿 컨테이너라고 함
- 서블릿 컨테이너는 서블릿 객체를 생성, 초기화, 호출, 종료하는 생명주기 관리 
- 서블릿 객체(helloServlet)는 싱글톤으로 관리
    - 고객의 요청이 올 때 마다 계속 객체를 생성하는 것은 비효율 
    - 최초 로딩 시점에 서블릿 객체를 미리 만들어두고 재활용 
    - 모든 고객 요청은 동일한 서블릿 객체 인스턴스에 접근
    - ⭐️공유 변수 사용 주의
    - 서블릿 컨테이너 종료시 함께 종료
- JSP도 서블릿으로 변환되어서 사용
- ⭐️동시 요청을 위한 멀티 쓰레드 처리 지원



### 동시 요청 - 멀티 쓰레드
- 백엔드 개발자에게 매우 중요함

<img width="700" alt="스크린샷 2023-02-11 오후 1 43 14" src="https://user-images.githubusercontent.com/96857599/218240435-4518d697-257d-4d43-a91a-b205704cdb42.png">

<img width="683" alt="스크린샷 2023-02-11 오후 1 43 28" src="https://user-images.githubusercontent.com/96857599/218240445-bc4ea44d-275f-4dd4-8076-9ba8ce4cc850.png">

- 클라이언트가 서버에 요청을 하면 servlet을 호출함. 근데 servlet을 누가 호출할까?
<img width="676" alt="스크린샷 2023-02-11 오후 1 43 34" src="https://user-images.githubusercontent.com/96857599/218240450-24670225-bf15-49cc-922d-493c2abe1408.png">

#### 쓰레드

- 애플리케이션 코드를 하나하나 순차적으로 실행하는 것은 쓰레드 
- 자바 메인 메서드를 처음 실행하면 main이라는 이름의 쓰레드가 실행 
- 쓰레드가 없다면 자바 애플리케이션 실행이 불가능
- 쓰레드는 한번에 하나의 코드 라인만 수행
- 동시 처리가 필요하면 쓰레드를 추가로 생성


#### 단일 요청 - 쓰레드 하나 사용
- 클라이언트가 WAS에 연결하면, 쓰레드를 할당한다.
- 그 쓰레드로 servlet 코드를 실행한다.
- 응답 후, 휴식
<img width="681" alt="스크린샷 2023-02-11 오후 1 46 14" src="https://user-images.githubusercontent.com/96857599/218240558-23b6b185-efdf-42e5-a6b2-c2089eee3e9c.png">

<img width="674" alt="스크린샷 2023-02-11 오후 1 46 20" src="https://user-images.githubusercontent.com/96857599/218240566-1f62fc26-38d3-43f3-b5e5-c4d69de868da.png">

<img width="666" alt="스크린샷 2023-02-11 오후 1 47 11" src="https://user-images.githubusercontent.com/96857599/218240603-ae4142a2-0c3a-48e8-a30c-cecbd63dc1ba.png">

<img width="685" alt="스크린샷 2023-02-11 오후 1 48 01" src="https://user-images.githubusercontent.com/96857599/218240630-c370213a-9ab9-4df3-914f-c5af9d62f8af.png">

#### 다중 요청 - 쓰레드 하나 사용

- 다수의 클라이언트가 연결 요청, 요청1에서 처리 지연 발생.
- 요청2는 쓰레드 할당을 위해 대기함.
- 요청1, 요청2 둘다 죽음. 오류발생
<img width="680" alt="스크린샷 2023-02-11 오후 1 48 39" src="https://user-images.githubusercontent.com/96857599/218240668-7d90b640-adff-4548-98fb-f00c023ea904.png">

<img width="693" alt="스크린샷 2023-02-11 오후 1 50 08" src="https://user-images.githubusercontent.com/96857599/218240727-0ae7a31d-d2ea-498b-b400-a9f8ba499e83.png">

<img width="699" alt="스크린샷 2023-02-11 오후 1 50 14" src="https://user-images.githubusercontent.com/96857599/218240730-b77d3972-d4e4-4c50-b21d-8a33df329132.png">

#### 요청 마다 쓰레드 생성

<img width="666" alt="스크린샷 2023-02-11 오후 1 52 10" src="https://user-images.githubusercontent.com/96857599/218240798-305a9bb4-9d30-4258-8261-23f2442d0fb2.png">

**장단점**

- 장점
    - 동시 요청을 처리할 수 있다.
    - 리소스(CPU, 메모리)가 허용할 때 까지 처리가능
    - 하나의 쓰레드가 지연 되어도, 나머지 쓰레드는 정상 동작한다.

- 단점
    - 쓰레드는 생성 비용은 매우 비싸다. (cpu를 많이 먹음)
        - 고객의 요청이 올 때 마다 쓰레드를 생성하면, 응답 속도가 늦어진다.
    - 쓰레드는 컨텍스트 스위칭 비용이 발생한다.(멀티 쓰레드일 때, 예를들어 cpu 코어가 하나라면 2개의 쓰레드를 하나의 코어가 처리하는 것인데 이 전환 속도가 너무 빨라 동시에 하는 것처럼 보이는 것임. 이때 전환되는 비용)
    - 쓰레드 생성에 제한이 없다.
        - 고객 요청이 너무 많이 오면, CPU, 메모리 임계점을 넘어서 서버가 죽을 수 있다. (수강신청, 치킨 할인)
        


#### 쓰레드 풀
- 위의 단점을 해결하기 위해 쓰레드 풀이 등장한다.

- 쓰레드 풀에 사용하지 않는 쓰레드들이 대기한다.
<img width="675" alt="스크린샷 2023-02-11 오후 1 57 37" src="https://user-images.githubusercontent.com/96857599/218240955-eef86d79-29fa-42d9-bf24-e2eca692e0a3.png">

- 요청시에 쓰레드를 사용하고, 사용이 완료된 쓰레드는 다시 쓰레드 풀로 들어간다. 
- 쓰레드 풀에 있는 쓰레드의 수보다 더 많은 요청이 온다면, 대기(대기 허용 수 설정) 또는 거절한다.
<img width="660" alt="스크린샷 2023-02-11 오후 1 58 22" src="https://user-images.githubusercontent.com/96857599/218240982-93db89ac-f8ae-41cf-9af4-d4c77b426fc8.png">


- 특징
    - 필요한 쓰레드를 쓰레드 풀에 보관하고 관리한다.
    - 쓰레드 풀에 생성 가능한 쓰레드의 최대치를 관리한다. 톰캣은 최대 200개 기본 설정 (변경 가능- Tomcat max connect) 
- 사용
    - 쓰레드가 필요하면, 이미 생성되어 있는 쓰레드를 쓰레드 풀에서 꺼내서 사용한다.
    - 사용을 종료하면 쓰레드 풀에 해당 쓰레드를 반납한다.
    - 최대 쓰레드가 모두 사용중이어서 쓰레드 풀에 쓰레드가 없으면?
        - 기다리는 요청은 거절하거나 특정 숫자만큼만 대기하도록 설정할 수 있다.
- 장점
    - 쓰레드가 미리 생성되어 있으므로, 쓰레드를 생성하고 종료하는 비용(CPU)이 절약되고, 응답 시간이 빠르다.
    - 생성 가능한 쓰레드의 최대치가 있으므로 너무 많은 요청이 들어와도 기존 요청은 안전하게 처리할 수 있다.

#### 실무 팁

- WAS의 주요 튜닝 포인트는 최대 쓰레드(max thread) 수이다. 
- 이 값을 너무 낮게 설정하면?
    - 동시 요청이 많으면, 서버 리소스는 여유롭지만, 클라이언트는 금방 응답 지연
- 이 값을 너무 높게 설정하면?
    - 동시 요청이 많으면, CPU, 메모리 리소스 임계점 초과로 서버 다운 
- 장애 발생시?
    - 클라우드면 일단 서버부터 늘리고, 이후에 튜닝 
    - 클라우드가 아니면 열심히 튜닝
    
#### 쓰레드 풀 - 너무 낮게 설정
- 동시 요청이 많으면, 서버 리소스는 여유롭지만, 클라이언트는 금방 응답 지연 (이걸 모르면 설정치만 늘리면 될 것을, 서버를 증설하는 부끄러운 상황 발생)
<img width="685" alt="스크린샷 2023-02-11 오후 2 07 48" src="https://user-images.githubusercontent.com/96857599/218241274-795eae4c-d990-4cd0-a7c1-a39cebaa8bf1.png">


#### 쓰레드 풀의 적정 숫자

- 적정 숫자는 어떻게 찾나요?
- 애플리케이션 로직의 복잡도, CPU, 메모리, IO 리소스 상황에 따라 모두 다름 
- 성능 테스트
    - 최대한 실제 서비스와 유사하게 성능 테스트 시도 
    - 툴: 아파치 ab, 제이미터, nGrinder(네이버 오픈소스임, 추천)


### ⭐️ WAS의 멀티 쓰레드 지원
#### 핵심
- 멀티 쓰레드에 대한 부분은 WAS가 처리
- 개발자가 멀티 쓰레드 관련 코드를 신경쓰지 않아도 됨
- 개발자는 마치 싱글 쓰레드 프로그래밍을 하듯이 편리하게 소스 코드를 개발
- ⭐️멀티 쓰레드 환경이므로 싱글톤 객체(서블릿, 스프링 빈)는 주의해서 사용

### HTML, HTTP API, CSR, SSR

### 정적 리소스
- 고정된 HTML 파일, CSS, JS, 이미지, 영상 등을 제공 
- 주로 웹 브라우저
<img width="557" alt="스크린샷 2023-02-11 오후 2 15 04" src="https://user-images.githubusercontent.com/96857599/218241554-bf85802c-7c96-4472-b850-4b130727b418.png">



#### HTML 페이지
- 동적으로 필요한 HTML 파일을 생성해서 전달 
- 웹 브라우저: HTML 해석

<img width="651" alt="스크린샷 2023-02-11 오후 2 15 15" src="https://user-images.githubusercontent.com/96857599/218241563-b0222ac5-f4b5-453b-90fb-be45557c1411.png">

#### HTTP API
- HTML이 아니라 데이터를 전달 
- 주로 JSON 형식 사용
- 다양한 시스템에서 호출(HTML에서 JSON을 바로 해석하는 용도가 아님)
<img width="646" alt="스크린샷 2023-02-11 오후 2 16 43" src="https://user-images.githubusercontent.com/96857599/218241610-9c61c951-d779-45dd-b396-7f25ffba3cdb.png">


- 다양한 시스템에서 호출
- 데이터만 주고 받음, UI 화면이 필요하면, 클라이언트가 별도 처리
- 앱, 웹 클라이언트, 서버 to 서버
<img width="646" alt="스크린샷 2023-02-11 오후 2 18 26" src="https://user-images.githubusercontent.com/96857599/218241658-0997a2ad-8324-4354-8354-386bc57644be.png">

#### 다양한 시스템 연동
- 주로 JSON 형태로 데이터 통신 
- UI 클라이언트 접점 (앱, 웹 클라이언트 to 서버)
    - 앱 클라이언트(아이폰, 안드로이드, PC 앱)
    - 웹 브라우저에서 자바스크립트를 통한 HTTP API 호출 
    - React, Vue.js 같은 웹 클라이언트
- 서버 to 서버
    - 주문 서버 -> 결제 서버
    - 기업간 데이터 통신


#### ⭐️백엔드 개발자가 고민해야할 것

1. 정적 리소스 어떻게 제공할지
2. 동적으로 제공되는 HTML 페이지를 어떻게 제공할지
3. HTTP API 어떻게 제공할지

#### 서버사이드 렌더링, 클라이언트 사이드 렌더링


- SSR - 서버 사이드 렌더링 (서버에서 HTML을 모두 만들어서 클라이언트에게 제공)
<img width="683" alt="스크린샷 2023-02-11 오후 2 26 20" src="https://user-images.githubusercontent.com/96857599/218241955-fef44080-ab71-4967-a6ac-54c43da19a3f.png">
    - HTML 최종 결과를 서버에서 만들어서 웹 브라우저에 전달 
    - 주로 정적인 화면에 사용
    - 관련기술: JSP, 타임리프 -> 백엔드 개발자
    
- CSR - 클라이언트 사이드 렌더링
<img width="709" alt="스크린샷 2023-02-11 오후 2 26 42" src="https://user-images.githubusercontent.com/96857599/218241971-2ea0a453-60d3-4913-a50a-be28c13b3861.png">
    - HTML 결과를 자바스크립트를 사용해 웹 브라우저에서 동적으로 생성해서 적용
    - 주로 동적인 화면에 사용, 웹 환경을 마치 앱 처럼 필요한 부분부분 변경할 수 있음
    - 예) 구글 지도, Gmail, 구글 캘린더
    - 관련기술: React, Vue.js -> 웹 프론트엔드 개발자
    
- 참고
    - React, Vue.js를 CSR + SSR 동시에 지원하는 웹 프레임워크도 있음
    - SSR을 사용하더라도, 자바스크립트를 사용해서 화면 일부를 동적으로 변경 가능


#### 어디까지 알아야 하나요?
- 백엔드 개발자 입장에서 UI 기술

- 백엔드 - 서버 사이드 렌더링 기술
    - JSP, 타임리프(spring에서 미는 것)
    - 화면이 정적이고, 복잡하지 않을 때 사용
    - 백엔드 개발자는 서버 사이드 렌더링 기술 학습 필수
- 웹 프론트엔드 - 클라이언트 사이드 렌더링 기술
    - React, Vue.js
    - 복잡하고 동적인 UI 사용
    - 웹 프론트엔드 개발자의 전문 분야
- 선택과 집중
    - 백엔드 개발자의 웹 프론트엔드 기술 학습은 옵션
    - 백엔드 개발자는 서버, DB, 인프라 등등 수 많은 백엔드 기술을 공부해야 한다.
    - 웹 프론트엔드도 깊이있게 잘 하려면 숙련에 오랜 시간이 필요하다.


### 자바 웹 기술 역사
#### 과거 기술
- 서블릿 - 1997
    - HTML 생성이 어려움 (JAVA 코드로 짜야함)
- JSP - 1999
    - HTML 생성은 편리하지만, 비즈니스 로직까지 너무 많은 역할 담당
- 서블릿, JSP 조합 MVC 패턴 사용
    - 모델, 뷰 컨트롤러로 역할을 나누어 개발
- MVC 프레임워크 춘추 전국 시대 - 2000년 초 ~ 2010년 초
    - MVC 패턴 자동화, 복잡한 웹 기술을 편리하게 사용할 수 있는 다양한 기능 지원
    - 스트럿츠, 웹워크, 스프링 MVC(과거 버전)

#### 현재 사용 기술

- 애노테이션 기반의 스프링 MVC 등장
    - @Controller
    - MVC 프레임워크의 춘추 전국 시대 마무리
- 스프링 부트의 등장
    - 스프링 부트는 서버를 내장
    - 과거에는 서버에 WAS를 직접 설치하고, 소스는 War 파일을 만들어서 설치한 WAS에 배포 
    - 스프링 부트는 빌드 결과(Jar)에 WAS 서버 포함 -> 빌드 배포 단순화

#### 최신 기술 - 스프링 웹 기술의 분화
- Web Servlet - Spring MVC
- Web Reactive - Spring WebFlux

#### 스프링 웹 플럭스(WebFlux)

- 특징
    - 비동기 넌 블러킹 처리
    - 최소 쓰레드로 최대 성능 - 쓰레드 컨텍스트 스위칭 비용 효율화 
    - 함수형 스타일로 개발 - 동시처리 코드 효율화
    - 서블릿 기술 사용X
- 그런데
    - 웹 플럭스는 기술적 난이도 매우 높음
    - 아직은 RDB 지원 부족
    - 일반 MVC의 쓰레드 모델도 충분히 빠르다. 
    - 실무에서 아직 많이 사용하지는 않음 (전체 1% 이하)



#### 자바 뷰 템플릿 역사
- HTML을 편리하게 생성하는 뷰 기능


- JSP
    - 속도 느림, 기능 부족
- 프리마커(Freemarker), Velocity(벨로시티)
    - 속도 문제 해결, 다양한 기능
- 타임리프(Thymeleaf)
    - 내추럴 템플릿: HTML의 모양을 유지하면서 뷰 템플릿 적용 가능
    - 스프링 MVC와 강력한 기능 통합
    - 최선의 선택, 단 성능은 프리마커, 벨로시티가 더 빠름


## 서블릿

### 프로젝트 생성

- Java 11 설치
- IDE: IntelliJ 또는 Eclipse 설치

스프링 부트 스타터 사이트로 이동해서 스프링 프로젝트 생성
[스프링 스타터](https://start.spring.io)

- 프로젝트 선택
    - Project: Gradle - Groovy Project 
    - Language: Java
    - Spring Boot: 2.4.x
- Project Metadata 
    - Group: hello
    - Artifact: servlet
    - Name: servlet
    - Package name: hello.servlet
    - Packaging: War (주의!) 
    - Java: 11

- Dependencies: Spring Web, Lombok

> Packaging에서 War를 선택하는 이유는 JSP를 실행하기 위해서 임.

- 동작 확인
    - 기본 메인 클래스 실행( ServletApplication.main() ) 
    - http://localhost:8080 호출해서 Whitelabel Error Page가 나오면 정상 동작


#### IntelliJ Gradle 대신에 자바 직접 실행
-> 최근 IntelliJ 버전은 Gradle을 통해서 실행 하는 것이 기본 설정이다. 이렇게 하면 실행속도가 느리다.
다음과 같이 변경하면 자바로 바로 실행해서 실행속도가 더 빠르다

- Preferences -> Build, Execution, Deployment -> Build Tools -> Gradle 
    - Build and run using: Gradle IntelliJ IDEA
    - Run tests using: Gradle IntelliJ IDEA


> 주의!
> IntelliJ 무료 버전의 경우 해당 설정을 IntelliJ IDEA가 아니라 Gradle로 설정해야 한다.
> Jar 파일의 경우는 문제가 없는데, War의 경우 톰캣이 정상 시작되지 않는 문제가 발생한다.
> 유료 버전은 모두 정상 동작한다.
>
> 또는 build.gradle 에 있는 다음 코드를 제거해도 된다.
> providedRuntime 'org.springframework.boot:spring-boot-starter-tomcat'

#### 롬복 적용

1. Preferences plugin lombok 검색 실행 (재시작)
2. Preferences Annotation Processors 검색 Enable annotation processing 체크 (재시작) 
3. 임의의 테스트 클래스를 만들고 @Getter, @Setter 확인




#### Postman을 설치하자
-> 다음 사이트에서 Postman을 다운로드 받고 설치해두자 (API )

[https://www.postman.com/downloads](https://www.postman.com/downloads)


## [서블릿 프로젝트 링크](https://github.com/Hoya324/servlet)

### Hello 서블릿
- 스프링 부트 환경에서 서블릿 등록하고 사용해보자.

> 서블릿은 톰캣 같은 웹 애플리케이션 서버를 직접 설치하고,그 위에 서블릿 코드를 클래스 파일로 빌드해서
올린 다음, 톰캣 서버를 실행하면 된다. 하지만 이 과정은 매우 번거롭다.
> 스프링 부트는 톰캣 서버를 내장하고 있으므로, 톰캣 서버 설치 없이 편리하게 서블릿 코드를 실행할 수
있다.


### 스프링 부트 서블릿 환경 구성

#### @ServletComponentScan
스프링 부트는 서블릿을 직접 등록해서 사용할 수 있도록 @ServletComponentScan을 지원한다. 다음과
같이 추가하자.
<img width="1378" alt="스크린샷 2023-02-12 오후 9 05 37" src="https://user-images.githubusercontent.com/96857599/218310011-97ac5582-33d3-4d0a-8c20-96e0328eaf3d.png">


#### 서블릿 등록

<img width="1378" alt="스크린샷 2023-02-12 오후 9 04 47" src="https://user-images.githubusercontent.com/96857599/218309983-ca738d62-00dd-4ca3-8d96-32fc52163b13.png">

- 실행 로그 및 화면

<img width="1378" alt="스크린샷 2023-02-12 오후 9 06 16" src="https://user-images.githubusercontent.com/96857599/218310037-890c47a1-7d5d-42df-8181-7d56a8059ba2.png">

<img width="1348" alt="스크린샷 2023-02-12 오후 9 06 25" src="https://user-images.githubusercontent.com/96857599/218310045-f28a9108-c662-468c-ab73-4609161b840c.png">


- tomcat이 서블릿 인터페이스를 구현한 구현체
<img width="1378" alt="스크린샷 2023-02-12 오후 9 08 29" src="https://user-images.githubusercontent.com/96857599/218310154-be8d2ec6-f07e-45bd-9727-55c3fa09b172.png">



- request.getParameter로 HTTP 쿼리 파라미터 

<img width="1378" alt="스크린샷 2023-02-12 오후 9 25 46" src="https://user-images.githubusercontent.com/96857599/218310939-a0c2cc55-5d20-4502-adc6-04d3a0db5104.png">

![스크린샷 2023-02-12 오후 9 25 42](https://user-images.githubusercontent.com/96857599/218310972-08478f1d-4aa1-4233-b7b6-5ca32f87aad7.png)

- HTTP 헤더, 바디에 response 메세지 담기
<img width="1334" alt="스크린샷 2023-02-12 오후 9 32 05" src="https://user-images.githubusercontent.com/96857599/218311243-e2c325de-830d-4981-889d-56c5772dc594.png">

<img width="1348" alt="스크린샷 2023-02-12 오후 9 32 15" src="https://user-images.githubusercontent.com/96857599/218311245-2b9989cf-b686-4103-9da1-465ce8462d13.png">

- 한글도 됨
<img width="1348" alt="스크린샷 2023-02-12 오후 9 33 55" src="https://user-images.githubusercontent.com/96857599/218311318-465ccd71-2f35-4853-9b89-8c304193d8bc.png">


- @WebServlet 서블릿 애노테이션
    - name: 서블릿 이름
    - urlPatterns: URL 매핑
    - 두 가지 모두 겹치면 안 됨
    


#### TIP💡 HTTP 요청 메세지 모두 보기
    - application.properties에 아래 내용 추가
    logging.level.org.apache.coyote.http11=debug
<img width="1378" alt="스크린샷 2023-02-12 오후 9 37 51" src="https://user-images.githubusercontent.com/96857599/218311515-bb2e7839-bb1e-47b2-b206-3e276faaa920.png">

> 참고
> 운영서버에 이렇게 모든 요청 정보를 다 남기면 성능저하가 발생할 수 있다. 개발 단계에서만 적용하자.
    
    
### 서블릿 컨테이너 동작 방식 설명

#### 내장 톰캣 서버 생성

- 스프링 부트가 실행하면서 내장 톰켓 서버를 생성해준다.
- 내장 톰켓 서버가 서블릿 컨테이너를 통해 helloServlet을 생성해준다.
<img width="534" alt="스크린샷 2023-02-12 오후 9 40 05" src="https://user-images.githubusercontent.com/96857599/218311633-ddb6434d-43b8-4de7-9cab-c7c178dc5a69.png">

- HTTP 요청, HTTP 응답 메시지 작성
<img width="520" alt="스크린샷 2023-02-12 오후 9 40 12" src="https://user-images.githubusercontent.com/96857599/218311641-755df0ba-d407-4ca2-b6f5-b850fcd5584d.png">

- WAS의 요청 응답 구조
<img width="546" alt="스크린샷 2023-02-12 오후 9 40 20" src="https://user-images.githubusercontent.com/96857599/218311649-bdd61df4-34e8-4ce2-a39c-c3c49473bf46.png">

    
> 참고
> HTTP 응답에서 Content-Length는 웹 애플리케이션 서버가 자동으로 생성
    
    
### welcome 페이지 추가

- webapp 경로에 index.html 을 두면 http://localhost:8080 호출시 index.html 페이지가 열린다.
<img width="1378" alt="스크린샷 2023-02-12 오후 9 49 26" src="https://user-images.githubusercontent.com/96857599/218312057-2cf19979-3f49-4b51-9c72-de7dff692706.png">

<img width="1348" alt="스크린샷 2023-02-12 오후 9 50 05" src="https://user-images.githubusercontent.com/96857599/218312087-720160a3-9e84-4c87-94cb-0f311b61dbe8.png">


- 이번 장에서 학습할 내용은 다음 basic.html 이다.

<img width="1378" alt="스크린샷 2023-02-12 오후 9 49 51" src="https://user-images.githubusercontent.com/96857599/218312074-197581a9-db31-4fe6-8e15-981f3ab4543c.png">

<img width="1348" alt="스크린샷 2023-02-12 오후 9 50 18" src="https://user-images.githubusercontent.com/96857599/218312096-9d4f39bd-5f18-4092-9b96-c597021b107a.png">

    
### HttpServletRequest - 개요

### HttpServletRequest 역할

- HTTP 요청 메시지를 개발자가 직접 파싱해서 사용해도 되지만, 매우 불편할 것이다. 서블릿은 개발자가 HTTP 요청 메시지를 편리하게 사용할 수 있도록 개발자 대신에 HTTP 요청 메시지를 파싱한다. 그리고 그 결과를 HttpServletRequest 객체에 담아서 제공한다.

- HttpServletRequest를 사용하면 다음과 같은** HTTP 요청 메시지를 편리하게 조회**할 수 있다.
    

#### HTTP 요청 메시지

<img width="518" alt="스크린샷 2023-02-13 오후 3 01 41" src="https://user-images.githubusercontent.com/96857599/218382435-b46fdf2a-7fb0-4189-8614-a8f8e59dd311.png">


- START LINE
    - HTTP 메소드
    - URL
    - 쿼리 스트링
    - 스키마, 프로토콜 
- 헤더
    - 헤더 조회
- 바디
    - form 파라미터 형식 조회 (쿼리 파라미터 조회 가능)
    - message body 데이터 직접 조회 (json 데이터 조회)


- HttpServletRequest 객체는 추가로 여러가지 부가기능도 함께 제공한다.


#### 임시 저장소 기능

- 해당 HTTP 요청이 시작부터 끝날 때 까지 유지되는 임시 저장소 기능 
    - 저장: request.setAttribute(name, value)
    - 조회: request.getAttribute(name)

#### 세션 관리 기능

- request.getSession(create: true)

> 중요 ⭐️
> HttpServletRequest, HttpServletResponse를 사용할 때 가장 중요한 점은 이 객체들이 HTTP 요청 메시지, HTTP 응답 메시지를 편리하게 사용하도록 도와주는 객체라는 점이다. 따라서 이 기능에 대해서 깊이있는 이해를 하려면 HTTP 스펙이 제공하는 요청, 응답 메시지 자체를 이해해야 한다.


### HttpServletRequest - 기본 사용법

- HttpServletRequest가 제공하는 기본 기능들을 알아보자.


- hello.servlet.basic.resquest에 RequestHeaderServlet을 만든다.
- @WebServlet(name = "requestHeaderServlet", urlPatterns = "/request-header")
- cmd + O 로 service 메서드를 오버라이딩해준다.
<img width="1378" alt="스크린샷 2023-02-13 오후 3 12 31" src="https://user-images.githubusercontent.com/96857599/218384002-504e6074-9777-445f-be81-55f5c37c9193.png">


#### HTTP request startline 메시지 보기

<img width="1348" alt="스크린샷 2023-02-13 오후 3 22 04" src="https://user-images.githubusercontent.com/96857599/218385520-bf787cb5-940e-4171-93f5-ce148c6688da.png">

<img width="1378" alt="스크린샷 2023-02-13 오후 3 21 22" src="https://user-images.githubusercontent.com/96857599/218385411-8f5f1c2f-0e07-4ade-81e9-befc3f052f93.png">


#### 헤더 정보(Enumeration- 옛날 방식)
<img width="1378" alt="스크린샷 2023-02-13 오후 3 29 02" src="https://user-images.githubusercontent.com/96857599/218386669-f2b9b383-bf73-40a1-9ff7-6a6b798b5502.png">

#### 헤더 정보(요즘 방식)
<img width="1378" alt="스크린샷 2023-02-13 오후 3 31 18" src="https://user-images.githubusercontent.com/96857599/218387021-8712be5d-a500-435c-a3ff-57d7b628fca7.png">

#### Header 편리한 조회

<img width="1378" alt="스크린샷 2023-02-13 오후 3 36 59" src="https://user-images.githubusercontent.com/96857599/218387901-f4293fa1-1bd6-43aa-82cf-e68637e4f3b7.png">

- 선호 언어, 쿠키, Content의 정보를 보여줌
<img width="1378" alt="스크린샷 2023-02-13 오후 3 36 46" src="https://user-images.githubusercontent.com/96857599/218387874-f56db745-9c2b-4eb4-8f1a-e9a873444829.png">


- 위의 상황은 Get으로 조회한 Http의 헤더 정보이기 때문에 postman으로 Post 방식으로 정보를 받아본다.

<img width="1484" alt="스크린샷 2023-02-13 오후 3 47 05" src="https://user-images.githubusercontent.com/96857599/218389495-4cb392b9-a3e6-4175-bf53-276a8d82b180.png">

<img width="1484" alt="스크린샷 2023-02-13 오후 3 47 13" src="https://user-images.githubusercontent.com/96857599/218389533-f3d86f27-bd68-4a9b-98d4-ae6f1368f06c.png">

- 결과 (Content 내용이 변경된 것을 알 수 있다.)

<img width="1378" alt="스크린샷 2023-02-13 오후 3 47 47" src="https://user-images.githubusercontent.com/96857599/218389629-9e8246e7-a5bb-4a10-9260-c964d4bb9514.png">

- header에서 정보 하나만 가지고 싶으면.
<img width="571" alt="스크린샷 2023-02-13 오후 3 50 03" src="https://user-images.githubusercontent.com/96857599/218390017-9866b700-f8d5-429b-914a-c0e85835f231.png">

#### 기타 정보
- ![image](https://user-images.githubusercontent.com/96857599/218390150-4488b28e-1392-4dc2-a833-0f2edd7117e1.png)

<img width="1378" alt="스크린샷 2023-02-13 오후 3 53 17" src="https://user-images.githubusercontent.com/96857599/218390567-6b4d22cc-614f-4dbc-a99d-810d6fe7516f.png">

>참고
> 로컬에서 테스트하면 IPv6 정보가 나오는데, IPv4 정보를 보고 싶으면 다음 옵션을 VM options에
넣어주면 된다.
> -Djava.net.preferIPv4Stack=true

- 지금까지 HttpServletRequest를 통해서 HTTP 메시지의 start-line, header 정보 조회 방법을 이해했다. 이제 본격적으로 HTTP 요청 데이터를 어떻게 조회하는지 알아보자.


### HTTP 요청 데이터 - 개요

-> HTTP 요청 메시지를 통해 클라이언트에서 서버로 데이터를 전달하는 방법을 알아보자.

주로 다음 3가지 방법을 사용한다. 
- GET - 쿼리 파라미터
    - /url?username=hello&age=20
    - 메시지 바디 없이, URL의 쿼리 파라미터에 데이터를 포함해서 전달 
    - 예) 검색, 필터, 페이징등에서 많이 사용하는 방식
- POST - HTML Form
<img width="484" alt="스크린샷 2023-02-18 오후 2 55 36" src="https://user-images.githubusercontent.com/96857599/219843827-be76a03d-a983-47d8-8095-9411ab3c6425.png">
    - content-type: application/x-www-form-urlencoded
    - 메시지 바디에 쿼리 파리미터 형식으로 전달 username=hello&age=20
    - 예) 회원 가입, 상품 주문, HTML Form 사용
- HTTP message body에 데이터를 직접 담아서 요청 
    - HTTP API에서 주로 사용, JSON, XML, TEXT
- 데이터 형식은 주로 JSON 사용 
    - POST, PUT, PATCH
    
    
### HTTP 요청 데이터 - GET 쿼리 파라미터
-> 다음 데이터를 클라이언트에서 서버로 전송해보자

전달 데이터
username=hello age=20

- 메시지 바디 없이, URL의 쿼리 파라미터를 사용해서 데이터를 전달하자. 
- 예) 검색, 필터, 페이징등에서 많이 사용하는 방식

- 쿼리파라미터는URL에다음과같이 ?를시작으로보낼수있다.추가파라미터는 &로구분하면된다. 
    - http://localhost:8080/request-param?username=hello&age=20
    
    
- 서버에서는 HttpServletRequest 가 제공하는 다음 메서드를 통해 쿼리 파라미터를 편리하게 조회할 수 있다.

#### 쿼리 파라미터 조회 메서드

URL 및 쿼리 : http://localhost:8080/request-param?username=hello&age=20 

- 서버 작동 여부 확인
<img width="1582" alt="스크린샷 2023-02-18 오후 3 08 04" src="https://user-images.githubusercontent.com/96857599/219844239-85e5b5bd-2d65-48a4-88f6-cbaf276b5f3a.png">

- 전체 파라미터 조회
<img width="1495" alt="스크린샷 2023-02-18 오후 3 13 32" src="https://user-images.githubusercontent.com/96857599/219844474-0f29ac62-51fe-432f-8574-c89dc2e00ccc.png">

- 단일 파라미터 조회
<img width="1495" alt="스크린샷 2023-02-18 오후 3 25 03" src="https://user-images.githubusercontent.com/96857599/219844898-efe9b60a-05f9-4717-9f1e-3a7c972c0f06.png">

- 이름이 같은 복수 파라미터 조회
- URL 및 쿼리 : http://localhost:8080/request-param?username=hello&age=20&username=hello2
<img width="1495" alt="스크린샷 2023-02-18 오후 3 32 03" src="https://user-images.githubusercontent.com/96857599/219845229-90587507-9a08-42a4-853e-fd375ef1043f.png">
> 복수 파라미터에서 단일 파라미터 조회
> username=hello&username=kim 과 같이 파라미터 이름은 하나인데, 값이 중복이면 어떻게 될까? request.getParameter() 는 하나의 파라미터 이름에 대해서 단 하나의 값만 있을 때 사용해야 한다. 지금처럼 중복일 때는 request.getParameterValues() 를 사용해야 한다.
> 참고로 이렇게 중복일 때 request.getParameter() 를 사용하면 request.getParameterValues() 의 첫 번째 값을 반환한다.

- response 해보기
<img width="1495" alt="스크린샷 2023-02-18 오후 3 33 54" src="https://user-images.githubusercontent.com/96857599/219845299-0aefdb66-2aec-4c80-9281-9d42a5ca3cc8.png">

> HTTP 요청 데이터 - GET 쿼리 파라미터에서 request.getParameter를 가장 많이 쓴다.



### HTTP 요청 데이터 - POST HTML Form
-> 이번에는 HTML의 Form을 사용해서 클라이언트에서 서버로 데이터를 전송해보자.
-> 주로 회원 가입, 상품 주문 등에서 사용하는 방식이다.

#### 특징
- content-type: application/x-www-form-urlencoded
- 메시지 바디에 쿼리 파리미터 형식으로 데이터를 전달한다. username=hello&age=20

#### src/main/webapp/basic/hello-form.html 생성
<img width="1495" alt="스크린샷 2023-02-18 오후 3 43 08" src="https://user-images.githubusercontent.com/96857599/219845733-db79f851-5905-466b-b64d-f9780e46afc5.png">

- 실행
<img width="1208" alt="스크린샷 2023-02-18 오후 3 43 32" src="https://user-images.githubusercontent.com/96857599/219845756-c4acb6c5-8488-4b8f-b2fe-f28b08e1da9f.png">

- 응답
<img width="1208" alt="스크린샷 2023-02-18 오후 3 43 54" src="https://user-images.githubusercontent.com/96857599/219845775-af80a60f-6aa3-45a9-a0c9-458c2e650cf3.png">

- 전에 작성했던 /request-param의 로그가 나옴
<img width="1495" alt="스크린샷 2023-02-18 오후 3 44 16" src="https://user-images.githubusercontent.com/96857599/219845790-d84896da-82b9-4da5-887e-66567de4924e.png">

- Form Data
<img width="1208" alt="스크린샷 2023-02-18 오후 3 46 11" src="https://user-images.githubusercontent.com/96857599/219845867-e48d8243-0115-49d8-a6ca-0f7bf79e0a14.png">

- Form Data resource
<img width="1208" alt="스크린샷 2023-02-18 오후 3 46 51" src="https://user-images.githubusercontent.com/96857599/219845903-2cea9608-d91b-433f-9bb0-eb70d92d77d9.png">

> 웹 브라우저가 전송한 데이터와 content-Type을 작성해주는 것임

> 주의
> 웹 브라우저가 결과를 캐시하고 있어서, 과거에 작성했던 html 결과가 보이는 경우도 있다. 이때는 웹 브라우저의 새로 고침을 직접 선택해주면 된다. 물론 서버를 재시작 하지 않아서 그럴 수도 있다.

- POST의 HTML Form을 전송하면 웹 브라우저는 다음 형식으로 HTTP 메시지를 만든다. (웹 브라우저 개발자 모드 확인)
- 요청 URL: http://localhost:8080/request-param
- content-type: application/x-www-form-urlencoded 
- message body: username=hello&age=20

- application/x-www-form-urlencoded 형식은 앞서 GET에서 살펴본 쿼리 파라미터 형식과 같다.
- 따라서 쿼리 파라미터 조회 메서드를 그대로 사용하면 된다.
- 클라이언트(웹 브라우저) 입장에서는 두 방식에 차이가 있지만, 서버 입장에서는 둘의 형식이 동일하므로, 
- request.getParameter() 로 편리하게 구분없이 조회할 수 있다.
 
- ⭐️정리하면 request.getParameter() 는 GET URL 쿼리 파라미터 형식도 지원하고, POST HTML Form 형식도 둘 다 지원한다.

> 참고
> content-type은 HTTP 메시지 바디의 데이터 형식을 지정한다.
>**GET URL 쿼리 파라미터 형식** 으로 클라이언트에서 서버로 데이터를 전달할 때는 HTTP 메시지 바디를
사용하지 않기 때문에 content-type이 없다.
> **POST HTML Form** 형식으로 데이터를 전달하면 HTTP 메시지 바디에 해당 데이터를 포함해서 보내기
때문에 바디에 포함된 데이터가 어떤 형식인지 content-type을 꼭 지정해야 한다. 이렇게 폼으로 데이터를 전송하는 형식을 application/x-www-form-urlencoded 라 한다.

#### Postman을 사용한 테스트
이런 간단한 테스트에 HTML form을 만들기는 귀찮다. 이때는 Postman을 사용하면 된다.

Postman 테스트 주의사항 
- POST 전송시
- Body -> x-www-form-urlencoded 선택
- Headers에서 content-type: application/x-www-form-urlencoded 로 지정된 부분 꼭 확인


- http://localhost:8080/request-param에 Post 방식으로 Key, Value를 넘김
- x-www-form-urlencoded 선택
<img width="1484" alt="스크린샷 2023-02-18 오후 3 59 20" src="https://user-images.githubusercontent.com/96857599/219846435-dcbd51f9-5eac-4cab-89dd-1f70902d512a.png">

- Content-Type 확인
<img width="1484" alt="스크린샷 2023-02-18 오후 4 00 32" src="https://user-images.githubusercontent.com/96857599/219846486-5e002f96-ea3b-4888-8095-5cf7244507a5.png">

- 결과
<img width="1495" alt="스크린샷 2023-02-18 오후 4 01 02" src="https://user-images.githubusercontent.com/96857599/219846506-772d9201-252c-4a2e-910a-7ab09f860c63.png">

### HTTP 요청 데이터 - API 메시지 바디 - 단순 텍스트
- **HTTP message body**에 데이터를 직접 담아서 요청
    - HTTP API에서 주로 사용, JSON, XML, TEXT 
    - 데이터 형식은 주로 JSON 사용
    - POST, PUT, PATCH

- 먼저 가장 단순한 텍스트 메시지를 HTTP 메시지 바디에 담아서 전송하고, 읽어보자. 
- HTTP 메시지 바디의 데이터를 InputStream을 사용해서 직접 읽을 수 있다.

<img width="1495" alt="스크린샷 2023-02-18 오후 4 09 36" src="https://user-images.githubusercontent.com/96857599/219846872-a85dc840-9bb6-4838-9255-590a67eb5b41.png">

Postman을 사용해서 테스트 해보자.

> 참고
> inputStream은 byte 코드를 반환한다. byte 코드를 우리가 읽을 수 있는 문자(String)로 보려면 문자표
(Charset)를 지정해주어야 한다. 여기서는 UTF_8 Charset을 지정해주었다.

- 문자 전송
    - POST http://localhost:8080/request-body-string content-type: text/plain
    - message body: hello
    - 결과: messageBody = hello

<img width="1484" alt="스크린샷 2023-02-18 오후 4 11 39" src="https://user-images.githubusercontent.com/96857599/219846944-b0925a5c-b3ca-4d57-b07a-31926abc3c45.png">

- 결과
<img width="1495" alt="스크린샷 2023-02-18 오후 4 12 01" src="https://user-images.githubusercontent.com/96857599/219846962-cb34cf2e-85b8-4200-9d0b-1648877f64ae.png">



### HTTP 요청 데이터 - API 메시지 바디 - JSON
- 이번에는 HTTP API에서 주로 사용하는 JSON 형식으로 데이터를 전달해보자.

**JSON 형식 전송**
- POST http://localhost:8080/request-body-json 
- content-type: application/json
- message body: {"username": "hello", "age": 20} 
- 결과: messageBody = {"username": "hello", "age": 20}


#### JSON 형식 파싱 추가
-JSON 형식으로 파싱할 수 있게 객체를 하나 생성하자

hello.servlet.basic.HelloData
<img width="1495" alt="스크린샷 2023-02-18 오후 4 19 40" src="https://user-images.githubusercontent.com/96857599/219847274-5af6474b-45c9-4e56-88c2-cffcea9edc7c.png">

hello.servlet.basic.request.RequestBodyJsonServlet
<img width="1495" alt="스크린샷 2023-02-18 오후 4 27 49" src="https://user-images.githubusercontent.com/96857599/219847708-d2d0a2d1-dcbf-4eec-b723-3dc4b86082d7.png">

- postman으로 json 전송
<img width="1484" alt="스크린샷 2023-02-18 오후 4 24 33" src="https://user-images.githubusercontent.com/96857599/219847497-b172ae9e-1323-435b-b8d1-59c06e294ae3.png">

- 결과
<img width="1495" alt="스크린샷 2023-02-18 오후 4 24 46" src="https://user-images.githubusercontent.com/96857599/219847505-f3420195-d459-49d4-ab4b-38704b02ce69.png">

- Json 결과 파싱해서 사용

> 참고
> JSON 결과를 파싱해서 사용할 수 있는 자바 객체로 변환하려면 Jackson, Gson 같은 JSON 변환
> 라이브러리를 추가해서 사용해야 한다. 스프링 부트로 Spring MVC를 선택하면 기본으로 Jackson 라이브러리( ObjectMapper )를 함께 제공한다.

<img width="1495" alt="스크린샷 2023-02-18 오후 4 30 56" src="https://user-images.githubusercontent.com/96857599/219847827-588a0f00-f674-426f-9e63-773967101415.png">

<img width="1495" alt="스크린샷 2023-02-18 오후 4 53 43" src="https://user-images.githubusercontent.com/96857599/219848780-15215a91-e544-4d3b-940f-9f457f893290.png">

<img width="1484" alt="스크린샷 2023-02-18 오후 4 55 20" src="https://user-images.githubusercontent.com/96857599/219848844-643071f6-b95c-4845-bd31-4898efb386e9.png">


> 참고
> HTML form 데이터도 메시지 바디를 통해 전송되므로 직접 읽을 수 있다. 하지만 편리한 파리미터 조회 기능( request.getParameter(...) )을 이미 제공하기 때문에 파라미터 조회 기능을 사용하면 된다.



### HttpServletResponse - 기본 사용법
- HTTPServletResponse 역할

#### HTTP 응답 메시지 생성
- HTTP 응답코드 지정
- 헤더 생성
- 바디 생성

**편의 기능 제공**
- Content-Type, 쿠키, Redirect

- hello.servlet.basic.response.ResponseHeaderServlet
<img width="1337" alt="스크린샷 2023-02-20 오후 3 05 34" src="https://user-images.githubusercontent.com/96857599/220023252-7762796d-d5f9-42ee-bcb4-e122a19c86ee.png">

- 응답 상태코드
<img width="1337" alt="스크린샷 2023-02-20 오후 3 04 42" src="https://user-images.githubusercontent.com/96857599/220023051-3bf9ee9e-3bba-4390-acd6-5f5ba051227f.png">

### 기본 사용법

- 성공
<img width="1337" alt="스크린샷 2023-02-20 오후 3 17 36" src="https://user-images.githubusercontent.com/96857599/220026142-28d23123-095e-4872-a53a-85c0631b57da.png">

<img width="1208" alt="스크린샷 2023-02-20 오후 3 18 02" src="https://user-images.githubusercontent.com/96857599/220026252-43a2cacc-97cc-41f6-96eb-81943b054420.png">

- 실패
<img width="1337" alt="스크린샷 2023-02-20 오후 3 20 05" src="https://user-images.githubusercontent.com/96857599/220026756-be3305c8-efd2-48b8-9f9e-58543d7a9aad.png">

<img width="1208" alt="스크린샷 2023-02-20 오후 3 20 29" src="https://user-images.githubusercontent.com/96857599/220026871-807223f4-10a9-4247-a7ab-7910446f7c62.png">

- Header 편의 메서드
Content, Cookie, Redirect
<img width="1337" alt="스크린샷 2023-02-20 오후 3 37 16" src="https://user-images.githubusercontent.com/96857599/220031222-a2348e1b-62d4-4279-b961-4bce5abc2045.png">


- Content, Cookie 편의 메서드 사용 결과 Response Headers와 Request Headers
- Content : Content-Type: text/plain;charset=utf-8
            Content-Length: 2
            위를 표현하기 위해
            
            response.setHeader("Content-Type", "text/plain;charset=utf-8");
            response.setContentLength(2); //(생략시 자동 생성, 입력시 임의 설정 가능)
            를 사용할 수 있지만,
            
            response.setContentType("text/plain");
            response.setCharacterEncoding("utf-8");
            를 사용하는 것이 더 깔끔함.
            
 - Cookie : Set-Cookie: myCookie=testing; Max-Age=600
            위를 표현하기 위해
            
            response.setHeader("Set-Cookie", "myCookie=testing; Max-Age=600");
            보단,
            
            Cookie cookie = new Cookie("myCookie", "testing");
            cookie.setMaxAge(600); //600초
            response.addCookie(cookie);
            를 사용.

<img width="1114" alt="스크린샷 2023-02-20 오후 3 51 03" src="https://user-images.githubusercontent.com/96857599/220033700-4d17036e-8ae2-48cd-a712-5caffcf1e2d1.png">


- Redirect 편의 메서드 사용 결과 
- Redirect : Status Code 302
             Location: /basic/hello-form.html
             위를 표현하기 위해
             
             response.setStatus(HttpServletResponse.SC_FOUND); //302
             response.setHeader("Location", "/basic/hello-form.html");
             보단, 
             
             response.sendRedirect("/basic/hello-form.html");
             를 사용.
<img width="1114" alt="스크린샷 2023-02-20 오후 3 59 00" src="https://user-images.githubusercontent.com/96857599/220034977-597aa105-8746-45fa-8752-a5ccd8b9c4d7.png">

- message body
<img width="1337" alt="스크린샷 2023-02-20 오후 4 02 15" src="https://user-images.githubusercontent.com/96857599/220035535-6dd9aa38-4d19-4aaf-975c-dbc70eec01bc.png">



### HTTP 응답 데이터 - HTML

<img width="1582" alt="스크린샷 2023-02-23 오후 1 22 00" src="https://user-images.githubusercontent.com/96857599/220820807-1eac6fbf-310e-4d99-bac6-c44d8aaed518.png">

- 결과
	
<img width="1057" alt="스크린샷 2023-02-23 오후 1 23 55" src="https://user-images.githubusercontent.com/96857599/220821006-c6c41ab8-9657-4943-bf89-88f9bd10e63c.png">


<img width="1057" alt="스크린샷 2023-02-23 오후 1 24 22" src="https://user-images.githubusercontent.com/96857599/220821046-bd933f8d-ceea-46e7-b4c3-941873d64c6f.png">

	
	
### HTTP 응답 데이터 - API JSON
	
- HTTP API(rest API)를 보낼 때 사용
	
<img width="1439" alt="스크린샷 2023-02-23 오후 1 33 47" src="https://user-images.githubusercontent.com/96857599/220822031-d1281d5f-516d-4d59-b9ef-b27a1022a571.png">

- 결과	
<img width="1057" alt="스크린샷 2023-02-23 오후 1 33 38" src="https://user-images.githubusercontent.com/96857599/220822017-25f1224c-d1de-400d-be32-54dff48cd033.png">

- HTTP 응답으로 JSON을 반환할 때는 content-type을 application/json 로 지정해야 한다. Jackson 라이브러리가 제공하는 objectMapper.writeValueAsString() 를 사용하면 객체를 JSON 문자로 변경할 수 있다.

> 참고
> application/json 은 스펙상 utf-8 형식을 사용하도록 정의되어 있다. 그래서 스펙에서 charset=utf-8
과 같은 추가 파라미터를 지원하지 않는다. 따라서 application/json 이라고만 사용해야지
> application/json;charset=utf-8 이라고 전달하는 것은 의미 없는 파라미터를 추가한 것이 된다. 
> response.getWriter()를 사용하면 추가 파라미터를 자동으로 추가해버린다. 이때는
>  response.getOutputStream()으로 출력하면 그런 문제가 없다.
	

## 서블릿, JSP, MVC

### 회원 관리 웹 애플리케이션 요구사항
회원 정보
이름: username 나이: age
기능 요구사항
- 회원 저장
- 회원 목록 조회

#### 회원 도메인 모델
<img width="1439" alt="스크린샷 2023-02-23 오후 2 22 59" src="https://user-images.githubusercontent.com/96857599/220827224-5cfaa5a6-bcd4-4217-9acc-3e1498dc2bda.png">

#### 회원 저장소
<img width="1439" alt="스크린샷 2023-02-23 오후 2 32 13" src="https://user-images.githubusercontent.com/96857599/220828109-33b5f81d-feb7-4a0e-8bad-64ac37825fdc.png">
<img width="1439" alt="스크린샷 2023-02-23 오후 2 32 21" src="https://user-images.githubusercontent.com/96857599/220828123-5ee51cb2-a6f8-47f3-b14f-d476b4c5540e.png">


- save 테스트코드 작성 (MemberRepository에서 cmd+shift+t 하면 생성됨)
<img width="1439" alt="스크린샷 2023-02-23 오후 2 38 24" src="https://user-images.githubusercontent.com/96857599/220828863-574fffde-20bc-4de9-bb3b-ca448998d5da.png">

- findAll 테스트코드 작성
<img width="1439" alt="스크린샷 2023-02-23 오후 2 46 30" src="https://user-images.githubusercontent.com/96857599/220829706-455b2f76-83ec-4005-80ff-0b804d686d67.png">

### 서블릿으로 회원 관리 웹 애플리케이션 만들기

#### MemberFormServlet - 회원 등록 폼
<img width="1496" alt="스크린샷 2023-02-23 오후 3 19 21" src="https://user-images.githubusercontent.com/96857599/220833652-230e71c9-2c90-40cf-a2b2-e8de942593e9.png">

- MemberFormServlet 은 단순하게 회원 정보를 입력할 수 있는 HTML Form을 만들어서 응답한다. 자바 코드로 HTML을 제공해야 하므로 쉽지 않은 작업이다.

<img width="1057" alt="스크린샷 2023-02-23 오후 3 30 34" src="https://user-images.githubusercontent.com/96857599/220835060-86b0f114-761d-4d6e-a94e-61195a04c3f1.png">

#### MemberSaveServlet - 회원 저장


MemberSaveServlet은 다음 순서로 동작한다.
1. 파라미터를 조회해서 Member 객체를 만든다. (MemberFormServlet에서 회원 등록에 대한 정보를 전송)
2. Member 객체를 MemberRepository를 통해서 저장한다.
3. Member 객체를 사용해서 결과 화면용 HTML을 동적으로 만들어서 응답한다.


<img width="1496" alt="스크린샷 2023-02-23 오후 3 23 39" src="https://user-images.githubusercontent.com/96857599/220834208-2fcf023d-507a-42ef-8458-bef9be038e5a.png">

<img width="1057" alt="스크린샷 2023-02-23 오후 3 30 50" src="https://user-images.githubusercontent.com/96857599/220835092-2d1c75c4-5d92-475b-b1c1-83c4a222bd69.png">


#### MemberListServlet - 회원 목록
<img width="1467" alt="스크린샷 2023-02-23 오후 3 45 38" src="https://user-images.githubusercontent.com/96857599/220837103-14251cd1-204a-4b7c-88e1-5c4844b026b5.png">

<img width="1467" alt="스크린샷 2023-02-23 오후 3 45 45" src="https://user-images.githubusercontent.com/96857599/220837124-3950decf-d597-4b70-899b-ea11202ec579.png">

MemberListServlet 은 다음 순서로 동작한다.
1. memberRepository.findAll()을 통해 모든 회원을 조회한다.
2. 회원 목록 HTML을 for 루프를 통해서 회원 수 만큼 동적으로 생성하고 응답한다.

<img width="1057" alt="스크린샷 2023-02-23 오후 3 45 09" src="https://user-images.githubusercontent.com/96857599/220837041-7f7d3fa0-0c0f-40bb-ae9e-1b53fdf39f24.png">

<img width="1057" alt="스크린샷 2023-02-23 오후 3 46 33" src="https://user-images.githubusercontent.com/96857599/220837242-8b697a14-42ed-43d9-b9c6-0bfa545534fb.png">

<img width="1057" alt="스크린샷 2023-02-23 오후 3 46 41" src="https://user-images.githubusercontent.com/96857599/220837264-e2ec2855-219c-48d6-8be1-ba72c2c1c7b5.png">


**템플릿 엔진으로**
지금까지 서블릿과 자바 코드만으로 HTML을 만들어보았다. 서블릿 덕분에 동적으로 원하는 HTML을 마음껏 만들 수 있다. 정적인 HTML 문서라면 화면이 계속 달라지는 회원의 저장 결과라던가, 회원 목록 같은 동적인 HTML을 만드는 일은 불가능 할 것이다.
그런데, 코드에서 보듯이 이것은 매우 복잡하고 비효율 적이다. 자바 코드로 HTML을 만들어 내는 것 보다 차라리 HTML 문서에 동적으로 변경해야 하는 부분만 자바 코드를 넣을 수 있다면 더 편리할 것이다. 이것이 바로 템플릿 엔진이 나온 이유이다. 템플릿 엔진을 사용하면 HTML 문서에서 필요한 곳만 코드를 적용해서 동적으로 변경할 수 있다.
템플릿 엔진에는 JSP, Thymeleaf, Freemarker, Velocity등이 있다. 다음 시간에는 JSP로 동일한 작업을 진행해보자.


> 참고
> JSP는 성능과 기능면에서 다른 템플릿 엔진과의 경쟁에서 밀리면서, 점점 사장되어 가는 추세이다. 템플릿
> 엔진들은 각각 장단점이 있는데, 강의에서는 JSP는 앞부분에서 잠깐 다루고, 스프링과 잘 통합되는 Thymeleaf를 사용한다.

### JSP로 회원 관리 웹 애플리케이션 만드릭

#### JSP 라이브러리 추가

**스프링 부트 3.0 미만**
- build.gradle 에 추가
<img width="224" alt="스크린샷 2023-02-24 오후 1 18 39" src="https://user-images.githubusercontent.com/96857599/221090720-e0aa2fd0-a274-4c2c-a6ef-e0eb5f9e8ebd.png">

**스프링 부트 3.0 이상**
- build.gradle 에 추가

```java
//JSP 추가 시작
implementation 'org.apache.tomcat.embed:tomcat-embed-jasper'
implementation 'jakarta.servlet:jakarta.servlet-api' //스프링부트 3.0 이상 
implementation 'jakarta.servlet.jsp.jstl:jakarta.servlet.jsp.jstl-api' 
//스프링부트 3.0 이상
implementation 'org.glassfish.web:jakarta.servlet.jsp.jstl' //스프링부트 3.0 이상 
//JSP 추가 끝
```

> 스프링 부트 3.0 이상이면 javax.servlet:jstl 을 제거하고 위 코드를 추가해야 한다.


#### 회원 등록 폼 JSP
- main/webapp/jsp/members/new-form.jsp
- webapp에 만들어야 함.
<img width="1582" alt="스크린샷 2023-02-24 오후 1 24 41" src="https://user-images.githubusercontent.com/96857599/221091374-f7b2384c-7a0b-49f3-abc7-cd0666d94ae7.png">

- index.html에서 지정한 경로로 이동함
<img width="1286" alt="스크린샷 2023-02-24 오후 1 26 33" src="https://user-images.githubusercontent.com/96857599/221091583-9eb45601-89c5-42a4-b83d-759d742aef04.png">

<img width="1057" alt="스크린샷 2023-02-24 오후 1 27 00" src="https://user-images.githubusercontent.com/96857599/221091639-33475b99-0189-4f74-ba71-e5e9d011c874.png">

- 회원 등록 폼
<img width="1057" alt="스크린샷 2023-02-24 오후 1 27 14" src="https://user-images.githubusercontent.com/96857599/221091668-1c651c03-f284-4d97-b3a0-6e89d778083b.png">

- <%@ page contentType="text/html;charset=UTF-8" language="java" %>
	- 첫 줄은 JSP문서라는 뜻이다. JSP 문서는 이렇게 시작해야 한다.

> 회원 등록 폼 JSP를 보면 첫 줄을 제외하고는 완전히 HTML와 똑같다. JSP는 서버 내부에서 서블릿으로 변환되는데, 우리가 만들었던 MemberFormServlet과 거의 비슷한 모습으로 변환된다.

#### 회원 저장 JSP
<img width="1228" alt="스크린샷 2023-02-24 오후 1 46 34" src="https://user-images.githubusercontent.com/96857599/221094099-056e5e8a-57b8-4491-ac9b-4e1eeaf7ca18.png">

JSP는 자바 코드를 그대로 다 사용할 수 있다.
- <%@ page import="hello.servlet.domain.member.MemberRepository" %>
	- 자바의 import 문과 같다. 
- <% ~~ %>
	- 이 부분에는 자바 코드를 입력할 수 있다. 
- <%= ~~ %>
	- 이 부분에는 자바 코드를 출력할 수 있다.

회원 저장 JSP를 보면, 회원 저장 서블릿 코드와 같다. 다른 점이 있다면, HTML을 중심으로 하고, 자바
코드를 부분부분 입력해주었다. <% ~ %> 를 사용해서 HTML 중간에 자바 코드를 출력하고 있다.


#### 회원 목록 JSP
<img width="1228" alt="스크린샷 2023-02-24 오후 1 49 24" src="https://user-images.githubusercontent.com/96857599/221094537-dfd04178-f6dd-44d3-ba4e-af280f6d626d.png">


- 회원 리포지토리를 먼저 조회하고, 결과 List를 사용해서 중간에 <tr><td> HTML 태그를 반복해서 출력하고 있다.

### 서블릿과 JSP의 한계

서블릿으로 개발할 때는 뷰(View)화면을 위한 HTML을 만드는 작업이 자바 코드에 섞여서 지저분하고 복잡했다.
JSP를 사용한 덕분에 뷰를 생성하는 HTML 작업을 깔끔하게 가져가고, 중간중간 동적으로 변경이 필요한 부분에만 자바 코드를 적용했다. 그런데 이렇게 해도 해결되지 않는 몇가지 고민이 남는다.
 
회원 저장 JSP를 보자. 코드의 상위 절반은 회원을 저장하기 위한 비즈니스 로직이고, 나머지 하위 절반만 결과를 HTML로 보여주기 위한 뷰 영역이다. 회원 목록의 경우에도 마찬가지다.
코드를 잘 보면, JAVA 코드, 데이터를 조회하는 리포지토리 등등 다양한 코드가 모두 JSP에 노출되어 있다. JSP가 너무 많은 역할을 한다. 이렇게 작은 프로젝트도 벌써 머리가 아파오는데, 수백 수천줄이 넘어가는 JSP를 떠올려보면 정말 지옥과 같을 것이다.
	

### MVC 패턴 등장

비즈니스 로직은 서블릿 처럼 다른곳에서 처리하고, JSP는 목적에 맞게 HTML로 화면(View)을 그리는 일에 집중하도록 하자. 과거 개발자들도 모두 비슷한 고민이 있었고, 그래서 MVC 패턴이 등장했다. 우리도 직접 MVC 패턴을 적용해서 프로젝트를 리팩터링 해보자.


## MVC 패턴 - 개요
	
**너무 많은 역할**
하나의 서블릿이나 JSP만으로 비즈니스 로직과 뷰 렌더링까지 모두 처리하게 되면, 너무 많은 역할을 하게되고, 결과적으로 유지보수가 어려워진다. 비즈니스 로직을 호출하는 부분에 변경이 발생해도 해당 코드를 손대야 하고, UI를 변경할 일이 있어도 비즈니스 로직이 함께 있는 해당 파일을 수정해야 한다. HTML 코드 하나 수정해야 하는데, 수백줄의 자바 코드가 함께 있다고 상상해보라! 또는 비즈니스 로직을 하나 수정해야 하는데 수백 수천줄의 HTML 코드가 함께 있다고 상상해보라.

**변경의 라이프 사이클**
사실 이게 정말 중요한데, 진짜 문제는 둘 사이에 변경의 라이프 사이클이 다르다는 점이다. 예를 들어서 UI 를 일부 수정하는 일과 비즈니스 로직을 수정하는 일은 각각 다르게 발생할 가능성이 매우 높고 대부분 서로에게 영향을 주지 않는다. 이렇게 변경의 라이프 사이클이 다른 부분을 하나의 코드로 관리하는 것은 유지보수하기 좋지 않다. (물론 UI가 많이 변하면 함께 변경될 가능성도 있다.)

**기능 특화**
특히 JSP 같은 뷰 템플릿은 화면을 렌더링 하는데 최적화 되어 있기 때문에 이 부분의 업무만 담당하는 것이 가장 효과적이다.

**Model View Controller**
MVC 패턴은 지금까지 학습한 것 처럼 하나의 서블릿이나, JSP로 처리하던 것을 컨트롤러(Controller)와 뷰(View)라는 영역으로 서로 역할을 나눈 것을 말한다. 웹 애플리케이션은 보통 이 MVC 패턴을 사용한다.

## MVC 핵심!
**컨트롤러**: HTTP 요청을 받아서 파라미터를 검증하고, 비즈니스 로직을 실행한다. 그리고 뷰에 전달할 결과 데이터를 조회해서 모델에 담는다.
**모델**: 뷰에 출력할 데이터를 담아둔다. 뷰가 필요한 데이터를 모두 모델에 담아서 전달해주는 덕분에 뷰는 비즈니스 로직이나 데이터 접근을 몰라도 되고, 화면을 렌더링 하는 일에 집중할 수 있다.
**뷰**: 모델에 담겨있는 데이터를 사용해서 화면을 그리는 일에 집중한다. 여기서는 HTML을 생성하는 부분을 말한다.

> 참고
> 컨트롤러에 비즈니스 로직을 둘 수도 있지만, 이렇게 되면 컨트롤러가 너무 많은 역할을 담당한다. 그래서
일반적으로 비즈니스 로직은 서비스(Service)라는 계층을 별도로 만들어서 처리한다. 그리고 컨트롤러는 비즈니스 로직이 있는 서비스를 호출하는 역할을 담당한다. 참고로 비즈니스 로직을 변경하면 비즈니스 로직을 호출하는 컨트롤러의 코드도 변경될 수 있다. 앞에서는 이해를 돕기 위해 비즈니스 로직을 호출한다는 표현 보다는, 비즈니스 로직이라 설명했다.

**MVC 패턴 이전**

<img width="591" alt="스크린샷 2023-02-24 오후 1 56 17" src="https://user-images.githubusercontent.com/96857599/221095525-719b1875-f999-4352-85b1-c7249bf5434a.png">


**MVC 패턴 1**

<img width="591" alt="스크린샷 2023-02-24 오후 2 23 34" src="https://user-images.githubusercontent.com/96857599/221098921-20ad5999-963e-49d3-966f-4c2430816a06.png">


**MVC 패턴 2(실제 MVC)**
<img width="592" alt="스크린샷 2023-02-24 오후 2 23 42" src="https://user-images.githubusercontent.com/96857599/221098946-423bb260-88fb-4627-b0d1-b736b8abc292.png">

### MVC패턴- 적용
서블릿을 컨트롤러로 사용하고, JSP를 뷰로 사용해서 MVC 패턴을 적용해보자.
Model은 HttpServletRequest 객체를 사용한다. request는 내부에 데이터 저장소를 가지고 있는데, request.setAttribute() , request.getAttribute() 를 사용하면 데이터를 보관하고, 조회할 수 있다.

#### 회원 등록

**회원 등록 폼- 컨트롤러**
- 기존에 Servlet에서 웹 페이지의 로직을 실행하고, html 페이지를 보여준 것과
<img width="1496" alt="스크린샷 2023-02-24 오후 2 42 33" src="https://user-images.githubusercontent.com/96857599/221101262-8160b9c2-6668-4515-a14e-d589e9e62f1a.png">

-  Jsp에서 직접 웹 페이지의 로직을 실행하고, html 페이지를 보여준 것과는 달리
<img width="1496" alt="스크린샷 2023-02-24 오후 2 44 33" src="https://user-images.githubusercontent.com/96857599/221101553-5fd8426b-3b45-4d56-b440-a59fb2a182af.png">

- Servlet을 컨트롤러로 사용하고(/WEB-INF/views/new-form.jsp를 불러옴), JSP를 뷰로 이용했다.
<img width="1496" alt="스크린샷 2023-02-24 오후 2 46 50" src="https://user-images.githubusercontent.com/96857599/221101946-f0f8c316-6ca1-467d-b15a-3e533dcc5b02.png">

<img width="1496" alt="스크린샷 2023-02-24 오후 2 47 32" src="https://user-images.githubusercontent.com/96857599/221102050-5b6ca32f-6721-42cb-9b9e-dec2d431a09c.png">

### 전체적인 실행 정리
1. index.html에 있는 url pattern으로 컨트롤러에 접근 (예: index.html에서 /servlet-mvc/members/new-form로 이동하면 @WebServlet(name = "mvcMemberFormServlet", urlPatterns = "/servlet-mvc/members/new-form")를 가진 컨트롤러 서블릿으로 이동함.)
2. 컨트롤러에서 String viewPath = "/WEB-INF/views/new-form.jsp"로 이동할 뷰 경로를 설정함. (model에 데이터르 저장할 수도 있음. 비지니스 로직 실행)
3. 뷰에서 결과를 클라이언트에게 보여줌.
4. 위의 방식 반복

-> dispatcher.forward() : 다른 서블릿이나 JSP로 이동할 수 있는 기능이다. 서버 내부에서 다시 호출이 발생한다. (redirect와 달리 서버 내부에서 재호출됨.)

> /WEB-INF
> 이 경로안에 JSP가 있으면 외부에서 직접 JSP를 호출할 수 없다. 우리가 기대하는 것은 항상 컨트롤러를 통해서 JSP를 호출하는 것이다.

- jsp 하위 파일와 WEB-INF 하위 파일 차이
<img width="1057" alt="스크린샷 2023-02-24 오후 2 55 09" src="https://user-images.githubusercontent.com/96857599/221103055-da2b77ec-72bc-47d8-ae41-626eb4df400c.png">
<img width="1057" alt="스크린샷 2023-02-24 오후 2 55 49" src="https://user-images.githubusercontent.com/96857599/221103123-2809628c-3417-4c73-a726-a96d738d7b6c.png">

>  redirect vs forward
> 리다이렉트는 실제 클라이언트(웹 브라우저)에 응답이 나갔다가, 클라이언트가 redirect 경로로 다시 요청한다. 따라서 클라이언트가 인지할 수 있고, URL 경로도 실제로 변경된다. 반면에 포워드는 서버 내부에서 일어나는 호출이기 때문에 클라이언트가 전혀 인지하지 못한다.

<img width="1496" alt="스크린샷 2023-02-24 오후 2 47 32" src="https://user-images.githubusercontent.com/96857599/221102050-5b6ca32f-6721-42cb-9b9e-dec2d431a09c.png">

> 상대경로를 사용하면 현재 경로가 http://localhost:8080/servlet-mvc/members/new-form 일 때, 다음 경로가 http://localhost:8080/servlet-mvc/members/save로 변경된다.
> 
> 다음에 편하게 사용하기 위해 상대 경로를 사용했고, 기본적으로 절대 경로르 사용하는 것이 좋다.
<img width="1057" alt="스크린샷 2023-02-24 오후 2 48 20" src="https://user-images.githubusercontent.com/96857599/221102158-dc08988a-af37-459e-92d1-ebf250d13942.png">

> 주의!
> 이후 코드에서 해당 jsp를 계속 사용하기 때문에 상대경로를 사용한 부분을 그대로 유지해야 한다.

#### 회원 저장- 컨트롤러

<img width="1582" alt="스크린샷 2023-02-24 오후 3 46 52" src="https://user-images.githubusercontent.com/96857599/221110889-4af969e5-8db4-4a71-9035-2417d30b9953.png">

HttpServletRequest를 Model로 사용한다.
request가 제공하는 setAttribute() 를 사용하면 request 객체에 데이터를 보관해서 뷰에 전달할 수 있다.
뷰는 request.getAttribute() 를 사용해서 데이터를 꺼내면 된다.

#### 회원 저장- 뷰

<img width="1582" alt="스크린샷 2023-02-24 오후 3 49 09" src="https://user-images.githubusercontent.com/96857599/221111319-7b68e185-0dea-4bed-b149-31fb8812c69d.png">

<%= request.getAttribute("member")%> 로 모델에 저장한 member 객체를 꺼낼 수 있지만, 너무 복잡해진다.
JSP는 ${} 문법을 제공하는데, 이 문법을 사용하면 request의 attribute에 담긴 데이터를 편리하게 조회할 수 있다.

#### 회원 목록 조회- 컨트롤러

<img width="1303" alt="스크린샷 2023-02-24 오후 3 57 17" src="https://user-images.githubusercontent.com/96857599/221112928-ef29bcfa-afdb-4bec-a888-62bf85ae5140.png">

- request 객체를 사용해서 List<Member> members를 모델에 보관했다.

#### 회원 목록 조회- 뷰
<img width="1303" alt="스크린샷 2023-02-24 오후 3 57 37" src="https://user-images.githubusercontent.com/96857599/221112996-d98c94bf-ef5b-40be-8266-c9ad0e4cecce.png">


- 모델에 담아둔 members를 JSP가 제공하는 taglib기능을 사용해서 반복하면서 출력했다. members 리스트에서 member 를 순서대로 꺼내서 item 변수에 담고, 출력하는 과정을 반복한다.

> <c:forEach> 이 기능을 사용하려면 다음과 같이 선언해야 한다.
> <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>

> 참고
> 앞서 설명했듯이 JSP를 학습하는 것이 이 강의의 주 목적이 아니다. JSP가 더 궁금한 분들은 이미 수 많은
> 자료들이 있으므로 JSP로 검색하거나 관련된 책을 참고하길 바란다. (반나절이면 대부분의 기능을 학습할 수 있다.)

### MVC 패턴 - 한계

MVC 패턴을 적용한 덕분에 컨트롤러의 역할과 뷰를 렌더링 하는 역할을 명확하게 구분할 수 있다.
특히 뷰는 화면을 그리는 역할에 충실한 덕분에, 코드가 깔끔하고 직관적이다. 
단순하게 모델에서 필요한 데이터를 꺼내고, 화면을 만들면 된다.
그런데 컨트롤러는 딱 봐도 중복이 많고, 필요하지 않는 코드들도 많이 보인다.


#### MVC 컨트롤러의 단점

**포워드 중복**
- View로 이동하는 코드가 항상 중복 호출되어야 한다. 물론 이 부분을 메서드로 공통화해도 되지만, 해당 메서드도 항상 직접 호출해야 한다.

```java
RequestDispatcher dispatcher = request.getRequestDispatcher(viewPath);
dispatcher.forward(request, response);
```

**ViewPath에 중복**

```java
String viewPath = "/WEB-INF/views/new-form.jsp";
```
- prefix: /WEB-INF/views/
- suffix: .jsp
- 그리고 만약 jsp가 아닌 thymeleaf 같은 다른 뷰로 변경한다면 전체 코드를 다 변경해야 한다.

**사용하지 않는 코드**
다음 코드를 사용할 때도 있고, 사용하지 않을 때도 있다. 특히 response는 현재 코드에서 사용되지 않는다.
```java
 HttpServletRequest request, HttpServletResponse response
```
그리고 이런 HttpServletRequest , HttpServletResponse 를 사용하는 코드는 테스트 케이스를 작성하기도 어렵다.


**⭐️공통 처리가 어렵다.**
기능이 복잡해질 수 록 컨트롤러에서 공통으로 처리해야 하는 부분이 점점 더 많이 증가할 것이다. 단순히 공통 기능을 메서드로 뽑으면 될 것 같지만, 결과적으로 해당 메서드를 항상 호출해야 하고, 실수로 호출하지 않으면 문제가 될 것이다. 그리고 호출하는 것 자체도 중복이다.

**정리하면 공통 처리가 어렵다는 문제가 있다.**
이 문제를 해결하려면 컨트롤러 호출 전에 먼저 공통 기능을 처리해야 한다. 소위 **수문장 역할**을 하는 기능이 필요하다. 프론트 컨트롤러(Front Controller) 패턴을 도입하면 이런 문제를 깔끔하게 해결할 수 있다. (입구를 하나로!)
스프링 MVC의 핵심도 바로 이 프론트 컨트롤러에 있다.

## MVC 프레임워크 만들기

	
### 프론트 컨트롤러 패턴 소개
	
- 프론트 컨트롤러 도입 전
<img width="563" alt="스크린샷 2023-02-24 오후 4 42 02" src="https://user-images.githubusercontent.com/96857599/221120704-fd83406a-1065-4def-b707-26186822a605.png">

- 프론트 컨트롤러 도입 후
<img width="566" alt="스크린샷 2023-02-24 오후 4 42 13" src="https://user-images.githubusercontent.com/96857599/221120746-db94b749-7275-4937-b01d-c1f2a11ecf6a.png">

<img width="1582" alt="스크린샷 2023-02-26 오후 2 02 52" src="https://user-images.githubusercontent.com/96857599/221393305-415d0bc7-cc24-45f0-98c7-3cf964e88c6b.png">


#### FrontController 패턴 특징
- 프론트 컨트롤러 서블릿 하나로 클라이언트의 요청을 받음
- 프론트 컨트롤러가 요청에 맞는 컨트롤러를 찾아서 호출
- 입구를 하나로!
- 공통 처리 가능
- 프론트 컨트롤러를 제외한 나머지 컨트롤러는 서블릿을 사용하지 않아도 됨

#### 스프링 웹 MVC와 프론트 컨트롤러
스프링 웹 MVC의 핵심도 바로 FrontController
스프링 웹 MVC의 DispatcherServlet이 FrontController 패턴으로 구현되어 있음


### 프론트 컨트롤러 도입 - v1

프론트 컨트롤러를 단계적으로 도입해보자.
이번 목표는 기존 코드를 최대한 유지하면서, 프론트 컨트롤러를 도입하는 것이다. 먼저 구조를 맞추어두고 점진적으로 리펙터링 해보자.

#### V1 구조

<img width="555" alt="스크린샷 2023-02-26 오후 1 41 35" src="https://user-images.githubusercontent.com/96857599/221392682-94f2bdf0-a326-4b9a-96d0-c2102a5937c7.png">

#### Controller V1



서블릿과 비슷한 모양의 컨트롤러 인터페이스를 도입한다. 각 컨트롤러들은 이 인터페이스를 구현하면 된다. 프론트 컨트롤러는 이 인터페이스를 호출해서 구현과 관계없이 로직의 일관성을 가져갈 수 있다.

이제 이 인터페이스를 구현한 컨트롤러를 만들어보자. 지금 단계에서는 기존 로직을 최대한 유지하는게 핵심이다.

- MemberFormControllerV1 - 회원 등록 컨트롤러

<img width="1496" alt="스크린샷 2023-02-26 오후 2 29 54" src="https://user-images.githubusercontent.com/96857599/221394018-08878fd2-9078-4caa-a3dd-f366853e3dad.png">

- MemberSaveControllerV1 - 회원 저장 컨트롤러

<img width="1496" alt="스크린샷 2023-02-26 오후 2 30 59" src="https://user-images.githubusercontent.com/96857599/221394052-70bab236-162f-4ce6-91ad-563b7b352903.png">


- MemberListControllerV1 - 회원 목록 컨트롤러

<img width="1496" alt="스크린샷 2023-02-26 오후 2 32 08" src="https://user-images.githubusercontent.com/96857599/221394100-e60f4701-121c-443f-9a83-bbe5614f0ef4.png">


- FrontControllerServletV1 - 프론트 컨트롤러

<img width="1496" alt="스크린샷 2023-02-26 오후 2 40 51" src="https://user-images.githubusercontent.com/96857599/221394361-652f105b-0c01-4e7c-862f-9b5cb2d40401.png">


#### 프론트 컨트롤러 분석

**urlPatterns**
- urlPatterns = "/front-controller/v1/*" : /front-controller/v1 를 포함한 하위 모든 요청은 이 서블릿에서 받아들인다.
- 예) /front-controller/v1 , /front-controller/v1/a , /front-controller/v1/a/b

**controllerMap**
- key: 매핑 URL
- value: 호출될 컨트롤러

**service()**
먼저 requestURI 를 조회해서 실제 호출할 컨트롤러를 controllerMap 에서 찾는다. 만약 없다면 404(SC_NOT_FOUND) 상태 코드를 반환한다.
컨트롤러를 찾고 controller.process(request, response); 을 호출해서 해당 컨트롤러를 실행한다.

**JSP**
JSP는 이전 MVC에서 사용했던 것을 그대로 사용한다.

<img width="368" alt="스크린샷 2023-02-26 오후 2 49 12" src="https://user-images.githubusercontent.com/96857599/221394581-11f85040-e130-4515-9eab-1d1dd5150fb1.png">


### View 분리 - v2
모든 컨트롤러에서 뷰로 이동하는 부분에 중복이 있고, 깔끔하지 않다.

```java
String viewPath = "/WEB-INF/views/new-form.jsp";
RequestDispatcher dispatcher = request.getRequestDispatcher(viewPath);
dispatcher.forward(request, response);

```
이 부분을 깔끔하게 분리하기 위해 별도로 뷰를 처리하는 객체를 만들자.


#### V2

<img width="579" alt="스크린샷 2023-02-26 오후 2 50 37" src="https://user-images.githubusercontent.com/96857599/221394627-f062b7e5-d519-40be-80d9-c6804188a3c4.png">


#### MyView
뷰 객체는 이후 다른 버전에서도 함께 사용하므로 패키지 위치를 frontcontroller 에 두었다.

<img width="1496" alt="스크린샷 2023-02-26 오후 3 23 07" src="https://user-images.githubusercontent.com/96857599/221395651-90b8793a-74f1-42c7-9b12-5245d34e9d1a.png">

#### ControllerV2
<img width="1496" alt="스크린샷 2023-02-26 오후 3 24 57" src="https://user-images.githubusercontent.com/96857599/221395712-5dc65dae-2ff9-4521-b4f0-24a7944bd06b.png">


#### MemberFormControllerV2 - 회원 등록 폼

<img width="1496" alt="스크린샷 2023-02-26 오후 3 25 15" src="https://user-images.githubusercontent.com/96857599/221395722-c4e63372-f19b-4155-ba06-471e78378a64.png">

- 이제 각 컨트롤러는 복잡한 dispatcher.forward() 를 직접 생성해서 호출하지 않아도 된다. 단순히 MyView 객체를 생성하고 거기에 뷰 이름만 넣고 반환하면 된다.
- ControllerV1 을 구현한 클래스와 ControllerV2 를 구현한 클래스를 비교해보면, 이 부분의 중복이 확실하게 제거된 것을 확인할 수 있다.


#### MemberSaveControllerV2 - 회원 저장

<img width="1496" alt="스크린샷 2023-02-26 오후 3 25 49" src="https://user-images.githubusercontent.com/96857599/221395738-7ad7d505-5dcb-435f-ab72-38718027fb89.png">

#### MemberListControllerV2 - 회원 목록

<img width="1496" alt="스크린샷 2023-02-26 오후 3 26 13" src="https://user-images.githubusercontent.com/96857599/221395753-c82250b4-0d9b-42a9-b53c-78e7b7f2ec5e.png">

#### 프론트 컨트롤러 V2

<img width="1496" alt="스크린샷 2023-02-26 오후 3 26 30" src="https://user-images.githubusercontent.com/96857599/221395756-847fc632-38aa-4b45-8360-e0a0e1e25ab1.png">

ControllerV2의 반환 타입이 MyView 이므로 프론트 컨트롤러는 컨트롤러의 호출 결과로 MyView 를 반환 받는다. 그리고 view.render() 를 호출하면 forward 로직을 수행해서 JSP가 실행된다.

MyView.render()
```java
public void render(HttpServletRequest request, HttpServletResponse response)
throws ServletException, IOException {
RequestDispatcher dispatcher = request.getRequestDispatcher(viewPath);
dispatcher.forward(request, response);
}
```
- 프론트 컨트롤러의 도입으로 MyView 객체의 render()를 호출하는 부분을 모두 일관되게 처리할 수 있다. 각각의 컨트롤러는 MyView 객체를 생성만 해서 반환하면 된다.
  
  
### 전체 흐름 정리
1. url을 요청한다.
2. FrontControllerServletV2에서 처리할 수 있는 url인지 판단한다.
3. ControllerV2 controller = controllerV2Map.get(requestURI); 에서 controller에 요청 url에 해당하는 컨트롤러를 호출한다.
4. 각 컨트롤러에 해당하는 로직을 실행한다.
5. (예: return new MyView("/WEB-INF/views/new-form.jsp");) 예시처럼 MyView 객체에 "/WEB-INF/views/new-form.jsp"와 같은 url이 넘어간다.
6. view.render()을 통해 url에 맞는 jsp를 호출한다.
 
### Model 추가 - v3

**서블릿 종속성 제거**
컨트롤러 입장에서 HttpServletRequest, HttpServletResponse이 꼭 필요할까?
요청 파라미터 정보는 자바의 Map으로 대신 넘기도록 하면 지금 구조에서는 컨트롤러가 서블릿 기술을 몰라도 동작할 수 있다.
그리고 request 객체를 Model로 사용하는 대신에 별도의 Model 객체를 만들어서 반환하면 된다. 우리가 구현하는 컨트롤러가 서블릿 기술을 전혀 사용하지 않도록 변경해보자.
이렇게 하면 구현 코드도 매우 단순해지고, 테스트 코드 작성이 쉽다.

**뷰 이름 중복 제거**
컨트롤러에서 지정하는 뷰 이름에 중복이 있는 것을 확인할 수 있다.
컨트롤러는 뷰의 논리 이름을 반환하고, 실제 물리 위치의 이름은 프론트 컨트롤러에서 처리하도록 단순화 하자.
이렇게 해두면 향후 뷰의 폴더 위치가 함께 이동해도 프론트 컨트롤러만 고치면 된다.

- /WEB-INF/views/new-form.jsp -> new-form
- /WEB-INF/views/save-result.jsp -> save-result 
- /WEB-INF/views/members.jsp -> members

### V3 구조

<img width="557" alt="스크린샷 2023-03-02 오후 3 41 47" src="https://user-images.githubusercontent.com/96857599/222350991-3fe2b00b-0b67-493b-9953-2df504ef76c7.png">


#### ModelView
지금까지 컨트롤러에서 서블릿에 종속적인 HttpServletRequest를 사용했다. 그리고 Model도 request.setAttribute() 를 통해 데이터를 저장하고 뷰에 전달했다.
서블릿의 종속성을 제거하기 위해 Model을 직접 만들고, 추가로 View 이름까지 전달하는 객체를 만들어보자.
(이번 버전에서는 컨트롤러에서 HttpServletRequest를 사용할 수 없다. 따라서 직접 request.setAttribute() 를 호출할 수도 없다. 따라서 Model이 별도로 필요하다.)

참고로 ModelView 객체는 다른 버전에서도 사용하므로 패키지를 frontcontroller 에 둔다.

<img width="1416" alt="스크린샷 2023-03-02 오후 4 35 40" src="https://user-images.githubusercontent.com/96857599/222361807-b340fcae-c243-4795-873d-312e34624be4.png">

뷰의 이름과 뷰를 렌더링할 때 필요한 model 객체를 가지고 있다. model은 단순히 map으로 되어 있으므로 컨트롤러에서 뷰에 필요한 데이터를 key, value로 넣어주면 된다.

#### ControllerV3

<img width="1416" alt="스크린샷 2023-03-02 오후 4 37 58" src="https://user-images.githubusercontent.com/96857599/222362220-935894a6-0644-4615-a4b1-2af38ad06258.png">

이 컨트롤러는 서블릿 기술을 전혀 사용하지 않는다. 따라서 구현이 매우 단순해지고, 테스트 코드 작성시 테스트 하기 쉽다.
HttpServletRequest가 제공하는 파라미터는 프론트 컨트롤러가 paramMap에 담아서 호출해주면 된다. 응답 결과로 뷰 이름과 뷰에 전달할 Model 데이터를 포함하는 ModelView 객체를 반환하면 된다.

#### MemberFormControllerV3 - 회원 등록 폼

<img width="1416" alt="스크린샷 2023-03-02 오후 4 38 31" src="https://user-images.githubusercontent.com/96857599/222362322-ef61a4ef-1100-420c-86b7-e9cab44b8f84.png">

ModelView 를 생성할 때 new-form 이라는 view의 논리적인 이름을 지정한다. 실제 물리적인 이름은 프론트 컨트롤러에서 처리한다.

#### MemberSaveControllerV3 - 회원 저장

<img width="1416" alt="스크린샷 2023-03-02 오후 4 39 16" src="https://user-images.githubusercontent.com/96857599/222362496-5641a3b1-b739-444c-bc4f-2c5727b1f855.png">

- paramMap.get("username");
파라미터 정보는 map에 담겨있다. map에서 필요한 요청 파라미터를 조회하면 된다. 

- mv.getModel().put("member", member);
모델은 단순한 map이므로 모델에 뷰에서 필요한 member 객체를 담고 반환한다.


#### MemberListControllerV3 - 회원 목록
	
<img width="1582" alt="스크린샷 2023-03-09 오후 3 42 52" src="https://user-images.githubusercontent.com/96857599/223941553-9a841059-aa15-4544-9209-6e1952f81b02.png">


#### FrontControllerServletV3

<img width="1580" alt="스크린샷 2023-03-02 오후 4 41 59" src="https://user-images.githubusercontent.com/96857599/222363064-11727a72-22f9-4772-a0af-a2207879f647.png">

<img width="1580" alt="스크린샷 2023-03-02 오후 4 42 05" src="https://user-images.githubusercontent.com/96857599/222363083-84aa1e86-d0b7-4dd4-98d3-ce339f51da6f.png">

createParamMap()
HttpServletRequest에서 파라미터 정보를 꺼내서 Map으로 변환한다. 그리고 해당 Map( paramMap )을
컨트롤러에 전달하면서 호출한다.

view.render(mv.getModel(), request, response) 코드에서 컴파일 오류가 발생할 것이다. 다음 코드를 참고해서 MyView 객체에 필요한 메서드를 추가하자.


<img width="1580" alt="스크린샷 2023-03-02 오후 4 43 26" src="https://user-images.githubusercontent.com/96857599/222363389-7f2f1f83-cab1-4aaa-ba80-a68eb52c4036.png">

#### 뷰 리졸버

MyView view = viewResolver(viewName)
컨트롤러가 반환한 논리 뷰 이름을 실제 물리 뷰 경로로 변경한다. 그리고 실제 물리 경로가 있는 MyView 객체를 반환한다.
- 논리 뷰 이름: members
- 물리 뷰 경로: /WEB-INF/views/members.jsp

view.render(mv.getModel(), request, response)
- 뷰 객체를 통해서 HTML 화면을 렌더링 한다.
- 뷰 객체의 render() 는 모델 정보도 함께 받는다.
- JSP는 request.getAttribute() 로 데이터를 조회하기 때문에, 모델의 데이터를 꺼내서 request.setAttribute() 로 담아둔다.
- JSP로 포워드 해서 JSP를 렌더링 한다.

<img width="1580" alt="스크린샷 2023-03-02 오후 4 45 00" src="https://user-images.githubusercontent.com/96857599/222363791-6984bb1d-041f-4cf2-b748-83a1d5bb9877.png">


### 전체 흐름 정리

1. URL 입력 (http://localhost:8080/front-controller/v3/members/new-form)
2. 매핑되어있는(urlPatterns = "/front-controller/v3/*") FrontControllerServletV3로 들어감
3. controllerMap.put("/front-controller/v3/members/new-form", new MemberFormControllerV3()); 가 호출 됨.
4. Map<String, String> paramMap = createParamMap(request); 가 실행되면 createParamMap 메서드로 paramMap 생성
	```java
	private static Map<String, String> createParamMap(HttpServletRequest request) {
        Map<String, String> paramMap = new HashMap<>();
        request.getParameterNames().asIterator()
                .forEachRemaining(paramName -> paramMap.put(paramName, request.getParameter(paramName)));
        return paramMap;
    }
	```
5. MemberFormControllerV3에서 ModelView에 URL 정보 넘김(논리 이름만)
```java
public class MemberFormControllerV3 implements ControllerV3 {
    @Override
    public ModelView process(Map<String, String> paramMap) {
        return new ModelView("new-form");
    }
}
```
6. MyView view = viewResolver(viewName);로 물리 이름 완성
7. view.render(mv.getModel(), request, response); 
	- model에 들어간 값으 모두 request에 넘김
    
### 단순하고 실용적인 컨트롤러 - v4

앞서 만든 v3 컨트롤러는 서블릿 종속성을 제거하고 뷰 경로의 중복을 제거하는 등, 잘 설계된 컨트롤러이다. 그런데 실제 컨트톨러 인터페이스를 구현하는 개발자 입장에서 보면, 항상 ModelView 객체를 생성하고 반환해야 하는 부분이 조금은 번거롭다.
좋은 프레임워크는 아키텍처도 중요하지만, 그와 더불어 실제 개발하는 개발자가 단순하고 편리하게 사용할 수 있어야 한다. 소위 실용성이 있어야 한다.
이번에는 v3를 조금 변경해서 실제 구현하는 개발자들이 매우 편리하게 개발할 수 있는 v4 버전을 개발해보자.

**V4 구조**
<img width="597" alt="스크린샷 2023-03-08 오후 6 40 22" src="https://user-images.githubusercontent.com/96857599/223677835-3453e405-dc13-49d6-a914-d82fda81095f.png">

- 기본적인 구조는 V3와 같다. 대신에 컨트롤러가 ModelView 를 반환하지 않고, ViewName 만 반환한다.

- ControllerV4
<img width="1343" alt="스크린샷 2023-03-08 오후 6 57 22" src="https://user-images.githubusercontent.com/96857599/223681906-8c8e404d-cc08-4b03-b506-7ec2e744a179.png">


이번 버전은 인터페이스에 ModelView가 없다. model 객체는 파라미터로 전달되기 때문에 그냥 사용하면 되고, 결과로 뷰의 이름만 반환해주면 된다.


- MemberFormControllerV4
<img width="1343" alt="스크린샷 2023-03-08 오후 6 57 32" src="https://user-images.githubusercontent.com/96857599/223681957-d248f01c-5416-4030-bca9-92a93aa25033.png">

정말 단순하게 new-form 이라는 뷰의 논리 이름만 반환하면 된다.


- MemberSaveControllerV4

<img width="1343" alt="스크린샷 2023-03-08 오후 6 57 39" src="https://user-images.githubusercontent.com/96857599/223681976-8cb03940-0f6e-455d-ad14-503ad33a3319.png">

model.put("member", member)
모델이 파라미터로 전달되기 때문에, 모델을 직접 생성하지 않아도 된다.


- MemberListControllerV4
<img width="1343" alt="스크린샷 2023-03-08 오후 6 57 49" src="https://user-images.githubusercontent.com/96857599/223682002-6443b92f-c060-4ead-9a2e-c92d021e10a2.png">


- FrontControllerServletV4
<img width="1343" alt="스크린샷 2023-03-08 오후 6 58 04" src="https://user-images.githubusercontent.com/96857599/223682063-282a796e-517a-4b09-b21c-aeff2ddaf44f.png">
<img width="1343" alt="스크린샷 2023-03-08 오후 6 58 11" src="https://user-images.githubusercontent.com/96857599/223682096-f5500d61-b513-4192-a8de-2b96dc1006e5.png">


FrontControllerServletV4 는 사실 이전 버전과 거의 동일하다.

#### 모델 객체 전달Map<String, Object> model = new HashMap<>(); //추가

모델 객체를 프론트 컨트롤러에서 생성해서 넘겨준다. 컨트롤러에서 모델 객체에 값을 담으면 여기에 그대로 담겨있게 된다.

#### 뷰의 논리 이름을 직접 반환

```java
  String viewName = controller.process(paramMap, model);
  MyView view = viewResolver(viewName);
```
컨트롤로가 직접 뷰의 논리 이름을 반환하므로 이 값을 사용해서 실제 물리 뷰를 찾을 수 있다.


#### 정리

이번 버전의 컨트롤러는 매우 단순하고 실용적이다. 기존 구조에서 모델을 파라미터로 넘기고, 뷰의 논리 이름을 반환한다는 작은 아이디어를 적용했을 뿐인데, 컨트롤러를 구현하는 개발자 입장에서 보면 이제 군더더기 없는 코드를 작성할 수 있다.
또한 중요한 사실은 여기까지 한번에 온 것이 아니라는 점이다. 프레임워크가 점진적으로 발전하는 과정 속에서 이런 방법도 찾을 수 있었다.
프레임워크나 공통 기능이 수고로워야 사용하는 개발자가 편리해진다.

### 유연한 컨트롤러 1 - v5

- 만약 어떤 개발자는 ControllerV3 방식으로 개발하고 싶고, 어떤 개발자는 ControllerV4 방식으로 개발하고 싶다면 어떻게 해야할까?

```java
 public interface ControllerV3 {
        ModelView process(Map<String, String> paramMap);
}
```

```java
public interface ControllerV4 {
        String process(Map<String, String> paramMap, Map<String, Object> model);
}
```

### 어댑터 패턴
지금까지 우리가 개발한 프론트 컨트롤러는 한가지 방식의 컨트롤러 인터페이스만 사용할 수 있다. ControllerV3 , ControllerV4 는 완전히 다른 인터페이스이다. 따라서 호환이 불가능하다. 마치 v3는 110v이고, v4는 220v 전기 콘센트 같은 것이다. 이럴 때 사용하는 것이 바로 어댑터이다.
어댑터 패턴을 사용해서 프론트 컨트롤러가 다양한 방식의 컨트롤러를 처리할 수 있도록 변경해보자.

### V5 구조

<img width="614" alt="스크린샷 2023-03-09 오후 3 08 09" src="https://user-images.githubusercontent.com/96857599/223935104-c2a10f35-6c10-4574-b861-9374d67b74b4.png">

- 핸들러 어댑터: 중간에 어댑터 역할을 하는 어댑터가 추가되었는데 이름이 핸들러 어댑터이다. 여기서 어댑터 역할을 해주는 덕분에 다양한 종류의 컨트롤러를 호출할 수 있다.
- 핸들러: 컨트롤러의 이름을 더 넓은 범위인 핸들러로 변경했다. 그 이유는 이제 어댑터가 있기 때문에 꼭 컨트롤러의 개념 뿐만 아니라 어떠한 것이든 해당하는 종류의 어댑터만 있으면 다 처리할 수 있기 때문이다.

#### MyHandler Adapter

<img width="1530" alt="스크린샷 2023-03-09 오후 3 23 20" src="https://user-images.githubusercontent.com/96857599/223938023-50cabb13-2618-4000-89ec-6451b35ecc21.png">

- 어댑터는 이렇게 구현해야 한다는 어댑터용 인터페이스이다.

- boolean supports(Object handler)
	- handler는 컨트롤러를 말한다.
	- 어댑터가 해당 컨트롤러를 처리할 수 있는지 판단하는 메서드다.

- ModelView handle(HttpServletRequest request, HttpServletResponse response, Object
handler)
	- 어댑터는 실제 컨트롤러를 호출하고, 그 결과로 ModelView를 반환해야 한다.
	- 실제 컨트롤러가 ModelView를 반환하지 못하면, 어댑터가 ModelView를 직접 생성해서라도 반환해야 한다.
	- 이전에는 프론트 컨트롤러가 실제 컨트롤러를 호출했지만 이제는 이 어댑터를 통해서 실제 컨트롤러가 호출된다.


- ControllerV3HandlerAdapter

<img width="1564" alt="스크린샷 2023-03-09 오후 4 51 53" src="https://user-images.githubusercontent.com/96857599/223956088-8842ee3e-6ccc-4fea-9c95-eda658c5c3ae.png">

하나씩 분석해보자.
```java
public boolean supports(Object handler) {
      return (handler instanceof ControllerV3);
}
```
ControllerV3 을 처리할 수 있는 어댑터를 뜻한다.
	
```java
ControllerV3 controller = (ControllerV3) handler;
Map<String, String> paramMap = createParamMap(request);
ModelView mv = controller.process(paramMap);
return mv;
```
	
handler를 컨트롤러 V3로 변환한 다음에 V3 형식에 맞도록 호출한다.
supports() 를 통해 ControllerV3 만 지원하기 때문에 타입 변환은 걱정없이 실행해도 된다. ControllerV3는 ModelView를 반환하므로 그대로 ModelView를 반환하면 된다.
	
	
- FrontControllerServletV5
	
<img width="1564" alt="스크린샷 2023-03-09 오후 4 52 27" src="https://user-images.githubusercontent.com/96857599/223956297-2cb1a9d7-e88f-49b7-b921-4959eb64f091.png">
<img width="1564" alt="스크린샷 2023-03-09 오후 4 52 31" src="https://user-images.githubusercontent.com/96857599/223956350-112a3c16-5c60-4ff7-b69e-5588415bca8e.png">
<img width="1564" alt="스크린샷 2023-03-09 오후 4 52 33" src="https://user-images.githubusercontent.com/96857599/223956225-de7f7f8d-3157-4a37-b20b-ecce49ed0453.png">

**컨트롤러(Controller) -> 핸들러(Handler)**
이전에는 컨트롤러를 직접 매핑해서 사용했다. 그런데 이제는 어댑터를 사용하기 때문에, 컨트롤러 뿐만 아니라 어댑터가 지원하기만 하면, 어떤 것이라도 URL에 매핑해서 사용할 수 있다. 그래서 이름을 컨트롤러에서 더 넒은 범위의 핸들러로 변경했다.

**생성자**
```java
public FrontControllerServletV5() { 
	initHandlerMappingMap(); //핸들러 매핑 초기화 
	initHandlerAdapters(); //어댑터 초기화
}
```
생성자는 핸들러 매핑과 어댑터를 초기화(등록)한다.


**매핑 정보**
```java
private final Map<String, Object> handlerMappingMap = new HashMap<>();
```
매핑 정보의 값이 ControllerV3 , ControllerV4 같은 인터페이스에서 아무 값이나 받을 수 있는
Object 로 변경되었다.
	
**핸들러 매핑**
Object handler = getHandler(request)

```java
private Object getHandler(HttpServletRequest request) {
  String requestURI = request.getRequestURI();
  return handlerMappingMap.get(requestURI);
}
```
핸들러 매핑 정보인 handlerMappingMap 에서 URL에 매핑된 핸들러(컨트롤러) 객체를 찾아서 반환한다.

**핸들러를 처리할 수 있는 어댑터 조회**
MyHandlerAdapter adapter = getHandlerAdapter(handler)
```java
for (MyHandlerAdapter adapter : handlerAdapters) {
      if (adapter.supports(handler)) {
          return adapter;
      }
}
```
handler 를 처리할 수 있는 어댑터를 adapter.supports(handler) 를 통해서 찾는다. handler가 ControllerV3 인터페이스를 구현했다면, ControllerV3HandlerAdapter 객체가 반환된다.


**어댑터 호출**
ModelView mv = adapter.handle(request, response, handler);

어댑터의 handle(request, response, handler) 메서드를 통해 실제 어댑터가 호출된다. 
어댑터는 handler(컨트롤러)를 호출하고 그 결과를 어댑터에 맞추어 반환한다. ControllerV3HandlerAdapter 의 경우 어댑터의 모양과 컨트롤러의 모양이 유사해서 변환 로직이 단순하다.

**실행 - 오류**

- 실행했더니 오류가 발생했다.
<img width="845" alt="스크린샷 2023-03-09 오후 4 33 53" src="https://user-images.githubusercontent.com/96857599/223951978-7c43ab24-b345-4312-8e55-80f75af28070.png">

- 전에 설정해둔 디버그를 읽는다.
<img width="1524" alt="스크린샷 2023-03-09 오후 4 33 22" src="https://user-images.githubusercontent.com/96857599/223951873-dcf89206-9846-4a1b-8aee-5154e5caf50e.png">
<img width="1524" alt="스크린샷 2023-03-09 오후 4 35 00" src="https://user-images.githubusercontent.com/96857599/223952185-2385de63-cdce-4dcd-8c04-397aad3d3343.png">

- frontController의 mapping 정보의 오류가 있었다.	
<img width="828" alt="스크린샷 2023-03-09 오후 4 36 12" src="https://user-images.githubusercontent.com/96857599/223952410-4267e3b6-82b8-4623-9db6-abb84154742e.png">

- 수정
<img width="816" alt="스크린샷 2023-03-09 오후 4 37 13" src="https://user-images.githubusercontent.com/96857599/223952626-cba71528-3da7-4eb5-9673-44e8ae56613c.png">

**정리**
지금은 V3 컨트롤러를 사용할 수 있는 어댑터와 ControllerV3 만 들어 있어서 크게 감흥이 없을 것이다. ControllerV4 를 사용할 수 있도록 기능을 추가해보자.
	
### 유연한 컨트롤러2 - v5

- FrontControllerServletV5 에 ControllerV4 기능도 추가.
<img width="1364" alt="스크린샷 2023-03-12 오후 3 19 43" src="https://user-images.githubusercontent.com/96857599/224527948-0b66fe64-b69b-4fa1-99b6-3bb3bf7fe9a1.png">

핸들러 매핑( handlerMappingMap )에 ControllerV4 를 사용하는 컨트롤러를 추가하고, 해당 컨트롤러를 처리할 수 있는 어댑터인 ControllerV4HandlerAdapter 도 추가하자.

<img width="1582" alt="스크린샷 2023-03-12 오후 3 21 29" src="https://user-images.githubusercontent.com/96857599/224528030-e545f9dc-0dcf-4751-a100-6b17be9534e9.png">

<img width="1582" alt="스크린샷 2023-03-12 오후 3 21 53" src="https://user-images.githubusercontent.com/96857599/224528048-c8b76ac1-0250-48ab-9c2a-c955bd5767f0.png">


### 정리
1. HTTP 요청 (http://localhost:8080/front-controller/v5/v4/members/new-form 으로 접속)
2. 핸들러 어댑터 목록 조회 (new MemberFormControllerV4() 반환)
<img width="1426" alt="스크린샷 2023-03-12 오후 3 27 30" src="https://user-images.githubusercontent.com/96857599/224528302-772e3121-2c50-45c7-82dc-643bc7720cd2.png">
3. service 메서드에 handler로 MemberFormControllerV4 저장
<img width="933" alt="스크린샷 2023-03-12 오후 3 33 08" src="https://user-images.githubusercontent.com/96857599/224528493-2555b923-0d19-4ae9-bae5-eff6914e3bf5.png">
4. adapter의 support 메서드로 입력받은 handler가 어떤 컨트롤러의 인스턴스인지 확인
<img width="1091" alt="스크린샷 2023-03-12 오후 3 36 24" src="https://user-images.githubusercontent.com/96857599/224528616-4f720bfd-78f8-48a6-b626-838688a85dcd.png">
5. ControllersV4HandlerAdapter의 handle 실행
<img width="1352" alt="스크린샷 2023-03-12 오후 3 38 32" src="https://user-images.githubusercontent.com/96857599/224528706-cc6bb4e8-ba41-40c7-8e3b-2b01445c9c48.png">
6. 이후의 프로세스는 위의 과정과 동일


**분석**

```java
public boolean supports(Object handler) {
      return (handler instanceof ControllerV4);
}
```
- handler 가 ControllerV4 인 경우에만 처리하는 어댑터이다.

```java
ControllerV4 controller = (ControllerV4) handler;
Map<String, String> paramMap = createParamMap(request);
Map<String, Object> model = new HashMap<>();
String viewName = controller.process(paramMap, model);

- handler를 ControllerV4로 케스팅 하고, paramMap, model을 만들어서 해당 컨트롤러를 호출한다. 그리고 viewName을 반환 받는다.

**어댑터 변환**
```java

ModelView mv = new ModelView(viewName);
mv.setModel(model);

return mv;
```
어댑터에서 이 부분이 단순하지만 중요한 부분이다.

어댑터가 호출하는 ControllerV4 는 뷰의 이름을 반환한다. 그런데 어댑터는 뷰의 이름이 아니라 ModelView 를 만들어서 반환해야 한다. 여기서 어댑터가 꼭 필요한 이유가 나온다.
ControllerV4 는 뷰의 이름을 반환했지만, 어댑터는 이것을 ModelView로 만들어서 형식을 맞추어 반환한다. 마치 110v 전기 콘센트를 220v 전기 콘센트로 변경하듯이!

**어댑터와 ControllerV4**
```java
 public interface ControllerV4 {
      String process(Map<String, String> paramMap, Map<String, Object> model);
  }
  
  public interface MyHandlerAdapter {
      ModelView handle(HttpServletRequest request, HttpServletResponse response, Object handler) throws ServletException, IOException;
 }
 ```

## 정리

지금까지 v1 ~ v5로 점진적으로 프레임워크를 발전시켜 왔다. 지금까지 한 작업을 정리해보자.

- v1: 프론트 컨트롤러를 도입
	- 기존 구조를 최대한 유지하면서 프론트 컨트롤러를 도입
- v2: View 분류
	- 단순 반복 되는 뷰 로직 분리
- v3: Model 추가 서블릿 종속성 제거
	- 뷰 이름 중복 제거
- v4: 단순하고 실용적인 컨트롤러 v3와 거의 비슷
	- 구현 입장에서 ModelView를 직접 생성해서 반환하지 않도록 편리한 인터페이스 제공
- v5: 유연한 컨트롤러 어댑터 도입
	- 어댑터를 추가해서 프레임워크를 유연하고 확장성 있게 설계

여기에 애노테이션을 사용해서 컨트롤러를 더 편리하게 발전시킬 수도 있다. 만약 애노테이션을 사용해서 컨트롤러를 편리하게 사용할 수 있게 하려면 어떻게 해야할까? 바로 애노테이션을 지원하는 어댑터를 추가하면 된다!
다형성과 어댑터 덕분에 기존 구조를 유지하면서, 프레임워크의 기능을 확장할 수 있다.

### 스프링 MVC
여기서 더 발전시키면 좋겠지만, 스프링 MVC의 핵심 구조를 파악하는데 필요한 부분은 모두 만들어보았다. 사실은 여러분이 지금까지 작성한 코드는 스프링 MVC 프레임워크의 핵심 코드의 축약 버전이고, 구조도 거의 같다.
스프링 MVC는 지금까지 우리가 학습한 내용과 거의 같은 구조를 가지고 있다.

## 스프링 MVC - 구조이해

### 스프링 MVC 전체 구조

**직접 만든 MVC 프레임워크 구조**
<img width="575" alt="스크린샷 2023-03-12 오후 4 02 36" src="https://user-images.githubusercontent.com/96857599/224529598-a93d5ae1-9430-4572-916b-1807b55f1b1d.png">

**SpringMVC 구조**
<img width="577" alt="스크린샷 2023-03-12 오후 4 05 05" src="https://user-images.githubusercontent.com/96857599/224529702-2afe4fa8-eb30-4d01-bd1a-84112a7ff04e.png">

#### 직접 만든 프레임워크 스프링 MVC 비교 
- FrontController -> DispatcherServlet (가장 중요)
- handlerMappingMap -> HandlerMapping 
- MyHandlerAdapter -> HandlerAdapter
- ModelView -> ModelAndView
- viewResolver -> ViewResolver
- MyView -> View

#### DispatcherServlet 구조 살펴보기

org.springframework.web.servlet.DispatcherServlet

스프링 MVC도 프론트 컨트롤러 패턴으로 구현되어 있다.
스프링 MVC의 프론트 컨트롤러가 바로 디스패처 서블릿(DispatcherServlet)이다. 
그리고 이 디스패처 서블릿이 바로 스프링 MVC의 핵심이다.

#### DispacherServlet 서블릿 등록
- DispacherServlet 도 부모 클래스에서 HttpServlet 을 상속 받아서 사용하고, 서블릿으로 동작한다.
	- DispatcherServlet FrameworkServlet HttpServletBean HttpServlet
- 스프링 부트는 DispacherServlet 을 서블릿으로 자동으로 등록하면서 모든 경로( urlPatterns="/" )에 대해서 매핑한다.
	- 참고: 더 자세한 경로가 우선순위가 높다. 그래서 기존에 등록한 서블릿도 함께 동작한다.

**요청흐름**

서블릿이 호출되면 HttpServlet 이 제공하는 serivce() 가 호출된다.
스프링 MVC는 DispatcherServlet 의 부모인 FrameworkServlet 에서 service() 를 오버라이드 해두었다.
<img width="1175" alt="스크린샷 2023-03-14 오후 11 46 00" src="https://user-images.githubusercontent.com/96857599/225038185-6b116507-b49e-4f16-b58c-3543b84e0818.png">

FrameworkServlet.service() 를 시작으로 여러 메서드가 호출되면서 **DispacherServlet.doDispatch() 가 호출된다.**
<img width="1175" alt="스크린샷 2023-03-14 오후 11 47 02" src="https://user-images.githubusercontent.com/96857599/225038455-3e75e351-ecd2-41e8-a130-9e4500345986.png">
- handler
<img width="951" alt="스크린샷 2023-03-14 오후 11 48 32" src="https://user-images.githubusercontent.com/96857599/225038880-f9f3a74e-6f00-458e-9ce2-111a747a94ef.png">


지금부터 DispacherServlet 의 핵심인 doDispatch() 코드를 분석해보자. 최대한 간단히 설명하기 위해 예외처리, 인터셉터 기능은 제외했다.

**DispacherServlet.doDispatch()**

```java
protected void doDispatch(HttpServletRequest request, HttpServletResponse response) throws Exception {
    HttpServletRequest processedRequest = request;
    HandlerExecutionChain mappedHandler = null;
    ModelAndView mv = null;
	
	// 1. 핸들러 조회
	mappedHandler = getHandler(processedRequest); 
	if (mappedHandler == null) {
		noHandlerFound(processedRequest, response);
		return; 
	}
	
	//2.핸들러 어댑터 조회-핸들러를 처리할 수 있는 어댑터
	HandlerAdapter ha = getHandlerAdapter(mappedHandler.getHandler());
	
	// 3. 핸들러 어댑터 실행 -> 4. 핸들러 어댑터를 통해 핸들러 실행 -> 5. ModelAndView 반환 
	mv = ha.handle(processedRequest, response, mappedHandler.getHandler());
    
	processDispatchResult(processedRequest, response, mappedHandler, mv, dispatchException);
}

private void processDispatchResult(HttpServletRequest request,
HttpServletResponse response, HandlerExecutionChain mappedHandler, ModelAndView
mv, Exception exception) throws Exception {
	// 뷰 렌더링 호출
	render(mv, request, response);
}
protected void render(ModelAndView mv, HttpServletRequest request, HttpServletResponse response) throws Exception {
    View view;
	String viewName = mv.getViewName(); 
	
	//6. 뷰 리졸버를 통해서 뷰 찾기, 7.View 반환
    view = resolveViewName(viewName, mv.getModelInternal(), locale, request);
	
	// 8. 뷰 렌더링
    view.render(mv.getModelInternal(), request, response);
}


```

#### SpringMVC 구조
<img width="561" alt="스크린샷 2023-03-14 오후 11 54 41" src="https://user-images.githubusercontent.com/96857599/225041001-4a314245-e43d-4d30-99c8-5ff12cecdd88.png">

동작 순서
1. 핸들러 조회: 핸들러 매핑을 통해 요청 URL에 매핑된 핸들러(컨트롤러)를 조회한다.
2. 핸들러 어댑터 조회: 핸들러를 실행할 수 있는 핸들러 어댑터를 조회한다.
3. 핸들러 어댑터 실행: 핸들러 어댑터를 실행한다.
4. 핸들러 실행: 핸들러 어댑터가 실제 핸들러를 실행한다.
5. ModelAndView 반환: 핸들러 어댑터는 핸들러가 반환하는 정보를 ModelAndView로 변환해서
반환한다.
6. viewResolver 호출: 뷰 리졸버를 찾고 실행한다.
JSP의 경우: InternalResourceViewResolver 가 자동 등록되고, 사용된다.
7. View반환:뷰리졸버는뷰의논리이름을물리이름으로바꾸고,렌더링역할을담당하는뷰객체를
반환한다.
JSP의 경우 InternalResourceView(JstlView) 를 반환하는데, 내부에 forward() 로직이 있다.
8. 뷰렌더링:뷰를통해서뷰를렌더링한다.


**인터페이스 살펴보기**
- 스프링 MVC의 큰 강점은 DispatcherServlet 코드의 변경 없이, 원하는 기능을 변경하거나 확장할 수 있다는 점이다. 지금까지 설명한 대부분을 확장 가능할 수 있게 인터페이스로 제공한다.
- 이 인터페이스들만 구현해서 DispatcherServlet 에 등록하면 여러분만의 컨트롤러를 만들 수도 있다.

**주요 인터페이스 목록**
- 핸들러 매핑: org.springframework.web.servlet.HandlerMapping 
- 핸들러 어댑터: org.springframework.web.servlet.HandlerAdapter 
- 뷰 리졸버: org.springframework.web.servlet.ViewResolver
- 뷰: org.springframework.web.servlet.View

**정리**
스프링 MVC는 코드 분량도 매우 많고, 복잡해서 내부 구조를 다 파악하는 것은 쉽지 않다. 사실 해당 기능을 직접 확장하거나 나만의 컨트롤러를 만드는 일은 없으므로 걱정하지 않아도 된다. 왜냐하면 스프링 MVC는 전세계 수 많은 개발자들의 요구사항에 맞추어 기능을 계속 확장해왔고, 그래서 여러분이 웹 애플리케이션을 만들 때 필요로 하는 대부분의 기능이 이미 다 구현되어 있다.
그래도 이렇게 핵심 동작방식을 알아두어야 향후 문제가 발생했을 때 어떤 부분에서 문제가 발생했는지 쉽게 파악하고, 문제를 해결할 수 있다. 그리고 확장 포인트가 필요할 때, 어떤 부분을 확장해야 할지 감을 잡을 수 있다. 실제 다른 컴포넌트를 제공하거나 기능을 확장하는 부분들은 강의를 진행하면서 조금씩 설명하겠다. 지금은 전체적인 구조가 이렇게 되어 있구나 하고 이해하면 된다.
우리가 지금까지 함께 개발한 MVC 프레임워크와 유사한 구조여서 이해하기 어렵지 않았을 것이다.


### 핸들러 매핑과 핸들러 어댑터

핸들러 매핑과 핸들러 어댑터가 어떤 것들이 어떻게 사용되는지 알아보자.
지금은 전혀 사용하지 않지만, 과거에 주로 사용했던 스프링이 제공하는 간단한 컨트롤러로 핸들러 매핑과 어댑터를 이해해보자.

#### Controller 인터페이스
**과거 버전 스프링 컨트롤러**
org.springframework.web.servlet.mvc.Controller
```java
public interface Controller {
	ModelAndView handleRequest(HttpServletRequest request, HttpServletResponse response) throws Exception;
}
```

- 스프링도 처음에는 이런 딱딱한 형식의 컨트롤러를 제공했다.

> 참고
> Controller 인터페이스는 @Controller 애노테이션과는 전혀 다르다.


<img width="999" alt="스크린샷 2023-03-15 오후 8 05 23" src="https://user-images.githubusercontent.com/96857599/225290960-81b3f59e-3485-4ed9-940a-ff84e5f8ff62.png">

- @Component : 이 컨트롤러는 /springmvc/old-controller 라는 이름의 스프링 빈으로 등록되었다. 
- 빈의 이름으로 URL을 매핑할 것이다.

**스프링 MVC 구조**
<img width="537" alt="스크린샷 2023-03-15 오후 8 06 57" src="https://user-images.githubusercontent.com/96857599/225291241-594528d1-5aa8-4e08-a5f3-97f75a95b621.png">

- HandlerMapping(핸들러 매핑)
	- 핸들러 매핑에서 이 컨트롤러를 찾을 수 있어야 한다.
	- 예) 스프링 빈의 이름으로 핸들러를 찾을 수 있는 핸들러 매핑이 필요하다.

- HandlerAdapter(핸들러 어댑터)
	- 핸들러 매핑을 통해서 찾은 핸들러를 실행할 수 있는 핸들러 어댑터가 필요하다.
	- 예) Controller 인터페이스를 실행할 수 있는 핸들러 어댑터를 찾고 실행해야 한다.

> 스프링은 이미 필요한 핸들러 매핑과 핸들러 어댑터를 대부분 구현해두었다. 개발자가 직접 핸들러 매핑과 핸들러 어댑터를 만드는 일은 거의 없다.

**스프링 부트가 자동 등록하는 핸들러 매핑과 핸들러 어댑터**
(실제로는 더 많지만, 중요한 부분 위주로 설명하기 위해 일부 생략)
#### 
#### HandlerMapping
```java
0 = RequestMappingHandlerMapping : 애노테이션 기반의 컨트롤러인 @RequestMapping에서
사용
1= BeanNameUrlHandlerMapping : 스프링 빈의 이름으로 핸들러를 찾는다.
```

#### HandlerAdapter
```java
0 = RequestMappingHandlerAdapter : 애노테이션 기반의 컨트롤러인 @RequestMapping에서 사용
1 = HttpRequestHandlerAdapter : HttpRequestHandler 처리
2 = SimpleControllerHandlerAdapter : Controller 인터페이스(애노테이션X, 과거에 사용) 처리
```
핸들러 매핑도, 핸들러 어댑터도 모두 순서대로 찾고 만약 없으면 다음 순서로 넘어간다.


1. 핸들러 매핑으로 핸들러 조회
- HandlerMapping 을 순서대로 실행해서, 핸들러를 찾는다.
- 이 경우 빈 이름으로 핸들러를 찾아야 하기 때문에 이름 그대로 빈 이름으로 핸들러를 찾아주는 BeanNameUrlHandlerMapping 가 실행에 성공하고 핸들러인 OldController 를 반환한다.

2. 핸들러 어댑터 조회
- HandlerAdapter 의 supports() 를 순서대로 호출한다.
- SimpleControllerHandlerAdapter 가 Controller 인터페이스를 지원하므로 대상이 된다.

3. 핸들러 어댑터 실행
- 디스패처 서블릿이 조회한 SimpleControllerHandlerAdapter 를 실행하면서 핸들러 정보도 함께 넘겨준다.
- SimpleControllerHandlerAdapter 는 핸들러인 OldController 를 내부에서 실행하고, 그 결과를 반환한다.

#### 정리 - OldController 핸들러매핑, 어댑터
OldController 를 실행하면서 사용된 객체는 다음과 같다.
- HandlerMapping = BeanNameUrlHandlerMapping
- HandlerAdapter = SimpleControllerHandlerAdapter

#### HttpRequestHandler
핸들러 매핑과, 어댑터를 더 잘 이해하기 위해 Controller 인터페이스가 아닌 다른 핸들러를 알아보자. HttpRequestHandler 핸들러(컨트롤러)는 서블릿과 가장 유사한 형태의 핸들러이다.

**HttpRequestHandler**
```java
public interface HttpRequestHandler {
       void handleRequest(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException;
}
```
간단하게 구현해보자.

**MyHttpRequestHandler**

<img width="1496" alt="스크린샷 2023-03-15 오후 8 21 29" src="https://user-images.githubusercontent.com/96857599/225294569-4da9f5b6-800f-4405-854b-4be75bd555ea.png">

- 빈이름을 @Component("/springmvc/request-handler")으로 찾음

순서

1. 핸들러 매핑으로 핸들러 조회
- HandlerMapping 을 순서대로 실행해서, 핸들러를 찾는다.
- 이 경우 빈 이름으로 핸들러를 찾아야 하기 때문에 이름 그대로 빈 이름으로 핸들러를 찾아주는  BeanNameUrlHandlerMapping 가 실행에 성공하고 핸들러인 MyHttpRequestHandler 를 반환한다.

2. 핸들러 어댑터 조회
- HandlerAdapter 의 supports() 를 순서대로 호출한다.
- HttpRequestHandlerAdapter 가 HttpRequestHandler 인터페이스를 지원하므로 대상이 된다.

3. 핸들러 어댑터 실행
- 디스패처 서블릿이 조회한 HttpRequestHandlerAdapter 를 실행하면서 핸들러 정보도 함께 넘겨준다.
- HttpRequestHandlerAdapter 는 핸들러인 MyHttpRequestHandler 를 내부에서 실행하고, 그 결과를 반환한다.


**정리 - MyHttpRequestHandler 핸들러매핑, 어댑터**
- MyHttpRequestHandler 를 실행하면서 사용된 객체는 다음과 같다.
- HandlerMapping = BeanNameUrlHandlerMapping
- HandlerAdapter = HttpRequestHandlerAdapter


**@RequestMapping**
조금 뒤에서 설명하겠지만, 가장 우선순위가 높은 핸들러 매핑과 핸들러 어댑터는 
RequestMappingHandlerMapping ,
RequestMappingHandlerAdapter 이다.
@RequestMapping 의 앞글자를 따서 만든 이름인데, 이것이 바로 지금 스프링에서 주로 사용하는 애노테이션 기반의 컨트롤러를 지원하는 매핑과 어댑터이다. 실무에서는 99.9% 이 방식의 컨트롤러를 사용한다.

### 뷰 리졸버

**OldController- View 조회할 수 있도록 변경**
<img width="1299" alt="스크린샷 2023-03-17 오후 8 55 20" src="https://user-images.githubusercontent.com/96857599/225897665-f1583872-0e6c-4be9-b668-c49d7be835ce.png">

- 실행해보면 컨트롤러를 정상 호출되지만, Whitelabel Error Page 오류가 발생한다.

#### application.properties 에 다음 코드를 추가하자
```
  spring.mvc.view.prefix=/WEB-INF/views/
  spring.mvc.view.suffix=.jsp
```

**뷰 리졸버 - InternalResourceViewResolver**
스프링 부트는 InternalResourceViewResolver 라는 뷰 리졸버를 자동으로 등록하는데, 이때 application.properties 에 등록한 spring.mvc.view.prefix , spring.mvc.view.suffix 설정 정보를 사용해서 등록한다.
참고로 권장하지는 않지만 설정 없이 다음과 같이 전체 경로를 주어도 동작하기는 한다. return new ModelAndView("/WEB-INF/views/new-form.jsp");

- 아래 코드를 스프링이 알아서 해준다.
```java
@Bean
View Resolver internalResourceViewResolver() {
	return new InternalResourceViewResolver("/WEB-INF/views/", ".jsp");
}
```

#### 뷰 리졸버 동작 방식

**스프링 MVC 구조**

<img width="556" alt="스크린샷 2023-03-17 오후 8 49 22" src="https://user-images.githubusercontent.com/96857599/225896486-345c2fe3-39e5-4779-a338-1606015552fe.png">

**스프링 부트가 자동 등록하는 뷰 리졸버**
(실제로는 더 많지만, 중요한 부분 위주로 설명하기 위해 일부 생략)
```
1 = BeanNameViewResolver 			: 빈 이름으로 뷰를 찾아서 반환한다. (예: 엑셀 파일 생성 기능에 사용)
2 = InternalResourceViewResolver 	: JSP를 처리할 수 있는 뷰를 반환한다.
```

1. 핸들러 어댑터 호출
핸들러 어댑터를 통해 new-form 이라는 논리 뷰 이름을 획득한다.

2. ViewResolver 호출
- new-form 이라는 뷰 이름으로 viewResolver를 순서대로 호출한다.
- BeanNameViewResolver 는 new-form 이라는 이름의 스프링 빈으로 등록된 뷰를 찾아야 하는데 없다. 
- InternalResourceViewResolver 가 호출된다.

3. InternalResourceViewResolver (내부에서 자원을 찾을 수 있을 때 사용)
이 뷰 리졸버는 InternalResourceView 를 반환한다. 

4. 뷰 - InternalResourceView
InternalResourceView 는 JSP처럼 포워드 forward() 를 호출해서 처리할 수 있는 경우에 사용한다.

5. view.render()
view.render() 가 호출되고 InternalResourceView 는 forward() 를 사용해서 JSP를 실행한다.

> 참고
> InternalResourceViewResolver 는 만약 JSTL 라이브러리가 있으면 InternalResourceView 를 상속받은 JstlView 를 반환한다. JstlView 는 JSTL 태그 사용시 약간의 부가 기능이 추가된다.

> 참고
> 다른 뷰는 실제 뷰를 렌더링하지만, JSP의 경우 forward() 통해서 해당 JSP로 이동(실행)해야 렌더링이 된다. JSP를 제외한 나머지 뷰 템플릿들은 forward() 과정 없이 바로 렌더링 된다.

> 참고
> Thymeleaf 뷰 템플릿을 사용하면 ThymeleafViewResolver 를 등록해야 한다. 최근에는 라이브러리만 추가하면 스프링 부트가 이런 작업도 모두 자동화해준다.



### 스프링 시작하기
스프링이 제공하는 컨트롤러는 애노테이션 기반으로 동작해서, 매우 유연하고 실용적이다. 과거에는 자바
언어에 애노테이션이 없기도 했고, 스프링도 처음부터 이런 유연한 컨트롤러를 제공한 것은 아니다.

@RequestMapping
스프링은 애노테이션을 활용한 매우 유연하고, 실용적인 컨트롤러를 만들었는데 이것이 바로 @RequestMapping 애노테이션을 사용하는 컨트롤러이다. 다들 한번쯤 사용해보았을 것이다. 여담이지만 과거에는 스프링 프레임워크가 MVC 부분이 약해서 스프링을 사용하더라도 MVC 웹 기술은 스트럿츠 같은 다른 프레임워크를 사용했었다. 그런데 @RequestMapping 기반의 애노테이션 컨트롤러가 등장하면서, MVC 부분도 스프링의 완승으로 끝이 났다.


 @RequestMapping
 	- RequestMappingHandlerMapping
 	- RequestMappingHandlerAdapter
	
앞서 보았듯이 가장 우선순위가 높은 핸들러 매핑과 핸들러 어댑터는 RequestMappingHandlerMapping , RequestMappingHandlerAdapter 이다.
@RequestMapping의 앞글자를 따서 만든 이름인데, 이것이 바로 지금 스프링에서 주로 사용하는 애노테이션 기반의 컨트롤러를 지원하는 핸들러 매핑과 어댑터이다. 실무에서는 99.9% 이 방식의 컨트롤러를 사용한다.

그럼 이제 본격적으로 애노테이션 기반의 컨트롤러를 사용해보자.
지금까지 만들었던 프레임워크에서 사용했던 컨트롤러를 @RequestMapping 기반의 스프링 MVC 컨트롤러 변경해보자.

#### SpringMemberFormControllerV1 - 회원 등록 폼

<img width="1299" alt="스크린샷 2023-03-20 오후 10 21 27" src="https://user-images.githubusercontent.com/96857599/226351656-125d9d43-ca55-4370-9b7e-1b536df40988.png">

- @Controller :
	- 스프링이 자동으로 스프링 빈으로 등록한다. (내부에 @Component 애노테이션이 있어서 컴포넌트 스캔의 대상이 됨)
<img width="1299" alt="스크린샷 2023-03-20 오후 10 21 59" src="https://user-images.githubusercontent.com/96857599/226351897-af9d343b-4a79-428b-a5a3-12906e895e7c.png">

	- 스프링 MVC에서 애노테이션 기반 컨트롤러로 인식한다.
- @RequestMapping : 요청 정보를 매핑한다. 해당 URL이 호출되면 이 메서드가 호출된다. 애노테이션을 기반으로 동작하기 때문에, 메서드의 이름은 임의로 지으면 된다.
- ModelAndView : 모델과 뷰 정보를 담아서 반환하면 된다.

RequestMappingHandlerMapping 은 스프링 빈 중에서 @RequestMapping 또는 @Controller 가 **클래스 레벨**에 붙어 있는 경우에 매핑 정보로 인식한다.
따라서 다음 코드도 동일하게 동작한다.

<img width="1299" alt="스크린샷 2023-03-20 오후 10 25 52" src="https://user-images.githubusercontent.com/96857599/226353648-cbeed56c-7fb0-4eeb-ace1-53b670e3e8f7.png">

**주의! - 스프링 3.0 이상**
스프링 부트 3.0(스프링 프레임워크 6.0)부터는 클래스 레벨에 @RequestMapping 이 있어도 스프링 컨트롤러로 인식하지 않는다. 오직 @Controller 가 있어야 스프링 컨트롤러로 인식한다. 참고로 @RestController 는 해당 애노테이션 내부에 @Controller 를 포함하고 있으므로 인식 된다. 따라서 @Controller 가 없는 위의 두 코드는 스프링 컨트롤러로 인식되지 않는다.
( RequestMappingHandlerMapping 에서 @RequestMapping 는 이제 인식하지 않고, Controller 만 인식한다.)

#### SpringMemberSaveControllerV1 - 회원 저장
<img width="1246" alt="스크린샷 2023-03-20 오후 10 38 16" src="https://user-images.githubusercontent.com/96857599/226356724-afdde316-7890-443f-b125-c1eea48844af.png">
- mv.addObject("member", member)
	- 스프링이 제공하는 ModelAndView 를 통해 Model 데이터를 추가할 때는 addObject() 를 사용하면 된다. 이 데이터는 이후 뷰를 렌더링 할 때 사용된다.


#### SpringMemberListControllerV1 - 회원 목록
<img width="1246" alt="스크린샷 2023-03-20 오후 10 38 50" src="https://user-images.githubusercontent.com/96857599/226356847-325ec66c-5f66-4c55-9d31-3bc1da5e467c.png">


### 스프링 MVC - 컨트롤러 통합

@RequestMapping 을 잘 보면 클래스 단위가 아니라 메서드 단위에 적용된 것을 확인할 수 있다. 따라서
컨트롤러 클래스를 유연하게 하나로 통합할 수 있다.

#### SpringMemberControllerV2

<img width="1246" alt="스크린샷 2023-03-21 오후 7 44 09" src="https://user-images.githubusercontent.com/96857599/226583472-000282f2-cc2f-42ae-a98f-1dc0a770c492.png">


**조합**
컨트롤러 클래스를 통합하는 것을 넘어서 조합도 가능하다.
다음 코드는 /springmvc/v2/members 라는 부분에 중복이 있다.
- @RequestMapping("/springmvc/v2/members/new-form")
- @RequestMapping("/springmvc/v2/members")
- @RequestMapping("/springmvc/v2/members/save")

**조합 결과**
- 클래스 레벨 @RequestMapping("/springmvc/v2/members")
	- 메서드 레벨 @RequestMapping("/new-form") /springmvc/v2/members/new-form 
	- 메서드 레벨 @RequestMapping("/save") /springmvc/v2/members/save
	- 메서드 레벨 @RequestMapping /springmvc/v2/members


### 스프링 MVC - 실용적인 방식

MVC 프레임워크 만들기에서 v3은 ModelView를 개발자가 직접 생성해서 반환했기 때문에, 불편했던
기억이 날 것이다. 물론 v4를 만들면서 실용적으로 개선한 기억도 날 것이다.

스프링 MVC는 개발자가 편리하게 개발할 수 있도록 수 많은 편의 기능을 제공한다.
실무에서는 지금부터 설명하는 방식을 주로 사용한다. 

**SpringMemberControllerV3**
<img width="1513" alt="스크린샷 2023-03-21 오후 7 57 22" src="https://user-images.githubusercontent.com/96857599/226586403-a9c37953-25e8-4a72-9c1d-e4e0a76e0aac.png">

**Model 파라미터**
save() , members() 를 보면 Model을 파라미터로 받는 것을 확인할 수 있다. 스프링 MVC도 이런 편의 기능을 제공한다.

**ViewName 직접 반환**
뷰의 논리 이름을 반환할 수 있다.

**@RequestParam 사용**
스프링은 HTTP 요청 파라미터를 @RequestParam 으로 받을 수 있다. 
@RequestParam("username") 은 request.getParameter("username") 와 거의 같은 코드라 생각하면 된다.
물론 GET 쿼리 파라미터, POST Form 방식을 모두 지원한다.

#### request 방식을 지정해줄 수 있다. (이게 더 좋은 개발)

1. method = RequestMethod.Get 방식으로 받기

<img width="1513" alt="스크린샷 2023-03-21 오후 8 02 25" src="https://user-images.githubusercontent.com/96857599/226587540-dae3b3ad-b94f-4c05-b850-be485fa48824.png">

- postman을 통해  method = RequestMethod.GET 방식으로 받는 페이지를 열면 오류를 발생시킨다.

<img width="1484" alt="스크린샷 2023-03-21 오후 8 05 00" src="https://user-images.githubusercontent.com/96857599/226588039-421f70b6-bf15-4b29-bf10-31ac41fc18d8.png">

**2. @RequestMapping @GetMapping, @PostMapping**
@RequestMapping 은 URL만 매칭하는 것이 아니라, HTTP Method도 함께 구분할 수 있다.
예를 들어서 URL이 /new-form 이고, HTTP Method가 GET인 경우를 모두 만족하는 매핑을 하려면 다음과 같이 처리하면 된다.
```
  @RequestMapping(value = "/new-form", method = RequestMethod.GET)
```

이것을 @GetMapping , @PostMapping 으로 더 편리하게 사용할 수 있다. 
참고로 Get, Post, Put, Delete, Patch 모두 애노테이션이 준비되어 있다.
<img width="1150" alt="스크린샷 2023-03-21 오후 8 08 19" src="https://user-images.githubusercontent.com/96857599/226588757-fda136e5-5f50-4c10-9e18-ad90d3742607.png">


@GetMapping 코드를 열어서 @RequestMapping 애노테이션을 내부에 가지고 있는 모습을 확인하자.
<img width="1150" alt="스크린샷 2023-03-21 오후 8 08 38" src="https://user-images.githubusercontent.com/96857599/226588799-defbce96-a902-4e29-ba20-f65d7b1ffc9c.png">

- 프로젝트 선택
	- Project: Gradle Project 
	- Language: Java 
	- Spring Boot: 2.4.x
- Project Metadata 
	- Group: hello
	- Artifact: springmvc
	- Name: springmvc
	- Package name: hello.springmvc
	- Packaging: Jar (주의!) 
	- Java: 11

- Dependencies: Spring Web, Thymeleaf, Lombok

> 주의!
> Packaging는 War가 아니라 Jar를 선택해주세요. JSP를 사용하지 않기 때문에 Jar를 사용하는 것이
좋습니다. 앞으로 스프링 부트를 사용하면 이 방식을 주로 사용하게 됩니다.
> Jar를 사용하면 항상 내장 서버(톰캣등)를 사용하고, webapp 경로도 사용하지 않습니다. 내장 서버 사용에
최적화 되어 있는 기능입니다. 최근에는 주로 이 방식을 사용합니다.
> War를 사용하면 내장 서버도 사용가능 하지만, 주로 외부 서버에 배포하는 목적으로 사용합니다.


#### Welcome 페이지 만들기

이번 장에서 학습할 내용을 편리하게 참고하기 위해 Welcome 페이지를 만들자.

스프링 부트에 Jar 를 사용하면 /resources/static/ 위치에 index.html 파일을 두면 Welcome 페이지로 처리해준다. (스프링 부트가 지원하는 정적 컨텐츠 위치에 /index.html 이 있으면 된다.


```HTML
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<ul>
    <li>로그 출력
        <ul>
            <li><a href="/log-test">로그 테스트</a></li>
        </ul>
    </li>
    <!-- -->
    <li>요청 매핑
    <ul>
        <li><a href="/hello-basic">hello-basic</a></li>
        <li><a href="/mapping-get-v1">HTTP 메서드 매핑</a></li>
        <li><a href="/mapping-get-v2">HTTP 메서드 매핑 축약</a></li>
        <li><a href="/mapping/userA">경로 변수</a></li>
        <li><a href="/mapping/users/userA/orders/100">경로 변수 다중</a></li>
        <li><a href="/mapping-param?mode=debug">특정 파라미터 조건 매핑</a></li>
        <li><a href="/mapping-header">특정 헤더 조건 매핑(POST MAN 필요)</a></li>
        <li><a href="/mapping-consume">미디어 타입 조건 매핑 Content-Type(POST MAN 필요)</a></li>
        <li><a href="/mapping-produce">미디어 타입 조건 매핑 Accept(POST MAN 필요)</a></li>
        </ul>
    </li>
    <li>요청 매핑 - API 예시
        <ul>
            <li>POST MAN 필요</li>
        </ul>
    </li>
    <li>HTTP 요청 기본
        <ul>
            <li><a href="/headers">기본, 헤더 조회</a></li>
        </ul>
    </li>
    <li>HTTP 요청 파라미터
        <ul>
            <li><a href="/request-param-v1?username=hello&age=20">요청 파라미터 v1</a></li>
            <li><a href="/request-param-v2?username=hello&age=20">요청 파라미터 v2</a></li>
            <li><a href="/request-param-v3?username=hello&age=20">요청 파라미터 v3</a></li>
            <li><a href="/request-param-v4?username=hello&age=20">요청 파라미터 v3</a></li>
            <li><a href="/request-param-required?username=hello&age=20">요청 파라미터 필수</a></li>
            <li><a href="/request-param-default?username=hello&age=20">요청 파라미터 기본 값</a></li>
            <li><a href="/request-param-map?username=hello&age=20">요청 파라미터 MAP</a></li>
            <li><a href="/model-attribute-v1?username=hello&age=20">요청 파라미터 @ModelAttribute v1</a></li>
            <li><a href="/model-attribute-v2?username=hello&age=20">요청 파라미터 @ModelAttribute v2</a></li>
        </ul>
    </li>
    <li>HTTP 요청 메시지
        <ul>
            <li>POST MAN</li>
        </ul>
    </li>
    <li>HTTP 응답 - 정적 리소스, 뷰 템플릿
        <ul>
            <li><a href="/basic/hello-form.html">정적 리소스</a></li>
            <li><a href="/response-view-v1">뷰 템플릿 v1</a></li>
            <li><a href="/response-view-v2">뷰 템플릿 v2</a></li>
        </ul>
    </li>
    <li>HTTP 응답 - HTTP API, 메시지 바디에 직접 입력
        <ul>
            <li><a href="/response-body-string-v1">HTTP API String v1</a></li>
            <li><a href="/response-body-string-v2">HTTP API String v2</a></li>
            <li><a href="/response-body-string-v3">HTTP API String v3</a></li>
            <li><a href="/response-body-json-v1">HTTP API Json v1</a></li>
            <li><a href="/response-body-json-v2">HTTP API Json v2</a></li>
        </ul>
    </li>
</ul>
</body>
</html>

```
<img width="916" alt="스크린샷 2023-03-25 오전 12 41 07" src="https://user-images.githubusercontent.com/96857599/227572888-a82c2fa2-1f77-48d9-9f1d-0cf6ee974485.png">


<img width="956" alt="스크린샷 2023-03-25 오전 12 40 09" src="https://user-images.githubusercontent.com/96857599/227572619-fe79faad-0589-4310-b911-ae3390e20fa4.png">


## 로깅 간단히 알아보기
## 중요

앞으로 로그를 사용할 것이기 때문에, 이번시간에는 로그에 대해서 간단히 알아보자.

운영 시스템에서는 System.out.println() 같은 시스템 콘솔을 사용해서 필요한 정보를 출력하지 않고, 별도의 로깅 라이브러리를 사용해서 로그를 출력한다.
참고로 로그 관련 라이브러리도 많고, 깊게 들어가면 끝이 없기 때문에, 여기서는 최소한의 사용 방법만 알아본다.

**로깅 라이브러리**
스프링 부트 라이브러리를 사용하면 스프링 부트 로깅 라이브러리( spring-boot-starter-logging )가 함께 포함된다.
스프링 부트 로깅 라이브러리는 기본으로 다음 로깅 라이브러리를 사용한다.

- SLF4J - http://www.slf4j.org 
- Logback - http://logback.qos.ch

로그 라이브러리는 Logback, Log4J, Log4J2 등등 수 많은 라이브러리가 있는데, 그것을 통합해서 인터페이스로 제공하는 것이 바로 SLF4J 라이브러리다.
쉽게 이야기해서 SLF4J는 인터페이스이고, 그 구현체로 Logback 같은 로그 라이브러리를 선택하면 된다. 실무에서는 스프링 부트가 기본으로 제공하는 Logback을 대부분 사용한다.

**로그 선언**
- private Logger log = LoggerFactory.getLogger(getClass());
- private static final Logger log = LoggerFactory.getLogger(Xxx.class) 
- @Slf4j : 롬복 사용 가능


**로그 호출**
log.info("hello")
System.out.println("hello")
시스템 콘솔로 직접 출력하는 것 보다 로그를 사용하면 다음과 같은 장점이 있다. 실무에서는 항상 로그를 사용해야 한다.

<img width="1313" alt="스크린샷 2023-03-25 오후 2 31 55" src="https://user-images.githubusercontent.com/96857599/227698377-1d77510f-f417-4b69-8a77-106665925acc.png">

- 시간, 프로세스 이름, 스레드 이름, 실행 클래스 이름, 출력

- application.properties에서 로그 출력 레벨 설정
- 실무에서는 각 서버마다 다르게 설정함
<img width="1122" alt="스크린샷 2023-03-25 오후 2 39 43" src="https://user-images.githubusercontent.com/96857599/227698673-136f1f39-1cc2-4110-8e10-631662d329b7.png">

**로그 레벨 설정**
- application.properties
```
#전체 로그 레벨 설정(기본 info) logging.level.root=info
#hello.springmvc 패키지와 그 하위 로그 레벨 설정 logging.level.hello.springmvc=debug
```

**매핑 정보**
- @RestController
	- @Controller 는 반환 값이 String 이면 뷰 이름으로 인식된다. 그래서 뷰를 찾고 뷰가 랜더링 된다. 
	- @RestController 는 반환 값으로 뷰를 찾는 것이 아니라, HTTP 메시지 바디에 바로 입력한다. 따라서 실행 결과로 ok 메세지를 받을 수 있다. @ResponseBody 와 관련이 있는데, 뒤에서 더 자세히 설명한다.

**테스트**
- 로그가 출력되는 포멧 확인
	- 시간, 로그 레벨, 프로세스 ID, 쓰레드 명, 클래스명, 로그 메시지
- 로그 레벨 설정을 변경해서 출력 결과를 보자.
	- LEVEL: TRACE > DEBUG > INFO > WARN > ERROR 
	- 개발 서버는 debug 출력
	- 운영 서버는 info 출력
- @Slf4j 로 변경

**올바른 로그 사용법**
- log.debug("data="+data)
	- 로그 출력 레벨을 info로 설정해도 해당 코드에 있는 "data="+data가 실제 실행이 되어 버린다. 결과적으로 문자 더하기 연산이 발생한다. 
	- 연산이 일어나는 것이 핵심임. 로그를 사용하지 않아도 쓸모없는 리소스를 사용하게 됨.
- log.debug("data={}", data)
	- 로그 출력 레벨을 info로 설정하면 아무일도 발생하지 않는다. 따라서 앞과 같은 의미없는 연산이 발생하지 않는다.


**로그 사용시 장점**
- 쓰레드 정보, 클래스 이름 같은 부가 정보를 함께 볼 수 있고, 출력 모양을 조정할 수 있다.
- 로그 레벨에 따라 개발 서버에서는 모든 로그를 출력하고, 운영서버에서는 출력하지 않는 등 **로그를 상황에 맞게 조절할 수 있다.**
- 시스템 아웃 콘솔에만 출력하는 것이 아니라, **파일이나 네트워크 등, 로그를 별도의 위치에 남길 수 있다. 특히 파일로 남길 때는 일별, 특정 용량에 따라 로그를 분할하는 것도 가능하다.**
- 성능도 일반 System.out보다 좋다. (내부 버퍼링, 멀티 쓰레드 등등) 그래서 실무에서는 꼭 로그를 사용해야 한다. (수 십배 차이남)

**더 공부하실 분**
- 로그에 대해서 더 자세한 내용은 slf4j, logback을 검색해보자. 
	- SLF4J - http://www.slf4j.org
	- Logback - http://logback.qos.ch
- 스프링 부트가 제공하는 로그 기능은 다음을 참고하자. 
	- https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot- features.html#boot-features-logging

### 요청 매핑-API 예시 

#### MappingController
<img width="1252" alt="스크린샷 2023-03-30 오후 7 14 31" src="https://user-images.githubusercontent.com/96857599/228805005-3aa1c0e2-632f-4777-879f-1e3c07799aa1.png">

**매핑 정보(한번 더)**
- @RestController
	- @Controller 는 반환 값이 String 이면 뷰 이름으로 인식된다. 그래서 뷰를 찾고 뷰가 랜더링 된다.
	- @RestController 는 반환 값으로 뷰를 찾는 것이 아니라, HTTP 메시지 바디에 바로 입력한다. 따라서 실행 결과로 ok 메세지를 받을 수 있다. @ResponseBody 와 관련이 있는데, 뒤에서 더 자세히 설명한다.
- @RequestMapping("/hello-basic")
	- /hello-basic URL 호출이 오면 이 메서드가 실행되도록 매핑한다.
	- 대부분의 속성을 배열[] 로 제공하므로 다중 설정이 가능하다. {"/hello-basic", "/hello-go"}

<img width="1371" alt="스크린샷 2023-03-30 오후 7 18 50" src="https://user-images.githubusercontent.com/96857599/228806144-73a70d69-5998-40ce-9b1d-a7a76a8a7adf.png">


**Postman으로 테스트 해보자.**


**둘다 허용 - 스프링 부트 3.0 이전**
다음 두가지 요청은 다른 URL이지만, 스프링은 다음 URL 요청들을 같은 요청으로 매핑한다. 매핑: /hello-basic
URL 요청: /hello-basic , /hello-basic/


**HTTP 메서드**
@RequestMapping 에 method 속성으로 HTTP 메서드를 지정하지 않으면 HTTP 메서드와 무관하게 호출된다.
모두 허용 GET, HEAD, POST, PUT, PATCH, DELETE

**HTTP 메서드 매핑**
<img width="1010" alt="스크린샷 2023-03-30 오후 7 22 33" src="https://user-images.githubusercontent.com/96857599/228807121-c7780bd8-067c-41f4-9a73-d4e3c56fbcfa.png">

<img width="1033" alt="스크린샷 2023-03-30 오후 7 22 41" src="https://user-images.githubusercontent.com/96857599/228807160-c0a4af73-e69f-4eff-95c8-049095ae61b9.png">

- 만약 여기에 POST 요청을 하면 스프링 MVC는 HTTP 405 상태코드(Method Not Allowed)를 반환한다.
<img width="1033" alt="스크린샷 2023-03-30 오후 7 22 49" src="https://user-images.githubusercontent.com/96857599/228807208-ab892d82-b89b-49ca-9fff-1f5f969971ca.png">


**HTTP 메서드 매핑 축약**
<img width="1010" alt="스크린샷 2023-03-30 오후 7 25 40" src="https://user-images.githubusercontent.com/96857599/228807970-e5bce6ac-ecb2-42d3-b8f8-fef2873218da.png">

<img width="1033" alt="스크린샷 2023-03-30 오후 7 26 34" src="https://user-images.githubusercontent.com/96857599/228808177-4e82e686-d556-42dc-8b72-4141fcc77a28.png">
<img width="1033" alt="스크린샷 2023-03-30 오후 7 26 47" src="https://user-images.githubusercontent.com/96857599/228808227-81e2c8fa-5597-4ab7-b410-1c9d6bea9d98.png">


## **PathVariable(경로 변수) 사용**

<img width="1010" alt="스크린샷 2023-03-30 오후 7 31 18" src="https://user-images.githubusercontent.com/96857599/228809297-408556ba-6568-4663-88e0-a70d47a0854c.png">
<img width="1033" alt="스크린샷 2023-03-30 오후 7 31 24" src="https://user-images.githubusercontent.com/96857599/228809325-c42044d8-2e4d-4701-9e27-690d4033ea31.png">

**최근 HTTP API는 다음과 같이 리소스 경로에 식별자를 넣는 스타일을 선호한다.**
- /mapping/userA
- /users/1

- @RequestMapping 은 URL 경로를 템플릿화 할 수 있는데, @PathVariable 을 사용하면 매칭 되는 부분을 편리하게 조회할 수 있다.
@PathVariable 의 이름과 파라미터 이름이 같으면 생략할 수 있다.
```java
public String mappingPath(@PathVariable String userId) {
	log.info("mappingPath userId={}", userId);
	return "ok";
}
```
**PathVariable 사용-다중**
<img width="1010" alt="스크린샷 2023-03-30 오후 7 38 12" src="https://user-images.githubusercontent.com/96857599/228810904-030a448c-72ed-4d5d-af81-f915986fd98c.png">

<img width="845" alt="스크린샷 2023-03-30 오후 7 38 26" src="https://user-images.githubusercontent.com/96857599/228810964-085c6319-9a4e-40f5-a083-68e7fc78b9fb.png">

**특정 파라미터 조건 매핑**
<img width="1010" alt="스크린샷 2023-03-30 오후 7 41 34" src="https://user-images.githubusercontent.com/96857599/228811661-2d22c019-0bfa-4fee-bfc9-504a6e7b87b9.png">

<img width="845" alt="스크린샷 2023-03-30 오후 7 41 42" src="https://user-images.githubusercontent.com/96857599/228811689-0b08fdf7-92fe-498c-81ae-0f66bac3610b.png">
- 특정 파라미터가 있거나 없는 조건을 추가할 수 있다. 잘 사용하지는 않는다.
**특정 헤더 조건 매핑**

<img width="1010" alt="스크린샷 2023-03-30 오후 7 46 30" src="https://user-images.githubusercontent.com/96857599/228812758-552342c5-abba-43ce-90a7-0478d055e7bc.png">
<img width="845" alt="스크린샷 2023-03-30 오후 7 46 53" src="https://user-images.githubusercontent.com/96857599/228812818-2fa26638-afe2-4242-8568-0c29cdf6cb26.png">

- 파라미터 매핑과 비슷하지만, HTTP 헤더를 사용한다.


**미디어 타입 조건 매핑 - HTTP 요청 Content-Type, consume**

<img width="1010" alt="스크린샷 2023-03-30 오후 7 50 09" src="https://user-images.githubusercontent.com/96857599/228813608-87766784-d5d3-4c69-ab93-e3ad0008bda3.png">

<img width="845" alt="스크린샷 2023-03-30 오후 7 50 00" src="https://user-images.githubusercontent.com/96857599/228813569-f42b95aa-2109-4e70-a132-3d8f2ef2fe34.png">

HTTP 요청의 Content-Type 헤더를 기반으로 미디어 타입으로 매핑한다.
만약 맞지 않으면 HTTP 415 상태코드(Unsupported Media Type)을 반환한다. 
예시) consumes
```
  consumes = "text/plain"
  consumes = {"text/plain", "application/*"}
  consumes = MediaType.TEXT_PLAIN_VALUE
```

**미디어 타입 조건 매핑 - HTTP 요청 Accept, produce**
<img width="1010" alt="스크린샷 2023-03-30 오후 7 53 00" src="https://user-images.githubusercontent.com/96857599/228814255-e68bc307-321a-4477-a455-9310eedbf24b.png">

<img width="845" alt="스크린샷 2023-03-30 오후 7 52 50" src="https://user-images.githubusercontent.com/96857599/228814219-67654618-51ce-4de7-a166-11f142e16f83.png">

<img width="1085" alt="스크린샷 2023-03-30 오후 7 54 32" src="https://user-images.githubusercontent.com/96857599/228814608-ced08b63-1154-4a5b-acf0-a05a98485051.png">

HTTP 요청의 Accept 헤더를 기반으로 미디어 타입으로 매핑한다. 만약 맞지 않으면 HTTP 406 상태코드(Not Acceptable)을 반환한다.

예시)
```
  produces = "text/plain"
  produces = {"text/plain", "application/*"}
  produces = MediaType.TEXT_PLAIN_VALUE
  produces = "text/plain;charset=UTF-8"
```

### 요청 매핑 -API 예시

회원 관리를 HTTP API로 만든다 생각하고 매핑을 어떻게 하는지 알아보자.
(실제 데이터가 넘어가는 부분은 생략하고 URL 매핑만)

**회원 관리 API**
- 회원 목록 조회: GET /users
- 회원 등록: POST 	 /users
- 회원 조회: GET	 /users/{userId} 
- 회원수정: PATCH 	 /users/{userId} 
- 회원 삭제: DELETE  /users/{userId}

**MappingClassController**
<img width="959" alt="스크린샷 2023-04-05 오후 6 32 37" src="https://user-images.githubusercontent.com/96857599/230041594-cf20d5fd-52de-4cd1-93ba-b2da6f1738b5.png">

**postman**
- Get
<img width="1085" alt="스크린샷 2023-04-05 오후 6 33 25" src="https://user-images.githubusercontent.com/96857599/230041783-01561476-e675-4ba8-8c8b-9e886a1e56c6.png">
<img width="1085" alt="스크린샷 2023-04-05 오후 6 33 40" src="https://user-images.githubusercontent.com/96857599/230041842-28dfbee0-eca9-4915-8d05-cab332c26ad0.png">

- Patch
<img width="1085" alt="스크린샷 2023-04-05 오후 6 34 04" src="https://user-images.githubusercontent.com/96857599/230041926-8a7f5dc7-ff23-48e0-af1d-c3ed8136e6c4.png">

- Delete
<img width="1085" alt="스크린샷 2023-04-05 오후 6 34 24" src="https://user-images.githubusercontent.com/96857599/230042010-65db0db2-1738-4d72-b33d-e06a40bc8ac9.png">

- @RequestMapping("/mapping/users")
	- 클래스 레벨에 매핑 정보를 두면 메서드 레벨에서 해당 정보를 조합해서 사용한다.

<img width="959" alt="스크린샷 2023-04-05 오후 6 36 34" src="https://user-images.githubusercontent.com/96857599/230042550-17c262f5-77f7-4e16-9e97-5f38cd12abfe.png">


매핑 방법을 이해했으니, 이제부터 HTTP 요청이 보내는 데이터들을 스프링 MVC로 어떻게 조회하는지 알아보자.


### HTTP 요청 - 기본, 헤더 조회
	
애노테이션 기반의 스프링 컨트롤러는 다양한 파라미터를 지원한다.
이번 시간에는 HTTP 헤더 정보를 조회하는 방법을 알아보자.

**RequestHeaderController**
	- postmand으로 Get 전송
<img width="1159" alt="스크린샷 2023-04-05 오후 6 54 24" src="https://user-images.githubusercontent.com/96857599/230047014-2ef6c7f6-2fe2-4033-9c2c-763dad091e37.png">


- HttpServletRequest
- HttpServletResponse
- HttpMethod : HTTP 메서드를 조회한다. org.springframework.http.HttpMethod 
- Locale : Locale 정보를 조회한다.
- @RequestHeader MultiValueMap<String, String> headerMap
	- 모든 HTTP 헤더를 MultiValueMap 형식으로 조회한다.
- @RequestHeader("host") String host
	- 특정 HTTP 헤더를 조회한다. 
	- 속성
		- 필수 값 여부: required
		- 기본 값 속성: defaultValue
- @CookieValue(value = "myCookie", required = false) String cookie
	- 특정 쿠키를 조회한다. 
	- 속성
		- 필수 값 여부: required 
		- 기본 값: defaultValue
	
MultiValueMap
	- MAP과 유사한데, 하나의 키에 여러 값을 받을 수 있다.
	- HTTP header, HTTP 쿼리 파라미터와 같이 하나의 키에 여러 값을 받을 때 사용한다.
		- keyA=value1&keyA=value2

```java
MultiValueMap<String, String> map = new LinkedMultiValueMap(); // 요청 매핑에서도 그대로 씀.
map.add("keyA", "value1");
map.add("keyA", "value2");
	
//[value1,value2]
List<String> values = map.get("keyA"); 배열로 반환
```
> 참고
> @Controller 의 사용 가능한 파라미터 목록은 다음 공식 메뉴얼에서 확인할 수 있다.
> https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-ann-arguments

> 참고
> @Controller 의 사용 가능한 응답 값 목록은 다음 공식 메뉴얼에서 확인할 수 있다.
> https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-ann-return-types

### HTTP 요청 파라미터 - 쿼리 파라미터, HTML Form 

#### HTTP 요청 데이터 조회 - 개요

서블릿에서 학습했던 HTTP 요청 데이터를 조회 하는 방법을 다시 떠올려보자. 그리고 서블릿으로 학습했던 내용을 스프링이 얼마나 깔끔하고 효율적으로 바꾸어주는지 알아보자.

HTTP 요청 메시지를 통해 클라이언트에서 서버로 데이터를 전달하는 방법을 알아보자.

**클라이언트에서 서버로 요청 데이터를 전달할 때는 주로 다음 3가지 방법을 사용한다.**

- GET - 쿼리 파라미터
	- /url?username=hello&age=20
	- 메시지 바디 없이, URL의 쿼리 파라미터에 데이터를 포함해서 전달 
	- 예) 검색, 필터, 페이징등에서 많이 사용하는 방식
- POST - HTML Form
	- content-type: application/x-www-form-urlencoded
	- 메시지 바디에 쿼리 파리미터 형식으로 전달 username=hello&age=20 
	- 예) 회원 가입, 상품 주문, HTML Form 사용
- HTTP message body에 데이터를 직접 담아서 요청 
	- HTTP API에서 주로 사용, JSON, XML, TEXT 
	- 데이터 형식은 주로 JSON 사용
	- POST, PUT, PATCH


#### 요청 파라미터 - 쿼리 파라미터, HTML Form
HttpServletRequest 의 request.getParameter() 를 사용하면 다음 두가지 요청 파라미터를 조회할 수 있다.

#### GET, 쿼리 파라미터 전송
예시 
```
http://localhost:8080/request-param?username=hello&age=20
```

#### POST, HTML Form 전송 
예시
```
POST /request-param ...
content-type: application/x-www-form-urlencoded
username=hello&age=20
```

GET 쿼리 파리미터 전송 방식이든, POST HTML Form 전송 방식이든 둘다 형식이 같으므로 구분없이 조회할 수 있다.
이것을 간단히 **요청 파라미터(request parameter) 조회**라 한다.

**RequestParamController**
<img width="1302" alt="스크린샷 2023-04-09 오전 12 55 42" src="https://user-images.githubusercontent.com/96857599/230730845-c7b502a2-c8d4-439b-b4e8-8e45fc702c6c.png">

<img width="890" alt="스크린샷 2023-04-09 오전 12 55 49" src="https://user-images.githubusercontent.com/96857599/230730854-cd72bb27-5573-412d-8997-3f65522a0b8f.png">

- 반환 타입이 없으면서 이렇게 응답에 값을 직접 집어넣으면, view 조회X

- request.getParameter(): 여기서는 단순히 HttpServletRequest가 제공하는 방식으로 요청 파라미터를 조회했다.


**Post Form 페이지 생성**
먼저 테스트용 HTML Form을 만들어야 한다.
리소스는 /resources/static 아래에 두면 스프링 부트가 자동으로 인식한다.

main/resources/static/basic/hello-form.html
<img width="1012" alt="스크린샷 2023-04-09 오전 1 02 09" src="https://user-images.githubusercontent.com/96857599/230731138-e4d89944-f97b-46b1-a17f-92fda7b3d9f6.png">
<img width="890" alt="스크린샷 2023-04-09 오전 1 02 25" src="https://user-images.githubusercontent.com/96857599/230731153-daa2bbad-e456-4b08-a2a8-f2ac79acb869.png">

> 참고

> Jar 를 사용하면 webapp 경로를 사용할 수 없다. 이제부터 정적 리소스도 클래스 경로에 함께 포함해야 한다.


### HTTP 요청 파라미터 - @RequestParam
스프링이 제공하는 @RequestParam 을 사용하면 요청 파라미터를 매우 편리하게 사용할 수 있다.

**requestParamV2**
<img width="1231" alt="스크린샷 2023-04-10 오전 12 39 32" src="https://user-images.githubusercontent.com/96857599/230782323-3d0b8e76-11ee-459c-9251-41c600baff94.png">

<img width="1231" alt="스크린샷 2023-04-10 오전 12 39 21" src="https://user-images.githubusercontent.com/96857599/230782315-3ab8a0e3-d70f-4160-9031-dcbe06875a70.png">

- @RequestParam : 파라미터 이름으로 바인딩
- @ResponseBody : View 조회를 무시하고, HTTP message body에 직접 해당 내용 입력

@RequestParam의 name(value) 속성이 파라미터 이름으로 사용 
- @RequestParam("username") String memberName
->request.getParameter("username")

**requestParmamV3**
<img width="1231" alt="스크린샷 2023-04-10 오전 12 42 08" src="https://user-images.githubusercontent.com/96857599/230782447-9f90f54d-d5b2-43ec-97c4-a0c8f239dce8.png">

HTTP 파라미터 이름이 변수 이름과 같으면 @RequestParam(name="xx") 생략 가능


**requestParamV4**
<img width="1231" alt="스크린샷 2023-04-10 오전 12 46 59" src="https://user-images.githubusercontent.com/96857599/230782708-58b8c3e2-6e30-43da-a5cc-7f624a63db49.png">
- String , int , Integer 등의 단순 타입이면 @RequestParam 도 생략 가능

> 참고 <br>
> 이렇게 애노테이션을 완전히 생략해도 되는데, 너무 없는 것도 약간 과하다는 주관적 생각이 있다. 
> @RequestParam 이 있으면 명확하게 요청 파리미터에서 데이터를 읽는 다는 것을 알 수 있다.

> 주의 <br>
> @RequestParam 애노테이션을 생략하면 스프링 MVC는 내부에서 required=false 를 적용한다. required 옵션은 바로 다음에 설명한다.

**파라미터 필수 여부 - requestParamRequired**
<img width="1231" alt="스크린샷 2023-04-10 오전 12 51 51" src="https://user-images.githubusercontent.com/96857599/230782958-c7e50992-cb51-4ca6-abe8-c8685bd95237.png">

- required 값이 true인 username을 안 넣었을 떄 400 에러
<img width="847" alt="스크린샷 2023-04-10 오전 12 53 05" src="https://user-images.githubusercontent.com/96857599/230783018-5b67735d-2790-4c11-b8fe-06930932df07.png">

- required 값이 false인 age를 안 넣었을 때 (int 값에 null이 들어가서 오류가 생김-> Integer 객체로 변경
<img width="847" alt="스크린샷 2023-04-10 오전 12 54 16" src="https://user-images.githubusercontent.com/96857599/230783073-33b89fb2-c91c-4e97-acd5-bdbea7019f67.png">
<img width="1231" alt="스크린샷 2023-04-10 오전 12 55 22" src="https://user-images.githubusercontent.com/96857599/230783138-2378ae0f-3cb0-4716-a7f4-db6929510663.png">


- @RequestParam.required
	- 파라미터 필수 여부
	- 기본값이 파라미터 필수( true )이다.
- /request-param 요청
	- username 이 없으므로 400 예외가 발생한다.

**주의! - 파라미터 이름만 사용**
- /request-param?username=
- 파라미터 이름만 있고 값이 없는 경우 빈문자("")로 통과

**주의! - 기본형(primitive)에 null 입력**
- /request-param 요청 
- @RequestParam(required = false) int age

null 을 int 에 입력하는 것은 불가능(500 예외 발생)
따라서 null 을 받을 수 있는 Integer 로 변경하거나, 또는 다음에 나오는 defaultValue 사용

**기본 값 적용 - requestParamDefault**
<img width="1231" alt="스크린샷 2023-04-10 오전 1 02 01" src="https://user-images.githubusercontent.com/96857599/230783454-e250d423-4e87-40af-b82e-eba399dc1fe2.png">

파라미터에 값이 없는 경우 defaultValue 를 사용하면 기본 값을 적용할 수 있다. 
이미 기본 값이 있기 때문에 required 는 의미가 없다.

defaultValue는 빈 문자의 경우에도 설정한 기본 값이 적용된다. 
/request-param-default?username=
<img width="1231" alt="스크린샷 2023-04-10 오전 1 02 58" src="https://user-images.githubusercontent.com/96857599/230783495-c1bb05a8-f6f4-4127-a668-4d413a4735b2.png">

**파라미터를 Map으로 조회하기 - requestParamMap**
<img width="1231" alt="스크린샷 2023-04-10 오전 1 05 00" src="https://user-images.githubusercontent.com/96857599/230783583-5593e364-dcfc-4165-9ffa-a2fac0b5c193.png">

파라미터를 Map, MultiValueMap으로 조회할 수 있다.

- @RequestParam Map ,
	- Map(key=value)
- @RequestParam MultiValueMap
    - MultiValueMap(key=[value1, value2, ...] ex) (key=userIds, value=[id1, id2])
	
파라미터의 값이 1개가 확실하다면 Map 을 사용해도 되지만, 그렇지 않다면 MultiValueMap 을 사용하자. 
-> 거의 파라미터의 값은 1개이긴 한다
   
### HTTP 요청 파라미터 - @ModelAttribute

실제 개발을 하면 요청 파라미터를 받아서 필요한 객체를 만들고 그 객체에 값을 넣어주어야 한다. 보통
다음과 같이 코드를 작성할 것이다.

```java
@RequestParam String username;
  @RequestParam int age;
  HelloData data = new HelloData();
  data.setUsername(username);
  data.setAge(age);
```

스프링은 이 과정을 완전히 자동화해주는 @ModelAttribute 기능을 제공한다.

먼저 요청 파라미터를 바인딩 받을 객체를 만들자.

**HelloData, @ModelAttribute 적용 - modelAttributeV1**
<img width="1121" alt="스크린샷 2023-04-11 오후 4 13 50" src="https://user-images.githubusercontent.com/96857599/231084170-0a41938a-3aa8-4319-9b87-d927ba974dc6.png">


- 롬복 @Data
	- @Getter , @Setter , @ToString , @EqualsAndHashCode , @RequiredArgsConstructor 를 자동으로 적용해준다.

<img width="1121" alt="스크린샷 2023-04-11 오후 4 15 36" src="https://user-images.githubusercontent.com/96857599/231084523-a811b76e-f2f8-4186-ac58-741eb40a9bc3.png">


마치 마법처럼 HelloData 객체가 생성되고, 요청 파라미터의 값도 모두 들어가 있다.

스프링MVC는 @ModelAttribute 가 있으면 다음을 실행한다.
- HelloData 객체를 생성한다.
- 요청 파라미터의 이름으로 HelloData 객체의 프로퍼티를 찾는다. 그리고 해당 프로퍼티의 setter를 호출해서 파라미터의 값을 입력(바인딩) 한다.
- 예) 파라미터 이름이 username 이면 setUsername() 메서드를 찾아서 호출하면서 값을 입력한다.

**프로퍼티**
객체에 getUsername() , setUsername() 메서드가 있으면, 이 객체는 username 이라는 프로퍼티를 가지고 있다.
username 프로퍼티의 값을 변경하면 setUsername() 이 호출되고, 조회하면 getUsername() 이 호출된다.
```java
@Data
class HelloData {
      getUsername();
      setUsername();
}
```

**바인딩 오류**
- 바인딩은 데이터를 넣는 것을 뜻함
age=abc 처럼 숫자가 들어가야 할 곳에 문자를 넣으면 BindException 이 발생한다. 이런 바인딩 오류를 처리하는 방법은 검증 부분에서 다룬다.


**@ModelAttribute 생략 - modelAttributeV2**
<img width="1180" alt="스크린샷 2023-04-13 오전 1 06 15" src="https://user-images.githubusercontent.com/96857599/231516930-97b8115f-ea39-45c7-8b73-7b6d8d526afe.png">

@ModelAttribute 는 생략할 수 있다.
그런데 @RequestParam 도 생략할 수 있으니 혼란이 발생할 수 있다.

스프링은 해당 생략시 다음과 같은 규칙을 적용한다.
- String , int , Integer 같은 단순 타입 = @RequestParam
- 나머지 = @ModelAttribute (argument resolver 로 지정해둔 타입 외) 

> 참고

> argument resolver는 뒤에서 학습한다.

### HTTP 요청 메시지 - 단순 텍스트 

서블릿에서 학습한 내용을 떠올려보자.
	
HTTP message body에 데이터를 직접 담아서 요청 
	- HTTP API에서 주로 사용, JSON, XML, TEXT 
	- 데이터 형식은 주로 JSON 사용	
	- POST, PUT, PATCH
	
	
요청 파라미터와 다르게, HTTP 메시지 바디를 통해 데이터가 직접 넘어오는 경우는 @RequestParam , @ModelAttribute 를 사용할 수 없다. (물론 HTML Form 형식으로 전달되는 경우는 요청 파라미터로 인정된다.)

- 먼저 가장 단순한 텍스트 메시지를 HTTP 메시지 바디에 담아서 전송하고, 읽어보자. 
- HTTP 메시지 바디의 데이터를 InputStream 을 사용해서 직접 읽을 수 있다.

**RequestBodyStringController**
	
<img width="997" alt="스크린샷 2023-05-10 오후 9 30 20" src="https://github.com/Hoya324/SpringNote/assets/96857599/a637f992-af46-4d86-ae6b-3399f72c9177">

- postMan
	
<img width="1204" alt="스크린샷 2023-05-10 오후 9 34 57" src="https://github.com/Hoya324/SpringNote/assets/96857599/09246d81-5cd9-47f0-8984-7d048c5cfe79">

- 결과
	
<img width="1286" alt="스크린샷 2023-05-10 오후 9 35 15" src="https://github.com/Hoya324/SpringNote/assets/96857599/3d898fa0-d72b-4c64-aa42-fae039b7ca54">

**Input, Output 스트림, Reader - requestBodyStringV2**
	
<img width="1211" alt="스크린샷 2023-05-10 오후 9 38 37" src="https://github.com/Hoya324/SpringNote/assets/96857599/e6e088ba-205f-4378-a86a-54a2e7c1af5b">
	
- postMan
	
<img width="1204" alt="스크린샷 2023-05-10 오후 9 39 50" src="https://github.com/Hoya324/SpringNote/assets/96857599/b3dc3e26-a0b0-40a5-9ab6-1a17d72f88f7">

- 결과
	
<img width="1211" alt="스크린샷 2023-05-10 오후 9 40 17" src="https://github.com/Hoya324/SpringNote/assets/96857599/a4d8c90a-3fc8-451d-bd30-1f0cf755e0bd">



	
**스프링 MVC는 다음 파라미터를 지원한다.**
- InputStream(Reader): **HTTP 요청 메시지** 바디의 내용을 직접 조회 
- OutputStream(Writer):** HTTP 응답 메시지**의 바디에 직접 결과 출력
	
	
**HttpEntity - requestBodyStringV3**
	
<img width="1284" alt="스크린샷 2023-05-10 오후 9 42 56" src="https://github.com/Hoya324/SpringNote/assets/96857599/8969741a-96f9-4618-b5b6-789e8e6676ae">



**스프링 MVC는 다음 파라미터를 지원한다.**
- **HttpEntity**: HTTP header, body 정보를 편리하게 조회
	- 메시지 바디 정보를 직접 조회
	- **요청 파라미터를 조회하는 기능과 관계 없음 @RequestParam X, @ModelAttribute X **
		- 요청파라미터는 GET에 queryParameter 오는 것,
- **HttpEntity는** **응답에도** 사용 가능
	- 메시지 바디 정보 직접 반환 
	- 헤더 정보 포함 가능
	- view 조회X
  
**HttpEntity 를 상속받은 다음 객체들도 같은 기능을 제공한다. **
- **RequestEntity**
	- HttpMethod, url 정보가 추가, 요청에서 사용 
- **ResponseEntity**
	- HTTP 상태 코드 설정 가능, 응답에서 사용
	- 'return new ResponseEntity<String>("Hello World", responseHeaders, HttpStatus.CREATED)'
	

> 참고

> 스프링MVC 내부에서 HTTP 메시지 바디를 읽어서 문자나 객체로 변환해서 전달해주는데, 이때 HTTP
메시지 컨버터( HttpMessageConverter )라는 기능을 사용한다. 이것은 조금 뒤에 HTTP 메시지 컨버터에서 자세히 설명한다.
	
