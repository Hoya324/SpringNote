# 실전! 스프링 부트와 JPA 활용1 - 웹 애플리케이션 개발

<img width="1054" alt="스크린샷 2023-06-14 오후 3 21 10" src="https://github.com/Hoya324/SpringNote/assets/96857599/9976fb42-4149-416a-aa0b-8c3637de862e">

### 라이브러리 살펴보기

**gradle 의존관계 보기**

`./gradlew dependencies —configuration compileClasspath`

**스프링 부트 라이브러리 살펴보기**
- spring-boot-starter-web 
   - spring-boot-starter-tomcat: 톰캣 (웹서버) 
   - spring-webmvc: 스프링 웹 MVC
- spring-boot-starter-thymeleaf: 타임리프 템플릿 엔진(View) 
- spring-boot-starter-data-jpa
  - spring-boot-starter-aop 
  - spring-boot-starter-jdbc
    - HikariCP 커넥션 풀 (부트 2.0 기본)
  - hibernate + JPA: 하이버네이트 + JPA 
  - spring-data-jpa: 스프링 데이터 JPA
- spring-boot-starter(공통): 스프링 부트 + 스프링 코어 + 로깅 
  - spring-boot
    - spring-core 
  - spring-boot-starter-logging
    - logback, slf4j
    
**테스트 라이브러리**
- spring-boot-starter-test
  - junit: 테스트 프레임워크
  - mockito: 목 라이브러리
  - assertj: 테스트 코드를 좀 더 편하게 작성하게 도와주는 라이브러리 
  - spring-test: 스프링 통합 테스트 지원

**핵심 라이브러리 **
- 스프링 MVC 
- 스프링 ORM
- JPA, 하이버네이트
- 스프링 데이터 JPA 

**기타 라이브러리**
- H2 데이터베이스 클라이언트
- 커넥션 풀: 부트 기본은 HikariCP
- WEB(thymeleaf)
- 로깅 SLF4J & LogBack
- 테스트


### View 환경 설정

