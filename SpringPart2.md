2022.12.14 ~
# springStudyBasic
스프링 핵심 원리-기본편

### 스프링이란?
스프링에서 지원
<img width="538" alt="스크린샷 2022-12-14 오후 2 42 54" src="https://user-images.githubusercontent.com/96857599/207515594-f04dffb0-d6ff-4d07-b78d-6f46ca8d73be.png">

- 스프링 프레임워크
<img width="535" alt="스크린샷 2022-12-14 오후 2 42 25" src="https://user-images.githubusercontent.com/96857599/207515510-8efba835-ec80-4494-adff-46d272477c18.png">

- 스프링 부트
<img width="518" alt="스크린샷 2022-12-14 오후 2 44 02" src="https://user-images.githubusercontent.com/96857599/207515758-3c53c601-b25e-43ec-88d5-cf084f799494.png">


예전에는 Tomcat 같은 서버를 따로 빌드하고 설정하는 것이 복잡했지만, 스프링부트를 이용하면 간결해짐.
예전에는 외부 라이브러리와의 버전 궁합에 대해 어려움을 겪었지만, 스프링부트가 알아서 해줌.

- 스프링이라는 단어는 무엇을 의미하는가?
1. 스프링 DI 컨테이너 기술
2. 스프링 프레임워크
3. 스프링 부트, 스프링 프레임워크 등을 모두 포함한 스프링 생태계

- 스프링을 왜 만들었을까?

1. 스프링의 핵심
- 스프링은 자바 언어 기반의 프레임워크
- 자바 언어의 가장 큰 특징 - 객체 지향 언어
- 스프링은 객체 지향 언어가 가진 강력한 특징을 살려내는 프레임워크
- 스프링은 좋은 객체 지향 애플리케이션을 개발할 수 있게 도와주는 프레임워크이다.

### 좋은 객체 지향 프로그래밍이란?
- 인터페이스가 바뀌는 일이 없도로 안정적으로 잘 설계하는 것이 중요함
<img width="554" alt="스크린샷 2022-12-15 오후 10 06 24" src="https://user-images.githubusercontent.com/96857599/207866882-bde63eb0-c6a7-4bfc-80aa-a42a93179377.png">
- 객체 지향의 꽃은 다형성이다.<img width="1299" alt="스크린샷 2022-12-18 오후 3 32 07" src="https://user-images.githubusercontent.com/96857599/208284887-5ac5ae8c-6799-4458-b7f4-fc258dde1db9.png">

- 스프링은 다형성을 극대화해서 이용하게 해준다.
- 스프링에서 이야기하는 제어의 역전(IoC), 의존관계 주입(DI)은 다형성을 활용해서 역할과 구현 편리하게 다룰 수 있도록 지원한다.
- 스프링을 사용하면 마치 레고 블러 조립하듯, 공연 무대 배우를 선택하듯, 구현을 편리하게 변경할 수 있다.

 
### 좋은 객체 지향 설계의 5가지 원칙(SOLID)
1. SRP 단일 책임 원칙 Single responsibility principle
 
- 한 클래스는 하나의 책임만 가져야 한다. 
- 하나의 책임이라는 것은 모호하다.
 	- 클 수 있고, 작을 수 있다.
 	- 문맥과 상황에 따라 다르다.
- 중요한 기준은 변경이다. 변경이 있을 때 파급 효과가 적으면 단일 책임 원칙을 잘 따른 것 
- 예) UI 변경, 객체의 생성과 사용을 분리

2. OCP 개방-폐쇄 원칙 Open/closed principle (가장 중요한 원칙)

- 소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.
- 이런 거짓말 같은 말이? 확장을 하려면, 당연히 기존 코드를 변경? 
- 다형성을 활용해보자
- 인터페이스를 구현한 새로운 클래스를 하나 만들어서 새로운 기능을 구현 
- 지금까지 배운 역할과 구현의 분리를 생각해보자
<img width="645" alt="스크린샷 2022-12-16 오후 1 55 28" src="https://user-images.githubusercontent.com/96857599/208025395-8f5bed75-0e48-4c17-b3cc-7087bb502302.png">

#### OCP 개방-폐쇄 원칙 문제점
- MemberService 클라이언트가 구현 클래스를 직접 선택
 	- MemberRepository m = new MemoryMemberRepository(); //기존 코드
 	- MemberRepository m = new JdbcMemberRepository(); //변경 코드 
- 구현 객체를 변경하려면 클라이언트 코드를 변경해야 한다.
- 분명 다형성을 사용했지만 OCP 원칙을 지킬 수 없다.
- 이 문제를 어떻게 해결해야 하나?
- 객체를 생성하고, 연관관계를 맺어주는 별도의 조립, 설정자가 필요하다. (스프링 컨테이너의 역할)

3. LSP 리스코프 치환 원칙 Liskov substitution principle

- 프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다
- 다형성에서 하위 클래스는 인터페이스 규약을 다 지켜야 한다는 것, 다형성을 지원하기 위 한 원칙, 인터페이스를 구현한 구현체는 믿고 사용하려면, 이 원칙이 필요하다.
- 단순히 컴파일에 성공하는 것을 넘어서는 이야기
- 예) 자동차 인터페이스의 엑셀은 앞으로 가라는 기능, 뒤로 가게 구현하면 LSP 위반, 느리더라도 앞으로 가야함

4. ISP 인터페이스 분리 원칙 Interface segregation principle

- 특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다 
- 자동차 인터페이스 -> 운전 인터페이스, 정비 인터페이스로 분리
- 사용자 클라이언트 -> 운전자 클라이언트, 정비사 클라이언트로 분리
- 분리하면 정비 인터페이스 자체가 변해도 운전자 클라이언트에 영향을 주지 않음 
- 인터페이스가 명확해지고, 대체 가능성이 높아진다.

5. DIP 의존관계 역전 원칙 Dependency inversion principle(중요)

- 프로그래머는 “추상화에 의존해야지, 구체화에 의존하면 안된다.” 의존성 주입은 이 원칙 을 따르는 방법 중 하나다.
- 쉽게 이야기해서 구현 클래스에 의존하지 말고, 인터페이스에 의존하라는 뜻
- 앞에서 이야기한 역할(Role)에 의존하게 해야 한다는 것과 같다. 객체 세상도 클라이언트 가 인터페이스에 의존해야 유연하게 구현체를 변경할 수 있다! 구현체에 의존하게 되면 변경이 아주 어려워진다.

#### DIP 의존관계 역전 원칙 Dependency inversion principle

- 그런데 OCP에서 설명한 MemberService는 인터페이스에 의존하지만, 구현 클래스도 동시에 의존한다.
- MemberService 클라이언트가 구현 클래스를 직접 선택
- MemberRepository m = new MemoryMemberRepository();
- DIP 위반

#### 정리

- 객체 지향의 핵심은 다형성
- 다형성 만으로는 쉽게 부품을 갈아 끼우듯이 개발할 수 없다.
- 다형성 만으로는 구현 객체를 변경할 때 클라이언트 코드도 함께 변경된다. 다형성 만으로는 OCP, DIP를 지킬 수 없다.
- 뭔가 더 필요하다.(이후에 알아갈 내용)

### 객체 지향 설계와 스프링

- 스프링은 다음 기술로 다형성 + OCP,DIP를 가능하게 지원
	- DI(Dependency Injection): 의존관계, 의존성 주입
 	- DI 컨테이너 제공
- 클라이언트 코드의 변경 없이 기능 확장 
- 쉽게 부품을 교체하듯이 개발


- 옛날 어떤 개발자가 좋은 객체 지향 개발을 하려고 OCP, DIP 원칙을 지키면서 개발을 해 보니, 너무 할일이 많았다. 배보다 배꼽이 크다. 그래서 프레임워크로 만들어버림
- 순수하게 자바로 OCP, DIP 원칙들을 지키면서 개발을 해보면, 결국 스프링 프레임워크를 만들게 된다. (더 정확히는 DI 컨테이너)
- DI 개념은 말로 설명해도 이해가 잘 안된다. 코드로 짜봐야 필요성을 알게된다! 
- 그러면 이제 스프링이 왜? 만들어졌는지 코드로 이해해보자

### 프로젝트 생성
1. Spring Initializr에서 스프링 생성
<img width="958" alt="스크린샷 2022-12-16 오후 2 29 38" src="https://user-images.githubusercontent.com/96857599/208028995-9eb8f072-1b4c-452c-89bc-74e9d854efed.png">
2. Preference에서 gradle 설정 변경 Buid and Run Using과 Run test using 설정을 모두 IntelliJ IDEA로 변경(실행시 더 빨라짐)
<img width="966" alt="스크린샷 2022-12-16 오후 2 28 59" src="https://user-images.githubusercontent.com/96857599/208029222-aaba1f73-1cff-4aa0-9552-0a3fbb88ffea.png">

### 비지니스 요구사항과 설계
<img width="881" alt="스크린샷 2022-12-16 오후 2 35 57" src="https://user-images.githubusercontent.com/96857599/208029656-380786fe-f59d-42bc-80e6-7f130450c5c4.png">

### 회원 도메인 설계

<img width="638" alt="스크린샷 2022-12-17 오후 3 53 27" src="https://user-images.githubusercontent.com/96857599/208229657-7bbd7708-40fb-467b-ae45-e508c9157f0c.png">


<img width="633" alt="스크린샷 2022-12-17 오후 3 53 45" src="https://user-images.githubusercontent.com/96857599/208229668-8741f591-c7fb-4dac-829d-7b29309303c4.png">

#### 회원 속성

1. member 패키지에 Grade 열거형 상수로 BASIC과 VIP를 입력한다.

<img width="900" alt="스크린샷 2022-12-17 오후 4 04 01" src="https://user-images.githubusercontent.com/96857599/208230090-aaa2374b-b834-40e0-872f-987f276f4f03.png">

2. member 패키지에 Member 클래스를 만들고, 각 속성의 생성자와 getter setter를 만들어준다.
<img width="1041" alt="스크린샷 2022-12-17 오후 4 07 38" src="https://user-images.githubusercontent.com/96857599/208230218-00dd6848-fe12-4c10-ba6f-3182a7cc33c9.png">

#### 회원 레포지토리

3. member 패키지에 MemberRepository 인터페이스를 만들어주고, save, findById 기능을 넣어준다.
<img width="1041" alt="스크린샷 2022-12-17 오후 4 12 21" src="https://user-images.githubusercontent.com/96857599/208230385-20955dbc-2a78-43e4-8022-9bc632068a5f.png">

4. MemberRepository 인터페이스와 다른 패키지에 생성하는 것이 좋지만 지금 예제에서는 복잡해지기 때문에 같은 member 패키지에 MemoryMemberRepository를 생성한다.(오류처리도 해야하지만, 예제이기 때문에 넘어감.)

<img width="1235" alt="스크린샷 2022-12-17 오후 4 22 11" src="https://user-images.githubusercontent.com/96857599/208230691-8b6985b7-eaff-4d23-aac3-e6543c4aba3a.png">

