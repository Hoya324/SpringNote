# 실전! 스프링 부트와 JPA 활용1 - 웹 애플리케이션 개발

## 프로젝트 환경설정

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



## 도메인 분석 설계

### 요구사항 분석

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

**회원 엔티티, 주문 엔티티**

> 참고: 엔티티의 식별자는 id 를 사용하고 PK 컬럼명은 member_id 를 사용했다. 엔티티는 타입(여기서는 Member )이 있으므로 id 필드만으로 쉽게 구분할 수 있다. 테이블은 타입이 없으므로 구분이 어렵다. 그리 고 테이블은 관례상 테이블명 + id 를 많이 사용한다. 참고로 객체에서 id 대신에 memberId 를 사용해도 된다. 중요한 것은 일관성이다.


- Member 도메인 객체에 Adress(@Embeddable-내장 타입이라는 뜻) 연결

<img width="1147" alt="스크린샷 2023-06-18 오후 2 53 14" src="https://github.com/Hoya324/SpringNote/assets/96857599/bd1e28eb-b7f1-4560-94c0-594175ea1cbb">

<img width="1147" alt="스크린샷 2023-06-18 오후 2 52 47" src="https://github.com/Hoya324/SpringNote/assets/96857599/1d49f24d-f48d-4b64-86d8-ba9729948aa8">

- Member는 Order에 일대다 관계, Order는 Member에 다대일 관계
- 이때, foreign key를 가지고 있는 Order를 연관관계의 주인으로 정하고, Member에 @OneToMany(mappedBy = "member")를 통해 Order의 member 인스턴스의 거울(?)정도라고 표시한다.

<img width="944" alt="스크린샷 2023-06-18 오후 4 19 42" src="https://github.com/Hoya324/SpringNote/assets/96857599/8d7cf93c-6993-4e10-8782-36d365f1087f">

<img width="944" alt="스크린샷 2023-06-18 오후 4 19 52" src="https://github.com/Hoya324/SpringNote/assets/96857599/166c713d-b6f7-4265-a915-fdd1a6d0a853">

**주소값 타입(Address)에서 주의할 점**

<img width="944" alt="스크린샷 2023-06-18 오후 6 08 20" src="https://github.com/Hoya324/SpringNote/assets/96857599/9ab50f4c-474e-4102-ac35-077c200b29ab">

> 참고: 값 타입은 변경 불가능하게 설계해야 한다.
> 
> @Setter 를 제거하고, 생성자에서 값을 모두 초기화해서 변경 불가능한 클래스를 만들자. JPA 스펙상 엔티
티나 임베디드 타입( @Embeddable )은 자바 기본 생성자(default constructor)를 public 또는 protected 로 설정해야 한다. public 으로 두는 것 보다는 protected 로 설정하는 것이 그나마 더 안전 하다.
> JPA가 이런 제약을 두는 이유는 JPA 구현 라이브러리가 객체를 생성할 때 리플랙션 같은 기술을 사용할 수 있도록 지원해야 하기 때문이다.

#### colum까지 만드는 전체 코드
#### @XTOOne 관계에 모두 지연로딩으로 설정 @XTOOne(fetch = FetchType.LAZY) 
#### cascade 설정 cascade = CascadeType.ALL
#### 연관관계 메서드 추가

- Cascade로 저장(persist), 삭제될 때 한번에 가능
- 조건:
   - Cascade되는 엔티티와 Cascade를 설정하는 엔티티의 라이프사이클이 동일하거나 비슷해야한다.
   - Cascade되는 엔티티가 Cascade를 설정하는 엔티티에서만 사용되어야 한다.
   - 해당 값을 참조중인 레코드들을 모두 종속적으로 수정/삭제