**thymeleaf 템플릿 엔진**
- [thymeleaf 공식 사이트](https://www.thymeleaf.org/)
- [스프링 공식 튜토리얼](https://spring.io/guides/gs/serving-web-content/)
- [스프링부트 메뉴얼](https://docs.spring.io/spring-boot/docs/2.1.6.RELEASE/reference/html/ boot-features-developing-web-applications.html#boot-features-spring-mvc-template- engines)

> html 파일을 컴파일만 해주면 서버 재시작 없이 View 파일 변경이 가능하다.
> 
> `implementation 'org.springframework.boot:spring-boot-devtools'`

<img width="1326" alt="스크린샷 2023-06-15 오후 4 50 45" src="https://github.com/Hoya324/SpringNote/assets/96857599/10a15c51-3637-4709-a048-e2676147f24b">

- 인텔리J 컴파일 방법: 메뉴 build Recompile
<img width="346" alt="스크린샷 2023-06-15 오후 4 52 29" src="https://github.com/Hoya324/SpringNote/assets/96857599/3573c4a4-52e4-4a20-845c-5928187094d1">


### h2 데이터베이스 실행
<img width="647" alt="스크린샷 2023-06-15 오후 5 06 07" src="https://github.com/Hoya324/SpringNote/assets/96857599/8a70f69d-ff62-4d16-bb8f-37c5679c7945">

- 데이터베이스 파일 생성 방법
- jdbc:h2:~/jpaShop (최소 한번)
   - ~/jpaShop.mv.db 파일 생성 확인
   - 이후 부터는 jdbc:h2:tcp://localhost/~/jpaShop 이렇게 접속

<img width="803" alt="스크린샷 2023-06-15 오후 5 13 13" src="https://github.com/Hoya324/SpringNote/assets/96857599/38c199c2-ab0f-4411-8947-be14249e66ea">

<img width="803" alt="스크린샷 2023-06-15 오후 5 12 20" src="https://github.com/Hoya324/SpringNote/assets/96857599/7c330f42-74db-40ac-8f7b-4e7a51f02219">

### JPA와 DB 설정, 동작확인

`main/resources/application.yml`

<img width="987" alt="스크린샷 2023-06-16 오후 12 46 53" src="https://github.com/Hoya324/SpringNote/assets/96857599/6e1c3533-223b-409e-8d6c-e978e5aa8d47">

- jdbc:h2:tcp://localhost/~/jpaShop;MVCC=TRUE
   - MVCC=TRUE 넣으면 여러 개가 접근했을 때 빠르게 처리

- spring.jpa.hibernate.ddl-auto: create
   - 이 옵션은 애플리케이션 실행 시점에 테이블을 drop 하고, 다시 생성한다.

> 참고: 모든 로그 출력은 가급적 로거를 통해 남겨야 한다.
>
> show_sql : 옵션은 System.out 에 하이버네이트 실행 SQL을 남긴다.
>
> org.hibernate.SQL : 옵션은 logger를 통해 하이버네이트 실행 SQL을 남긴다.


> 주의! application.yml 같은 yml 파일은 띄어쓰기(스페이스) 2칸으로 계층을 만듭니다. 따라서 띄어쓰 기 2칸을 필수로 적어주어야 합니다.
> 
> 예를 들어서 아래의 datasource 는 spring: 하위에 있고 앞에 띄어쓰기 2칸이 있으므로 spring.datasource 가 됩니다. 다음 코드에 주석으로 띄어쓰기를 적어두었습니다.


**실제 동작하는지 확인하기**

**회원 엔티티**

<img width="987" alt="스크린샷 2023-06-16 오후 12 49 06" src="https://github.com/Hoya324/SpringNote/assets/96857599/8ef7685f-a003-4845-932e-ace3f9643b0c">

**회원 리포지토리**

<img width="1327" alt="스크린샷 2023-06-16 오후 1 10 59" src="https://github.com/Hoya324/SpringNote/assets/96857599/a08fe116-1852-4ca7-9641-e39ee4ac0171">

**테스트**

<img width="1327" alt="스크린샷 2023-06-16 오후 1 11 12" src="https://github.com/Hoya324/SpringNote/assets/96857599/774fe1dd-cfc8-4d30-9f76-7fc909f28b8b">


- 위 상황에서 테스트 실행 시 오류 발생

` No EntityManager with actual transaction available for current thread - cannot reliably process 'persist' call`


**오류원인**
- transaction이 지금 없다.
- EntityManager을 통한 모든 데이터 명령은 항상 transaction 안에서 일어나야한다. (매우 중요) ⭐️⭐️⭐️ ->  추가 공부

만약 데이터베이스의 데이터를 수정하는 도중에 예외가 발생된다면 어떻게 해야 할까? DB의 데이터들은 수정이 되기 전의 상태로 다시 되돌아가져야 하고, 다시 수정 작업이 진행되어야 할 것이다.
이렇듯 여러 작업을 진행하다가 문제가 생겼을 경우 이전 상태로 롤백하기 위해 사용되는 것이 트랜잭션(Transaction) 이다.

[transaction 기술](https://mangkyu.tistory.com/154)
[transaction의 이해](https://velog.io/@byeongju/Spring-Transaction%EC%97%90-%EB%8C%80%ED%95%9C-%EA%B8%B0%EB%B3%B8-%EA%B0%9C%EB%85%90)

- @Transactional을 주입했더니 해결됐다.

<img width="1254" alt="스크린샷 2023-06-16 오후 1 22 48" src="https://github.com/Hoya324/SpringNote/assets/96857599/f8bdce25-6a64-4194-a5ee-39bb0fed6d19">

- @Transactional는 테스트에서 테스트가 끝나면 모두 Rollback 해버리기 때문에, 일반 환경에서는 상관없지만, 테스트에선 @Rollback(value = false) 추가

<img width="906" alt="스크린샷 2023-06-16 오후 1 34 42" src="https://github.com/Hoya324/SpringNote/assets/96857599/4eeb575a-04f3-49a7-ac0e-f24bffeabf96">

- 같은 트랜잭션 안에 저장하고 조회하 영속성 컨텍스트(persistent context:엔티티를 영구 저장하는 환경)이 같다.
- 같은 영속성 컨텍스트 안에서는 id 값이 같으면 같은 것으로 인식

<img width="1278" alt="스크린샷 2023-06-16 오후 1 44 53" src="https://github.com/Hoya324/SpringNote/assets/96857599/0399d104-93a2-4aec-8cdf-0d51a3d18c34">

[영속성 컨텍스트 이해](https://velog.io/@seongwon97/Spring-Boot-%EC%98%81%EC%86%8D%EC%84%B1-%EC%BB%A8%ED%85%8D%EC%8A%A4%ED%8A%B8Persistence-Context)

- jar 빌드해서 동작 확인

<img width="762" alt="스크린샷 2023-06-16 오후 1 48 59" src="https://github.com/Hoya324/SpringNote/assets/96857599/ec81631b-2218-4308-8477-f63a2ee71a96">

**쿼리 파라미터 로그 남기기 - 스프링 부트 3.0**
스프링 부트 3.0 이상을 사용하면 라이브러리 버전을 1.9.0 이상을 사용해야 한다.

`implementation 'com.github.gavlyukovskiy:p6spy-spring-boot-starter:1.9.0'`

- 개발, 공부 단계에서는 괜찮지만, 실제 배포 단계에서는 성능 저하 문제가 생길 수 있기 때문에 고민해야한다.



**도메인 분석 설계**

**요구사항 분석**

<img width="499" alt="스크린샷 2023-06-16 오후 2 16 33" src="https://github.com/Hoya324/SpringNote/assets/96857599/4b22ff3c-c935-453e-bb3d-e7497d6b9f23">

**실제 동작하는 화면을 먼저 확인한다.**
기능 목록
- 회원 기능 
   - 회원 등록
   - 회원 조회 
- 상품 기능
   - 상품 등록
   - 상품 수정
   - 상품 조회
- 주문 기능 
   - 상품 주문
   - 주문 내역 조회
   - 주문 취소
- 기타 요구사항
   - 상품은 재고 관리가 필요하다.
   - 상품의 종류는 도서, 음반, 영화가 있다. 
   - 상품을 카테고리로 구분할 수 있다.
   - 상품 주문시 배송 정보를 입력할 수 있다.


### 도메인 모델과 테이블 설계

<img width="535" alt="스크린샷 2023-06-16 오후 2 15 58" src="https://github.com/Hoya324/SpringNote/assets/96857599/28f2fc6a-e46a-4eca-a5cc-6f4081e25929">

**회원, 주문, 상품의 관계**: 회원은 여러 상품을 주문할 수 있다. 그리고 한 번 주문할 때 여러 상품을 선택할 수 있으므로 주문과 상품은 다대다 관계다. 하지만 이런 다대다 관계는 관계형 데이터베이스는 물론이고 엔티 티에서도 거의 사용하지 않는다. 따라서 그림처럼 주문상품이라는 엔티티를 추가해서 다대다 관계를 일대 다, 다대일 관계로 풀어냈다.

**상품 분류**: 상품은 도서, 음반, 영화로 구분되는데 상품이라는 공통 속성을 사용하므로 상속 구조로 표현했다.


**회원 엔티티 분석**

<img width="494" alt="스크린샷 2023-06-16 오후 3 15 24" src="https://github.com/Hoya324/SpringNote/assets/96857599/150f9f3a-223f-4941-9975-4577c5db7d2f">

**회원(Member)**: 이름과 임베디드 타입인 주소( Address ), 그리고 주문( orders ) 리스트를 가진다.

**주문(Order)**: 한 번 주문시 여러 상품을 주문할 수 있으므로 주문과 주문상품( OrderItem )은 일대다 관계 다. 주문은 상품을 주문한 회원과 배송 정보, 주문 날짜, 주문 상태( status )를 가지고 있다. 주문 상태는 열 거형을 사용했는데 주문( ORDER ), 취소( CANCEL )을 표현할 수 있다.

**주문상품(OrderItem)**: 주문한 상품 정보와 주문 금액( orderPrice ), 주문 수량( count ) 정보를 가지고 있다. (보통 OrderLine , LineItem 으로 많이 표현한다.)

**상품(Item)**: 이름, 가격, 재고수량( stockQuantity )을 가지고 있다. 상품을 주문하면 재고수량이 줄어든 다. 상품의 종류로는 도서, 음반, 영화가 있는데 각각은 사용하는 속성이 조금씩 다르다.

**배송(Delivery)**: 주문시 하나의 배송 정보를 생성한다. 주문과 배송은 일대일 관계다. 카테고리(Category): 상품과 다대다 관계를 맺는다. parent , child 로 부모, 자식 카테고리를 연결한
다.

**주소(Address)**: 값 타입(임베디드 타입)이다. 회원과 배송(Delivery)에서 사용한다.

> 참고: 회원이 주문을 하기 때문에, 회원이 주문리스트를 가지는 것은 얼핏 보면 잘 설계한 것 같지만, 객체 세 상은 실제 세계와는 다르다. 실무에서는 회원이 주문을 참조하지 않고, 주문이 회원을 참조하는 것으로 충분 하다. 여기서는 일대다, 다대일의 양방향 연관관계를 설명하기 위해서 추가했다.

**회원 테이블 분석**

<img width="498" alt="스크린샷 2023-06-16 오후 3 17 01" src="https://github.com/Hoya324/SpringNote/assets/96857599/c3e3f907-edf7-4255-af72-4708eca2028b">

**MEMBER**: 회원 엔티티의 Address 임베디드 타입 정보가 회원 테이블에 그대로 들어갔다. 이것은 DELIVERY 테이블도 마찬가지다.

**ITEM**: 앨범, 도서, 영화 타입을 통합해서 하나의 테이블로 만들었다. DTYPE 컬럼으로 타입을 구분한다.

> 참고: 테이블명이 ORDER 가 아니라 ORDERS 인 것은 데이터베이스가 order by 때문에 예약어로 잡고 있
는 경우가 많다. 그래서 관례상 ORDERS 를 많이 사용한다.

> **참고: 실제 코드에서는 DB에 소문자 + _(언더스코어) 스타일을 사용하겠다.**
> 
> 데이터베이스 테이블명, 컬럼명에 대한 관례는 회사마다 다르다. 보통은 대문자 + _(언더스코어)나 소문자 + _(언더스코어) 방식 중에 하나를 지정해서 일관성 있게 사용한다. 강의에서 설명할 때는 객체와 차이를 나타내기 위해 데이터베이스 테이블, 컬럼명은 대문자를 사용했지만, **실제 코드에서는 소문자 + _(언더스코 어) 스타일을 사용하겠다.**



#### 연관관계 매핑 분석

**회원과 주문**: 일대다 , 다대일의 양방향 관계다. 따라서 연관관계의 주인을 정해야 하는데, 외래 키가 있는 주문을 연관관계의 주인으로 정하는 것이 좋다. 그러므로 Order.member 를 ORDERS.MEMBER_ID 외래 키와 매핑한다.

**주문상품과 주문**: 다대일 양방향 관계다. 외래 키가 주문상품에 있으므로 주문상품이 연관관계의 주인이다. 그러므로 OrderItem.order 를 ORDER_ITEM.ORDER_ID 외래 키와 매핑한다.

**주문상품과 상품**: 다대일 단방향 관계다. OrderItem.item 을 ORDER_ITEM.ITEM_ID 외래 키와 매핑한다.

**주문과 배송**: 일대일 양방향 관계다. Order.delivery 를 ORDERS.DELIVERY_ID 외래 키와 매핑한다. 

**카테고리와 상품**: @ManyToMany 를 사용해서 매핑한다.(실무에서 @ManyToMany는 사용하지 말자. 여기서는 다대다 관계를 예제로 보여주기 위해 추가했을 뿐이다)

> 참고: 외래 키가 있는 곳을 연관관계의 주인으로 정해라.(연관관계의 주인 쪽에 값을 세팅해줘야 값이 바뀐다. 반대편 쪽(거울)은 조회용)
> 
> 연관관계의 주인은 단순히 외래 키를 누가 관리하냐의 문제이지 비즈니스상 우위에 있다고 주인으로 정하면
안된다.. 예를 들어서 자동차와 바퀴가 있으면, 일대다 관계에서 항상 다쪽에 외래 키가 있으므로 외래 키가 있는 바퀴를 연관관계의 주인으로 정하면 된다. 물론 자동차를 연관관계의 주인으로 정하는 것이 불가능 한 것은 아니지만, 자동차를 연관관계의 주인으로 정하면 자동차가 관리하지 않는 바퀴 테이블의 외래 키 값이 업데이트 되므로 관리와 유지보수가 어렵고, 추가적으로 별도의 업데이트 쿼리가 발생하는 성능 문제도 있다. 자세한 내용은 JPA 기본편을 참고하자.


### 엔티티 클래스 개발

- 예제에서는 설명을 쉽게하기 위해 엔티티 클래스에 Getter, Setter를 모두 열고, 최대한 단순하게 설계 
- 실무에서는 가급적 Getter는 열어두고, Setter는 꼭 필요한 경우에만 사용하는 것을 추천

> 참고: 이론적으로 Getter, Setter 모두 제공하지 않고, 꼭 필요한 별도의 메서드를 제공하는게 가장 이상적 이다. 하지만 실무에서 엔티티의 데이터는 조회할 일이 너무 많으므로, Getter의 경우 모두 열어두는 것이 편리하다. Getter는 아무리 호출해도 호출 하는 것 만으로 어떤 일이 발생하지는 않는다. 하지만 Setter는 문제가 다르다. Setter를 호출하면 데이터가 변한다. Setter를 막 열어두면 가까운 미래에 엔티티가 도대체 왜 변경되는지 추적하기 점점 힘들어진다. 그래서 엔티티를 변경할 때는 Setter 대신에 변경 지점이 명확하도록 변경을 위한 비즈니스 메서드를 별도로 제공해야 한다.