[HashTable, HashMap, concurrentHashMap에 대한 정리](https://devlog-wjdrbs96.tistory.com/269)

#### 회원 서비스

5. MemebrService 인터페이스를 만들어주고, 회원 가입, 회원 조회 기능을 넣어준다.

<img width="936" alt="스크린샷 2022-12-17 오후 4 29 29" src="https://user-images.githubusercontent.com/96857599/208230993-f72cc678-443a-4605-929e-e48d99b785bb.png">

6. MemberServiceImpl 구현 클래스를 만들고, MemberService 인터페이스를 구현해준다.(구현 클래스가 하나일 때 관례적으로 인터페이스 이름 뒤에 Impl을 붙여서 구현 클래스를 만든다.)

<img width="1145" alt="스크린샷 2022-12-17 오후 4 34 03" src="https://user-images.githubusercontent.com/96857599/208231166-6f0391cd-0263-4d3a-85bc-896ae7630595.png">

### 회원 도메인 실행과 테스트

1. MemberApp을 만들어 간단한 실행을 해본다. (권장하지 않는 방법) 

<img width="1127" alt="스크린샷 2022-12-17 오후 4 45 06" src="https://user-images.githubusercontent.com/96857599/208231564-d6125794-ea80-49dc-bac2-1f3bfa093747.png">

2. Junit을 이용한 테스트를 진행해본다.
<img width="1127" alt="스크린샷 2022-12-17 오후 4 54 25" src="https://user-images.githubusercontent.com/96857599/208231910-df015b8d-ace1-460d-b53c-fa6756af5edc.png">

#### 회원 도메인 설계의 문제점
- 이 코드의 설계상 문제점은 무엇일까요?
- 다른 저장소로 변경할 때 OCP 원칙을 잘 준수할까요?
- DIP를 잘 지키고 있을까요?
- 의존관계가 인터페이스 뿐만 아니라 구현까지 모두 의존하는 문제점이 있음
<img width="692" alt="스크린샷 2022-12-17 오후 4 59 29" src="https://user-images.githubusercontent.com/96857599/208232071-2e944ee2-d76d-4966-be95-c8b2a74edf61.png">
이 경우만 해도 MemberRepository라는 인터페이스와 MemoryMemberRepository라는 구현체 모두를 의존하고 있기 때문에 인터페이스만 의존했을 때 지켜지는 DIP원칙은 물론 OCP원칙도 지키지 못하고 있다.


### 주문과 할인 도메인 설계

<img width="685" alt="스크린샷 2022-12-17 오후 5 33 52" src="https://user-images.githubusercontent.com/96857599/208233403-bd43be4f-84cb-4390-bac0-09db6bbb06d2.png">

<img width="683" alt="스크린샷 2022-12-17 오후 5 34 21" src="https://user-images.githubusercontent.com/96857599/208233417-fb300e26-209d-41db-a29d-1e78d765708e.png">

<img width="685" alt="스크린샷 2022-12-17 오후 5 34 50" src="https://user-images.githubusercontent.com/96857599/208233437-1541b4b0-2028-4648-b2fd-78f1b3d34e5a.png">

- 주문 도메인 클래스 다이어그램
<img width="685" alt="스크린샷 2022-12-17 오후 5 35 31" src="https://user-images.githubusercontent.com/96857599/208233454-d593ce27-3f39-4699-abb3-58193f5518b0.png">

<img width="684" alt="스크린샷 2022-12-17 오후 5 35 46" src="https://user-images.githubusercontent.com/96857599/208233462-2ba85d7b-d9ee-4d73-a452-eeb920684079.png">

<img width="684" alt="스크린샷 2022-12-17 오후 5 36 06" src="https://user-images.githubusercontent.com/96857599/208233470-d4d5b935-fbc5-4997-b313-0e07384f8471.png">

## 설계된 클래스를 가장 깊숙한 곳부터 개발했음.

### 주문과 할인 도메인 개발

1. 할인 정책 인터페이스 설정

<img width="911" alt="스크린샷 2022-12-18 오후 1 27 14" src="https://user-images.githubusercontent.com/96857599/208281483-6227bf9a-7372-4a15-993e-513546bbacd9.png">

2. 정액 할인 정책 구현체

<img width="987" alt="스크린샷 2022-12-18 오후 1 31 36" src="https://user-images.githubusercontent.com/96857599/208281588-945a78f4-249f-4eb9-a108-6267717427d1.png">

3. order 패키지와 Order 클래스 생성 후, 생성자, getter setter 세팅 및 할인 가격 계산 메소드 생성
<img width="1041" alt="스크린샷 2022-12-18 오후 2 25 50" src="https://user-images.githubusercontent.com/96857599/208282968-11ba4b5f-e0bb-4d09-8833-0ad46319cc71.png">

4. 보기 쉽게 하기 위해 toString()
<img width="491" alt="스크린샷 2022-12-18 오후 2 27 31" src="https://user-images.githubusercontent.com/96857599/208283017-05155fc4-01b8-4705-9000-ee9679f00eae.png">

<img width="508" alt="스크린샷 2022-12-18 오후 2 27 47" src="https://user-images.githubusercontent.com/96857599/208283025-a42fbcfe-7ce9-4aed-90d0-0bd91d65edd0.png">

5. 주문서비스 인터페이스 생성
<img width="1041" alt="스크린샷 2022-12-18 오후 2 30 58" src="https://user-images.githubusercontent.com/96857599/208283097-493cd10e-b454-4fbd-aca3-2d887dc877c6.png">

6. 주문서비스 구현

<img width="1270" alt="스크린샷 2022-12-18 오후 3 33 49" src="https://user-images.githubusercontent.com/96857599/208284910-80404c77-8ac4-4bea-aedf-222263ed57d5.png">

### 주문과 할인 도메인 실행과 테스트

1. OrderApp으로 order 실행테스트

<img width="1100" alt="스크린샷 2022-12-18 오후 7 45 39" src="https://user-images.githubusercontent.com/96857599/208294048-72fa8279-c755-4c71-8787-a3df80b137f6.png">

2. Junit으로 테스트

<img width="1332" alt="스크린샷 2022-12-18 오후 8 05 22" src="https://user-images.githubusercontent.com/96857599/208294853-9b38b60e-809a-4c30-bac2-4eda340bece1.png">

#### 클라이언트가 주문서비스에 주문 생성을 하고, 회원 조회와 할인으 적용하는 것까지의 결과를 반환했다. 다음에는 정률 할인 정책으로 바꾸었을 때 깔끔하게 바꿀 수 있는지 확인할 것이다.

### 새로운 할인 정책 개발

<img width="641" alt="스크린샷 2022-12-18 오후 8 11 56" src="https://user-images.githubusercontent.com/96857599/208295104-3f050dd6-49f7-4597-85d5-cb73d6e1ca52.png">

1. 정률 할인 정책 클래스 생성 및 테스트 생성

<img width="954" alt="스크린샷 2022-12-18 오후 8 17 45" src="https://user-images.githubusercontent.com/96857599/208295379-c10bfcb9-388d-4ef1-ab0d-b7473e049d52.png">

cmd + shift + T로 테스트 생성

- 성공 테스트

<img width="1199" alt="스크린샷 2022-12-18 오후 8 21 21" src="https://user-images.githubusercontent.com/96857599/208295527-7dd531b0-ca4b-49c1-84af-d82893716ae7.png">

- 실패 테스트

<img width="1199" alt="스크린샷 2022-12-18 오후 8 24 05" src="https://user-images.githubusercontent.com/96857599/208295675-2274210a-5d2a-4521-9ad0-41428d59dfb9.png">

- 동시 테스트

<img width="1199" alt="스크린샷 2022-12-18 오후 8 25 08" src="https://user-images.githubusercontent.com/96857599/208295738-0af59391-4ebc-4c18-aae4-7908cbbfc43c.png">

- 원래 할인 정책에 대한 테스트는 실무에서 경계값을 모두 테스트 해볼 정도로 어려운 테스트이지만 지금은 예제로 공부하는 상태이고, 객체지향적인 코드를 만들었기 때문에 간단하게 할 수 있었다.

<img width="561" alt="스크린샷 2022-12-18 오후 8 27 33" src="https://user-images.githubusercontent.com/96857599/208295831-5ac95238-9f73-4a4f-9b56-fe3bfd18e64c.png">

이렇게 간단하지 않다..

### 새로운 할인 정책 적용과 문제점

새로운 할인 정책인 정률 할인 정책을 OrderServiceImpl에 적용해본다.
<img width="1207" alt="스크린샷 2022-12-18 오후 8 29 53" src="https://user-images.githubusercontent.com/96857599/208295924-9d79b39b-31d0-42f1-ba72-ede50ebf6146.png">

문제점 발견
- 우리는 역할과 구현을 충실하게 분리했다. -> OK
- 다형성도 활용하고, 인터페이스와 구현 객체를 분리했다. -> OK 
- OCP, DIP 같은 객체지향 설계 원칙을 충실히 준수했다?
   -> 그렇게 보이지만 사실은 아니다.
- DIP: 주문서비스 클라이언트( OrderServiceImpl )는 DiscountPolicy 인터페이스에 의존하면서 DIP를 지킨 것 같은데?
   -> 클래스 의존관계를 분석해 보자. 추상(인터페이스) 뿐만 아니라 구체(구현) 클래스에도 의존하고 있다.
      - 추상(인터페이스) 의존: DiscountPolicy
      - 구체(구현) 클래스: FixDiscountPolicy , RateDiscountPolicy 

<img width="628" alt="스크린샷 2022-12-18 오후 8 37 43" src="https://user-images.githubusercontent.com/96857599/208296234-3eed8475-9b7f-4969-95b9-0185da13406b.png">


<img width="640" alt="스크린샷 2022-12-18 오후 8 35 47" src="https://user-images.githubusercontent.com/96857599/208296163-3ff71114-0d4a-43c5-bfba-333fdaab6d5e.png">

또한, 할인 정책을 변경하는 순간

<img width="615" alt="스크린샷 2022-12-18 오후 8 38 13" src="https://user-images.githubusercontent.com/96857599/208296258-1612534d-667b-4f2f-8b7b-23c6f6d07c2a.png">

<img width="641" alt="스크린샷 2022-12-18 오후 8 38 33" src="https://user-images.githubusercontent.com/96857599/208296271-8e7275a2-1428-4443-bfa6-d18090bfe49c.png">

- OCP: 변경하지 않고 확장할 수 있다고 했는데!
   -> 지금 코드는 기능을 확장해서 변경하면, 클라이언트 코드에 영향을 준다! 따라서 OCP를 위반한다.

## 어떻게 문제를 해결할 수 있을까?

- 클라이언트 코드인 OrderServiceImpl은 DiscountPolicy의 인터페이스 뿐만 아니라 구체 클래스도 함께 의존한다.
- 그래서 구체 클래스를 변경할 때 클라이언트 코드도 함께 변경해야 한다.
- DIP 위반 -> 추상에만 의존하도록 변경(인터페이스에만 의존)
- DIP를 위반하지 않도록 인터페이스에만 의존하도록 의존관계를 변경하면 된다.

- 인터페이스에만 의존하도록 설계를 변경하자.

<img width="639" alt="스크린샷 2022-12-18 오후 8 40 47" src="https://user-images.githubusercontent.com/96857599/208296357-0870a75d-626d-47c3-b8ac-803ab0d84e36.png">

<img width="755" alt="스크린샷 2022-12-18 오후 8 42 01" src="https://user-images.githubusercontent.com/96857599/208296409-170be7a9-d07c-4fe3-bab5-284155cbad2e.png">

- 인터페이스에만 의존하도록 설계와 코드를 변경했다.
- 그런데 구현체가 없는데 어떻게 코드를 실행할 수 있을까?
- 실제 실행을 해보면 NPE(null pointer exception)가 발생한다. -> 당연하게도 discountPolicy는 현재 인터페이스이므로 비어있다.
<img width="1258" alt="스크린샷 2022-12-18 오후 8 44 15" src="https://user-images.githubusercontent.com/96857599/208296487-42fe98ce-5d0c-4157-93d4-ade4583de0f1.png">

#### 해결방안

- 이 문제를 해결하려면 누군가가 클라이언트인 OrderServiceImpl에 DiscountPolicy의 구현 객체를 대신 생성하고 주입해주어야 한다.

### 관심사의 분리

#### AppConfig 등장

애플리케이션의 전체 동작 방식을 구성(config)하기 위해, **구현 객체를 생성**하고, **연결**하는 책임을 가지는 별도의 설정 클래스를 만들자.

#### MemberServiceImpl에서 MemberRepository를 바로 MemoryMemberRepository로 지정하는 것이 아니라, 생성자를 만들고, AppConfig에서 설정하도록 변경한다. 즉, AppConfig에서 어떤 구현체를 사용할지 정할 수 있도록 바꾸고, MemberServiceImpl같은 클라이언트가 직접 구현 클래스를 의존하는 것을 막고 연결시키는 것이다.

- AppConfig에서 MemberService가 사용할 repository를 설정할 수 있도록 한다.
<img width="1364" alt="스크린샷 2022-12-18 오후 8 51 52" src="https://user-images.githubusercontent.com/96857599/208296819-6e6dd87a-4a4d-48f6-9f8b-df2b5f17c426.png">

- 구현체와의 직접 연결을 끊고 생성자를 만든다.
<img width="1305" alt="스크린샷 2022-12-18 오후 8 55 36" src="https://user-images.githubusercontent.com/96857599/208296984-c3b95eeb-15b5-4be5-b69c-c879560ab728.png">

- AppConfig에서 MemberService와 MemoryMemberRepository를 연결해준다.
<img width="1430" alt="스크린샷 2022-12-18 오후 9 13 00" src="https://user-images.githubusercontent.com/96857599/208297714-63ed2480-c409-457e-8519-a772ae892389.png">

#### 마찬가지로 OrderServiceImpl도 바꾸어준다.

- AppConfig에서 OrderService가 사용할 repository와 할인 정책을 설정할 수 있도록 한다.
<img width="1430" alt="스크린샷 2022-12-18 오후 9 11 15" src="https://user-images.githubusercontent.com/96857599/208297645-1aedb884-8c2b-4a4f-92fe-d65537ad65cd.png">

- 구현체와의 직접 연결을 끊고 생성자를 만든다.
<img width="1430" alt="스크린샷 2022-12-18 오후 9 11 35" src="https://user-images.githubusercontent.com/96857599/208297657-34e4dc0c-cd9b-48ca-b59a-ef05174eafb8.png">

- AppConfig에서 OrderService와 MemoryMemberRepository, RateDiscountPolicy를 연결해준다.
<img width="1430" alt="스크린샷 2022-12-18 오후 9 11 47" src="https://user-images.githubusercontent.com/96857599/208297661-98a6a4cf-bb3d-4298-89ee-3ffc1b5ef7c2.png">

그림 - 클래스 다이어그램

<img width="641" alt="스크린샷 2022-12-18 오후 9 48 00" src="https://user-images.githubusercontent.com/96857599/208299209-b236fbae-9d31-4bd2-9bc4-95c41921cfce.png">

그림 - 회원 객체 인스턴스 다이어그램
<img width="640" alt="스크린샷 2022-12-18 오후 9 48 45" src="https://user-images.githubusercontent.com/96857599/208299262-ea277d89-84bf-4d98-8bcd-373f4183c1bc.png">

#### main 클래스 테스트 DI 변경 후 실행

- MemberApp 실행에서 필요한 memberService 인터페이스에 AppConfig에서 설정한 MemoryMemberRepository를 주입한 memberService 객체를 생성한다.
<img width="1226" alt="스크린샷 2022-12-18 오후 9 58 57" src="https://user-images.githubusercontent.com/96857599/208299746-4779bf30-4640-4f94-b6b2-ee2f8fc20af6.png">

- OrderApp 실행에서 필요한 memberService 인터페이스, orderService 인터페이스에 AppConfig에서 설정한 MemoryMemberRepository를 주입한 memberService 객체와 FixDiscountPolicy를 주입한 orderService를 생성 한다.

#### Junit 테스트 DI 변경 후 실행

- 테스트의 가장 처음에 memberService를 AppConfig에서 가져온다.
<img width="1043" alt="스크린샷 2022-12-18 오후 10 12 36" src="https://user-images.githubusercontent.com/96857599/208300314-58aac663-9bdb-4d62-98a3-d8120de52d71.png">

- 테스트의 가장 처음에 memberService와 orderService를 AppConfig에서 가져온다.
<img width="1043" alt="스크린샷 2022-12-18 오후 10 14 16" src="https://user-images.githubusercontent.com/96857599/208300379-4f0abee7-e2b6-4312-adb2-228b1f574802.png">

### AppConfig 리팩터링
- 현재 AppConfig를 보면 **중복**이 있고, **역할**에 따른 **구현**이 잘 안 보인다.

기대하는 그림
<img width="639" alt="스크린샷 2022-12-18 오후 10 18 48" src="https://user-images.githubusercontent.com/96857599/208300593-a3085576-7900-4209-842f-07f84f15ed2f.png">

리팩터링 전
<img width="1321" alt="스크린샷 2022-12-18 오후 10 19 23" src="https://user-images.githubusercontent.com/96857599/208300613-223650da-9731-42e5-a8c2-97f0250caf7b.png">

**TIP💡 cmd + option + M을 누르면 method를 추가할 수 있다.**

리팩토링 후
<img width="1121" alt="스크린샷 2022-12-18 오후 10 25 39" src="https://user-images.githubusercontent.com/96857599/208300873-cc288d73-4a27-4701-9841-8c596803f695.png">

- new MemoryMemberRepository()이 부분이 중복 제거되었다. 이제 MemoryMemberRepository를 다른 구현체로 변경할 때 한 부분만 변경하면 된다.
- AppConfig를 보면 역할과 구현 클래스가 한눈에 들어온다. 애플리케이션 전체 구성이 어떻게 되어있는지 빠르게 파악할 수 있다.

### 새로운 구조와 할인 정책 적용

- AppConfig의 등장으로 애플리케이션이 크게 사용 영역과, 객체를 생성하고 구성(Configuration)하는 영역으로 분리되었다.

<img width="640" alt="스크린샷 2022-12-18 오후 10 29 55" src="https://user-images.githubusercontent.com/96857599/208301072-d7b03eef-989b-4867-9463-c2b947e782f3.png">

<img width="1297" alt="스크린샷 2022-12-18 오후 10 31 04" src="https://user-images.githubusercontent.com/96857599/208301104-ad8d27bc-7b1e-4879-a8b5-147454559f48.png">

- AppConfig에서 할인 정책 역할을 담당하는 구현을 FixDiscountPolicy 객체로 변경했다.
- 이제 할인 정책을 변경해도, 애플리케이션의 구성 역할을 담당하는 AppConfig만 변경하면 된다. 클라이언트 코드인 OrderServiceImpl를 포함해서 사용 영역의 어떤 코드도 변경할 필요가 없다.
- 구성 영역은 당연히 변경된다. 구성 역할을 담당하는 AppConfig를 애플리케이션이라는 공연의 기획자로 생각하자. 공연 기획자는 공연 참여자인 구현 객체들을 모두 알아야 한다.

### 좋은 객체 지향 설계의 5가지 원칙 적용

여기서 3가지 SRP, DIP, OCP 적용
#### SRP 단일 책임 원칙
**한 클래스는 하나의 책임만 가져야 한다.**

- 클라이언트 객체는 직접 구현 객체를 생성하고, 연결하고, 실행하는 다양한 책임을 가지고 있음
- SRP 단일 책임 원칙을 따르면서 관심사를 분리함
- 구현 객체를 생성하고 연결하는 책임은 AppConfig가 담당
- 클라이언트 객체는 실행하는 책임만 담당


#### DIP 의존관계 역전 원칙
**프로그래머는 “추상화에 의존해야지, 구체화에 의존하면 안된다.” 의존성 주입은 이 원칙을 따르는 방법 중 하나다.**

- 새로운 할인 정책을 개발하고, 적용하려고 하니 클라이언트 코드도 함께 변경해야 했다. 왜냐하면 기존 클라이언트 코드(OrderServiceImpl)는 DIP를 지키며 DiscountPolicy 추상화 인터페이스에 의존하는 것 같았지만, FixDiscountPolicy 구체화 구현 클래스에도 함께 의존했다.
- 클라이언트 코드가 DiscountPolicy 추상화 인터페이스에만 의존하도록 코드를 변경했다.
- 하지만 클라이언트 코드는 인터페이스만으로는 아무것도 실행할 수 없다.
- AppConfig가 FixDiscountPolicy 객체 인스턴스를 클라이언트 코드 대신 생성해서 클라이언트 코드에 의존관계를 주입했다. 이렇게해서 DIP 원칙을 따르면서 문제도 해결했다.


#### OCP
**소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.**

- 다형성 사용하고 클라이언트가 DIP를 지킴
- 애플리케이션을 사용 영역과 구성 영역으로 나눔
- AppConfig가 의존관계를 FixDiscountPolicy RateDiscountPolicy 로 변경해서 클라이언트 코드에 주입하므로 클라이언트 코드는 변경하지 않아도 됨
- 소프트웨어 요소를 새롭게 확장해도 사용 영역의 변경은 닫혀 있다!


### IoC, DI, 그리고 컨테이너

#### 제어의 역전 IoC(Inversion of Control)
- 기존 프로그램은 클라이언트 구현 객체가 스스로 필요한 서버 구현 객체를 생성하고, 연결하고, 실행했다. 한마디로 구현 객체가 프로그램의 제어 흐름을 스스로 조종했다. 개발자 입장에서는 자연스러운 흐름이다.
- 반면에 AppConfig가 등장한 이후에 구현 객체는 자신의 로직을 실행하는 역할만 담당한다. 프로그램의 제어 흐름은 이제 AppConfig가 가져간다. 예를 들어서 OrderServiceImpl은 필요한 인터페이스들을 호출하지만 어떤 구현 객체들이 실행될지 모른다.
- 프로그램에 대한 제어 흐름에 대한 권한은 모두 AppConfig가 가지고 있다. 심지어 OrderServiceImpl 도 AppConfig가 생성한다. 그리고 AppConfig는 OrderServiceImpl이 아닌 OrderService 인터페이스의 다른 구현 객체를 생성하고 실행할 수도 있다. 그런 사실도 모른체 OrderServiceImpl은 묵묵히 자신의 로직을 실행할 뿐이다.
- 이렇듯 프로그램의 제어 흐름을 직접 제어하는 것이 아니라 외부(AppConfig)에서 관리하는 것을 제어의 역전(IoC)이라 한다.


#### 프레임워크 vs 라이브러리
- 프레임워크가 내가 작성한 코드를 제어하고, 대신 실행하면 그것은 프레임워크가 맞다. (JUnit)
<img width="1007" alt="스크린샷 2022-12-19 오후 1 12 29" src="https://user-images.githubusercontent.com/96857599/208346119-48c9c1c5-a568-499a-a43d-74f3a81c1533.png">

- 반면에 내가 작성한 코드가 직접 제어의 흐름을 담당한다면 그것은 프레임워크가 아니라 라이브러리다.


#### 의존관계 주입 DI(Dependency Injection)
- OrderServiceImpl 은 DiscountPolicy 인터페이스에 의존한다. 실제 어떤 구현 객체가 사용될지는
모른다.
- 의존관계는 정적인 클래스 의존 관계와, 실행 시점에 결정되는 동적인 객체(인스턴스) 의존 관계 둘을 분리해서 생각해야 한다.


#### 정적인 클래스 의존관계
클래스가 사용하는 import 코드만 보고 의존관계를 쉽게 판단할 수 있다. 정적인 의존관계는 애플리케이션을 실행하지 않아도 분석할 수 있다. 클래스 다이어그램을 보자
OrderServiceImpl은 MemberRepository, DiscountPolicy에 의존한다는 것을 알 수 있다.
그런데 이러한 클래스 의존관계 만으로는 실제 어떤 객체가 OrderServiceImpl에 주입 될지 알 수 없다.
- 클래스 다이어그램
<img width="633" alt="스크린샷 2022-12-19 오후 1 16 47" src="https://user-images.githubusercontent.com/96857599/208346532-fe9f4a64-bd29-442f-8050-317affff4857.png">


#### 동적인 객체 인스턴스 의존 관계
애플리케이션 실행 시점에 실제 생성된 객체 인스턴스의 참조가 연결된 의존관계이다.

<img width="641" alt="스크린샷 2022-12-19 오후 1 20 51" src="https://user-images.githubusercontent.com/96857599/208346910-1119d0ef-ac9f-42a4-a890-8abebbd6ec77.png">

#### IoC 컨테이너, DI 컨테이너
- AppConfig 처럼 객체를 생성하고 관리하면서 의존관계를 연결해 주는 것을 IoC 컨테이너 또는 DI 컨테이너라 한다.
- 의존관계 주입에 초점을 맞추어 최근에는 주로 DI 컨테이너라 한다.
- 또는 어샘블러, 오브젝트 팩토리 등으로 불리기도 한다.

## 스프링으로의 전환

1. AppConfig에서 @Configuration을 붙임으로써 애플리케이션의 구성, 설정 정보를 나타내는 것을 알린다.
2. @Bean을 각각의 메소드에 붙이면 스프링 컨테이너에 등록됨.
<img width="1406" alt="스크린샷 2022-12-19 오후 1 35 01" src="https://user-images.githubusercontent.com/96857599/208348617-299723d9-b43d-4b83-b21a-fbb817f762f4.png">

3. MemberApp에서 spring 컨테이너를 통해 위에서 등록한 메소드를 찾아 실행한다.

<img width="1406" alt="스크린샷 2022-12-19 오후 1 34 40" src="https://user-images.githubusercontent.com/96857599/208348527-b5016600-3a4c-43e3-a52d-e59c01b1f3ca.png">

3-1. 등록된 내역을 확인할 수 있다.

<img width="1363" alt="스크린샷 2022-12-19 오후 1 36 26" src="https://user-images.githubusercontent.com/96857599/208348864-90814507-0c6b-432c-90b3-b3b41f8645e3.png">

4. OrderApp에서도 마찬가지다.
<img width="1373" alt="스크린샷 2022-12-19 오후 1 42 00" src="https://user-images.githubusercontent.com/96857599/208349437-7546c805-96dd-4f04-a166-12eaf8363b64.png">

#### 스프링 컨테이너
- ApplicationContext를 스프링 컨테이너라 한다.
- 기존에는 개발자가 AppConfig를 사용해서 직접 객체를 생성하고 DI를 했지만, 이제부터는 스프링 컨테이너를 통해서 사용한다.
- 스프링 컨테이너는 @Configuration이 붙은 AppConfig를 설정(구성) 정보로 사용한다. 여기서 @Bean 이라 적힌 메서드를 모두 호출해서 반환된 객체를 스프링 컨테이너에 등록한다. 이렇게 스프링 컨테이너에 등록된 객체를 **스프링 빈**이라 한다.
- 스프링 빈은 @Bean 이 붙은 메서드의 명을 스프링 빈의 이름으로 사용한다. ( memberService , orderService )
- 이전에는 개발자가 필요한 객체를 AppConfig를 사용해서 직접 조회했지만, 이제부터는 스프링 컨테이너를 통해서 필요한 스프링 빈(객체)를 찾아야 한다. 스프링 빈은 applicationContext.getBean() 메서드를 사용해서 찾을 수 있다.
- 기존에는 개발자가 직접 자바코드로 모든 것을 했다면 이제부터는 스프링 컨테이너에 객체를 스프링 빈으로 등록하고, 스프링 컨테이너에서 스프링 빈을 찾아서 사용하도록 변경되었다.

- 코드가 약간 더 복잡해진 것 같은데, 스프링 컨테이너를 사용하면 어떤 장점이 있을까?????

### 스프링 컨테이너와 스프링 빈

```java
//스프링 컨테이너 생성
ApplicationContext applicationContext =
                            new
    AnnotationConfigApplicationContext(AppConfig.class);
```
- ApplicationContext 를 스프링 컨테이너라 한다.
- ApplicationContext 는 인터페이스이다.
- 스프링 컨테이너는 XML을 기반으로 만들 수 있고, 애노테이션 기반의 자바 설정 클래스로 만들 수 있다.
- 직전에 AppConfig 를 사용했던 방식이 애노테이션 기반의 자바 설정 클래스로 스프링 컨테이너를 만든
것이다.
- 자바 설정 클래스를 기반으로 스프링 컨테이너( ApplicationContext )를 만들어보자.
	- new AnnotationConfigApplicationContext(AppConfig.class);
  	- 이 클래스는 ApplicationContext 인터페이스의 구현체이다.
  
  
> 참고: 더 정확히는 스프링 컨테이너를 부를 때 BeanFactory, ApplicationContext로 구분해서 이야기한다. 이 부분은 뒤에서 설명하겠다. BeanFactory를 직접 사용하는 경우는 거의 없으므로 일반적으로 ApplicationContext를 스프링 컨테이너라 한다.

#### 스프링 컨테이너 생성 과정

1. 스프링 컨테이너 생성
<img width="526" alt="스크린샷 2022-12-19 오후 10 21 40" src="https://user-images.githubusercontent.com/96857599/208435345-8d9eebb3-cacd-461e-b8f4-c2300dfbd82a.png">
- new AnnotationConfigApplicationContext(AppConfig.class)
- 스프링 컨테이너를 생성할 때는 구성 정보를 지정해주어야 한다.
- 여기서는 AppConfig.class 를 구성 정보로 지정했다.

2. 스프링 빈 등록
<img width="526" alt="스크린샷 2022-12-19 오후 10 22 24" src="https://user-images.githubusercontent.com/96857599/208435476-fddebc00-9e57-42e9-a008-36506cdc0a02.png">

- 스프링 컨테이너는 파라미터로 넘어온 설정 클래스 정보를 사용해서 스프링 빈을 등록한다.

**빈 이름**

- 빈 이름은 메서드 이름을 사용한다.
- 빈 이름을 직접 부여할 수 도 있다.
  - @Bean(name="memberService2")
  
> 주의: 빈 이름은 항상 다른 이름을 부여해야 한다. 같은 이름을 부여하면, 다른 빈이 무시되거나, 기존 빈을 덮어버리거나 설정에 따라 오류가 발생한다.

3. 스프링 빈 의존관계 설정 - 준비
<img width="528" alt="스크린샷 2022-12-19 오후 10 23 36" src="https://user-images.githubusercontent.com/96857599/208435676-b4995556-d910-40b3-b9f3-81d51a8e29aa.png">

4. 스프링 빈 의존관계 설정 - 완료
<img width="527" alt="스크린샷 2022-12-19 오후 10 23 49" src="https://user-images.githubusercontent.com/96857599/208435718-9b790dba-763a-46cd-9d84-61c3d10fffb3.png">

- 스프링 컨테이너는 설정 정보를 참고해서 의존관계를 주입(DI)한다.
- 단순히 자바 코드를 호출하는 것 같지만, 차이가 있다. 이 차이는 뒤에 싱글톤 컨테이너에서 설명한다.


**참고**
스프링은 빈을 생성하고, 의존관계를 주입하는 단계가 나누어져 있다. 그런데 이렇게 자바 코드로 스프링 빈을 등록하면 생성자를 호출하면서 의존관계 주입도 한번에 처리된다. 여기서는 이해를 돕기 위해 개념적으로 나누어 설명했다. 자세한 내용은 의존관계 자동 주입에서 다시 설명하겠다.


### 컨테이너에 등록된 모든 빈 조회

1. 스프링 컨테이너에 실제 스프링 빈들이 잘 등록되었는지 확인.

** TIP💡 리스트 형식의 객체가 있을 때, iter + tap을 누르면 for문이 자동 생성된다. **

- 전체 빈 확인
<img width="1235" alt="스크린샷 2022-12-19 오후 10 44 03" src="https://user-images.githubusercontent.com/96857599/208439404-b6ce1bf8-66ec-4187-8c5b-a217680a8665.png">

- 내가 입력한 스프링 빈만 보고싶을 때(혹은 스프링 내부에서 사용하는 빈을 보고싶을 때는 Role ROLE_INFRASTRUCTURE)

<img width="1235" alt="스크린샷 2022-12-19 오후 10 45 53" src="https://user-images.githubusercontent.com/96857599/208439740-64e636a2-5b2d-4c40-b0a4-c99e64a4feae.png">

- ac.getBeanDefinitionNames() : 스프링에 등록된 모든 빈 이름을 조회한다.
- ac.getBean() : 빈 이름으로 빈 객체(인스턴스)를 조회한다.

### 스프링 빈 조회 - 기본

#### 스프링 컨테이너에서 스프링 빈을 찾는 가장 기본적인 조회 방법
- ac.getBean(빈이름, 타입) ac.getBean(타입)
       
#### 조회 대상 스프링 빈이 없으면 예외 발생
- NoSuchBeanDefinitionException: No bean named 'xxxxx' available

<img width="1412" alt="스크린샷 2022-12-24 오전 12 51 31" src="https://user-images.githubusercontent.com/96857599/209363191-8c196df3-a364-469e-8ae8-0f24d798eb84.png">


> 참고: 구체 타입으로 조회하면 변경시 유연성이 떨어진다.

### 스프링 빈 조회 - 동일한 타입이 둘 이상
- 타입으로 조회시 같은 타입의 스프링 빈이 둘 이상이면 오류가 발생한다. 이때는 빈 이름을 지정하자.
- ac.getBeansOfType()을 사용하면 해당 타입의 모든 빈을 조회할 수 있다.


- org.springframework.beans.factory.NoUniqueBeanDefinitionException 오류 발생

<img width="1375" alt="스크린샷 2022-12-24 오전 12 57 48" src="https://user-images.githubusercontent.com/96857599/209363926-80ded56a-5f93-425f-85be-75133d10da5f.png">

<img width="1167" alt="스크린샷 2022-12-24 오전 1 08 09" src="https://user-images.githubusercontent.com/96857599/209365201-99b88d64-22dd-4ed7-a2a5-c179a328b3a3.png">

### 스프링 빈 - 상속 관계

- 부모 타입으로 조회하면, 자식 타입도 함께 조회한다.
- 그래서 모든 자바 객체의 최고 부모인 Object 타입으로 조회하면, 모든 스프링 빈을 조회한다.


<img width="692" alt="스크린샷 2022-12-25 오전 10 53 36" src="https://user-images.githubusercontent.com/96857599/209454880-4b2f7234-1ec3-4212-b256-a5394b51ee9b.png">


- 부모 타입으로 조회할 경우, 자식(rateDiscountPolicy, fixDiscountPolicy)이 함께 조회되므로 중복 오류(NoUniqueBeanDefinitionException)가 발생한다.

<img width="941" alt="스크린샷 2022-12-25 오전 11 02 20" src="https://user-images.githubusercontent.com/96857599/209455004-4d792f22-8f60-4061-82f9-868537c35a4f.png">

- 해결방법은 빈 이름을 지정하면된다.

<img width="1105" alt="스크린샷 2022-12-25 오전 11 11 38" src="https://user-images.githubusercontent.com/96857599/209455085-25f23449-35fc-44c4-bab7-d94d198d83dd.png">

- 특정 하위 타입으로 조회할 수도 있지만, DIP에 위반된다.
<img width="1105" alt="스크린샷 2022-12-25 오전 11 12 26" src="https://user-images.githubusercontent.com/96857599/209455090-8d7bc94a-3468-4831-8cf0-661a96b3408d.png">

- 부모 타입으로 모두 조회하기, 연습이기 때문에 출력하여 확인한 것이다.

<img width="1129" alt="스크린샷 2022-12-25 오전 11 19 51" src="https://user-images.githubusercontent.com/96857599/209455157-785b1fd0-9dfe-4070-bef3-33f6f97aa183.png">


- 부모 타입으로 모두 조회하기 - Object

<img width="1129" alt="스크린샷 2022-12-25 오전 11 23 31" src="https://user-images.githubusercontent.com/96857599/209455215-33fb5207-49f0-4e21-8af6-adf1ab558359.png">

### BeanFactory와 ApplicationContext

<img width="523" alt="스크린샷 2022-12-25 오전 11 26 53" src="https://user-images.githubusercontent.com/96857599/209455261-65382573-d3d6-4d74-8458-7d967ea8b79d.png">

#### BeanFactory
- 스프링 컨테이너의 최상위 인터페이스다.
- 스프링 빈을 관리하고 조회하는 역할을 담당한다.
- getBean()을 제공한다.
- 지금까지 우리가 사용했던 대부분의 기능은 BeanFactory가 제공하는 기능이다.

#### ApplicationContext
- BeanFactory 기능을 모두 상속받아서 제공한다.
- 빈을 관리하고 검색하는 기능을 BeanFactory가 제공해주는데, 그러면 둘의 차이가 뭘까?
- 애플리케이션을 개발할 때는 빈을 관리하고 조회하는 기능은 물론이고, 수 많은 부가기능이 필요하다.

** TIP💡 cmd + O를 누르면 외부 라이브러리까지 볼 수 있음.

<img width="1129" alt="스크린샷 2022-12-25 오전 11 30 41" src="https://user-images.githubusercontent.com/96857599/209455325-2d4a27f5-c14a-4289-b3f6-6bf3c08bed89.png">
cmd + B
<img width="1129" alt="스크린샷 2022-12-25 오전 11 32 19" src="https://user-images.githubusercontent.com/96857599/209455356-43e4ec6c-ed7d-4385-be59-7c239945a935.png">

<img width="691" alt="스크린샷 2022-12-25 오전 11 33 48" src="https://user-images.githubusercontent.com/96857599/209455375-582f3e11-740f-487f-947f-9f78c7650dcc.png">


#### 정리
- ApplicationContext는 BeanFactory의 기능을 상속받는다.
- ApplicationContext는 빈 관리기능 + 편리한 부가 기능을 제공한다.
- BeanFactory를 직접 사용할 일은 거의 없다. 부가기능이 포함된 ApplicationContext를 사용한다. 
- BeanFactory나 ApplicationContext를 스프링 컨테이너라 한다.

### 다양한 설정 형식 지원 - 자바 코드, XML

- 스프링 컨테이너는 다양한 형식의 설정 정보를 받아드릴 수 있게 유연하게 설계되어 있다.
 	- 자바 코드, XML, Groovy 등등 (요즘엔 자바 코드를 주로 많이 씀)

<img width="524" alt="스크린샷 2022-12-25 오전 11 37 54" src="https://user-images.githubusercontent.com/96857599/209455417-5c290586-d51e-418a-aced-545f9b176968.png">

#### 애노테이션 기반 자바 코드 설정 사용
- 지금까지 했던 것이다.
- new AnnotationConfigApplicationContext(AppConfig.class) 
- AnnotationConfigApplicationContext 클래스를 사용하면서 자바 코드로된 설정 정보를 넘기면 된다.


#### XML 설정 사용
- 최근에는 스프링 부트를 많이 사용하면서 XML기반의 설정은 잘 사용하지 않는다. 아직 많은 레거시
프로젝트 들이 XML로 되어 있고, 또 XML을 사용하면 컴파일 없이 빈 설정 정보를 변경할 수 있는 장점도 있으므로 한번쯤 배워두는 것도 괜찮다.
- GenericXmlApplicationContext를 사용하면서 xml 설정 파일을 넘기면 된다.

<img width="1358" alt="스크린샷 2022-12-25 오전 11 52 45" src="https://user-images.githubusercontent.com/96857599/209455625-785a05c5-bca2-41bd-ab57-9fafde39fef1.png">

<img width="1358" alt="스크린샷 2022-12-25 오전 11 53 10" src="https://user-images.githubusercontent.com/96857599/209455629-ea009a06-fb61-4dcc-b395-a6e61cbeb8ac.png">

- xml 기반의 appConfig.xml 스프링 설정 정보와 자바 코드로 된 AppConfig.java 설정 정보를 비교해보면 거의 비슷하다는 것을 알 수 있다.
- xml 기반으로 설정하는 것은 최근에 잘 사용하지 않으므로 이정도로 마무리 하고, 필요하면 스프링 공식 레퍼런스 문서를 확인하자.

 
 
 ### 스프링 빈 설정 메타 정보 - BeanDefinition
 
- 스프링은 어떻게 이런 다양한 설정 형식을 지원하는 것일까? 그 중심에는 BeanDefinition 이라는 추상화가 있다.
- 쉽게 이야기해서 역할과 구현을 개념적으로 나눈 것이다!
	- XML을 읽어서 BeanDefinition을 만들면 된다.
	- 자바 코드를 읽어서 BeanDefinition을 만들면 된다.
	- 스프링 컨테이너는 자바 코드인지, XML인지 몰라도 된다. 오직 BeanDefinition만 알면 된다.
- BeanDefinition을 빈 설정 메타정보라 한다.
 	- @Bean , <bean> 당 각각 하나씩 메타 정보가 생성된다.
- 스프링 컨테이너는 이 메타정보를 기반으로 스프링 빈을 생성한다.
 
 <img width="689" alt="스크린샷 2022-12-26 오후 4 49 13" src="https://user-images.githubusercontent.com/96857599/209520552-311c7e3f-091f-4be8-b9df-8c37cc69abee.png">

-  AnnotationConfigApplicationContext는 AnnotatedBeanDefinitionReader를 사용해서 AppConfig.class 를 읽고 BeanDefinition 을 생성한다.
- GenericXmlApplicationContext는 XmlBeanDefinitionReader를 사용해서 appConfig.xml 설정 정보를 읽고 BeanDefinition 을 생성한다.
- 새로운 형식의 설정 정보가 추가되면, XxxBeanDefinitionReader를 만들어서 BeanDefinition 을 생성하면 된다.

#### BeanDefinition 살펴보기
- BeanDefinition 정보
- BeanClassName: 생성할 빈의 클래스 명(자바 설정 처럼 팩토리 역할의 빈을 사용하면 없음) 
- factoryBeanName: 팩토리 역할의 빈을 사용할 경우 이름, 예) appConfig
- factoryMethodName: 빈을 생성할 팩토리 메서드 지정, 예) memberService
- Scope: 싱글톤(기본값)
- lazyInit: 스프링 컨테이너를 생성할 때 빈을 생성하는 것이 아니라, 실제 빈을 사용할 때 까지 최대한 생성을 지연처리 하는지 여부
- InitMethodName: 빈을 생성하고, 의존관계를 적용한 뒤에 호출되는 초기화 메서드 명
- DestroyMethodName: 빈의 생명주기가 끝나서 제거하기 직전에 호출되는 메서드 명
- Constructor arguments, Properties: 의존관계 주입에서 사용한다. (자바 설정 처럼 팩토리 역할의
빈을 사용하면 없음)
 
 <img width="1355" alt="스크린샷 2022-12-26 오후 5 01 28" src="https://user-images.githubusercontent.com/96857599/209521970-f8e9f518-3abd-4f43-a765-590d50dba4d0.png">

 