[Cascade 정리](https://hongchangsub.com/jpa-cascade-2/)


**Member-회원 엔티티**

```java
package jpaBook.jpaShop.domain;

import jakarta.persistence.*;
import lombok.Getter;
import lombok.Setter;

import java.util.ArrayList;
import java.util.List;

@Entity
@Getter @Setter
public class Member {

    @Id @GeneratedValue
    @Column(name = "member_id")
    private Long id;

    private String name;

    @Embedded
    private Address address;

    @OneToMany(mappedBy = "member")
    private List<Order> orders = new ArrayList<>();
}

```

**Order-주문 엔티티**

```java
package jpaBook.jpaShop.domain;

import jakarta.persistence.*;
import lombok.Getter;
import lombok.Setter;


import java.time.LocalDateTime;
import java.util.ArrayList;
import java.util.List;

@Entity
@Table(name = "orders") // 테이블멸을 관례적으로 orders로 설정
@Getter @Setter
public class Order {

    @Id @GeneratedValue
    @Column(name = "order_id")
    private Long id;

    @ManyToOne(fetch = FetchType.LAZY, )
    @JoinColumn(name = "member_id") // foreign key
    private Member member;

    @OneToMany(mappedBy = "order", cascade = CascadeType.ALL)
    private List<OrderItem> orderItems = new ArrayList<>();

    @OneToOne(fetch = FetchType.LAZY, cascade = CascadeType.ALL)
    @JoinColumn(name = "delivery_id")
    private Delivery delivery;

    private LocalDateTime orderDate; // 주문 시간

    @Enumerated(EnumType.STRING)
    private OrderStatus status; // 주문 상태 [ORDER, CANCEL]

   //==연관관계 메서드==// -> 호출하는 쪽에 생성
    public void setMember(Member member) {
        this.member = member;
        member.getOrders().add(this);
    }

    public void addOrderItem(OrderItem orderItem) {
        orderItems.add(orderItem);
        orderItem.setOrder(this);
    }

    public void setDelivery(Delivery delivery) {
        this.delivery = delivery;
        delivery.setOrder(this );
    }

}

```

**OrderSatus-주문 상태**

```java
package jpaBook.jpaShop.domain;

public enum OrderStatus {
    ORDER,
    CANCEL
}

```

**OrderItem-주문상품 엔티티**

```java
package jpaBook.jpaShop.domain;


import jakarta.persistence.*;
import lombok.Getter;
import lombok.Setter;

@Entity
@Getter @Setter
public class OrderItem {

    @Id @GeneratedValue
    @Column(name = "order_item_id")
    private Long id;

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "item_id")
    private Item item;

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "order_id")
    private Order order;

    private int orderPrice; // 주문가격
    private int count; // 주문 수량
}

```

**Item-상품 엔티티**

```java
package jpaBook.jpaShop.domain;

import jakarta.persistence.*;
import lombok.Getter;
import lombok.Setter;

import java.util.ArrayList;
import java.util.List;

@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE) // 한 테이블에 몰아넣는 전략
@DiscriminatorColumn(name = "dtype")
@Getter @Setter
public class Item {

    @Id @GeneratedValue
    @Column(name = "item_id")
    private Long id;

    private String name;

    private int price;

    private int stockQuantity;

    // ManyToMany: 실무에서는 잘 사용하지 않지만, 예시를 위해 사용
    @ManyToMany(mappedBy = "items")
    private List<Category> categories = new ArrayList<>();

}

```

**Book-(상품-도서 엔티티), Album-(상품-음반 엔티티), Movie-(상품-영화 엔티티)**

```java
package jpaBook.jpaShop.domain.item;

import jakarta.persistence.DiscriminatorValue;
import jakarta.persistence.Entity;
import jpaBook.jpaShop.domain.Item;
import lombok.Getter;
import lombok.Setter;

@Entity
@DiscriminatorValue("B")
@Getter @Setter
public class Book extends Item {

    private String author;
    private String isbn;
}
```

```java
package jpaBook.jpaShop.domain.item;

import jakarta.persistence.DiscriminatorValue;
import jakarta.persistence.Entity;
import jpaBook.jpaShop.domain.Item;
import lombok.Getter;
import lombok.Setter;


@Entity
@DiscriminatorValue("A")
@Getter @Setter
public class Album extends Item {

    private String artist;
    private String etc;
}

```

```java
package jpaBook.jpaShop.domain.item;

import jakarta.persistence.DiscriminatorValue;
import jakarta.persistence.Entity;
import jpaBook.jpaShop.domain.Item;
import lombok.Getter;
import lombok.Setter;


@Entity
@DiscriminatorValue("M")
@Getter @Setter
public class Movie extends Item {

    private String director;
    private String actor;
}

```

**Delivery-배송 엔티티**

```java
package jpaBook.jpaShop.domain;

import jakarta.persistence.*;
import lombok.Getter;
import lombok.Setter;

@Entity
@Getter
@Setter
public class Delivery {

    @Id @GeneratedValue
    @Column(name = "delivery_id")
    private Long id;

    @OneToOne(mappedBy = "delivery", fetch = FetchType.LAZY)
    private Order order;

    @Embedded
    private Address address;

    // @Enumerated(EnumType.ORDINARY)는 인덱스로 찾기 때문에 중간에 추가되는 값이 생기면 문제가 생긴다.
    @Enumerated(EnumType.STRING)
    private DeliveryStatus status;


}

```

**DeliveryStatus-배송 상태**

```java
package jpaBook.jpaShop.domain;

public enum DeliveryStatus {
    READY, COMP
}

```

**Category-카테고리 엔티티**

```java
package jpaBook.jpaShop.domain;

import jakarta.persistence.*;
import lombok.Getter;
import lombok.Setter;

import java.util.ArrayList;
import java.util.List;

@Entity
@Getter @Setter
public class Category {

    @Id @GeneratedValue
    @Column(name = "category_id")
    private Long id;

    private String name;

    // ManyToMany: 실무에서는 잘 사용하지 않지만, 예시를 위해 사용
    @ManyToMany
    @JoinTable(name = "category_item",
            joinColumns = @JoinColumn(name = "category_id"),
            inverseJoinColumns = @JoinColumn(name = "item_id"))
    private List<Item> items = new ArrayList<>();

    // 카테고리 계층구조
    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "parent_id")
    private Category parent;

    @OneToMany(mappedBy = "parent")
    private List<Category> child = new ArrayList<>();

   //==연관관계 메서드==//
    public void addChildCategory(Category child) {
        this.child.add(child);
        child.setParent(this);
    }

}

```

> 참고: 실무에서는 @ManyToMany를 사용하지 말자
> 
>  @ManyToMany 는 편리한 것 같지만, 중간 테이블( CATEGORY_ITEM )에 컬럼을 추가할 수 없고, 세밀하게 쿼 리를 실행하기 어렵기 때문에 실무에서 사용하기에는 한계가 있다. 중간 엔티티( CategoryItem 를 만들고 @ManyToOne , @OneToMany 로 매핑해서 사용하자. 정리하면 다대다 매핑을 일대다, 다대일 매핑으로 풀어 내서 사용하자.


**Address-주소 값 타입**

```java
package jpaBook.jpaShop.domain;

import jakarta.persistence.Embeddable;
import lombok.Getter;

/**
 * 생성할 때만 값이 세팅되고, setter를 제공하지 않는 것이 좋은 설계
 */

@Embeddable // 내장 타입이라는 뜻
@Getter
public class Address {

    String city;
    String street;
    String zipcode;

    protected Address() {}

    public Address(String city, String street, String zipcode) {
        this.city = city;
        this.street = street;
        this.zipcode = zipcode;
    }
}

```

### 엔티티 설계시 주의점

**⭐️엔티티에는 가급적 Setter를 사용하지 말자**
Setter가 모두 열려있다. 변경 포인트가 너무 많아서, 유지보수가 어렵다. 나중에 리펙토링으로 Setter 제거


**⭐️모든 연관관계는 지연로딩으로 설정!**
- 즉시로딩( `EAGER` )은 예측이 어렵고, 어떤 SQL이 실행될지 추적하기 어렵다. 특히 JPQL을 실행할 때 N+1 문제가 자주 발생한다.
- 실무에서 모든 연관관계는 지연로딩( `LAZY` )으로 설정해야 한다.
- 연관된 엔티티를 함께 DB에서 조회해야 하면, fetch join 또는 엔티티 그래프 기능을 사용한다.
- @XToOne(OneToOne, ManyToOne) 관계는 기본이 즉시로딩(fetch = FetchType.EAGER)이므로 직접 지연(fetch = FetchType.LAZY)로딩으로 설정해야 한다.

**N+1 문제발생**
[JPA N+1 문제 해결 방법 및 실무 적용 팁](https://programmer93.tistory.com/83)
Order 클래스에서 Member과의 연관관계가 `@ManyToOne(fetch = FetchType.EAGER)`, 즉시로딩으로 되어있는 경우
- JPQL(JPA가 제공하는 쿼리)를 사용할 때, JPQL이 SQL로 바로 번역됨
`JPQL: SELECT o FROM order o;` -> `SQL: SELECT * FROM order`

- 첫번째 날린 쿼리(order 하나)가 가져온 결과가 N개면 N+1번 Member를 가져오기 위해서 쿼리가 날라오는 것이 N+1 문제

  
**컬렉션은 필드에서 초기화 하자.**
컬렉션은 필드에서 바로 초기화 하는 것이 안전하다.

- null 문제에서 안전하다.
- 하이버네이트는 엔티티를 영속화(persist) 할 때, 컬랙션을 감싸서 하이버네이트가 제공하는 내장 컬렉션으로 변경한다. 만약 `getOrders()`처럼 임의의 메서드에서 컬력션을 잘못 생성하면 하이버네이트 내부 메커니즘에 문제가 발생할 수 있다. 따라서 필드레벨에서 생성하는 것이 가장 안전하고, 코드도 간결하다.

```java
// Member 클래스
// @OneToMany(mappedBy = "member")
// private List<Order> orders = new ArrayList<>(); -> 이걸 바꾸지 못하게 하는게 Hibernate가 관리하는 대로 사용하는데 안전함

Member member = new Member();
System.out.println(member.getOrders().getClass());
em.persist(member); // db에 저장하겠다.
System.out.println(member.getOrders().getClass());

//출력 결과
class java.util.ArrayList
class org.hibernate.collection.internal.PersistentBag
```

**테이블, 컬럼명 생성 전략**
스프링 부트에서 하이버네이트 기본 매핑 전략을 변경해서 실제 테이블 필드명은 다름
- https://docs.spring.io/spring-boot/docs/2.1.3.RELEASE/reference/htmlsingle/#howto- configure-hibernate-naming-strategy
- http://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/ Hibernate_User_Guide.html#naming

하이버네이트 기존 구현: 엔티티의 필드명을 그대로 테이블의 컬럼명으로 사용 ( SpringPhysicalNamingStrategy )
스프링 부트 신규 설정 (엔티티(필드) 테이블(컬럼))
1. 카멜 케이스 언더스코어(memberPoint member_point)
2. .(점) _(언더스코어)
3. 대문자 소문자

**적용 2 단계**
1. 논리명 생성: 명시적으로 컬럼, 테이블명을 직접 적지 않으면 ImplicitNamingStrategy 사용
spring.jpa.hibernate.naming.implicit-strategy : 테이블이나, 컬럼명을 명시하지 않을 때 논리명
적용,
2. 물리명 적용:
spring.jpa.hibernate.naming.physical-strategy : 모든 논리명에 적용됨, 실제 테이블에 적용 (username usernm 등으로 회사 룰로 바꿀 수 있음)

**스프링 부트 기본 설정**
`spring.jpa.hibernate.naming.implicit-strategy:
org.springframework.boot.orm.jpa.hibernate.SpringImplicitNamingStrategy`
`spring.jpa.hibernate.naming.physical-strategy:
org.springframework.boot.orm.jpa.hibernate.SpringPhysicalNamingStrategy`

## 애플리케이션 구현 준비 

### 구현 요구사항

<img width="504" alt="스크린샷 2023-06-20 오후 2 57 01" src="https://github.com/Hoya324/SpringNote/assets/96857599/b50d04a7-7a34-4343-9352-3aead6518974">

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

**예제를 단순화 하기 위해 다음 기능은 구현X**
- 로그인과 권한 관리X
- 파라미터 검증과 예외 처리X
- 상품은 도서만 사용
- 카테고리는 사용X 배송 정보는 사용X

### 애플리케이션 아키텍처

<img width="525" alt="스크린샷 2023-06-20 오후 3 44 03" src="https://github.com/Hoya324/SpringNote/assets/96857599/677cf84e-8f59-4305-aad8-28227b5d4422">

**계층형 구조 사용**
- controller, web: 웹 계층
- service: 비즈니스 로직, 트랜잭션 처리
- repository: JPA를 직접 사용하는 계층, 엔티티 매니저 사용
- domain: 엔티티가 모여 있는 계층, 모든 계층에서 사용

**패키지 구조**
- jpabook.jpashop
   - domain
   - exception
   - repository
   - service
   - web

**개발 순서: 서비스, 리포지토리 계층을 개발하고, 테스트 케이스를 작성해서 검증, 마지막에 웹 계층 적용**

## 회원 도메인 개발

**구현 기능**
- 회원 등록
- 회원 목록 조회

**순서**
- 회원 엔티티 코드 다시 보기
- 회원 리포지토리 개발
- 회원 서비스 개발
- 회원 기능 테스트

### 회원 리포지토리 개발

**회원 리포지토리 코드**

```java
package jpaBook.jpaShop.repository;

import jakarta.persistence.EntityManager;
import jakarta.persistence.PersistenceContext;
import jpaBook.jpaShop.domain.Member;
import org.springframework.stereotype.Repository;

import java.util.List;

@Repository
public class MemberRepository {

    @PersistenceContext
    private EntityManager em;

    public void save(Member member) {
        em.persist(member);
    }

    public Member findOne(Long id) {
        return em.find(Member.class, id);
    }

    public List<Member> findAll() {
        return em.createQuery("select m from Member m", Member.class) // JPQL 작성-> em.createQuery(JPQL, 반환타입);
                .getResultList();
    }

    public List<Member> findByName(String name) {
        return em.createQuery("select m from Member m where m.name = :name", Member.class)
                .setParameter("name", name)
                .getResultList();
    }
}
```

**기술 설명**
- @Repository : 스프링 빈으로 등록, JPA 예외를 스프링 기반 예외로 예외 변환
- @PersistenceContext : 엔티티 메니저( EntityManager ) 주입
- @PersistenceUnit : 엔티티 메니터 팩토리( EntityManagerFactory ) 주입
  
**기능 설명**
- save()
- findOne()
- findAll()
- findByName()


### 회원 서비스 개발

**회원 서비스 코드**
```java

package jpabook.jpashop.service;
import jpabook.jpashop.domain.Member;
import jpabook.jpashop.repository.MemberRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;
import java.util.List;
@Service
@Transactional(readOnly = true)
public class MemberService {
   @Autowired
   MemberRepository memberRepository;
   /**
   * 회원가입
   */
   @Transactional //변경
   public Long join(Member member) { 
      validateDuplicateMember(member); //중복 회원 검증
      memberRepository.save(member);
      return member.getId();
   }
        
   private void validateDuplicateMember(Member member) {
       List<Member> findMembers = memberRepository.findByName(member.getName());
       if (!findMembers.isEmpty()) {
         throw new IllegalStateException("이미 존재하는 회원입니다."); 
       }
   }
   /**
   * 전체 회원 조회
   */
   public List<Member> findMembers() {
       return memberRepository.findAll();
   }

   public Member findOne(Long memberId) {
       return memberRepository.findOne(memberId);
   } 
}
```

**기술 설명**
- @Service
- @Transactional : 트랜잭션, 영속성 컨텍스트
   - readOnly=true : 데이터의 변경이 없는 읽기 전용 메서드에 사용, 영속성 컨텍스트를 플러시 하지 않으므로 약간의 성능 향상(읽기 전용에는 다 적용)
   - 데이터베이스 드라이버가 지원하면 DB에서 성능 향상
- @Autowired
   - 생성자 Injection 많이 사용, 생성자가 하나면 생략 가능

**기능 설명**
- join()
- findMembers()
- findOne()

> 참고: 실무에서는 검증 로직이 있어도 멀티 쓰레드 상황을 고려해서 회원 테이블의 회원명 컬럼에 유니크 제약 조건을 추가하는 것이 안전하다.

> 참고: 스프링 필드 주입 대신에 생성자 주입을 사용하자.
 
**필드 주입**
```java

public class MemberService {
   @Autowired
   MemberRepository memberRepository;
   ...
}
```

**생성자 주입**
```java
public class MemberService {
   private final MemberRepository memberRepository;
   
   public MemberService(MemberRepository memberRepository) {
      this.memberRepository = memberRepository;
   }
   ... 
}
```
- 생성자 주입 방식을 권장
- 변경 불가능한 안전한 객체 생성 가능
- 생성자가 하나면, @Autowired를 생략할 수 있다.
- final 키워드를 추가하면 컴파일 시점에 memberRepository를 설정하지 않는 오류를 체크할 수 있다. (보통 기본 생성자를 추가할 때 발견)


**lombok**
```java
@RequiredArgsConstructor
public class MemberService {
   private final MemberRepository memberRepository;
   ... 
}
```

> 참고: 스프링 데이터 JPA를 사용하면 EntityManager 도 주입 가능

```java
@Repository
@RequiredArgsConstructor
public class MemberRepository {
   private final EntityManager em;
   ... 
}
```

**MemberService 최종 코드**

```java
package jpaBook.jpaShop.service;

import jpaBook.jpaShop.domain.Member;
import jpaBook.jpaShop.repository.MemberRepository;
import lombok.RequiredArgsConstructor;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import java.util.List;

@Service
@Transactional(readOnly = true) // 스프링꺼 사용, 조회기능이 많기 때문에 default를 readOnly = true로 잡음
@RequiredArgsConstructor // 생성자 생성해줌
public class MemberService {

    private final MemberRepository memberRepository;

//    @Autowired -> 생성자 하나일 경우 필요없음
//    public MemberService(MemberRepository memberRepository) {
//        this.memberRepository = memberRepository;
//    }

    /**
     * 회원 가입
     */
    @Transactional // 조회가 아닌경우 @Transactional
    public Long join(Member member) {
        // 중복 처리
        validateDuplicateMember(member);
        memberRepository.save(member);
        // @GenerateValue로 인해 DB에 저장하지 않아도 조회할 수 있는 Key-Value 형태의 key id를 조회가능
        return member.getId();
    }

    private void validateDuplicateMember(Member member) {
        // 예외처리 -> 데이터베이스에서 UNIQUE 조건 걸어주는게 좋음
        List<Member> findMembers = memberRepository.findByName(member.getName());
        if (findMembers.size() > 0) {
            throw new IllegalStateException("이미 존재하는 회원입니다.");
        }
    }

    // 회원 전체 조회
    public List<Member> findMembers() {
        return memberRepository.findAll();
    }

    // 단건 조회
    public Member findOne(Long memberId) {
        return memberRepository.findOne(memberId);
    }
}
```

**MemberRepository EntityManager 주입**

```java
package jpaBook.jpaShop.repository;

import jakarta.persistence.EntityManager;
import jpaBook.jpaShop.domain.Member;
import lombok.RequiredArgsConstructor;
import org.springframework.stereotype.Repository;

import java.util.List;

@Repository
@RequiredArgsConstructor
public class MemberRepository {


    private final EntityManager em;

    public void save(Member member) {
        em.persist(member);
    }

    // 단건 조회
    public Member findOne(Long id) {
        return em.find(Member.class, id);
    }

    public List<Member> findAll() {
        return em.createQuery("select m from Member m", Member.class) // JPQL 작성-> em.createQuery(JPQL, 반환타입);
                .getResultList();
    }

    public List<Member> findByName(String name) {
        return em.createQuery("select m from Member m where m.name = :name", Member.class)
                .setParameter("name", name)
                .getResultList();
    }
}
```


### 회원 기능 테스트

**테스트 요구사항**
- 회원가입을 성공해야 한다.
- 회원가입 할 때 같은 이름이 있으면 예외가 발생해야 한다.


```java
package jpaBook.jpaShop.service;

import jakarta.persistence.EntityManager;
import jpaBook.jpaShop.domain.Member;
import jpaBook.jpaShop.repository.MemberRepository;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.annotation.Rollback;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.transaction.annotation.Transactional;

import static org.junit.Assert.*;

@RunWith(SpringRunner.class)
@SpringBootTest
@Transactional
//@Rollback(false) -> Transactional이 테스트에서는 데이터를 모두 날리기 때문에 Rollback 시키지 않고 확인하려면 입력해준다.
public class MemberServiceTest {

    @Autowired MemberService memberService;
    @Autowired MemberRepository memberRepository;

    @Test
    public void 회원가입() throws Exception {
        // given
        Member member = new Member();
        member.setName("kim");

        // when
        Long saveId = memberService.join(member);

        // then
//        em.flush();
        assertEquals(member, memberRepository.findOne(saveId));

     }

     @Test(expected = IllegalStateException.class)
     public void 중복_회원_예외() throws Exception {
         // given
         Member member1 = new Member();
         member1.setName("kim");
         Member member2 = new Member();
         member2.setName("kim");

         // when
         memberService.join(member1);
//         try {
//             memberService.join(member2); // 예외가 터져야함
//         } catch (IllegalStateException e) {
//             return;
//         }
         memberService.join(member2);



         // then
         fail("예외가 발생해야한다.");


      }


}
```


**기술 설명**
- @RunWith(SpringRunner.class) : 스프링과 테스트 통합
- @SpringBootTest : 스프링 부트 띄우고 테스트(이게 없으면 @Autowired 다 실패)
- @Transactional : 반복 가능한 테스트 지원, 각각의 테스트를 실행할 때마다 트랜잭션을 시작하고 **테스트가 끝나면 트랜잭션을 강제로 롤백** (이 어노테이션이 테스트 케이스에서 사용될 때만 롤백)

**기능 설명**
- 회원가입 테스트
- 중복 회원 예외처리 테스트

  
> 참고: 테스트 케이스 작성 고수 되는 마법: Given, When, Then (http://martinfowler.com/bliki/GivenWhenThen.html)
> 
> 이 방법이 필수는 아니지만 이 방법을 기본으로 해서 다양하게 응용하는 것을 권장한다.

**테스트 케이스를 위한 설정**

테스트는 케이스 격리된 환경에서 실행하고, 끝나면 데이터를 초기화하는 것이 좋다. 그런 면에서 메모리 DB를 사용하는 것이 가장 이상적이다.
추가로 테스트 케이스를 위한 스프링 환경과, 일반적으로 애플리케이션을 실행하는 환경은 보통 다르므로 설정 파일을 다르게 사용하자.
다음과 같이 간단하게 테스트용 설정 파일을 추가하면 된다.

`test/resources/application.yml`
```yml
spring:
#  datasource:
#    url: jdbc:h2:mem:test # 메모리 db
#    username: ng
#    password:
#    driver-class-name: org.h2.Driver
#
#  jpa:
#    hibernate:
#      ddl-auto: create-drop
#    properties:
#      hibernate:
#        show_sql: true
#        format_sql: true

logging.level:
  org.hibernate.SQL: debug
#  org.hibernate.orm.jdbc.bind: trace
```



### 상품 도메인 개발

**구현 기능**
- 상품 등록
- 상품 목록 조회
- 상품 수정
  
**순서**
- 상품 엔티티 개발(비즈니스 로직 추가)
- 상품 리포지토리 개발
- 상품 서비스 개발
- 상품 기능 테스트

### 상품 엔티티 개발(비즈니스 로직 추가) 

- **비지니스 로직에서 사용할 value들이 있는 엔티티에서 비지니스 로직을 짜는 것이 좋다.(가장 객체지향적인 방식)**

**상품 엔티티 코드**
```java
package jpaBook.jpaShop.domain;

import jakarta.persistence.*;
import jpaBook.jpaShop.exception.NotEnoughStockException;
import lombok.Getter;
import lombok.Setter;

import java.util.ArrayList;
import java.util.List;

@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE) // 한 테이블에 몰아넣는 전략
@DiscriminatorColumn(name = "dtype") // 각 상품들을 구분짓기
@Getter @Setter
public class Item {

    @Id @GeneratedValue
    @Column(name = "item_id")
    private Long id;

    private String name;

    private int price;

    private int stockQuantity;

    // ManyToMany: 실무에서는 잘 사용하지 않지만, 예시를 위해 사용
    @ManyToMany(mappedBy = "items")
    private List<Category> categories = new ArrayList<>();

    //==비지니스 로직=// - 상품 도메인 개발

    /**
     * stock(재고) 증가
     */
    public void addStock(int quantity) {
        this.stockQuantity += quantity;
    }

    /**
     * stock 감소
     */
    public void restStock(int quantity) {
        int restStock = this.stockQuantity - quantity;
        if (restStock < 0) {
            throw new NotEnoughStockException("need more stock");
        }
        this.stockQuantity = restStock;
    }
}
```

**예외 추가**
```java
package jpaBook.jpaShop.exception;

public class NotEnoughStockException extends RuntimeException{
    /**
     * RuntimeException 메서드 오버라이딩함
     */

    public NotEnoughStockException() {
        super();
    }

    public NotEnoughStockException(String message) {
        super(message);
    }

    public NotEnoughStockException(String message, Throwable cause) {
        super(message, cause);
    }

    public NotEnoughStockException(Throwable cause) {
        super(cause);
    }

}
```

**비즈니스 로직 분석**
- `addStock()` : 메서드는 파라미터로 넘어온 수만큼 재고를 늘린다. 이 메서드는 재고가 증가하거나 상품 주 문을 취소해서 재고를 다시 늘려야 할 때 사용한다.
- `removeStock()` : 메서드는 파라미터로 넘어온 수만큼 재고를 줄인다. 만약 재고가 부족하면 예외가 발생한 다. 주로 상품을 주문할 때 사용한다.
- 

### 상품 리포지토리 개발

**상품 리포지토리 코드**

```java
package jpaBook.jpaShop.repository;

import jakarta.persistence.EntityManager;
import jpaBook.jpaShop.domain.Item;
import lombok.RequiredArgsConstructor;
import org.springframework.stereotype.Repository;

import java.util.List;

@Repository
@RequiredArgsConstructor
public class ItemRepository {

    private final EntityManager em;

    public void save(Item item) {
        // jpa에서 저장하기 전까지는 id 값이 없기 때문에 새로 등록하는 것
        if (item.getId() == null) {
            em.persist(item);
        }
        // 이미 존재했던 item 업데이
        else {
            em.merge(item);
        }
    }

    public Item findOne(Long id) {
        return em.find(Item.class, id);
    }

    public List<Item> findAll() {
        return em.createQuery("select i from Item i", Item.class)
                .getResultList();
    }
}
```

**기능 설명**
- `save()`
   - id 가 없으면 신규로 보고 persist() 실행
   - id 가 있으면 이미 데이터베이스에 저장된 엔티티를 수정한다고 보고, merge() 를 실행, 자세한 내용은 뒤에 웹에서 설명(그냥 지금은 저장한다 정도로 생각하자)


### 상품 서비스 개발

**상품 서비스 코드**
```java
package jpaBook.jpaShop.service;

import jpaBook.jpaShop.domain.Item;
import jpaBook.jpaShop.repository.ItemRepository;
import lombok.RequiredArgsConstructor;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import java.util.List;

@Service
@Transactional(readOnly = true)
@RequiredArgsConstructor
public class ItemService {

    private final ItemRepository itemRepository;

    @Transactional
    public void saveItem(Item item) {
        itemRepository.save(item);
    }

    public List<Item> findItems() {
        return itemRepository.findAll();
    }

    public Item findOne(Long itemId) {
        return itemRepository.findOne(itemId);
    }
}
```

상품 서비스는 상품 리포지토리에 단순히 위임만 하는 클래스

### 주문 도메인 개발

**구현 기능**
- 상품 주문
- 주문 내역 조회
- 주문 취소

**순서**
- 주문 엔티티, 주문상품 엔티티 개발
- 주문 리포지토리 개발
- 주문 서비스 개발
- 주문 검색 기능 개발
- 주문 기능 테스트
  
### 주문, 주문상품 엔티티 개발 

주문 엔티티 개발

**주문 엔티티 코드**
```java
package jpaBook.jpaShop.domain;

import jakarta.persistence.*;
import lombok.Getter;
import lombok.Setter;


import java.time.LocalDateTime;
import java.util.ArrayList;
import java.util.List;

@Entity
@Table(name = "orders") // 테이블멸을 관례적으로 orders로 설정
@Getter @Setter
public class Order {

    @Id @GeneratedValue
    @Column(name = "order_id")
    private Long id;

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "member_id") // foreign key
    private Member member;

    @OneToMany(mappedBy = "order", cascade = CascadeType.ALL)
    private List<OrderItem> orderItems = new ArrayList<>();

    @OneToOne(fetch = FetchType.LAZY, cascade = CascadeType.ALL)
    @JoinColumn(name = "delivery_id")
    private Delivery delivery;

    private LocalDateTime orderDate; // 주문 시간

    @Enumerated(EnumType.STRING)
    private OrderStatus status; // 주문 상태 [ORDER, CANCEL]

    //==연관관계 메서드==// -> 호출하는 쪽에 생성
    public void setMember(Member member) {
        this.member = member;
        member.getOrders().add(this);
    }

    public void addOrderItem(OrderItem orderItem) {
        orderItems.add(orderItem);
        orderItem.setOrder(this);
    }

    public void setDelivery(Delivery delivery) {
        this.delivery = delivery;
        delivery.setOrder(this);
    }

    public static Order createOrder(Member member, Delivery delivery, OrderItem... orderItems) {
        Order order = new Order();
        order.setMember(member);
        order.setDelivery(delivery);
        for (OrderItem orderItem : orderItems) {
            order.addOrderItem(orderItem);
        }
        order.setStatus(OrderStatus.ORDER);
        order.setOrderDate(LocalDateTime.now());
        return order;
    }

    //==비지니스 로직==//
    /**
     * 주문 취소
     */
    public void cancel() {
        if (delivery.getStatus() == DeliveryStatus.COMP) {
            throw new IllegalStateException("이미 배송완료된 상품은 취소가 불가능합니다.");
        }

        this.setStatus(OrderStatus.CANCEL);
        for (OrderItem orderItem : orderItems) {
            orderItem.cancel();
        }
    }

    //==조회 로직==//

    /**
     * 전체 주문 가격 조회
     */
    public int getTotalPrice() {
        int totalPrice = 0;
        for (OrderItem orderItem : orderItems) {
            totalPrice += orderItem.getTotalPrice();
        }
        return totalPrice;
    }

}
```

**기능 설명**
- **생성 메서드**( createOrder() ): 주문 엔티티를 생성할 때 사용한다. 주문 회원, 배송정보, 주문상품의 정보 를 받아서 실제 주문 엔티티를 생성한다.
- **주문 취소**( cancel() ): 주문 취소시 사용한다. 주문 상태를 취소로 변경하고 주문상품에 주문 취소를 알린 다. 만약 이미 배송을 완료한 상품이면 주문을 취소하지 못하도록 예외를 발생시킨다.
- **전체 주문 가격 조회**: 주문 시 사용한 전체 주문 가격을 조회한다. 전체 주문 가격을 알려면 각각의 주문상품 가격을 알아야 한다. 로직을 보면 연관된 주문상품들의 가격을 조회해서 더한 값을 반환한다. (실무에서는 주로 주문에 전체 주문 가격 필드를 두고 역정규화 한다.)
  
주문상품 엔티티 개발

**주문상품 엔티티 코드**
```java
package jpaBook.jpaShop.domain;


import jakarta.persistence.*;
import lombok.Getter;
import lombok.Setter;

@Entity
@Getter @Setter
public class OrderItem {

    @Id @GeneratedValue
    @Column(name = "order_item_id")
    private Long id;

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "item_id")
    private Item item;

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "order_id")
    private Order order;

    private int orderPrice; // 주문가격
    private int count; // 주문 수량

    //==생성 메서드==//
    public static OrderItem createOrderItem(Item item, int orderPrice, int count) {
        OrderItem orderItem = new OrderItem();
        orderItem.setItem(item);
        orderItem.setOrderPrice(orderPrice);
        orderItem.setCount(count);

        item.removeStock(count);
        return orderItem;
    }

    //==비지니스 로직==//
    public void cancel() {
        getItem().addStock(count);
    }

    //==조회 로직==//

    /**
     * 주문상품 전체 가격 조회
     */
    public int getTotalPrice() {
        return getOrderPrice() * getCount();
    }
}
```

**기능 설명**
- **생성 메서드**( createOrderItem() ): 주문 상품, 가격, 수량 정보를 사용해서 주문상품 엔티티를 생성한다. 그리고 item.removeStock(count) 를 호출해서 주문한 수량만큼 상품의 재고를 줄인다.
- **주문 취소**( cancel() ): getItem().addStock(count) 를 호출해서 취소한 주문 수량만큼 상품의 재고를 증가시킨다.
- **주문 가격 조회**( getTotalPrice() ): 주문 가격에 수량을 곱한 값을 반환한다.


### 주문 리포지토리 개발
```java
package jpaBook.jpaShop.repository;

import jakarta.persistence.EntityManager;
import jpaBook.jpaShop.domain.Order;
import lombok.RequiredArgsConstructor;
import org.springframework.stereotype.Repository;

import java.util.List;

@Repository
@RequiredArgsConstructor
public class OrderRepository {

    private final EntityManager em;

    public void save(Order order) {
        em.persist(order);
    }

    public Order findOne(Long id) {
        return em.find(Order.class, id);
    }

//    public List<Order> findAll(OrderSearch orderSearch) {}
}
```

주문 리포지토리에는 주문 엔티티를 저장하고 검색하는 기능이 있다. 마지막의 findAll(OrderSearch orderSearch) 메서드는 조금 뒤에 있는 주문 검색 기능에서 자세히 알아보자.

### 주문 서비스 개발

**주문 서비스 코드**

`주문`
``java
package jpaBook.jpaShop.service;

import jpaBook.jpaShop.domain.*;
import jpaBook.jpaShop.repository.ItemRepository;
import jpaBook.jpaShop.repository.MemberRepository;
import jpaBook.jpaShop.repository.OrderRepository;
import lombok.RequiredArgsConstructor;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

@Service
@Transactional(readOnly = true)
@RequiredArgsConstructor
public class OrderService {

    private final OrderRepository orderRepository;
    private final MemberRepository memberRepository;
    private final ItemRepository itemRepository;

    /**
     * 주문
     */
    @Transactional
    public Long order(Long memberId, Long itemId, int count) {

        // 엔티티 조회
        Member member = memberRepository.findOne(memberId);
        Item item = itemRepository.findOne(itemId);

        // 배송정보 생성
        Delivery delivery = new Delivery();
        delivery.setAddress(member.getAddress());

        // 주문상품 생성
        OrderItem orderItem = OrderItem.createOrderItem(item, item.getPrice(), count);

        // 주문 생성
        Order order = Order.createOrder(member, delivery, orderItem);

        // 주문 저장
        orderRepository.save(order);

        return order.getId();

    }

    // 취소 

    // 검색

}
```
- Order과 OrderItem과 생성하지 않도록 하는 것이 좋음
- Order과 OrderItem에 `@NoArgsConstructor(access = AccessLevel.PROTECTED)` 또는 `protected OrderItem() {}` 추가

`취소`
```java
    // 취소
    @Transactional
    public void cancelOrder(Long orderId) {
        // 주문 엔티티 조회
        Order order = orderRepository.findOne(orderId);
        // 주문 취소
        order.cancel();
    }
```

- order에서 cancel()

```java
    //==비지니스 로직==//
    /**
     * 주문 취소
     */
    public void cancel() {
        if (delivery.getStatus() == DeliveryStatus.COMP) {
            throw new IllegalStateException("이미 배송완료된 상품은 취소가 불가능합니다.");
        }

        this.setStatus(OrderStatus.CANCEL);
        for (OrderItem orderItem : orderItems) {
            orderItem.cancel();
        }
    }
```

- orderItem에서 cancel()

```java
    //==비지니스 로직==//
    public void cancel() {
        getItem().addStock(count);
    }
```

주문 서비스는 주문 엔티티와 주문 상품 엔티티의 비즈니스 로직을 활용해서 주문, 주문 취소, 주문 내역 검색 기능을 제공한다.

> 참고: 예제를 단순화하려고 한 번에 하나의 상품만 주문할 수 있다.

- **주문**( order() ): 주문하는 회원 식별자, 상품 식별자, 주문 수량 정보를 받아서 실제 주문 엔티티를 생성한 후 저장한다.
- **주문 취소**( cancelOrder() ): 주문 식별자를 받아서 주문 엔티티를 조회한 후 주문 엔티티에 주문 취소를 요청한다.
- **주문 검색**( findOrders() ): OrderSearch 라는 검색 조건을 가진 객체로 주문 엔티티를 검색한다. 자세한 내용은 다음에 나오는 주문 검색 기능에서 알아보자.

> 참고: 주문 서비스의 주문과 주문 취소 메서드를 보면 비즈니스 로직 대부분이 엔티티에 있다.
> 서비스 계층은 단순히 엔티티에 필요한 요청을 위임하는 역할을 한다.
> 
> 이처럼 엔티티가 비즈니스 로직을 가지고 객체 지향의 특성을 적극 활용하는 것을 **도메인 모델 패턴**(http://martinfowler.com/eaaCatalog/domainModel.html)이라 한다.
>
> 반대로 엔티티에는 비즈니스 로직이 거의 없고 서비스 계층에서 대부분 의 비즈니스 로직을 처리하는 것을 **트랜잭션 스크립트 패턴**(http://martinfowler.com/eaaCatalog/transactionScript.html)이라 한다.


### 주문 기능 테스트

**테스트 요구사항**
- 상품 주문이 성공해야 한다.
- 상품을 주문할 때 재고 수량을 초과하면 안 된다.
- 주문 취소가 성공해야 한다.

**상품 주문 테스트 코드**

`상품 주문 테스트`

```java
package jpaBook.jpaShop.service;

import jakarta.persistence.EntityManager;
import jpaBook.jpaShop.domain.Address;
import jpaBook.jpaShop.domain.Member;
import jpaBook.jpaShop.domain.Order;
import jpaBook.jpaShop.domain.OrderStatus;
import jpaBook.jpaShop.domain.item.Book;
import jpaBook.jpaShop.repository.OrderRepository;
import org.junit.Test;
import org.junit.jupiter.api.Assertions;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.transaction.annotation.Transactional;

import static org.junit.Assert.*;

@RunWith(SpringRunner.class)
@SpringBootTest
@Transactional
public class OrderServiceTest {

    @Autowired EntityManager em;
    @Autowired OrderService orderService;
    @Autowired OrderRepository orderRepository;
    
    
    @Test
    public void 상품주문() throws Exception {
        // given
        Member member = new Member();
        member.setName("회원1");
        member.setAddress(new Address("서울", "강가", "12-244"));
        em.persist(member);

        Book book = new Book();
        book.setName("JPA");
        book.setPrice(10000);
        book.setStockQuantity(10);
        em.persist(book);

        int orderCount = 2;

        // when
        Long orderId = orderService.order(member.getId(), book.getId(), orderCount);

        // then
        Order getOrder = orderRepository.findOne(orderId);

        assertEquals("상품 주문시 상태는 ORDER", OrderStatus.ORDER, getOrder.getStatus());
        assertEquals("주문한 상품 종류 수가 정확해야한다.", 1, getOrder.getOrderItems().size());
        assertEquals("주문 가격은 가격 * 수량이다.", 10000 * orderCount, getOrder.getTotalPrice());
        assertEquals("주문 수량만큼 재고가 줄어야한다.", 8, book.getStockQuantity());
    }


    @Test
    public void 상품주문_재고수량초과() throws Exception {
        // given

        // when

        // then

    }


    @Test
    public void 주문취소() throws Exception {
     // given

     // when

     // then

    }


}
```

상품주문이 정상 동작하는지 확인하는 테스트다. Given 절에서 테스트를 위한 회원과 상품을 만들고 When 절에서 실제 상품을 주문하고 Then 절에서 주문 가격이 올바른지, 주문 후 재고 수량이 정확히 줄었는지 검증한다.

`상품주문 재고수량초과 테스트`

```java
    @Test(expected = NotEnoughStockException.class)
    public void 상품주문_재고수량초과() throws Exception {
        // given
        Member member = createMember();
        Item item = createBook("Jpa", 10000, 10);

        int orderCount = 11;

        // when
        orderService.order(member.getId(), item.getId(), orderCount);

        // then
        fail("재고 수량 부족 예외가 발생해야 한다.");

    }
```

재고 수량을 초과해서 상품을 주문해보자. 이때는 NotEnoughStockException 예외가 발생해야 한다.

코드를 보면 재고는 10권인데 orderCount = 11 로 재고보다 1권 더 많은 수량을 주문했다. 주문 초과로 다음 로직에서 예외가 발생한다.


- Member, book 생성 메서드
  
```java
    private Book createBook(String name, int price, int stockQuantity) {
        Book book = new Book();
        book.setName(name);
        book.setPrice(price);
        book.setStockQuantity(stockQuantity);
        em.persist(book);
        return book;
    }

    private Member createMember() {
        Member member = new Member();
        member.setName("회원1");
        member.setAddress(new Address("서울", "강가", "12-244"));
        em.persist(member);
        return member;
    }
```

`주문취소`

```java
    @Test
    public void 주문취소() throws Exception {
        // given
        Member member = createMember();
        Item item = createBook("Jpa", 10000, 10);

        int orderCount = 2;

        Long orderId = orderService.order(member.getId(), item.getId(), orderCount);

        // when
        orderService.cancelOrder(orderId);

        // then
        Order getOrder = orderRepository.findOne(orderId);

        assertEquals("주문 취소시 상태는 Cancel 이다.", OrderStatus.CANCEL, getOrder.getStatus());
        assertEquals("주문이 취소된 상품은 그만큼 재고가 증가해야 한다.", 10, item.getStockQuantity()); 


    }
```

주문 취소 테스트 코드를 작성하자. 주문을 취소하면 그만큼 재고가 증가해야 한다.
주문을 취소하려면 먼저 주문을 해야 한다. Given 절에서 주문하고 When 절에서 해당 주문을 취소했다. Then 절에서 주문상태가 주문 취소 상태인지( CANCEL ), 취소한 만큼 재고가 증가했는지 검증한다.


### 테스트 코드 작성 요령

- 각 로직(메서드) 하나당 단위테스트가 좋은 테스트다.(DB에 상관없이 짜는 것이 중요)


### 주문 검색 기능 개발

JPA에서 **동적 쿼리**를 어떻게 해결해야 하는가?

JPA Criteria는 JPA 표준 스펙이지만 실무에서 사용하기에 너무 복잡하다. 
결국 다른 대안이 필요하다. 많 은 개발자가 비슷한 고민을 했지만, 가장 멋진 해결책은 Querydsl이 제시했다.
**Querydsl** 소개장에서 간단히 언급하겠다. 지금은 이대로 진행하자.

```java
public List<Order> findAll(OrderSearch orderSearch) {
   QOrder order = QOrder. order;
   QMember member = QMember. member;

   return query
      .select (order)
      .from(order)
      .join(order. member, member)
      .where(statusEq(orderSearch.getOrderStatus()),
            nameLike (orderSearch.getMemberName()))
   .limit(1000)
   .fetch();
}

private BooleanExpression statusEq(OrderStatus statusCond) {
   if (statusCond == null) {
      return null;
   }
   return order.status.eq (statusCond);
}

private BooleanExpression nameLike(String nameCond) {
   if (!StringUtils.hasText (nameCond) ) {
      return null;
}
```

