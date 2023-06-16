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