#### 정리
- BeanDefinition을 직접 생성해서 스프링 컨테이너에 등록할 수 도 있다. 하지만 실무에서 BeanDefinition을 직접 정의하거나 사용할 일은 거의 없다.
- BeanDefinition에 대해서는 너무 깊이있게 이해하기 보다는, 스프링이 다양한 형태의 설정 정보를 BeanDefinition으로 추상화해서 사용하는 것 정도만 이해하면 된다.
- 가끔 스프링 코드나 스프링 관련 오픈 소스의 코드를 볼 때, BeanDefinition 이라는 것이 보일 때가 있다. 이때 이러한 메커니즘을 떠올리면 된다.


### 싱글톤 컨테이너 - 웹 애플리케이션과 싱글톤

- 웹 애플리케이션은 고객의 끊임 없는 요청이 발생한다.
<img width="689" alt="스크린샷 2022-12-30 오후 1 09 30" src="https://user-images.githubusercontent.com/96857599/210033606-ecce1bc6-d81b-41dd-b5d6-72b552d74dc2.png">

- 요청할 때마다 다른 객체가 생성됨.
<img width="1001" alt="스크린샷 2022-12-30 오후 1 15 28" src="https://user-images.githubusercontent.com/96857599/210033904-98a378ff-d0fe-4da7-b2df-ff7fc2634982.png">
<img width="1001" alt="스크린샷 2022-12-30 오후 1 18 19" src="https://user-images.githubusercontent.com/96857599/210034051-fb30c304-0fe9-4ec2-a3e5-f47c552af536.png">

- 우리가 만들었던 스프링 없는 순수한 DI 컨테이너인 AppConfig는 요청을 할 때 마다 객체를 새로 생성한다.
- 고객 트래픽이 초당 100이 나오면 초당 100개 객체가 생성되고 소멸된다! -> 메모리 낭비가 심하다.
- 해결방안은 해당 객체가 딱 1개만 생성되고, 공유하도록 설계하면 된다. -> 싱글톤 패턴


### 싱글톤 패턴
- 클래스의 인스턴스가 딱 1개만 생성되는 것을 보장하는 디자인 패턴이다.
- 그래서 객체 인스턴스를 2개 이상 생성하지 못하도록 막아야 한다.
- private 생성자를 사용해서 외부에서 임의로 new 키워드를 사용하지 못하도록 막아야 한다.
<img width="1426" alt="스크린샷 2022-12-30 오후 1 33 35" src="https://user-images.githubusercontent.com/96857599/210034791-c1104bc2-7d1c-4dc8-99fb-9f68cedb778b.png">


- new로 인한 객체 인스턴스 생성 막음
<img width="1115" alt="스크린샷 2022-12-30 오후 1 39 01" src="https://user-images.githubusercontent.com/96857599/210035071-d9c5e837-3329-4665-b707-b5fd5b69cec5.png">

- 같은 인스턴스를 사용하는 것을 알 수 있음
<img width="1006" alt="스크린샷 2022-12-30 오후 1 43 34" src="https://user-images.githubusercontent.com/96857599/210035308-04f59f68-1c17-4efd-a2f7-e0e2bfd24ac7.png">

> 참고: 싱글톤 패턴을 구현하는 방법은 여러가지가 있다. 여기서는 객체를 미리 생성해두는 가장 단순하고 안전한 방법을 선택했다.

#### 싱글톤 패턴 문제점
- 싱글톤 패턴을 구현하는 코드 자체가 많이 들어간다.
- 의존관계상 클라이언트가 구체 클래스에 의존한다. -> DIP를 위반한다.
- 클라이언트가 구체 클래스에 의존해서 OCP 원칙을 위반할 가능성이 높다.
- 테스트하기 어렵다.
- 내부 속성을 변경하거나 초기화 하기 어렵다.
- private 생성자로 자식 클래스를 만들기 어렵다.
- 결론적으로 유연성이 떨어진다.
- 안티패턴으로 불리기도 한다.


### 싱글톤 컨테이너

- 스프링 컨테이너는 싱글턴 패턴을 적용하지 않아도, 객체 인스턴스를 싱글톤으로 관리한다.
 	- 컨테이너는 객체를 하나만 생성해서 관리한다.
- 스프링 컨테이너는 싱글톤 컨테이너 역할을 한다. 이렇게 싱글톤 객체를 생성하고 관리하는 기능을 싱글톤 레지스트리라 한다.
- 스프링 컨테이너의 이런 기능 덕분에 싱글턴 패턴의 모든 단점을 해결하면서 객체를 싱글톤으로 유지할 수 있다.
	- 싱글톤 패턴을 위한 지저분한 코드가 들어가지 않아도 된다.
	- DIP, OCP, 테스트, private 생성자로 부터 자유롭게 싱글톤을 사용할 수 있다.
 
- 스프링 컨테이너를 사용하는 테스트 코드
<img width="1145" alt="스크린샷 2022-12-30 오후 2 23 05" src="https://user-images.githubusercontent.com/96857599/210037442-c7e6f63c-8385-4376-b76f-cfca9e3d5447.png">

<img width="690" alt="스크린샷 2022-12-30 오후 2 24 11" src="https://user-images.githubusercontent.com/96857599/210037491-725d9f33-de6f-4740-b158-31084fd9ea70.png">

## 싱글톤 방식의 주의점!!

- 싱글톤 패턴이든, 스프링 같은 싱글톤 컨테이너를 사용하든, 객체 인스턴스를 하나만 생성해서 공유하는 싱글톤 방식은 여러 클라이언트가 하나의 같은 객체 인스턴스를 공유하기 때문에 싱글톤 객체는 상태를 유지(stateful)하게 설계하면 안된다.
- 무상태(stateless)로 설계해야 한다!
	- 특정 클라이언트에 의존적인 필드가 있으면 안된다.
	- 특정 클라이언트가 값을 변경할 수 있는 필드가 있으면 안된다!
	- 가급적 읽기만 가능해야 한다.
 	- 필드 대신에 자바에서 공유되지 않는, 지역변수, 파라미터, ThreadLocal 등을 사용해야 한다.
	- 스프링 빈의 필드에 공유 값을 설정하면 정말 큰 장애가 발생할 수 있다!!!

<img width="1018" alt="스크린샷 2022-12-30 오후 2 45 33" src="https://user-images.githubusercontent.com/96857599/210038704-0071bb95-5605-4206-8734-c29a45e8e9f4.png">

<img width="1443" alt="스크린샷 2022-12-30 오후 2 46 02" src="https://user-images.githubusercontent.com/96857599/210038729-4e5fc526-0514-4d3a-bde2-8443b14d7306.png">

- 최대한 단순히 설명하기 위해, 실제 쓰레드는 사용하지 않았다.
- ThreadA가 사용자A 코드를 호출하고 ThreadB가 사용자B 코드를 호출한다 가정하자.
- StatefulService의 price 필드는 공유되는 필드인데, 특정 클라이언트가 값을 변경한다.
- 사용자A의 주문금액은 10000원이 되어야 하는데, 20000원이라는 결과가 나왔다.
- 실무에서 이런 경우를 종종 보는데, 이로인해 정말 해결하기 어려운 큰 문제들이 터진다.
- 진짜 공유필드는 조심해야 한다! 스프링 빈은 항상 무상태(stateless)로 설계하자.

해결코드
<img width="1443" alt="스크린샷 2022-12-30 오후 2 50 15" src="https://user-images.githubusercontent.com/96857599/210038919-f6eab37f-f15e-4dee-adb8-c231eda753d8.png">
<img width="1443" alt="스크린샷 2022-12-30 오후 2 50 50" src="https://user-images.githubusercontent.com/96857599/210038950-4242e097-a616-4d6c-a025-caf9dec63d45.png">

### @Configuration과 싱글톤

- @Configuration은 싱글톤을 위해 존재하는 것이다.

<img width="1180" alt="스크린샷 2022-12-30 오후 3 11 04" src="https://user-images.githubusercontent.com/96857599/210040062-c9da2750-5fbb-4b8d-931f-95896dd9da7d.png">
- AppConfig에서 memberService 빈을 만드는 코드를 보면 memberRepository()를 호출한다.
	- 이 메서드를 호출하면 new MemoryMemberRepository()를 호출한다.
- orderService 빈을 만드는 코드도 동일하게 memberRepository()를 호출한다. 
- 이 메서드를 호출하면 new MemoryMemberRepository()를 호출한다.

- 결과적으로 각각 다른 2개의 MemoryMemberRepository가 생성되면서 싱글톤이 깨지는 것 처럼 보인다. 스프링 컨테이너는 이 문제를 어떻게 해결할까?

- 테스트 해보자.

<img width="970" alt="스크린샷 2022-12-30 오후 3 16 26" src="https://user-images.githubusercontent.com/96857599/210040436-385c6046-2534-4980-bdb0-28b76ff6ab5d.png">
<img width="970" alt="스크린샷 2022-12-30 오후 3 16 35" src="https://user-images.githubusercontent.com/96857599/210040443-f3eb92ce-fd5c-449e-9d15-8414932f2437.png">

<img width="1375" alt="스크린샷 2022-12-30 오후 3 43 23" src="https://user-images.githubusercontent.com/96857599/210042196-85e4e015-3e93-47d7-a326-3263dd066755.png">

- 확인해보면 memberRepository 인스턴스는 모두 같은 인스턴스가 공유되어 사용된다.
- AppConfig의 자바 코드를 보면 분명히 각각 2번 new MemoryMemberRepository를 호출해서 다른 인스턴스가 생성되어야 하는데?
- 어떻게 된 일일까? 혹시 두 번 호출이 안되는 것일까? 실험을 통해 알아보자.

#### AppConfig 호출로그 남기기
<img width="932" alt="스크린샷 2022-12-30 오후 3 48 23" src="https://user-images.githubusercontent.com/96857599/210042589-f3f3d8ed-35be-4896-ae8b-f114a3166b1e.png">
- memberRepository가 3번 출력될 것이라는 예상과 다르게 1번만 출력되었다. 다음 강의에서 설명

### @Configuration과 바이트코드 조작의 마법

스프링 컨테이너는 싱글톤 레지스트리다. 따라서 스프링 빈이 싱글톤이 되도록 보장해주어야 한다. 그런데 스프링이 자바 코드까지 어떻게 하기는 어렵다. 저 자바 코드를 보면 분명 3번 호출되어야 하는 것이 맞다. 그래서 스프링은 클래스의 바이트코드를 조작하는 라이브러리를 사용한다.

<img width="1116" alt="스크린샷 2022-12-30 오후 3 55 22" src="https://user-images.githubusercontent.com/96857599/210043031-1285ca72-c971-4fb2-a6cc-ee7ee7a7b5df.png">

순수한 클래스라면 다음과 같이 출력되어야 한다. 
class hello.core.AppConfig

그런데 예상과는 다르게 클래스 명에 xxxCGLIB가 붙으면서 상당히 복잡해진 것을 볼 수 있다. 이것은 내가 만든 클래스가 아니라 스프링이 CGLIB라는 바이트코드 조작 라이브러리를 사용해서 AppConfig 클래스를 상속받은 임의의 다른 클래스를 만들고, 그 다른 클래스를 스프링 빈으로 등록한 것이다!

<img width="690" alt="스크린샷 2022-12-30 오후 3 57 35" src="https://user-images.githubusercontent.com/96857599/210043181-7dc360b5-72aa-4db0-b0d6-031a31154680.png">

```java
@Bean
public MemberRepository memberRepository() {
    if (memoryMemberRepository가 이미 스프링 컨테이너에 등록되어 있으면?) { 
        return 스프링 컨테이너에서 찾아서 반환;
    } else { //스프링 컨테이너에 없으면
        기존 로직을 호출해서 MemoryMemberRepository를 생성하고 스프링 컨테이너에 등록
        return 반환
    }
}
```

- @Bean이 붙은 메서드마다 이미 스프링 빈이 존재하면 존재하는 빈을 반환하고, 스프링 빈이 없으면 생성해서 스프링 빈으로 등록하고 반환하는 코드가 동적으로 만들어진다.
- 덕분에 싱글톤이 보장되는 것이다.

> 참고 AppConfig@CGLIB는 AppConfig의 자식 타입이므로, AppConfig 타입으로 조회 할 수 있다.

#### 정리
- @Bean만 사용해도 스프링 빈으로 등록되지만, 싱글톤을 보장하지 않는다.
- memberRepository()처럼 의존관계 주입이 필요해서 메서드를 직접 호출할 때 싱글톤을 보장하지
않는다.
- 크게 고민할 것이 없다. 스프링 설정 정보는 항상 @Configuration을 사용하자.

### 컴포넌트 스캔과 의존관계 자동 주입 시작하기

- 스프링은 설정 정보가 없어도 자동으로 스프링 빈을 등록하는 컴포넌트 스캔이라는 기능을 제공한다.

<img width="1038" alt="스크린샷 2022-12-31 오후 5 01 41" src="https://user-images.githubusercontent.com/96857599/210129932-9e741a81-8156-4b8e-910a-d3c4b48c51cc.png">
- 컴포넌트 스캔을 사용하려면 먼저 @ComponentScan을 설정 정보에 붙여주면 된다.
- 기존의 AppConfig와는 다르게 @Bean으로 등록한 클래스가 하나도 없다!

> 참고: 컴포넌트 스캔을 사용하면 @Configuration이 붙은 설정 정보도 자동으로 등록되기 때문에, AppConfig, TestConfig 등 앞서 만들어두었던 설정 정보도 함께 등록되고, 실행되어 버린다. 그래서 excludeFilters 를 이용해서 설정정보는 컴포넌트 스캔 대상에서 제외했다. 보통 설정 정보를 컴포넌트 스캔 대상에서 제외하지는 않지만, 기존 예제 코드를 최대한 남기고 유지하기 위해서 이 방법을 선택했다.

컴포넌트 스캔은 이름 그대로 @Component 애노테이션이 붙은 클래스를 스캔해서 스프링 빈으로 등록한다. @Component를 붙인다.

<img width="1038" alt="스크린샷 2022-12-31 오후 5 05 38" src="https://user-images.githubusercontent.com/96857599/210130012-17ea19dc-2692-4d66-9def-398b7c8b810d.png">

<img width="1038" alt="스크린샷 2022-12-31 오후 5 06 09" src="https://user-images.githubusercontent.com/96857599/210130025-e8b670e7-c859-47a9-81a5-b836f0f2deea.png">

<img width="1038" alt="스크린샷 2022-12-31 오후 5 06 46" src="https://user-images.githubusercontent.com/96857599/210130041-1e8662c0-d956-4da6-b087-d0420d0991a5.png">

- 의존관계를 주입하기 위한 방법 -> @Autowired를 붙이면 자동으로 의존관계를 주입해준다.

<img width="1154" alt="스크린샷 2022-12-31 오후 5 11 22" src="https://user-images.githubusercontent.com/96857599/210130105-49bf6621-1e0a-447a-b52b-171b046658b4.png">
<img width="1049" alt="스크린샷 2022-12-31 오후 5 13 00" src="https://user-images.githubusercontent.com/96857599/210130141-bd411476-796b-4a14-bbed-1ad8da0907ef.png">
<img width="1201" alt="스크린샷 2022-12-31 오후 5 34 54" src="https://user-images.githubusercontent.com/96857599/210130617-b135bcd6-30e6-41eb-89f1-b661ccaeaba3.png">

- @Autowired 를 사용하면 생성자에서 여러 의존관계도 한번에 주입받을 수 있다.

<img width="1420" alt="스크린샷 2022-12-31 오후 5 26 29" src="https://user-images.githubusercontent.com/96857599/210130448-d2df5414-4f1a-4769-90a1-d2cecdc22ccd.png">

- 로그를 잘 보면 컴포넌트 스캔이 잘 동작하는 것을 확인할 수 있다.
<img width="1507" alt="스크린샷 2022-12-31 오후 5 27 36" src="https://user-images.githubusercontent.com/96857599/210130472-7ca3b01e-8f20-4318-a47e-16a2a57ac26f.png">

<img width="842" alt="스크린샷 2022-12-31 오후 5 29 22" src="https://user-images.githubusercontent.com/96857599/210130522-d0740f0e-facd-420a-a501-ddc9a1996391.png">

- @ComponentScan 은 @Component 가 붙은 모든 클래스를 스프링 빈으로 등록한다.
- 이때 스프링 빈의 기본 이름은 클래스명을 사용하되 맨 앞글자만 소문자를 사용한다.
	- 빈 이름 기본 전략: MemberServiceImpl클래스 -> memberServiceImpl
	- 빈 이름 직접 지정: 만약 스프링 빈의 이름을 직접 지정하고 싶으면 @Component("memberService2") 이런식으로 이름을 부여하면 된다.
 
<img width="843" alt="스크린샷 2022-12-31 오후 5 31 04" src="https://user-images.githubusercontent.com/96857599/210130543-9783baf9-2286-4bbd-bbc8-767838a28143.png">

- 생성자에 @Autowired 를 지정하면, 스프링 컨테이너가 자동으로 해당 스프링 빈을 찾아서 주입한다.
- 이때 기본 조회 전략은 타입이 같은 빈을 찾아서 주입한다.
	- getBean(MemberRepository.class) 와 동일하다고 이해하면 된다. (더 자세한 내용은 뒤에서 설명한다.)
 
#### 정리
- @Component가 붙은 클래스 들이 스프링 컨테이너에 저장된다.
- @Autowired를 통해 의존성을 주입해준다.

### 탐색 위치와 스캔 대상

<img width="1248" alt="스크린샷 2022-12-31 오후 8 34 18" src="https://user-images.githubusercontent.com/96857599/210135194-692d8533-a28e-431a-ab8c-62dbac651183.png">

- basePackages : 탐색할 패키지의 시작 위치를 지정한다. 이 패키지를 포함해서 하위 패키지를 모두 탐색한다.
	- basePackages = {"hello.core", "hello.service"} 이렇게 여러 시작 위치를 지정할 수도 있다.
- basePackageClasses : 지정한 클래스의 패키지를 탐색 시작 위치로 지정한다.
- 만약 지정하지 않으면 @ComponentScan이 붙은 설정 정보 클래스의 패키지가 시작 위치가 된다.

#### 권장하는 방법
개인적으로 즐겨 사용하는 방법은 패키지 위치를 지정하지 않고, 설정 정보 클래스의 위치를 프로젝트 최상단에 두는 것이다. 최근 스프링 부트도 이 방법을 기본으로 제공한다.

예를 들어서 프로젝트가 다음과 같이 구조가 되어 있으면
- com.hello
- com.hello.serivce
- com.hello.repository
- com.hello 프로젝트 시작 루트, 여기에 AppConfig 같은 메인 설정 정보를 두고, @ComponentScan 애노테이션을 붙이고, basePackages 지정은 생략한다.

이렇게 하면 com.hello 를 포함한 하위는 모두 자동으로 컴포넌트 스캔의 대상이 된다. 그리고 프로젝트 메인 설정 정보는 프로젝트를 대표하는 정보이기 때문에 프로젝트 시작 루트 위치에 두는 것이 좋다 생각한다.

> 참고로 스프링 부트를 사용하면 스프링 부트의 대표 시작 정보인 @SpringBootApplication를 이 프로젝트 시작 루트 위치에 두는 것이 관례이다. (그리고 이 설정안에 바로 @ComponentScan이 들어있다.)

#### 컴포넌트 스캔 기본 대상
컴포넌트 스캔은 @Component 뿐만 아니라 다음과 내용도 추가로 대상에 포함한다. (모두 @Component를 포함한다.)
- @Component : 컴포넌트 스캔에서 사용
- @Controlller : 스프링 MVC 컨트롤러에서 사용
- @Service : 스프링 비즈니스 로직에서 사용
- @Repository : 스프링 데이터 접근 계층에서 사용
- @Configuration : 스프링 설정 정보에서 사용

> 참고: 사실 어노테이션에는 상속관계라는 것이 없다. 그래서 이렇게 어노테이션이 특정 어노테이션을 들고 있는 것을 인식할 수 있는 것은 자바 언어가 지원하는 기능은 아니고, 스프링이 지원하는 기능이다.

컴포넌트 스캔의 용도 뿐만 아니라 다음 애노테이션이 있으면 스프링은 부가 기능을 수행한다.
- @Controller : 스프링 MVC 컨트롤러로 인식
- @Repository : 스프링 데이터 접근 계층으로 인식하고, 데이터 계층의 예외를 스프링 예외로 변환해준다. (데이터 베이스에 따른 예외를 서비스 계층까지 가지 않도록 한다.)
- @Configuration : 앞서 보았듯이 스프링 설정 정보로 인식하고, 스프링 빈이 싱글톤을 유지하도록 추가
처리를 한다.
- @Service : 사실 @Service는 특별한 처리를 하지 않는다. 대신 개발자들이 핵심 비즈니스 로직이 여기에
있겠구나 라고 비즈니스 계층을 인식하는데 도움이 된다.

> 참고: useDefaultFilters 옵션은 기본으로 켜져있는데, 이 옵션을 끄면 기본 스캔 대상들이 제외된다.

### 필터

- includeFilters : 컴포넌트 스캔 대상을 추가로 지정한다. 
- excludeFilters : 컴포넌트 스캔에서 제외할 대상을 지정한다.

- MyIncludeComponent와 MyExcludeComponent 어노테이션을 생성한다.

<img width="1214" alt="스크린샷 2022-12-31 오후 9 05 21" src="https://user-images.githubusercontent.com/96857599/210136140-04c59334-6c6c-4066-acc9-39b7766c9608.png">

<img width="1214" alt="스크린샷 2022-12-31 오후 9 05 34" src="https://user-images.githubusercontent.com/96857599/210136142-432669a6-b048-4a85-b184-28308a268b3c.png">
- MyIncludeComponent 어노테이션을 갖는 BeanA를 생성한다.
<img width="1214" alt="스크린샷 2022-12-31 오후 9 06 29" src="https://user-images.githubusercontent.com/96857599/210136159-f4f6da67-55a0-4801-8b9f-100dc9ffe5fc.png">
- MyExcludeComponent 어노테이션을 갖는 BeanB를 생성한다.
<img width="1214" alt="스크린샷 2022-12-31 오후 9 07 55" src="https://user-images.githubusercontent.com/96857599/210136193-e8978c09-98d3-434f-8396-3d752684ce8a.png">
- includeFilters에 MyIncludeComponent 어노테이션을 추가해서 BeanA가 스프링 빈에 등록된다. excludeFilters에 MyExcludeComponent 어노테이션을 추가해서 BeanB는 스프링 빈에 등록되지 않는다.

<img width="1483" alt="스크린샷 2022-12-31 오후 9 08 27" src="https://user-images.githubusercontent.com/96857599/210136209-ea077854-f307-42cc-a661-ab1b10b73527.png">

#### FilterType 옵션
FilterType은 5가지 옵션이 있다.
- ANNOTATION: 기본값, 애노테이션을 인식해서 동작한다. ex) org.example.SomeAnnotation
- ASSIGNABLE_TYPE: 지정한 타입과 자식 타입을 인식해서 동작한다. ex) org.example.SomeClass
- ASPECTJ: AspectJ 패턴 사용 ex) org.example..*Service+
- REGEX: 정규 표현식 ex) org\.example\.Default.*
- CUSTOM: TypeFilter 이라는 인터페이스를 구현해서 처리 ex) org.example.MyTypeFilter

> 참고: @Component 면 충분하기 때문에, includeFilters를 사용할 일은 거의 없다. excludeFilters는 여러가지 이유로 간혹 사용할 때가 있지만 많지는 않다. 특히 최근 스프링 부트는 컴포넌트 스캔을 기본으로 제공하는데, 개인적으로는 옵션을 변경하면서 사용하기 보다는 스프링의 기본 설정에 최대한 맞추어 사용하는 것을 권장하고, 선호하는 편이다.

### 중복 등록과 충돌

1. 자동빈등록vs자동빈등록

컴포넌트 스캔에 의해 자동으로 스프링 빈이 등록되는데, 그 이름이 같은 경우 스프링은 오류를 발생시킨다.
 - ConflictingBeanDefinitionException 예외 발생

2. 수동빈등록vs자동빈등록
- AutoAppConfig에 memoryMemberRepository라는 이름으로 bean 등록을 해준다.
<img width="1239" alt="스크린샷 2022-12-31 오후 9 42 44" src="https://user-images.githubusercontent.com/96857599/210137098-357fd803-fd40-4863-b930-fc0462cf6302.png">

<img width="1239" alt="스크린샷 2022-12-31 오후 9 43 49" src="https://user-images.githubusercontent.com/96857599/210137132-c107e28d-6fa9-43ef-8dfd-1053be27abf2.png">

- 둘의 이름이 같아서 오류가 생겨야하지만 생기지 않았다.
<img width="1239" alt="스크린샷 2022-12-31 오후 9 44 33" src="https://user-images.githubusercontent.com/96857599/210137153-754c00f3-439d-4e6b-9a5b-6c6b0080e73c.png">

- 이유는 이런 경우에 수동 빈 등록이 우서권을 가진다. (수동 빈이 자동 빈을 오버라이딩 해버린다.)
- 해당 로그를 통해 알 수 있다.

<img width="1052" alt="스크린샷 2022-12-31 오후 9 46 58" src="https://user-images.githubusercontent.com/96857599/210137210-a13e28b9-cff0-46b6-bc62-614919e3d17b.png">

> 물론 개발자가 의도적으로 이런 결과를 기대했다면, 자동 보다는 수동이 우선권을 가지는 것이 좋다. 하지만 현실은 개발자가 의도적으로 설정해서 이런 결과가 만들어지기 보다는 여러 설정들이 꼬여서 이런 결과가 만들어지는 경우가 대부분이다! 그러면 정말 잡기 어려운 버그가 만들어진다. 항상 잡기 어려운 버그는 애매한 버그다.
> 그래서 최근 스프링 부트에서는 수동 빈 등록과 자동 빈 등록이 충돌나면 오류가 발생하도록 기본 값을 바꾸었다.

- 스프링부트 실행시
<img width="1469" alt="스크린샷 2022-12-31 오후 9 49 40" src="https://user-images.githubusercontent.com/96857599/210137281-b5c3aeb7-66f8-4f16-9b9a-ce1174a34076.png">

```
Description:

The bean 'memoryMemberRepository', defined in class path resource [hello/springStudyBasic/AutoAppConfig.class], could not be registered. A bean with that name has already been defined in file [/Users/gangho/Desktop/springStudyBasic/out/production/classes/hello/springStudyBasic/member/MemoryMemberRepository.class] and overriding is disabled.

Action:

Consider renaming one of the beans or enabling overriding by setting spring.main.allow-bean-definition-overriding=true
```
> 코드를 더 써야할지라도, 명확하고 확실하게 작성하는게 좋다. -> 그렇지 않으면 더 큰 버그가 발생한다!


### 다양한 의존관계 주입 방법

#### 생성자 주입

- 이름 그대로 생성자를 통해서 의존 관계를 주입 받는 방법이다.
- 특징
	- 생성자 호출시점에 딱 1번만 호출되는 것이 보장된다.
	- 불변, 필수 의존관계에 사용
	
	<img width="1018" alt="스크린샷 2023-01-01 오후 6 26 47" src="https://user-images.githubusercontent.com/96857599/210166244-d4b11c2e-6004-4cee-895a-eb679a5634d6.png">

##### 중요! 생성자가 딱 1개만 있으면 @Autowired를 생략해도 자동 주입 된다. 물론 스프링 빈에만 해당한다.

#### 수정자 주입

- setter라 불리는 필드의 값을 변경하는 수정자 메서드를 통해서 의존관계를 주입하는 방법이다.
- 특징
	- 선택, 변경 가능성이 있는 의존관계에 사용 (스프링 빈에 등록된 것만 선택할 수 있다.)
	- 자바빈 프로퍼티 규약의 수정자 메서드 방식을 사용하는 방법이다.

> 참고: @Autowired 의 기본 동작은 주입할 대상이 없으면 오류가 발생한다. 주입할 대상이 없어도 동작하게 하려면 @Autowired(required = false) 로 지정하면 된다.

<img width="654" alt="스크린샷 2023-01-01 오후 6 42 41" src="https://user-images.githubusercontent.com/96857599/210166605-c22a60dc-fae4-4c95-b071-8efc5f9fa120.png">

> 참고: 자바빈 프로퍼티, 자바에서는 과거부터 필드의 값을 직접 변경하지 않고, setXxx, getXxx 라는 메서드를 통해서 값을 읽거나 수정하는 규칙을 만들었는데, 그것이 자바빈 프로퍼티 규약이다. 더 자세한 내용이 궁금하면 자바빈 프로퍼티로 검색해보자.

- 자바빈 프로퍼티 규약 예시

```java
 class Data {
      private int age;
      public void setAge(int age) {
        this.age = age;
      }
      public int getAge() {
        return age;
	  }
}
```

#### 필드 주입

<img width="1170" alt="스크린샷 2023-01-01 오후 6 55 08" src="https://user-images.githubusercontent.com/96857599/210166870-9733ea62-47e8-4b2f-8659-9f009f3be956.png">

<img width="1046" alt="스크린샷 2023-01-01 오후 6 54 50" src="https://user-images.githubusercontent.com/96857599/210166865-833f5718-8bab-4ee1-8b40-bbed7e04057c.png">

- 이름 그대로 필드에 바로 주입하는 방법이다.
- 특징
	- 코드가 간결해서 많은 개발자들을 유혹하지만 외부에서 변경이 불가능해서 테스트 하기 힘들다는 치명적인 단점이 있다.
	- DI 프레임워크가 없으면 아무것도 할 수 없다.
	- 사용하지 말자!
		- 애플리케이션의 실제 코드와 관계 없는 테스트 코드
		- 스프링 설정을 목적으로 하는 @Configuration 같은 곳에서만 특별한 용도로 사용
```java
@Component
    public class OrderServiceImpl implements OrderService {
        @Autowired
        private MemberRepository memberRepository;
        @Autowired
        private DiscountPolicy discountPolicy;
}
```

> 참고: 순수한 자바 테스트 코드에는 당연히 @Autowired가 동작하지 않는다. @SpringBootTest 처럼 스프링 컨테이너를 테스트에 통합한 경우에만 가능하다.
> 참고: 다음 코드와 같이 @Bean 에서 파라미터에 의존관계는 자동 주입된다. 수동 등록시 자동 등록된 빈의 의존관계가 필요할 때 문제를 해결할 수 있다.
```java
@Bean
OrderService orderService(MemberRepository memberRepoisitory, DiscountPolicy
discountPolicy) {
    new OrderServiceImpl(memberRepository, discountPolicy)
}
```

#### 일반 메서드 주입
- 일반 메서드를 통해서 주입 받을 수 있다.
- 특징
	- 한번에 여러 필드를 주입 받을 수 있다.
	- 일반적으로 잘 사용하지 않는다.

> 참고: 어쩌면 당연한 이야기이지만 의존관계 자동 주입은 스프링 컨테이너가 관리하는 스프링 빈이어야 동작한다. 스프링 빈이 아닌 Member 같은 클래스에서 @Autowired 코드를 적용해도 아무 기능도 동작하지 않는다.

### 옵션 처리

주입할 스프링 빈이 없어도 동작해야 할 때가 있다.
그런데 @Autowired만 사용하면 required 옵션의 기본값이 true 로 되어 있어서 자동 주입 대상이 없으면 오류가 발생한다.

자동 주입 대상을 옵션으로 처리하는 방법은 다음과 같다.
- @Autowired(required=false) : 자동 주입할 대상이 없으면 수정자 메서드 자체가 호출 안됨 - org.springframework.lang.
- @Nullable : 자동 주입할 대상이 없으면 null이 입력된다. 
- Optional<> : 자동 주입할 대상이 없으면 Optional.empty가 입력된다.

<img width="1293" alt="스크린샷 2023-01-03 오후 3 01 47" src="https://user-images.githubusercontent.com/96857599/210306713-bb40a123-7728-4246-8f19-30774e897ccc.png">

- Member는 스프링 빈이 아니다
- setNoBean1()은 @Autowired(required = false)이므로 호출 자체가 안 된다.


### 생성자 주입을 선택하는 이유

1. 불변
- 대부분의 의존관계 주입은 한번 일어나면 애플리케이션 종료시점까지 의존관계를 변경할 일이 없다. 오히려 대부분의 의존관계는 애플리케이션 종료 전까지 변하면 안된다.(불변해야 한다.)
- 수정자 주입을 사용하면, setXxx 메서드를 public으로 열어두어야 한다.
- 누군가 실수로 변경할 수 도 있고, 변경하면 안되는 메서드를 열어두는 것은 좋은 설계 방법이 아니다. 
- 생성자 주입은 객체를 생성할 때 딱 1번만 호출되므로 이후에 호출되는 일이 없다. 따라서 불변하게 설계할 수 있다.

2. 누락
프레임워크 없이 순수한 자바 코드를 단위 테스트 하는 경우에 다음과 같이 수정자 의존관계인 경우
<img width="1253" alt="스크린샷 2023-01-03 오후 3 18 09" src="https://user-images.githubusercontent.com/96857599/210308225-65227387-38eb-483f-b47c-9fdfff4cae3c.png">

- @Autowired가 프레임워크 안에서 동작할 때는 의존관계가 없으면 오류가 발생하지만, 지금은 프레임워크
없이 순수한 자바 코드로만 단위 테스트를 수행하고 있다.

3. final 키워드
생성자 주입을 사용하면 필드에 final 키워드를 사용할 수 있다. 그래서 생성자에서 혹시라도 값이 설정되지 않는 오류를 컴파일 시점에 막아준다.
<img width="1113" alt="스크린샷 2023-01-03 오후 3 23 23" src="https://user-images.githubusercontent.com/96857599/210308711-22857761-ecd3-4ecb-8df8-cfa9f2b11303.png">
- 잘 보면 필수 필드인 discountPolicy 에 값을 설정해야 하는데, 이 부분이 누락되었다. 자바는 컴파일 시점에 다음 오류를 발생시킨다.
- java: variable discountPolicy might not have been initialized
- 기억하자! 컴파일 오류는 세상에서 가장 빠르고, 좋은 오류다!
 
> 참고: 수정자 주입을 포함한 나머지 주입 방식은 모두 생성자 이후에 호출되므로, 필드에 final 키워드를 사용할 수 없다. 오직 생성자 주입 방식만 final 키워드를 사용할 수 있다.

#### 정리
- 생성자 주입 방식을 선택하는 이유는 여러가지가 있지만, 프레임워크에 의존하지 않고, 순수한 자바 언어의 특징을 잘 살리는 방법이기도 하다.
- 기본으로 생성자 주입을 사용하고, 필수 값이 아닌 경우에는 수정자 주입 방식을 옵션으로 부여하면 된다. 생성자 주입과 수정자 주입을 동시에 사용할 수 있다.
- 항상 생성자 주입을 선택해라! 그리고 가끔 옵션이 필요하면 수정자 주입을 선택해라. 필드 주입은 사용하지 않는게 좋다.

### 롬복과 최신 트랜드
- build.gradle에 롬복 설정 추가
<img width="1279" alt="스크린샷 2023-01-03 오후 3 32 11" src="https://user-images.githubusercontent.com/96857599/210309562-468669dc-2a73-4d25-b86b-b598ef557530.png">

- Lombok plugin 설치
<img width="1094" alt="스크린샷 2023-01-03 오후 3 35 35" src="https://user-images.githubusercontent.com/96857599/210309906-8c8b30e3-7585-47f8-8395-5d69efdbafa8.png">

- Preferences -> annotation proces -> Compiler -> Annotation Processors에서 Enable annotation processing 선
<img width="1094" alt="스크린샷 2023-01-03 오후 3 36 30" src="https://user-images.githubusercontent.com/96857599/210309989-3eca658a-3e7f-4987-a31d-84a5b81ac9d4.png">

기본 코드
```java

@Component
public class OrderServiceImpl implements OrderService {
	private final MemberRepository memberRepository;
	private final DiscountPolicy discountPolicy;

	@Autowired
        public OrderServiceImpl(MemberRepository memberRepository, DiscountPolicy
    discountPolicy) {
            this.memberRepository = memberRepository;
            this.discountPolicy = discountPolicy;
        }
}
```

- Lombok 라이브러리 사용시 getter & setter 메소드를 어노테이션으로 해결할 수 있다.
<img width="534" alt="스크린샷 2023-01-03 오후 3 41 15" src="https://user-images.githubusercontent.com/96857599/210310426-be213f77-efd4-436a-bd9e-b01a35bc116b.png">

<img width="887" alt="스크린샷 2023-01-03 오후 3 43 38" src="https://user-images.githubusercontent.com/96857599/210310640-fd168b54-a0d6-47e1-8320-779a1830a3cc.png">

- @RequiredArgsConstructor가 객체에서 final이 붙은 것을 파라미터로 받아서 생성자를 대신 생성해줌. (cmd + F12를 통해 알 수 있음.)

<img width="887" alt="스크린샷 2023-01-03 오후 3 50 29" src="https://user-images.githubusercontent.com/96857599/210311315-57483f51-6003-4be2-b2c5-ddd2d049766e.png">
<img width="586" alt="스크린샷 2023-01-03 오후 3 52 48" src="https://user-images.githubusercontent.com/96857599/210311570-454be47e-67c7-4cc7-879a-e01b1505fd15.png">

최종 코드
<img width="1126" alt="스크린샷 2023-01-03 오후 3 54 37" src="https://user-images.githubusercontent.com/96857599/210311751-00be0407-828e-4e7d-abc8-9bee8815e6da.png">
롬복이 자바의 애노테이션 프로세서라는 기능을 이용해서 컴파일 시점에 생성자 코드를 자동으로 생성해준다.

#### 정리
최근에는 생성자를 딱 1개 두고, @Autowired를 생략하는 방법을 주로 사용한다. 여기에 Lombok 라이브러리의 @RequiredArgsConstructor 함께 사용하면 기능은 다 제공하면서, 코드는 깔끔하게 사용할 수 있다.

### 조회 빈이 2개 이상 - 문제

@Autowired는 타입(Type)으로 조회한다.
```java
@Autowired
private DiscountPolicy discountPolicy
```  

타입으로 조회하기 때문에, 마치 다음 코드와 유사하게 동작한다. (실제로는 더 많은 기능을 제공한다.) ac.getBean(DiscountPolicy.class)

스프링 빈 조회에서 학습했듯이 타입으로 조회하면 선택된 빈이 2개 이상일 때 문제가 발생한다. DiscountPolicy 의 하위 타입인 FixDiscountPolicy , RateDiscountPolicy 둘다 스프링 빈으로 선언해보자.
<img width="419" alt="스크린샷 2023-01-03 오후 4 06 41" src="https://user-images.githubusercontent.com/96857599/210312918-f163d4e3-8180-4c8f-be7a-cc280a93b6a7.png">
<img width="402" alt="스크린샷 2023-01-03 오후 4 06 51" src="https://user-images.githubusercontent.com/96857599/210312944-07e1e02a-6c43-43a8-b770-bc68d19b285c.png">

NoUniqueBeanDefinitionException 오류가 발생한다.
<img width="901" alt="스크린샷 2023-01-03 오후 4 08 21" src="https://user-images.githubusercontent.com/96857599/210313109-87766c3e-a4c5-44c4-ba6d-6f31ea42afc9.png">

<img width="857" alt="스크린샷 2023-01-03 오후 4 06 00" src="https://user-images.githubusercontent.com/96857599/210312836-d4f548de-7d6c-4234-b9f1-ea9a5ae53fe1.png">
오류메시지가 친절하게도 하나의 빈을 기대했는데 fixDiscountPolicy , rateDiscountPolicy 2개가 발견되었다고 알려준다.

이때 하위 타입으로 지정할 수 도 있지만, 하위 타입으로 지정하는 것은 DIP를 위배하고 유연성이 떨어진다. 그리고 이름만 다르고, 완전히 똑같은 타입의 스프링 빈이 2개 있을 때 해결이 안된다.
스프링 빈을 수동 등록해서 문제를 해결해도 되지만, 의존 관계 자동 주입에서 해결하는 여러 방법이 있다.


### 조회 대상 빈이 2개 이상일 때 해결방법
- @Autowired 필드 명 매칭
- @Quilifier -> @Quilifier끼리 매칭 -> 빈 이름 매칭
- @Primary 사용

#### @Autowired 필드 명 매칭(빈 이름으로 매칭을 시도하는 것)
- DiscountPolicy의 객체 인스턴스 명을 discountPolicy -> rateDiscountPolicy
<img width="1194" alt="스크린샷 2023-01-03 오후 4 21 01" src="https://user-images.githubusercontent.com/96857599/210314369-20d8ce57-8444-4ff5-ba13-be2c87c0de90.png">

- 테스트 성공
<img width="1194" alt="스크린샷 2023-01-03 오후 4 22 56" src="https://user-images.githubusercontent.com/96857599/210314558-9acd3988-1cbd-4c21-a9b6-232fe99cc788.png">

필드 명이 rateDiscountPolicy 이므로 정상 주입된다.
필드 명 매칭은 먼저 타입 매칭을 시도 하고 그 결과에 여러 빈이 있을 때 추가로 동작하는 기능이다.

@Autowired 매칭 정리
1. 타입 매칭
2. 타입 매칭의 결과가 2개 이상일 때 필드 명, 파라미터 명으로 빈 이름 매칭

#### @Qualifier 사용
@Qualifier 는 추가 구분자를 붙여주는 방법이다.
주입시 추가적인 방법을 제공하는 것이지 빈 이름을 변경하는 것은 아니다.


빈 등록시 @Qualifier를 붙여 준다.
<img width="475" alt="스크린샷 2023-01-03 오후 4 27 20" src="https://user-images.githubusercontent.com/96857599/210314972-cb20fb57-e8a1-431e-a425-2814e17b083e.png">

<img width="475" alt="스크린샷 2023-01-03 오후 4 28 01" src="https://user-images.githubusercontent.com/96857599/210315029-27d9fcf5-1cbd-4c5e-836f-33734f4f10c7.png">

- 중복되는 생성자의 객체 앞에 @Qualifier()을 넣어준다.
<img width="475" alt="스크린샷 2023-01-03 오후 4 28 01" src="https://user-images.githubusercontent.com/96857599/210315029-27d9fcf5-1cbd-4c5e-836f-33734f4f10c7.png">

<img width="1441" alt="스크린샷 2023-01-03 오후 4 30 17" src="https://user-images.githubusercontent.com/96857599/210315249-8a8750a5-2b82-4ec0-89c9-61b5caaf50e5.png">

@Qualifier 로 주입할 때 @Qualifier("mainDiscountPolicy")를 못찾으면 어떻게 될까?
그러면 mainDiscountPolicy라는 이름의 스프링 빈을 추가로 찾는다. 
하지만 경험상 @Qualifier는 @Qualifier를 찾는 용도로만 사용하는게 명확하고 좋다.

@Qualifier 정리
1. @Qualifier끼리 매칭
2. 빈 이름 매칭
3. NoSuchBeanDefinitionException 예외 발생

#### @Primary 사용 (자주 사용하는 방법)
@Primary 는 우선순위를 정하는 방법이다. @Autowired 시에 여러 빈이 매칭되면 @Primary 가 우선권을 가진다.

<img width="983" alt="스크린샷 2023-01-03 오후 5 27 37" src="https://user-images.githubusercontent.com/96857599/210322091-92630294-fa4e-444e-9c58-67c96bfd7781.png">

여기까지 보면 @Primary와 @Qualifier 중에 어떤 것을 사용하면 좋을지 고민이 될 것이다.
@Qualifier 의 단점은 주입 받을 때 다음과 같이 모든 코드에 @Qualifier를 붙여주어야 한다는 점이다.

#### 우선순위
@Primary는 기본값 처럼 동작하는 것이고, @Qualifier는 매우 상세하게 동작한다. 이런 경우 어떤 것이 우선권을 가져갈까? 
스프링은 자동보다는 수동이, 넒은 범위의 선택권 보다는 좁은 범위의 선택권이 우선 순위가 높다. 따라서 여기서도 @Qualifier가 우선권이 높다.

### 어노테이션 직접 만들기
@Qualifier("mainDiscountPolicy") 이렇게 문자를 적으면 컴파일시 타입 체크가 안된다. 다음과 같은 애노테이션을 만들어서 문제를 해결할 수 있다.

<img width="1297" alt="스크린샷 2023-01-03 오후 5 35 02" src="https://user-images.githubusercontent.com/96857599/210323000-0f34e345-879c-4d19-b98f-7d78d8308ab9.png">
<img width="1297" alt="스크린샷 2023-01-03 오후 5 35 13" src="https://user-images.githubusercontent.com/96857599/210323027-b43e9fd1-7036-4b14-847d-787a0e3c68fb.png">
<img width="1340" alt="스크린샷 2023-01-03 오후 5 35 49" src="https://user-images.githubusercontent.com/96857599/210323129-3a0dc49d-7e74-4b86-8280-95c260162021.png">

어노테이션에는 상속이라는 개념이 없다. 이렇게 여러 애노테이션을 모아서 사용하는 기능은 스프링이 지원해주는 기능이다. @Qulifier 뿐만 아니라 다른 애노테이션들도 함께 조합해서 사용할 수 있다. 단적으로 @Autowired도 재정의 할 수 있다. 물론 스프링이 제공하는 기능을 뚜렷


### 조회한 빈이 모두 필요할 때, List, Map

의도적으로 정말 해당 타입의 스프링 빈이 다 필요한 경우도 있다.
예를 들어서 할인 서비스를 제공하는데, 클라이언트가 할인의 종류(rate, fix)를 선택할 수 있다고 가정해보자. 
스프링을 사용하면 소위 말하는 전략 패턴을 매우 간단하게 구현할 수 있다.
	
- Map에는 key(Stirng), value(스프링 빈)이, List에는 value(스프링 빈)이 저장된다.
<img width="1582" alt="스크린샷 2023-01-04 오후 10 15 08" src="https://user-images.githubusercontent.com/96857599/210563039-26a9a44a-a0d1-40b2-8300-84782b5c3758.png">
<img width="1368" alt="스크린샷 2023-01-04 오후 10 52 00" src="https://user-images.githubusercontent.com/96857599/210569664-9cde46ef-462a-46dc-8d1a-f5b531bb6b42.png">
<img width="1368" alt="스크린샷 2023-01-04 오후 10 51 45" src="https://user-images.githubusercontent.com/96857599/210569608-0e8258f2-624c-4042-9e73-c7d503f650d4.png">
	
로직 분석
	
- DiscountService는 Map으로 모든 DiscountPolicy를 주입받는다. 이때 fixDiscountPolicy, rateDiscountPolicy가 주입된다.
- discount() 메서드는 discountCode로 "fixDiscountPolicy"가 넘어오면 map에서 fixDiscountPolicy 스프링 빈을 찾아서 실행한다. 물론 “rateDiscountPolicy”가 넘어오면 rateDiscountPolicy 스프링 빈을 찾아서 실행한다.
	
### 자동, 수동의 올바른 실무 운영 기준
	
#### 편리한 자동 기능을 기본으로 사용하자
그러면 어떤 경우에 컴포넌트 스캔과 자동 주입을 사용하고, 어떤 경우에 설정 정보를 통해서 수동으로 빈을 등록하고, 의존관계도 수동으로 주입해야 할까?
	
결론부터 이야기하면, 스프링이 나오고 시간이 갈 수록 점점 자동을 선호하는 추세다. 스프링은 @Component 뿐만 아니라 @Controller , @Service , @Repository 처럼 계층에 맞추어 일반적인 애플리케이션 로직을 자동으로 스캔할 수 있도록 지원한다. 거기에 더해서 최근 스프링 부트는 컴포넌트 스캔을 기본으로 사용하고, 스프링 부트의 다양한 스프링 빈들도 조건이 맞으면 자동으로 등록하도록 설계했다.
	
설정 정보를 기반으로 애플리케이션을 구성하는 부분과 실제 동작하는 부분을 명확하게 나누는 것이 이상적이지만, 개발자 입장에서 스프링 빈을 하나 등록할 때 @Component 만 넣어주면 끝나는 일을 @Configuration 설정 정보에 가서 @Bean 을 적고, 객체를 생성하고, 주입할 대상을 일일이 적어주는 과정은 상당히 번거롭다.
또 관리할 빈이 많아서 설정 정보가 커지면 설정 정보를 관리하는 것 자체가 부담이 된다. 그리고 결정적으로 자동 빈 등록을 사용해도 OCP, DIP를 지킬 수 있다.
	
	
#### 수동 빈 등록으 언제 사용하면 좋을까?
	
애플리케이션은 크게 업무 로직과 기술 지원 로직으로 나눌 수 있다.
- 업무 로직 빈: 웹을 지원하는 컨트롤러, 핵심 비즈니스 로직이 있는 서비스, 데이터 계층의 로직을 처리하는 리포지토리등이 모두 업무 로직이다. 보통 비즈니스 요구사항을 개발할 때 추가되거나 변경된다.
- 기술 지원 빈: 기술적인 문제나 공통 관심사(AOP)를 처리할 때 주로 사용된다. 데이터베이스 연결이나, 공통 로그 처리 처럼 업무 로직을 지원하기 위한 하부 기술이나 공통 기술들이다.


- 업무 로직은 숫자도 매우 많고, 한번 개발해야 하면 컨트롤러, 서비스, 리포지토리 처럼 어느정도 유사한 패턴이 있다. 이런 경우 자동 기능을 적극 사용하는 것이 좋다. 보통 문제가 발생해도 어떤 곳에서 문제가 발생했는지 명확하게 파악하기 쉽다.
- 기술 지원 로직은 업무 로직과 비교해서 그 수가 매우 적고, 보통 애플리케이션 전반에 걸쳐서 광범위하게 영향을 미친다. 그리고 업무 로직은 문제가 발생했을 때 어디가 문제인지 명확하게 잘 드러나지만, 기술 지원 로직은 적용이 잘 되고 있는지 아닌지 조차 파악하기 어려운 경우가 많다. 그래서 이런 기술 지원 로직들은 가급적 수동 빈 등록을 사용해서 명확하게 드러내는 것이 좋다.

#### 애플리케이션에 광범위하게 영향을 미치는 기술 지원 객체는 수동 빈으로 등록해서 딱! 설정 정보에 바로 나타나게 하는 것이 유지보수 하기 좋다.

#### 비즈니스 로직 중에서 다형성을 적극 활용할 때

의존관계 자동 주입 - 조회한 빈이 모두 필요할 때, List, Map을 다시 보자.
DiscountService 가 의존관계 자동 주입으로 Map<String, DiscountPolicy> 에 주입을 받는 상황을 생각해보자. 여기에 어떤 빈들이 주입될 지, 각 빈들의 이름은 무엇일지 코드만 보고 한번에 쉽게 파악할 수 있을까? 내가 개발했으니 크게 관계가 없지만, 만약 이 코드를 다른 개발자가 개발해서 나에게 준 것이라면 어떨까?
자동 등록을 사용하고 있기 때문에 파악하려면 여러 코드를 찾아봐야 한다.

이런 경우 수동 빈으로 등록하거나 또는 자동으로하면 **특정 패키지에 같이 묶어**두는게 좋다! 핵심은 딱 보고 이해가 되어야 한다!

이 부분을 별도의 설정 정보로 만들고 수동으로 등록하면 다음과 같다.
```java
@Configuration
public class DiscountPolicyConfig {
    @Bean
    public DiscountPolicy rateDiscountPolicy() {
        return new RateDiscountPolicy();
    }
    @Bean
    public DiscountPolicy fixDiscountPolicy() 
    	return new FixDiscountPolicy();
    }
}

```
이 설정 정보만 봐도 한눈에 빈의 이름은 물론이고, 어떤 빈들이 주입될지 파악할 수 있다. 그래도 빈 자동 등록을 사용하고 싶으면 파악하기 좋게 DiscountPolicy의 구현 빈들만 따로 모아서 특정 패키지에 모아두자.


참고로 스프링과 스프링 부트가 자동으로 등록하는 수 많은 빈들은 예외다. 이런 부분들은 스프링 자체를 잘 이해하고 스프링의 의도대로 잘 사용하는게 중요하다. 스프링 부트의 경우 DataSource 같은 데이터베이스 연결에 사용하는 기술 지원 로직까지 내부에서 자동으로 등록하는데, 이런 부분은 메뉴얼을 잘 참고해서 스프링 부트가 의도한 대로 편리하게 사용하면 된다. 반면에 스프링 부트가 아니라 내가 직접 기술 지원 객체를 스프링 빈으로 등록한다면 수동으로 등록해서 명확하게 드러내는 것이 좋다.

#### 정리
편리한 자동 기능을 기본으로 사용하자
직접 등록하는 기술 지원 객체는 수동 등록
다형성을 적극 활용하는 비즈니스 로직은 수동 등록을 고민해보자

### 빈 생명주기 콜백
	
빈 생명주기 콜백 시작
	
데이터베이스 커넥션 풀이나, 네트워크 소켓처럼 애플리케이션 시작 시점에 필요한 연결을 미리 해두고, 애플리케이션 종료 시점에 연결을 모두 종료하는 작업을 진행하려면, 객체의 초기화와 종료 작업이 필요하다.
이번시간에는 스프링을 통해 이러한 초기화 작업과 종료 작업을 어떻게 진행하는지 예제로 알아보자.
	
간단하게 외부 네트워크에 미리 연결하는 객체를 하나 생성한다고 가정해보자. 실제로 네트워크에 연결하는 것은 아니고, 단순히 문자만 출력하도록 했다. 
이 NetworkClient는 애플리케이션 시작 시점에 connect()를 호출해서 연결을 맺어두어야 하고, 애플리케이션이 종료되면 disConnect()를 호출해서 연결을 끊어야 한다.
	
<img width="1347" alt="스크린샷 2023-01-06 오후 8 31 52" src="https://user-images.githubusercontent.com/96857599/211004396-5dd60365-e729-4cf5-afb4-3b2ba18a6720.png">
	
<img width="1347" alt="스크린샷 2023-01-06 오후 8 32 15" src="https://user-images.githubusercontent.com/96857599/211004435-ef23a02e-67d0-4034-9c47-fe0ed9c0c5ad.png">

<img width="297" alt="스크린샷 2023-01-06 오후 8 33 05" src="https://user-images.githubusercontent.com/96857599/211004549-b14f90fb-e568-44ec-b26d-a40bfc2db551.png">
	
- 결과에 null값이 있는 이유는 객체가 생성되는 단계에는 url이 주입되지 않았기 때문이다.
	
스프링 빈은 객체를 생성하고, 의존관계 주입이 다 끝난 다음에야 필요한 데이터를 사용할 수 있는 준비가 완료된다. 따라서 초기화 작업은 의존관계 주입이 모두 완료되고 난 다음에 호출해야 한다. 그런데 개발자가 의존관계 주입이 모두 완료된 시점을 어떻게 알 수 있을까?
스프링은 의존관계 주입이 완료되면 스프링 빈에게 콜백 메서드를 통해서 초기화 시점을 알려주는 다양한 기능을 제공한다. 또한 스프링은 스프링 컨테이너가 종료되기 직전에 소멸 콜백을 준다. 따라서 안전하게 종료 작업을 진행할 수 있다.

스프링 빈의 이벤트 라이프사이클
스프링컨테이너 생성 -> 스프링빈생성 -> 의존관계주입 -> 초기화콜백 -> 사용 -> 소멸전콜백 -> 스프링 종료
	
- 초기화 콜백: 빈이 생성되고, 빈의 의존관계 주입이 완료된 후 호출 
- 소멸전 콜백: 빈이 소멸되기 직전에 호출
	
스프링은 다양한 방식으로 생명주기 콜백을 지원한다.
	
> 참고: 객체의 생성과 초기화를 분리하자.
> 생성자는 필수 정보(파라미터)를 받고, 메모리를 할당해서 객체를 생성하는 책임을 가진다. 반면에 초기화는
이렇게 생성된 값들을 활용해서 외부 커넥션을 연결하는등 무거운 동작을 수행한다.
> 따라서 생성자 안에서 무거운 초기화 작업을 함께 하는 것 보다는 객체를 생성하는 부분과 초기화 하는 부분을 명확하게 나누는 것이 유지보수 관점에서 좋다. 물론 초기화 작업이 내부 값들만 약간 변경하는
정도로 단순한 경우에는 생성자에서 한번에 다 처리하는게 더 나을 수 있다.
	
> 참고: 싱글톤 빈들은 스프링 컨테이너가 종료될 때 싱글톤 빈들도 함께 종료되기 때문에 스프링 컨테이너가 종료되기 직전에 소멸전 콜백이 일어난다. 뒤에서 설명하겠지만 싱글톤 처럼 컨테이너의 시작과 종료까지 생존하는 빈도 있지만, 생명주기가 짧은 빈들도 있는데 이 빈들은 컨테이너와 무관하게 해당 빈이 종료되기 직전에 소멸전 콜백이 일어난다. 자세한 내용은 스코프에서 알아보겠다.
	
스프링은 크게 3가지 방법으로 빈 생명주기 콜백을 지원한다. 
- 인터페이스(InitializingBean, DisposableBean)
- 설정 정보에 초기화 메서드, 종료 메서드 지정
- @PostConstruct, @PreDestroy 애노테이션 지원

### 인터페이스 InitializingBean, DisposableBean
	
- 인터페이스 InitializingBean, DisposableBean 추가
	
<img width="612" alt="스크린샷 2023-01-07 오후 1 20 35" src="https://user-images.githubusercontent.com/96857599/211130725-088ef5a9-ae45-454c-909f-bf322e358657.png">
<img width="1356" alt="스크린샷 2023-01-07 오후 1 20 45" src="https://user-images.githubusercontent.com/96857599/211130733-71bfb433-2db2-4284-9e23-42c634b1d923.png">

- 출력 결과
<img width="1356" alt="스크린샷 2023-01-07 오후 1 21 23" src="https://user-images.githubusercontent.com/96857599/211130747-a9493cf3-1f5b-46d5-bde6-99c35f51e4d7.png">

<img width="884" alt="스크린샷 2023-01-07 오후 1 21 43" src="https://user-images.githubusercontent.com/96857599/211130749-b3ccf5cc-6aaa-4350-a928-57876e89c476.png">

- 출력 결과를 보면 초기화 메서드가 주입 완료 후에 적절하게 호출 된 것을 확인할 수 있다. 
- 그리고 스프링 컨테이너의 종료가 호출되자 소멸 메서드가 호출 된 것도 확인할 수 있다.
	
#### 초기화, 소멸 인터페이스 단점
- 이 인터페이스는 스프링 전용 인터페이스다. 해당 코드가 스프링 전용 인터페이스에 의존한다. 
- 초기화, 소멸 메서드의 이름을 변경할 수 없다.
- 내가 코드를 고칠 수 없는 외부 라이브러리에 적용할 수 없다.

> 참고: 인터페이스를 사용하는 초기화, 종료 방법은 스프링 초창기에 나온 방법들이고, 지금은 다음의 더 나은 방법들이 있어서 거의 사용하지 않는다.
	
### 빈 등록 초기화, 소멸 메서드 지정

- 인터페이스 InitializingBean, DisposableBean를 삭제하고, 메소드 이름을 설정한다.
<img width="966" alt="스크린샷 2023-01-07 오후 1 32 20" src="https://user-images.githubusercontent.com/96857599/211131070-96eae377-11ef-4351-96e6-c6171c7d3e4f.png">

- 설정 정보에 @Bean(initMethod = "init", destroyMethod = "close") 처럼 초기화, 소멸 메서드를
지정할 수 있다.
<img width="966" alt="스크린샷 2023-01-07 오후 1 33 22" src="https://user-images.githubusercontent.com/96857599/211131104-8a734bc6-91ce-4065-a8e5-c461076d6639.png">

#### 설정 정보 사용 특징
메서드 이름을 자유롭게 줄 수 있다.
스프링 빈이 스프링 코드에 의존하지 않는다.
코드가 아니라 설정 정보를 사용하기 때문에 코드를 고칠 수 없는 외부 라이브러리에도 초기화, 종료 메서드를 적용할 수 있다.
	
#### 종료 메서드 추론
- @Bean의 destroyMethod 속성에는 아주 특별한 기능이 있다.
- 라이브러리는 대부분 close , shutdown 이라는 이름의 종료 메서드를 사용한다.
- @Bean의 destroyMethod는 기본값이 (inferred) (추론)으로 등록되어 있다.
- 이 추론 기능은 close , shutdown라는 이름의 메서드를 자동으로 호출해준다. 이름 그대로 종료 메서드를 추론해서 호출해준다.
- 따라서 직접 스프링 빈으로 등록하면 종료 메서드는 따로 적어주지 않아도 잘 동작한다.
- 추론 기능을 사용하기 싫으면 destroyMethod="" 처럼 빈 공백을 지정하면 된다.
	
	
### 어노테이션 @PostConstruct, @PreDestroy
- 이거 쓰면 된다.
	
<img width="922" alt="스크린샷 2023-01-07 오후 1 38 19" src="https://user-images.githubusercontent.com/96857599/211131238-78f11948-8edc-499b-82c1-ae873e6a81ec.png">
	
- javax로 import되는 것은 자바에서 공식 지원하는 것이다.
<img width="325" alt="스크린샷 2023-01-07 오후 1 38 33" src="https://user-images.githubusercontent.com/96857599/211131245-cead3d40-a96e-4b75-bed1-fd3be142483a.png">

<img width="966" alt="스크린샷 2023-01-07 오후 1 39 45" src="https://user-images.githubusercontent.com/96857599/211131299-5e9382d3-cda9-48c5-87cb-4e1fd958941e.png">

#### @PostConstruct, @PreDestroy 애노테이션 특징
- 최신 스프링에서 가장 권장하는 방법이다.
- 애노테이션 하나만 붙이면 되므로 매우 편리하다.
- 패키지를 잘 보면 javax.annotation.PostConstruct 이다. 스프링에 종속적인 기술이 아니라 JSR-250 라는 자바 표준이다. 따라서 스프링이 아닌 다른 컨테이너에서도 동작한다.
- 컴포넌트 스캔과 잘 어울린다.
- 유일한 단점은 외부 라이브러리에는 적용하지 못한다는 것이다. 외부 라이브러리를 초기화, 종료 해야 하면 @Bean의 기능을 사용하자.

#### 정리

- @PostConstruct, @PreDestroy 애노테이션을 사용하자
- 코드를 고칠 수 없는 외부 라이브러리를 초기화, 종료해야 하면 @Bean 의 initMethod, destroyMethod를 사용하자.
	
### 빈스코프란?

지금까지 우리는 스프링 빈이 스프링 컨테이너의 시작과 함께 생성되어서 스프링 컨테이너가 종료될 때 까지 유지된다고 학습했다. 이것은 스프링 빈이 기본적으로 싱글톤 스코프로 생성되기 때문이다. 스코프는 번역 그대로 빈이 존재할 수 있는 범위를 뜻한다.

	
스프링은 다음과 같은 다양한 스코프를 지원한다.
- 싱글톤: 기본 스코프, 스프링 컨테이너의 시작과 종료까지 유지되는 가장 넓은 범위의 스코프이다. 
- 프로토타입: 스프링 컨테이너는 프로토타입 빈의 생성과 의존관계 주입까지만 관여하고 더는 관리하지 않는 매우 짧은 범위의 스코프이다.
- 웹 관련 스코프
	- request: 웹 요청이 들어오고 나갈때 까지 유지되는 스코프이다. 
	- session: 웹 세션이 생성되고 종료될 때 까지 유지되는 스코프이다. 
	- application: 웹의 서블릿 컨텍스트와 같은 범위로 유지되는 스코프이다.


	
### 프로토타입 스코프

싱글톤 스코프의 빈을 조회하면 스프링 컨테이너는 항상 같은 인스턴스의 스프링 빈을 반환한다. 반면에 프로토타입 스코프를 스프링 컨테이너에 조회하면 스프링 컨테이너는 항상 새로운 인스턴스를 생성해서 반환한다.

<img width="536" alt="스크린샷 2023-01-07 오후 2 03 09" src="https://user-images.githubusercontent.com/96857599/211132001-9b10f7a0-2b50-4a0a-afe3-93122395a2cc.png">
1. 싱글톤 스코프의 빈을 스프링 컨테이너에 요청한다.
2. 스프링 컨테이너는 본인이 관리하는 스프링 빈을 반환한다.
3. 이후에 스프링 컨테이너에 같은 요청이 와도 같은 객체 인스턴스의 스프링 빈을 반환한다.

<img width="540" alt="스크린샷 2023-01-07 오후 2 04 31" src="https://user-images.githubusercontent.com/96857599/211132021-a2bca9a1-4812-40cd-9fbd-96736131468d.png">
1. 프로토타입 스코프의 빈을 스프링 컨테이너에 요청한다.
2. 스프링 컨테이너는 이 시점에 프로토타입 빈을 생성하고, 필요한 의존관계를 주입한다.

<img width="539" alt="스크린샷 2023-01-07 오후 2 05 39" src="https://user-images.githubusercontent.com/96857599/211132048-eb44c69a-63f2-4d7d-a6a3-f9c4064c8d44.png">
3. 스프링 컨테이너는 생성한 프로토타입 빈을 클라이언트에 반환한다.
4. 이후에 스프링 컨테이너에 같은 요청이 오면 항상 새로운 프로토타입 빈을 생성해서 반환한다.

#### 정리
- 여기서 핵심은 스프링 컨테이너는 프로토타입 빈을 생성하고, 의존관계 주입, 초기화까지만 처리한다는
것이다. 
- 클라이언트에 빈을 반환하고, 이후 스프링 컨테이너는 생성된 프로토타입 빈을 관리하지 않는다. 프로토타입 빈을 관리할 책임은 프로토타입 빈을 받은 클라이언트에 있다. 그래서 @PreDestroy 같은 종료 메서드가 호출되지 않는다.

- 싱글톤 스코프 빈 테스트
<img width="1474" alt="스크린샷 2023-01-07 오후 2 38 58" src="https://user-images.githubusercontent.com/96857599/211133053-40caaca2-635c-4f95-8734-6b2490fafe08.png">


- 빈 초기화 메서드를 실행하고,
- 같은 인스턴스의 빈을 조회하고,
- 종료 메서드까지 정상 호출 된 것을 확인할 수 있다.

- 프로토타입 스코프 빈 테스트
<img width="1345" alt="스크린샷 2023-01-07 오후 2 30 25" src="https://user-images.githubusercontent.com/96857599/211132782-ae122d1e-55f3-4ccf-bd69-89d6599346c7.png">

<img width="881" alt="스크린샷 2023-01-07 오후 2 30 36" src="https://user-images.githubusercontent.com/96857599/211132785-0d4dca85-e004-4021-84e7-719eb2e4b821.png">

- 싱글톤 빈은 스프링 컨테이너 생성 시점에 초기화 메서드가 실행 되지만, 프로토타입 스코프의 빈은 스프링 컨테이너에서 빈을 조회할 때 생성되고, 초기화 메서드도 실행된다.
- 프로토타입 빈을 2번 조회했으므로 완전히 다른 스프링 빈이 생성되고, 초기화도 2번 실행된 것을 확인할 수 있다.
- 싱글톤 빈은 스프링 컨테이너가 관리하기 때문에 스프링 컨테이너가 종료될 때 빈의 종료 메서드가 실행되지만, 프로토타입 빈은 스프링 컨테이너가 생성과 의존관계 주입 그리고 초기화 까지만 관여하고, 더는 관리하지 않는다. 따라서 프로토타입 빈은 스프링 컨테이너가 종료될 때 @PreDestroy 같은 종료 메서드가 전혀 실행되지 않는다.

#### 프로토타입 빈의 특징 정리
- 스프링 컨테이너에 요청할 때 마다 새로 생성된다.
- 스프링 컨테이너는 프로토타입 빈의 생성과 의존관계 주입 그리고 초기화까지만 관여한다.
- 종료 메서드가 호출되지 않는다.
- 그래서 프로토타입 빈은 프로토타입 빈을 조회한 클라이언트가 관리해야 한다. 종료 메서드에 대한 호출도
클라이언트가 직접 해야한다.

### 프로토타입 스코프 - 싱글톤 빈과 함께 사용시 문제점

스프링 컨테이너에 프로토타입 스코프의 빈을 요청하면 항상 새로운 객체 인스턴스를 생성해서 반환한다.  
하지만 싱글톤 빈과 함께 사용할 때는 의도한 대로 잘 동작하지 않으므로 주의해야 한다. 그림과 코드로 설명하겠다.

프로토타입 빈 직접 요청
<img width="538" alt="스크린샷 2023-01-07 오후 2 42 34" src="https://user-images.githubusercontent.com/96857599/211133163-790b98eb-f73c-477d-bb5b-69505543b105.png">
1. 클라이언트A는 스프링 컨테이너에 프로토타입 빈을 요청한다.
2. 스프링 컨테이너는 프로토타입 빈을 새로 생성해서 반환(x01)한다. 해당 빈의 count 필드 값은 0이다. 
3. 클라이언트는 조회한 프로토타입 빈에 addCount() 를 호출하면서 count 필드를 +1 한다. 결과적으로 프로토타입 빈(x01)의 count는 1이 된다.

<img width="539" alt="스크린샷 2023-01-07 오후 2 43 09" src="https://user-images.githubusercontent.com/96857599/211133181-9e6e9a1c-cd8e-48e0-b024-096c6a054e45.png">
1. 클라이언트B는 스프링 컨테이너에 프로토타입 빈을 요청한다.
2. 스프링 컨테이너는 프로토타입 빈을 새로 생성해서 반환(x02)한다. 해당 빈의 count 필드 값은 0이다. 
3. 클라이언트는 조회한 프로토타입 빈에 addCount()를 호출하면서 count 필드를 +1 한다. 결과적으로 프로토타입 빈(x02)의 count는 1이 된다.
<img width="1425" alt="스크린샷 2023-01-07 오후 3 05 40" src="https://user-images.githubusercontent.com/96857599/211133862-024c1eeb-6eeb-4c94-ba80-e3905e6a5f85.png">
<img width="1425" alt="스크린샷 2023-01-07 오후 3 05 50" src="https://user-images.githubusercontent.com/96857599/211133870-db87d96d-9d3e-416a-9c35-3f562d47fa0d.png">

#### 싱글톤 빈에서 프로토타입 빈 
<img width="536" alt="스크린샷 2023-01-07 오후 3 06 48" src="https://user-images.githubusercontent.com/96857599/211133900-36384fa7-8c1e-4297-8bf0-73d305b152e4.png">

- clientBean은 싱글톤이므로, 보통 스프링 컨테이너 생성 시점에 함께 생성되고, 의존관계 주입도 발생한다.
1. clientBean은 의존관계 자동 주입을 사용한다. 주입 시점에 스프링 컨테이너에 프로토타입 빈을 요청한다.
2. 스프링 컨테이너는 프로토타입 빈을 생성해서 clientBean에 반환한다. 프로토타입 빈의 count 필드 값은 0이다.
- 이제 clientBean은 프로토타입 빈을 내부 필드에 보관한다. (정확히는 참조값을 보관한다.)

<img width="537" alt="스크린샷 2023-01-07 오후 3 07 42" src="https://user-images.githubusercontent.com/96857599/211133925-a0ea3a14-ec58-4717-a1bf-c5c343ed6dd2.png">

- 클라이언트 A는 clientBean을 스프링 컨테이너에 요청해서 받는다. 싱글톤이므로 항상 같은 clientBean이 반환된다.
3. 클라이언트 A는 clientBean.logic()을 호출한다.
4. clientBean은 prototypeBean의 addCount()를 호출해서 프로토타입 빈의 count를 증가한다. count값이 1이 된다.
<img width="542" alt="스크린샷 2023-01-07 오후 3 08 42" src="https://user-images.githubusercontent.com/96857599/211133958-29602dad-24de-4253-9cfa-e1dc8edc2fc2.png">
- 클라이언트 B는 clientBean을 스프링 컨테이너에 요청해서 받는다. 싱글톤이므로 항상 같은 clientBean이 반환된다.
- 여기서 중요한 점이 있는데, clientBean이 내부에 가지고 있는 프로토타입 빈은 이미 과거에 주입이 끝난 빈이다. 주입 시점에 스프링 컨테이너에 요청해서 프로토타입 빈이 새로 생성이 된 것이지, 사용 할 때마다 새로 생성되는 것이 아니다!
5. 클라이언트 B는 clientBean.logic()을 호출한다.
6. clientBean은 prototypeBean의 addCount()를 호출해서 프로토타입 빈의 count를 증가한다. 원래 count 값이 1이었으므로 2가 된다.

- @RequiredArgsConstructor를 통해서 생성자 구현한 것
<img width="1236" alt="스크린샷 2023-01-07 오후 3 21 52" src="https://user-images.githubusercontent.com/96857599/211134407-fa8a6b43-1a3c-4269-a3b6-546ae5589e2d.png">

- 풀어서 작성한 것
<img width="1236" alt="스크린샷 2023-01-07 오후 3 21 37" src="https://user-images.githubusercontent.com/96857599/211134399-d5539e55-a3f8-4569-a966-f715a7893304.png">

<img width="1319" alt="스크린샷 2023-01-07 오후 3 24 02" src="https://user-images.githubusercontent.com/96857599/211134483-8f782807-aacf-4953-89a0-dc76587fc715.png">

스프링은 일반적으로 싱글톤 빈을 사용하므로, 싱글톤 빈이 프로토타입 빈을 사용하게 된다. 그런데 싱글톤 빈은 생성 시점에만 의존관계 주입을 받기 때문에, 프로토타입 빈이 새로 생성되기는 하지만, 싱글톤 빈과 함께 계속 유지되는 것이 문제다.

아마 원하는 것이 이런 것은 아닐 것이다. 프로토타입 빈을 주입 시점에만 새로 생성하는게 아니라, 사용할 때 마다 새로 생성해서 사용하는 것을 원할 것이다.

> 참고: 여러 빈에서 같은 프로토타입 빈을 주입 받으면, 주입 받는 시점에 각각 새로운 프로토타입 빈이 생성된다. 예를 들어서 clientA, clientB가 각각 의존관계 주입을 받으면 각각 다른 인스턴스의 프로토타입 빈을 주입 받는다.
> clientA prototypeBean@x01
> clientB prototypeBean@x02
> 물론 사용할 때 마다 새로 생성되는 것은 아니다.

### 프로토타입 스코프 - 싱글톤 빈과 함께 사용시 Provider로 문제
싱글톤 빈과 프로토타입 빈을 함께 사용할 때, 어떻게 하면 사용할 때 마다 항상 새로운 프로토타입 빈을
생성할 수 있을까? 

- 가장 간단한 방법은 싱글톤 빈이 프로토타입을 사용할 때 마다 스프링 컨테이너에 새로 요청하는 것이다.


```java
public class PrototypeProviderTest {
      @Test
      void providerTest() {
          AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(ClientBean.class, PrototypeBean.class);
          
	  ClientBean clientBean1 = ac.getBean(ClientBean.class);
          int count1 = clientBean1.logic();
          assertThat(count1).isEqualTo(1);
          
	  ClientBean clientBean2 = ac.getBean(ClientBean.class);
          int count2 = clientBean2.logic();
          assertThat(count2).isEqualTo(1);
      }
      
      static class ClientBean {
          
	  @Autowired
          private ApplicationContext ac;
         
	  public int logic() {
              PrototypeBean prototypeBean = ac.getBean(PrototypeBean.class);
              prototypeBean.addCount();
              int count = prototypeBean.getCount();
              return count;
	  }
      }
      
      @Scope("prototype")
      static class PrototypeBean {
          
	  private int count = 0;
          
	  public void addCount() {
              count++;
	  }
          
	  public int getCount() {
              return count;
	  }
          
	  @PostConstruct
          public void init() {
              System.out.println("PrototypeBean.init " + this);
          }
          
	  @PreDestroy
          public void destroy() {
              System.out.println("PrototypeBean.destroy");
          }
      }
      
      
}

```

- 실행해보면 ac.getBean()을 통해서 항상 새로운 프로토타입 빈이 생성되는 것을 확인할 수 있다. 
- 의존관계를 외부에서 주입(DI) 받는게 아니라 이렇게 직접 필요한 의존관계를 찾는 것을 Dependency Lookup (DL) 의존관계 조회(탐색)이라한다.
- 그런데 이렇게 스프링의 애플리케이션 컨텍스트 전체를 주입받게 되면, 스프링 컨테이너에 종속적인 코드가 되고, 단위 테스트도 어려워진다.
- 지금 필요한 기능은 지정한 프로토타입 빈을 컨테이너에서 대신 찾아주는 딱! DL 정도의 기능만 제공하는 무언가가 있으면 된다.

#### ObjectFactory, ObjectProvider
지정한 빈을 컨테이너에서 대신 찾아주는 DL 서비스를 제공하는 것이 바로 ObjectProvider 이다. 참고로 과거에는 ObjectFactory 가 있었는데, 여기에 편의 기능을 추가해서 ObjectProvider 가 만들어졌다.

<img width="1319" alt="스크린샷 2023-01-07 오후 4 00 39" src="https://user-images.githubusercontent.com/96857599/211135807-2e0576bc-c62b-4b6d-8ed6-0b5d0abdbdd1.png">

<img width="1319" alt="스크린샷 2023-01-07 오후 4 01 02" src="https://user-images.githubusercontent.com/96857599/211135946-8fb644a8-7305-4ed7-a3d1-a496b020cdaf.png">

- 실행해보면 prototypeBeanProvider.getObject() 을 통해서 항상 새로운 프로토타입 빈이 생성되는 것을 확인할 수 있다.
- ObjectProvider의 getObject()를 호출하면 내부에서는 스프링 컨테이너를 통해 해당 빈을 찾아서 반환한다. (DL)
- 스프링이 제공하는 기능을 사용하지만, 기능이 단순하므로 단위테스트를 만들거나 mock 코드를 만들기는 훨씬 쉬워진다.
- ObjectProvider는 지금 딱 필요한 DL 정도의 기능만 제공한다.

#### 특징
- ObjectFactory: 기능이 단순, 별도의 라이브러리 필요 없음, 스프링에 의존
- ObjectProvider: ObjectFactory 상속, 옵션, 스트림 처리등 편의 기능이 많고, 별도의 라이브러리 필요 없음, 스프링에 의존

#### JSR-330 Provider
- 마지막 방법은 javax.inject.Provider라는 JSR-330 자바 표준을 사용하는 방법이다.
- 이 방법을 사용하려면 javax.inject:javax.inject:1 라이브러리를 gradle에 추가해야 한다.

<img width="1151" alt="스크린샷 2023-01-07 오후 4 09 29" src="https://user-images.githubusercontent.com/96857599/211138714-658a85e3-35d2-4b60-8cc7-8405865ada41.png">

- 실행해보면 provider.get() 을 통해서 항상 새로운 프로토타입 빈이 생성되는 것을 확인할 수 있다. 
- provider의 get()을 호출하면 내부에서는 스프링 컨테이너를 통해 해당 빈을 찾아서 반환한다. (DL)
- 자바 표준이고, 기능이 단순하므로 단위테스트를 만들거나 mock 코드를 만들기는 훨씬 쉬워진다. 
- Provider 는 지금 딱 필요한 DL 정도의 기능만 제공한다.

#### 특징
- get() 메서드 하나로 기능이 매우 단순하다.
- 별도의 라이브러리가 필요하다.
- 자바 표준이므로 스프링이 아닌 다른 컨테이너에서도 사용할 수 있다.


#### 정리
- 그러면 프로토타입 빈을 언제 사용할까? 매번 사용할 때 마다 의존관계 주입이 완료된 새로운 객체가 필요하면 사용하면 된다. 그런데 실무에서 웹 애플리케이션을 개발해보면, 싱글톤 빈으로 대부분의 문제를 해결할 수 있기 때문에 프로토타입 빈을 직접적으로 사용하는 일은 매우 드물다.
- ObjectProvider, JSR330 Provider 등은 프로토타입 뿐만 아니라 DL이 필요한 경우는 언제든지 사용할 수 있다.


> 참고: 스프링이 제공하는 메서드에 @Lookup 애노테이션을 사용하는 방법도 있지만, 이전 방법들로 충분하고, 고려해야할 내용도 많아서 생략하겠다.

> 참고: 실무에서 자바 표준인 JSR-330 Provider를 사용할 것인지, 아니면 스프링이 제공하는 ObjectProvider를 사용할 것인지 고민이 될 것이다. ObjectProvider는 DL을 위한 편의 기능을 많이 제공해주고 스프링 외에 별도의 의존관계 추가가 필요 없기 때문에 편리하다. 만약(정말 그럴일은 거의 없겠지만) 코드를 스프링이 아닌 다른 컨테이너에서도 사용할 수 있어야 한다면 JSR-330 Provider를 사용해야한다.
>
> 스프링을 사용하다 보면 이 기능 뿐만 아니라 다른 기능들도 자바 표준과 스프링이 제공하는 기능이
겹칠때가 많이 있다. 대부분 스프링이 더 다양하고 편리한 기능을 제공해주기 때문에, 특별히 다른 컨테이너를 사용할 일이 없다면, 스프링이 제공하는 기능을 사용하면 된다.


### 웹 스코프
지금까지 싱글톤과 프로토타입 스코프를 학습했다. 싱글톤은 스프링 컨테이너의 시작과 끝까지 함께하는 매우 긴 스코프이고, 프로토타입은 생성과 의존관계 주입, 그리고 초기화까지만 진행하는 특별한 스코프이다.

이번에는 웹 스코프에 대해 알아보자.

#### 웹 스코프의 특징
- 웹 스코프는 웹 환경에서만 동작한다.
- 웹 스코프는 프로토타입과 다르게 스프링이 해당 스코프의 종료시점까지 관리한다. 따라서 종료 메서드가 호출된다.

#### 웹 스코프 종류
- request: HTTP 요청 하나가 들어오고 나갈 때 까지 유지되는 스코프, 각각의 HTTP 요청마다 별도의 빈 인스턴스가 생성되고, 관리된다.
- session: HTTP Session과 동일한 생명주기를 가지는 스코프
- application: 서블릿 컨텍스트( ServletContext )와 동일한 생명주기를 가지는 스코프
- websocket: 웹 소켓과 동일한 생명주기를 가지는 스코프

사실 세션이나, 서블릿 컨텍스트, 웹 소켓 같은 용어를 잘 모르는 분들도 있을 것이다. 여기서는 request
스코프를 예제로 설명하겠다. 나머지도 범위만 다르지 동작 방식은 비슷하다.
<img width="538" alt="스크린샷 2023-01-07 오후 4 30 11" src="https://user-images.githubusercontent.com/96857599/211139423-db174044-13a5-4308-919d-13a90b74ffdd.png">


### request 스코프 예제 만들기
#### 웹 환경 추가

웹 스코프는 웹 환경에서만 동작하므로 web 환경이 동작하도록 라이브러리를 추가하자.


> 참고: spring-boot-starter-web 라이브러리를 추가하면 스프링 부트는 내장 톰켓 서버를 활용해서 웹 서버와 스프링을 함께 실행시킨다.

> 참고: 스프링 부트는 웹 라이브러리가 없으면 우리가 지금까지 학습한 AnnotationConfigApplicationContext을 기반으로 애플리케이션을 구동한다. 웹 라이브러리가 추가되면 웹과 관련된 추가 설정과 환경들이 필요하므로 AnnotationConfigServletWebServerApplicationContext를 기반으로 애플리케이션을 구동한다.

만약 기본 포트인 8080 포트를 다른곳에서 사용중이어서 오류가 발생하면 포트를 변경해야 한다. 9090
포트로 변경하려면 다음 설정을 추가하자. main/resources/application.properties
```
server.port=9090
```

#### request 스코프 예제 개발
동시에 여러 HTTP 요청이 오면 정확히 어떤 요청이 남긴 로그인지 구분하기 어렵다.
이럴때 사용하기 딱 좋은것이 바로 request 스코프이다.

다음과 같이 로그가 남도록 request 스코프를 활용해서 추가 기능을 개발해보자.

```
[d06b992f...] request scope bean create
[d06b992f...][http://localhost:8080/log-demo] controller test
[d06b992f...][http://localhost:8080/log-demo] service id = testId
[d06b992f...] request scope bean close
```

- 기대하는 공통 포멧: [UUID][requestURL] {message}
- UUID를 사용해서 HTTP 요청을 구분하자.
- requestURL 정보도 추가로 넣어서 어떤 URL을 요청해서 남은 로그인지 확인하자.

<img width="1174" alt="스크린샷 2023-01-07 오후 5 00 23" src="https://user-images.githubusercontent.com/96857599/211140458-0e808937-4302-46f8-a2cc-7a6dc89e3f7a.png">
- 로그를 출력하기 위한 MyLogger 클래스이다.
- @Scope(value = "request") 를 사용해서 request 스코프로 지정했다. 이제 이 빈은 HTTP 요청 당 하나씩 생성되고, HTTP 요청이 끝나는 시점에 소멸된다.
- 이 빈이 생성되는 시점에 자동으로 @PostConstruct 초기화 메서드를 사용해서 uuid를 생성해서 저장해둔다. 이 빈은 HTTP 요청 당 하나씩 생성되므로, uuid를 저장해두면 다른 HTTP 요청과 구분할 수 있다.
- 이 빈이 소멸되는 시점에 @PreDestroy를 사용해서 종료 메시지를 남긴다.
- requestURL은 이 빈이 생성되는 시점에는 알 수 없으므로, 외부에서 setter로 입력 받는다.

<img width="1317" alt="스크린샷 2023-01-07 오후 5 24 55" src="https://user-images.githubusercontent.com/96857599/211141284-3f281a7c-a318-4a3a-b570-97fe186dd3ad.png">

<img width="1317" alt="스크린샷 2023-01-07 오후 5 24 22" src="https://user-images.githubusercontent.com/96857599/211141263-d0beb5f5-be5d-4e2b-bcf6-16bc0a4c3f2a.png">
- 로거가 잘 작동하는지 확인하는 테스트용 컨트롤러다. 
- 여기서 HttpServletRequest를 통해서 요청 URL을 받았다.
	- requestURL 값 http://localhost:8080/log-demo
- 이렇게 받은 requestURL 값을 myLogger에 저장해둔다. myLogger는 HTTP 요청 당 각각 구분되므로 다른 HTTP 요청 때문에 값이 섞이는 걱정은 하지 않아도 된다.
- 컨트롤러에서 controller test라는 로그를 남긴다.

> 참고: requestURL을 MyLogger에 저장하는 부분은 컨트롤러 보다는 공통 처리가 가능한 스프링 인터셉터나 서블릿 필터 같은 곳을 활용하는 것이 좋다. 여기서는 예제를 단순화하고, 아직 스프링 인터셉터를 학습하지 않은 분들을 위해서 컨트롤러를 사용했다. 스프링 웹에 익숙하다면 인터셉터를 사용해서 구현해보자.

<img width="1317" alt="스크린샷 2023-01-07 오후 5 24 33" src="https://user-images.githubusercontent.com/96857599/211141267-b232e5e4-fc10-426b-b852-8ae0208809c3.png">
- 비즈니스 로직이 있는 서비스 계층에서도 로그를 출력해보자.
- 여기서 중요한점이 있다. request scope를 사용하지 않고 파라미터로 이 모든 정보를 서비스 계층에 넘긴다면, 파라미터가 많아서 지저분해진다. 더 문제는 requestURL 같은 웹과 관련된 정보가 웹과 관련없는 서비스 계층까지 넘어가게 된다. 웹과 관련된 부분은 컨트롤러까지만 사용해야 한다. 서비스 계층은 웹 기술에 종속되지 않고, 가급적 순수하게 유지하는 것이 유지보수 관점에서 좋다.
- request scope의 MyLogger 덕분에 이런 부분을 파라미터로 넘기지 않고, MyLogger의 멤버변수에 저장해서 코드와 계층을 깔끔하게 유지할 수 있다.



- 위 코드를 실행하면 당연히 오류가 생긴다. request scope에서는 클라이언트의 request를 받은 순간 생명 주기가 시작인데, 현재는 request를 받지 않았다.
<img width="1317" alt="스크린샷 2023-01-07 오후 5 24 06" src="https://user-images.githubusercontent.com/96857599/211141252-9563908e-ecd4-464b-800c-c6f506698e14.png">

```오류 메세지
  Error creating bean with name 'myLogger': Scope 'request' is not active for the
  current thread; consider defining a scoped proxy for this bean if you intend to
  refer to it from a singleton;
```
	
### 스코프와 Provider
	
- ObjectProvider을 사용한다. (MyLogger을 받는게 아니라 MyLogger를 받을 수 있는 제공자를 주입받음)
<img width="1432" alt="스크린샷 2023-01-07 오후 7 03 57" src="https://user-images.githubusercontent.com/96857599/211144922-b29a792f-1a54-4d79-9001-bede324df1fe.png">
<img width="1432" alt="스크린샷 2023-01-07 오후 7 06 57" src="https://user-images.githubusercontent.com/96857599/211145017-0e3563b8-2b42-484b-bb4c-c2693bfebf69.png">
- 로그 (4개의 요청이 들어온 것을 확인할 수 있다.)
<img width="913" alt="스크린샷 2023-01-07 오후 7 08 40" src="https://user-images.githubusercontent.com/96857599/211145086-f8b6a628-3898-4c0b-9388-b908d9d3ff3f.png">

- ObjectProvider 덕분에 ObjectProvider.getObject()를 호출하는 시점까지 request scope 빈의 생성을 지연할 수 있다.(스프링 컨테이너에게 요청하는 것을 지연시킬 수 있음)
- ObjectProvider.getObject()를 호출하시는 시점에는 HTTP 요청이 진행중이므로 request scope 빈의 생성이 정상 처리된다.
- ObjectProvider.getObject()를 LogDemoController, LogDemoService에서 각각 한번씩 따로 호출해도 같은 HTTP 요청이면 같은 스프링 빈이 반환된다! 
	
#### 정리
LogDemoController에 있는 ObjectProvider.getObject()는 MyLogger빈을 생성하고LogDemoService에 있는 ObjectProvider.getObject()는 스프링컨테이너에 이미 생성된 MyLogger빈을 반환한다고 하셨는데, 그 이유가 같은 http요청에 대해서는 http요청이 끝나기 전까지 동일한 request scope bean이 사용되기때문
	
	
1. HTTP가 처음 요청 받으면 LogDemoController에 있는 ObjectProvider.getObject()에서 MyLogger 빈을 생성한다.
2. 이때, MyLogger에 있는 @PostConstruct init 메소드가 실행된다. -> uuid랑 HTTP request랑 묶음.(setRequestURL())
3. myLoggerd에서 log를 찍을 땐 이미 uuid와 requestURL이 있는 상태
4. logig() 실행
5. @PreDestroy close() 메소드가 실행
-> request scope bean이 사용되기 때문에 HTTP 요청이 들어오고 끝날 때까지 하나의 MyLogger 빈을 사용하게 됨. 


### 스코프와 프록시
	
<img width="1289" alt="스크린샷 2023-01-07 오후 7 38 23" src="https://user-images.githubusercontent.com/96857599/211146112-d7201e0a-235a-4376-ad26-552767a0745c.png">
<img width="1289" alt="스크린샷 2023-01-07 오후 7 38 47" src="https://user-images.githubusercontent.com/96857599/211146129-55ae702a-3b68-4429-92bb-9d33dd707f18.png">

<img width="1289" alt="스크린샷 2023-01-07 오후 7 38 36" src="https://user-images.githubusercontent.com/96857599/211146121-fcf4a3a9-0984-4bea-b3e4-312ea29853ea.png">

```
@Component
@Scope(value = "request", proxyMode = ScopedProxyMode.TARGET_CLASS)
public class MyLogger {
}
```
- 여기가 핵심이다. proxyMode = ScopedProxyMode.TARGET_CLASS 를 추가해주자. 
	- 적용 대상이 인터페이스가 아닌 클래스면 TARGET_CLASS 를 선택
	- 적용 대상이 인터페이스면 INTERFACES 를 선택
- 이렇게 하면 MyLogger의 가짜 프록시 클래스를 만들어두고 HTTP request와 상관 없이 가짜 프록시 클래스를 다른 빈에 미리 주입해 둘 수 있다.

입력
<img width="594" alt="스크린샷 2023-01-07 오후 7 42 48" src="https://user-images.githubusercontent.com/96857599/211146280-40719c66-d513-4fef-ac5f-a618009fafcc.png">
출력 
<img width="953" alt="스크린샷 2023-01-07 오후 7 42 33" src="https://user-images.githubusercontent.com/96857599/211146267-5cb1def8-1099-4e6f-b316-e5ec076df305.png">

	
#### CGLIB라는 라이브러리로 내 클래스를 상속 받은 가짜 프록시 객체를 만들어서 주입한다.
- @Scope 의 proxyMode = ScopedProxyMode.TARGET_CLASS) 를 설정하면 스프링 컨테이너는 CGLIB 라는 바이트코드를 조작하는 라이브러리를 사용해서, MyLogger를 상속받은 가짜 프록시 객체를 생성한다.
- 결과를 확인해보면 우리가 등록한 순수한 MyLogger 클래스가 아니라 MyLogger$ $EnhancerBySpringCGLIB 이라는 클래스로 만들어진 객체가 대신 등록된 것을 확인할 수 있다. 그리고 스프링 컨테이너에 "myLogger"라는 이름으로 진짜 대신에 이 가짜 프록시 객체를 등록한다.
- ac.getBean("myLogger", MyLogger.class)로 조회해도 프록시 객체가 조회되는 것을 확인할 수 있다.
- 그래서 의존관계 주입도 이 가짜 프록시 객체가 주입된다.
	
<img width="553" alt="스크린샷 2023-01-07 오후 7 44 15" src="https://user-images.githubusercontent.com/96857599/211146326-7163b857-6c87-43fb-b033-f591e84b3bce.png">

	
#### 가짜 프록시 객체는 요청이 오면 그때 내부에서 진짜 빈을 요청하는 위임 로직이 들어있다.
- 가짜 프록시 객체는 내부에 진짜 myLogger를 찾는 방법을 알고 있다.
- 클라이언트가 myLogger.logic()을 호출하면 사실은 가짜 프록시 객체의 메서드를 호출한 것이다. 
- 가짜 프록시 객체는 request 스코프의 진짜 myLogger.logic()를 호출한다.
- 가짜 프록시 객체는 원본 클래스를 상속 받아서 만들어졌기 때문에 이 객체를 사용하는 클라이언트 입장에서는 사실 원본인지 아닌지도 모르게, 동일하게 사용할 수 있다(다형성)
	
	
#### 동작 정리
- CGLIB라는 라이브러리로 내 클래스를 상속 받은 가짜 프록시 객체를 만들어서 주입한다.
- 이 가짜 프록시 객체는 실제 요청이 오면 그때 내부에서 실제 빈을 요청하는 위임 로직이 들어있다.
- 가짜 프록시 객체는 실제 request scope와는 관계가 없다. 그냥 가짜이고, 내부에 단순한 위임 로직만 있고, 싱글톤처럼 동작한다.

	
#### 특징 정리
- 프록시 객체 덕분에 클라이언트는 마치 싱글톤 빈을 사용하듯이 편리하게 request scope를 사용할 수 있다.
- 사실 Provider를 사용하든, 프록시를 사용하든 핵심 아이디어는 **진짜 객체 조회를 꼭 필요한 시점까지 지연처리 한다는 점이다**.
- 단지 애노테이션 설정 변경만으로 원본 객체를 프록시 객체로 대체할 수 있다. 이것이 바로 **다형성과 DI 컨테이너**가 가진 큰 강점이다.
- 꼭 웹 스코프가 아니어도 프록시는 사용할 수 있다.

	
#### 주의점
- 마치 싱글톤을 사용하는 것 같지만 다르게 동작하기 때문에 결국 주의해서 사용해야 한다.
- 이런 특별한 scope는 꼭 필요한 곳에만 최소화해서 사용하자, 무분별하게 사용하면 유지보수하기 어려워진다.




	
	
	
	
	
	
	
	
	
	
	
	
	
	
