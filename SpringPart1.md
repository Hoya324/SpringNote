2022.11.22(일) ~ 
복습



# 스프링 웹 개발 기초

### 정적 컨텐츠
 그냥 파일을 내려줌

### MVC와 템플릿 엔진<img width="327" alt="스크린샷 2022-12-05 오후 9 47 19" src="https://user-images.githubusercontent.com/96857599/205640802-5f903009-2ebd-45af-bc43-e7f138c1c9ca.png">

 템플릿 엔진을 model, view, controller 방식으로 쪼개서 뷰를 템플릿 엔진으로 html으로 랜더링해서 랜더링이 된 html을 고객에게 전달

### API
객체를 반환하는 것(Hello hello = new Hello();에서 hello)
-> HttpMessageConverter로 json 포맷으로 전달.
@ResponseBody를 사용

# 회원 관리 예제

### 비즈니스 요구사항 정리
- 데이터: 회원ID,이름
- 기능: 회원 등록, 조회
- 아직 데이터 저장소가 선정되지 않음(가상의 시나리오) 
<img width="369" alt="스크린샷 2022-11-20 오후 5 42 41" src="https://user-images.githubusercontent.com/96857599/202893212-1a6e420d-f81e-4872-9906-3dcbc4ee2582.png">

<img width="384" alt="스크린샷 2022-11-20 오후 5 50 48" src="https://user-images.githubusercontent.com/96857599/202893496-a70bb101-7789-4a55-a20d-d1ada18fdd4b.png">

### 회원 도메인과 레포지토리 만들기

1. domain 패키지 생성
- Member 클래스르 생성(ID 식별)
- id와 name을 getter setter 생성(cmd + N 누르면 설정가능)
<img width="478" alt="스크린샷 2022-12-01 오후 10 05 45" src="https://user-images.githubusercontent.com/96857599/205060327-2f19400b-5bd7-478d-bdb7-16f2e1ef77ac.png">

2.repository 패키지 생성
- MemberRepository 인터페이스 생성
- client 저장기능, 아이디로 찾기 기능, 이름으로 찾기 기능, 모두 찾는 기능 설계
<img width="370" alt="스크린샷 2022-12-01 오후 10 11 50" src="https://user-images.githubusercontent.com/96857599/205061503-8227bd29-57d7-4bd8-8f9c-d641d0973f69.png">
- MemberRepository 인터페이스를 상속받은 MemoryMemberRepository 클래스 생성
- HashMap으로 생성되 store 생성, member가 저장되는 순서를 id로 설정하기 위한 sequence 변수 생성
- save, findById, findByName, findAll 구현

### 테스트 케이스 작성
<img width="314" alt="스크린샷 2022-11-30 오후 2 49 31" src="https://user-images.githubusercontent.com/96857599/204717914-75b3dcfa-c2d7-4d02-a8d7-466db2d987bd.png">

1. test > hello.hellospring 폴더에 repository 폴더 생성(테스트하고자 하는 폴더라 같은 이름)
2. MemoryMemberRepository 클래스를 테스트할 것이므로 MemoryMemberRepositoryTest 클래스 생성
<img width="508" alt="스크린샷 2022-11-30 오후 2 53 27" src="https://user-images.githubusercontent.com/96857599/204718465-7cc7ffc1-0c48-4175-86db-60f603d761b9.png">
3. @Test를 작성하므로써 설계한 내용이 잘 작동하는지 확인하도록한다.

4. save 메서드 Test 작성
<img width="509" alt="스크린샷 2022-11-30 오후 2 57 10" src="https://user-images.githubusercontent.com/96857599/204718992-49b1dfdd-8105-4836-bd5e-bf128e264c13.png">
5. 확인방법 3가지

5-1. 같은지 확인하고 True/False 출력

<img width="438" alt="스크린샷 2022-11-30 오후 3 08 21" src="https://user-images.githubusercontent.com/96857599/204726464-17f69260-15e2-4dd7-a16e-87c9814c4deb.png">

5-2. Assertions junit jupiter api

<img width="557" alt="스크린샷 2022-11-30 오후 3 07 31" src="https://user-images.githubusercontent.com/96857599/204720952-463d39a3-147a-44b4-a38e-7646c5443745.png">

<img width="332" alt="스크린샷 2022-11-30 오후 3 11 00" src="https://user-images.githubusercontent.com/96857599/204721007-d1a96bd0-b3b6-4b34-af0c-0f3294f41d3f.png">

5-3. Assertions assertj core api (많이 씀)

<img width="335" alt="스크린샷 2022-11-30 오후 3 03 15" src="https://user-images.githubusercontent.com/96857599/204721167-7a1b08c6-d075-418e-be1e-26b51ee0953f.png">

<img width="398" alt="스크린샷 2022-11-30 오후 3 13 04" src="https://user-images.githubusercontent.com/96857599/204721352-ff5e8db2-e6fc-489e-9f51-7296193c2d87.png">

#### **💡TIP💡** 이때, option + enter 키를 누르면

<img width="466" alt="스크린샷 2022-11-30 오후 3 04 43" src="https://user-images.githubusercontent.com/96857599/204721590-2e48aef9-4be4-422a-9cfd-adf8f7a1a81d.png">

static 클래스로 사용가능하다.

6. 같은 방법으로 findByName()과 findAll() 테스트 코드를 작성한다.
<img width="494" alt="스크린샷 2022-11-30 오후 3 37 21" src="https://user-images.githubusercontent.com/96857599/204725142-bda02d97-273c-4c37-8aec-655dd5717c6b.png">
<img width="427" alt="스크린샷 2022-11-30 오후 3 37 34" src="https://user-images.githubusercontent.com/96857599/204725187-11e30c17-d0be-43f1-b9c9-fccaa79274c5.png">

#### **💡TIP💡** 같은 내용의 객체 이름만 다르다며 shift + F6키로 rename이 가능하다.


7. 이 상태로 테스트를 진행하며 repository에 이미 저장된 데이터가 중복되 수 있으므로, main 폴더의 MemoryMemberRepository 클래스에 데이터를 초기화시켜주는 메소드를 작성하고 Test에서 하나의 테스트가 끝나면 저장소 등 공용 데이터를 모두 지워주는 메서드를 작성한다.

- @AfterEach를 작성하지 않았을 때

<img width="208" alt="스크린샷 2022-11-30 오후 3 28 06" src="https://user-images.githubusercontent.com/96857599/204726011-edc42da5-e192-44e6-a790-c89fda258852.png">

- 작성

<img width="236" alt="스크린샷 2022-11-30 오후 3 30 47" src="https://user-images.githubusercontent.com/96857599/204726053-acf8c963-4f95-422b-b744-c9ae4be8f497.png">

<img width="249" alt="스크린샷 2022-11-30 오후 3 31 34" src="https://user-images.githubusercontent.com/96857599/204726070-25c57fbf-fc62-4399-925d-db44fee34cb1.png">

- 작성 후

<img width="196" alt="스크린샷 2022-11-30 오후 3 43 08" src="https://user-images.githubusercontent.com/96857599/204726137-8f31f3c8-4dac-428f-b401-ce51a8c9059d.png">


### 회원 서비스 개발

1. study.springStudy 패키지에 service 패키지 생성
2. 회원가입을 구현하기 위해서 MemberService 클래스에서 MemberRepository 를 생성하고 join 메소드를 생성한다.
3. 같은 이름이 있느 중복회원은 없어야하므로 member가 이미 존재하는지 파악한다.
TIP! memberRepository.findByName(member.getName()); 에서 cmd + option + v를 누르면 변수 자동 생성됨.
<img width="805" alt="스크린샷 2022-12-02 오전 1 50 44" src="https://user-images.githubusercontent.com/96857599/205111778-932dd2bc-6236-4b55-91e0-94316040b47b.png">
4. 이를 메소드로 따로 만들어주기 위해 control + t를 눌른 후, 메서드를 완성한다.
<img width="513" alt="스크린샷 2022-12-02 오전 1 41 34" src="https://user-images.githubusercontent.com/96857599/205112225-a3f9a23e-8bc2-4a72-99f8-2b52520ae89b.png">
<img width="649" alt="스크린샷 2022-12-02 오전 1 49 18" src="https://user-images.githubusercontent.com/96857599/205112285-e0f3fe62-73b7-4d64-b328-0c0865e731bf.png">
5. 전체 회원을 조회하기 위해서 findMembers와 한명의 회원을 조회하기 위해 findOne 메소드를 생성한다.
<img width="422" alt="스크린샷 2022-12-02 오전 2 00 29" src="https://user-images.githubusercontent.com/96857599/205113989-1914772c-bfae-483f-8d91-ace34fcd8c3d.png">

### 회원 서비스 테스트

#### **💡TIP💡** cmd + shift + T를 누르면 원하는 서비스의 테스트 파일을 쉽게 만들 수 있다.
<img width="533" alt="스크린샷 2022-12-02 오후 9 21 26" src="https://user-images.githubusercontent.com/96857599/205298222-09c81bf8-02ee-4446-931f-1c5f0bd9239b.png">

<img width="462" alt="스크린샷 2022-12-02 오후 9 22 26" src="https://user-images.githubusercontent.com/96857599/205298234-62b1b63a-2503-4605-bd8f-4d3dab93b5ee.png">

<img width="441" alt="스크린샷 2022-12-02 오후 9 22 38" src="https://user-images.githubusercontent.com/96857599/205298244-c6058b38-99cb-4041-9a06-865981cb92d2.png">

1. 회원가입 서비스를 테스트하기 위해 "client"라는 member가 주어졌을 때, 이 member를 회원가입 시키고, 이 회원이 member에 저장된 회원인지 확인한다.

<img width="677" alt="스크린샷 2022-12-02 오후 10 01 05" src="https://user-images.githubusercontent.com/96857599/205298682-7e5de1ba-9b22-4324-9ff2-a24a09e57010.png">

2. 중복되는 이름의 회원 예외처리하는 것을 확인하기 위해 member1과 member2의 이름을 같게 하고 이들을 회원가입 시켰을 때 validateDuplicateMember에서 설정한 "이미 존재하는 회원입니다"가 출력되는지 확인한다.
#### **💡TIP💡** cmd + B를 누르면 사용된 메소드의 위치로 이동시켜준다.

<img width="873" alt="스크린샷 2022-12-02 오후 10 23 29" src="https://user-images.githubusercontent.com/96857599/205302463-01221335-6781-488b-b77a-11c014146230.png">

테스트가 실행되기 전에 각각의 테스트에 새로운 객체가 생성되도록한다.
테스트가 끝난 후 memberRepository를 정리해준다.

<img width="503" alt="스크린샷 2022-12-02 오후 10 46 04" src="https://user-images.githubusercontent.com/96857599/205306778-119ac1f7-0c5a-41bb-8313-54d4c588d514.png">

## 스프링 빈을 등록하는 2가지 방법(컴포넌트 스캔과 의존관계 설정, 자바 코드로 직접 스프링 빈 등록)

### 컴포넌트 스캔과 자동 의존관계 설정

<img width="268" alt="스크린샷 2022-12-06 오후 2 34 46" src="https://user-images.githubusercontent.com/96857599/205825162-4a26056f-052d-40b1-8176-878f18ba1f32.png">

1. contorller 패키지에 MemberController를 생성한다. 
2. @Controller와 클래스를 생성해두면 스프링을 실행할 클래스의 객체를 생성하여 컨테이너에 넣어두고, 관리한다.
<img width="317" alt="스크린샷 2022-12-05 오후 9 47 56" src="https://user-images.githubusercontent.com/96857599/205640935-9e0ab085-96ef-49ab-98cb-6bb4968bd536.png">
<img width="678" alt="스크린샷 2022-12-05 오후 9 48 36" src="https://user-images.githubusercontent.com/96857599/205641066-2a78130c-69d1-48ed-a1eb-ead4f43fbc32.png">
<img width="777" alt="스크린샷 2022-12-05 오후 10 02 10" src="https://user-images.githubusercontent.com/96857599/205643944-05deda08-9ba2-4d6d-aa63-8a9cf45d319d.png">

2. 스프링 컨테이너에 객체를 인식시키기(@Component를 가진 모든 대상을 가져와서 빈에 등록하기 위해 찾는 과정)

스프링 빈 등록 이미지
<img width="321" alt="스크린샷 2022-12-06 오후 2 24 51" src="https://user-images.githubusercontent.com/96857599/205823809-3a821477-d576-4d73-ba88-65c938aaee59.png">


기본적인 컴포넌트 스캔 대상

@Component : 컴포넌트 스캔에서 사용

@Controller : 스프링 MVC 컨트롤러에서 사용

@Service : 스프링 비즈니스 로직에서 사용

@Repository : 스프링 데이터 접근 계층에서 사용

@Configuration : 스프링 설정 정보에서 사용

- @Controller와 @Autowired
<img width="777" alt="스크린샷 2022-12-05 오후 10 02 10" src="https://user-images.githubusercontent.com/96857599/205644026-3e489e49-5aca-4b07-9c47-e817672166da.png">


- @Repository
<img width="565" alt="스크린샷 2022-12-06 오후 2 23 36" src="https://user-images.githubusercontent.com/96857599/205823551-cf09d1b9-711e-4287-8955-75a96a0237b1.png">


- @Service
<img width="660" alt="스크린샷 2022-12-05 오후 10 06 59" src="https://user-images.githubusercontent.com/96857599/205644596-03cfef2d-4c64-4f88-a564-07c5bc83ab37.png">

- 이때 memberservice와 memberRepository가 연결되어있어야하므로 
<img width="657" alt="스크린샷 2022-12-06 오후 2 29 11" src="https://user-images.githubusercontent.com/96857599/205824363-094eba50-2773-497d-b232-0846d7d6bf28.png">
@Autowired로 연결해준다.

- 성공적으로 실행했을 때 (아직 아무런 기능이 없음)
<img width="635" alt="스크린샷 2022-12-06 오후 2 30 17" src="https://user-images.githubusercontent.com/96857599/205824581-aa063bc5-1c8c-4a8d-b6ea-4ef423edbb0f.png">

### 자바 코드로 직접 스프링 빈 등록하기
- 작성했던 컴포넌트 스캔 대상들을 지워준다.(@Controller 제외)
- MemberController - MemberService - MemberRepository를 연결지어 스프링 빈에 등록한다.
<img width="321" alt="스크린샷 2022-12-06 오후 2 24 51" src="https://user-images.githubusercontent.com/96857599/205828903-0754860e-032f-4d73-a9e8-a5489258218d.png">

 **DI에는 필드 주입, setter 주입, 생성자 주입으로 3가지 방법이 있는데, 의존관계가 실행중에 동적으로 변하는 경우가 거의 없으므로 아래코드와 같은 생성자 주입을 권장한다.**
<img width="747" alt="스크린샷 2022-12-06 오후 2 50 38" src="https://user-images.githubusercontent.com/96857599/205828972-1c003355-21ed-466e-a19d-69123b83f18f.png">

Java 패키지에 SpringConfig 클래스를 생성하여 직접 MemberService와 MemberRepository를 등록한다.
<img width="453" alt="스크린샷 2022-12-09 오후 3 11 28" src="https://user-images.githubusercontent.com/96857599/206636736-8ea0bac2-2d07-49b5-b97b-844bfc59609f.png">

## 이후 강의 목표: 정형화 되지 않거나, 상황에 따라 구현 클래스를 변경해야 하면 설정을 통해 스프링 빈으로 등록한다.(데이터베이스가 선정되지 않은 가상의 상황-MemberRepository를 다른 인터페이스를 바꿀 것임)
- 때문에 컴포넌트 스캔 방식 대신에 자바 코드로 스프링 빈을 설정한다.
- 주의: @Autowired를 통한 DI는 helloController, MemberService 등과 같이 스프링이 관리하는 객체에서만 동작한다. 스프링 빈으로 등록하지 않고 내가 직접 생성한 객체에서는 동작하지 않는다.

### 회원 웹 기능 - 홈 화면 추가

1. controller 패키지에 HomeController 생성
<img width="544" alt="스크린샷 2022-12-07 오후 10 52 52" src="https://user-images.githubusercontent.com/96857599/206197009-6adf0c1d-2f6f-4b70-b5b3-aa6c039981c7.png">
2. templates에 home.html 생성
<img width="424" alt="스크린샷 2022-12-07 오후 10 53 33" src="https://user-images.githubusercontent.com/96857599/206197171-cfcc3274-a1a8-4e4c-b967-2be53f0c0b66.png">

홈 화면
<img width="601" alt="스크린샷 2022-12-07 오후 11 19 02" src="https://user-images.githubusercontent.com/96857599/206202942-9ea454b8-54c3-4368-ab8b-82a28eda40f1.png">


### 회원 웹 기능 - 등록

원리
1. 홈 화면에서 회원 가입을 누르면 "/member/new" 로 들어간다.
<img width="466" alt="스크린샷 2022-12-07 오후 11 29 10" src="https://user-images.githubusercontent.com/96857599/206205481-8b2aa5d9-55e8-4b2d-8080-20145fd0fa40.png">

2. MemberController의 @GetMapping("/member/new")를 찾아가고, "members/creatMemberForm" HTML 화면을 보여주면서 이름을 등록할 페이지를 보여준다.

<img width="317" alt="스크린샷 2022-12-07 오후 11 26 10" src="https://user-images.githubusercontent.com/96857599/206204708-f141170f-0445-48b7-a7b9-10b2ed12a681.png">

3. form 태그에서 post 방식으로 "/members/new"에 input된 name="name"이 넘어간다. post 방식으로 넘겼기 때문에 같은 "members/new"가 있더라도 @PostMapping이 있는 곳으로 넘어가게 된다.(데이터를 form에 넣어서 전달할 때 사용)
<img width="699" alt="스크린샷 2022-12-07 오후 11 33 11" src="https://user-images.githubusercontent.com/96857599/206206613-784c68c5-20c0-46f8-9b80-35b543998a6e.png">

4. @PostMapping("/members/new")를 따라 들어온 name이 MemberForm의 name으로 들어가게 된다.
<img width="345" alt="스크린샷 2022-12-07 오후 11 39 54" src="https://user-images.githubusercontent.com/96857599/206208679-b110cfa5-f073-4c8f-a504-37e66b5892ef.png">
<img width="468" alt="스크린샷 2022-12-07 오후 11 42 27" src="https://user-images.githubusercontent.com/96857599/206208764-8a832e68-23a8-4bc0-bbec-ad68cf8ad084.png">

5. MemberForm에서 받은 name 즉, 입력된 고객의 이름을 Member 객체에 초기화하고, memberService로 회원가입하면(join), 중복을 검사하고, memberRepository에 저장된다.
<img width="476" alt="스크린샷 2022-12-07 오후 11 44 34" src="https://user-images.githubusercontent.com/96857599/206209301-eced20ed-dbeb-43c1-8b21-414a2c48ab22.png">

### 회원 웹 기능 - 조회
#### **💡TIP💡** cmd + E 누르면 최근 목록이 보임

1. MemberController에 홈에서 "/members"(회원 목록)으로 갔을 때, memberService의 전체 회원 조회 기능으로 List<Member> members에 저장한 후 model에 members를 넘겨준다. 그리고 memberList.html을 templates/members에 생성한다.

<img width="456" alt="스크린샷 2022-12-08 오전 12 16 22" src="https://user-images.githubusercontent.com/96857599/206217358-f68ddcfd-3355-4667-83cb-265723972739.png">
<img width="334" alt="스크린샷 2022-12-08 오전 12 11 14" src="https://user-images.githubusercontent.com/96857599/206216097-d58b2454-bf76-4777-98f8-b4dabdd7f2db.png">
<img width="442" alt="스크린샷 2022-12-08 오전 12 18 10" src="https://user-images.githubusercontent.com/96857599/206217864-491f7ff1-1611-4b5a-b47f-1e782db09bcd.png">

2. 이름(spring1, spring2)을 등록하고 실행하면 등록한 회원들이 조회된다.
<img width="305" alt="스크린샷 2022-12-08 오전 12 20 06" src="https://user-images.githubusercontent.com/96857599/206218428-86195742-6a1f-42be-a1e7-4b777bfa888e.png">

<img width="300" alt="스크린샷 2022-12-08 오전 12 19 14" src="https://user-images.githubusercontent.com/96857599/206218195-40b1bcbc-bf7c-4411-a923-a7166891a11c.png">

 ### H2데이터베이스 설치
 
 1. H2 Database 홈페이지에서 다운받는다
 2. iterm2에서 cd /Users/gangho/Desktop/springStudy/h2로 경로를 변경해준다.
 3. bin에 들어가서, ls -alther을 확인하면 h2.sh라는 파일이 있는데 맥북의 경우 실행 권한을 부여해야한다.(chmod 755 h2.sh)
<img width="643" alt="스크린샷 2022-12-08 오후 3 38 15" src="https://user-images.githubusercontent.com/96857599/206376007-a8cf6a3f-58e4-429d-8955-e5d54409aab9.png">

4. ./h2.sh를 입력해 실행하면 된다. 
<img width="472" alt="스크린샷 2022-12-08 오후 3 39 02" src="https://user-images.githubusercontent.com/96857599/206376145-13f1f8c6-4b37-4795-9a83-b4d550496936.png">

5. 이때 다시 iterm2에서 홈을 확인했을 때(ls - arlth) test.mv.db가 있는지 확인한다.
<img width="567" alt="스크린샷 2022-12-08 오후 3 40 48" src="https://user-images.githubusercontent.com/96857599/206376453-d2721d51-04a9-41ec-81e0-ede9cad5cf29.png">

6. 충돌 오류를 막기 위해 JDBC URL을 jdbc:h2:tcp://localhost/~/test로 바꿔준다. (소켓을 통해 접근)
<img width="471" alt="스크린샷 2022-12-08 오후 3 43 03" src="https://user-images.githubusercontent.com/96857599/206376838-894fa511-6fc5-4a2e-bae4-651729ca413c.png">

- 테이블 생성
<img width="1002" alt="스크린샷 2022-12-08 오후 3 50 40" src="https://user-images.githubusercontent.com/96857599/206378357-3cd94a34-0edb-424b-9f2b-db8e0214add1.png">

- id bigint generated by default as identity 은 id 값에 null값이 들어가면 자동으로 값을 넣어준다.

### 순수 JDBC
1. build.gradle에 추가한다.
<img width="602" alt="스크린샷 2022-12-09 오후 2 52 23" src="https://user-images.githubusercontent.com/96857599/206633820-c526e2bd-cf94-4552-8eef-9811568009ae.png">
2. 데이터베이스 주소와 드라이버를 추가한다.
<img width="447" alt="스크린샷 2022-12-09 오후 2 53 10" src="https://user-images.githubusercontent.com/96857599/206633932-cf08d45a-2fe6-4f7c-ba89-c1a050e9de8a.png">
3. 순수 JDBC 코드 입력(기억할 필요는 없지만 알아두기)
4. 스프링 설정 변경
<img width="647" alt="스크린샷 2022-12-09 오후 3 22 29" src="https://user-images.githubusercontent.com/96857599/206638289-47863526-5f18-4444-90cd-205a40c3c477.png">
5. 연동 확인
<img width="402" alt="스크린샷 2022-12-09 오후 11 39 04" src="https://user-images.githubusercontent.com/96857599/206726695-69e9152b-c9d9-4fa6-b031-42d84bdbc874.png">

### 스프링 통합 테스트

1. @SpringBootTest: 스프링 컨테이너와 테스트를 함께 실행한다.
2. @Transctional: 테스트 케이스에 이 어노테이션이 있으면, 테스트 시작 전에 트랜잭션을 시작하고, 테스트 완료 후에 항상 롤백. 이렇게 하면 DB에 데이터가 남지 않으므로 다음 테스트에 영향을 주지 않는다.
- 단위 테스트가 시간도 적게 걸리고 좋은 테스트임.
<img width="741" alt="스크린샷 2022-12-10 오후 4 11 01" src="https://user-images.githubusercontent.com/96857599/206837509-ce418364-450a-4649-b195-949474497302.png">
 
 ### 스프링 JdbcTemplate
 #### **💡TIP💡** option + Enter: lambda로 변경 가능(상황에 맞게)
 <img width="594" alt="스크린샷 2022-12-10 오후 4 56 23" src="https://user-images.githubusercontent.com/96857599/206839865-eab856e8-f9c2-481e-98a4-e0e024a21ed5.png">
<img width="481" alt="스크린샷 2022-12-12 오후 12 43 39" src="https://user-images.githubusercontent.com/96857599/206955975-a26cdcde-1cd3-405f-b62b-779c0b48817a.png">

 1. repository 폴더에 JdbcTemplateMemberRepository 클래스를 만들어준다.
 2. JdbcTemplateMemberRepository를 Spring 컨테이너와 연결한다.(생성자 만들기)
 <img width="495" alt="스크린샷 2022-12-12 오후 1 24 18" src="https://user-images.githubusercontent.com/96857599/206960367-0b1e6d59-8d42-440c-b27a-c12262ba727c.png"> 
 3. member row 저장 메소드
 <img width="485" alt="스크린샷 2022-12-12 오후 1 29 29" src="https://user-images.githubusercontent.com/96857599/206960944-e7e9001a-f945-46d9-aee3-bba0cc9a0812.png">

 4. save 구현
 <img width="753" alt="스크린샷 2022-12-12 오후 1 26 39" src="https://user-images.githubusercontent.com/96857599/206960607-585cbb3e-4988-4a27-ab6c-615c8e18e0ee.png">
 5. findById 구현
 <img width="854" alt="스크린샷 2022-12-12 오후 1 27 01" src="https://user-images.githubusercontent.com/96857599/206960652-8f5361dc-8040-4cf5-a1de-adeee70c2b04.png">
 6. findByName 구현
 <img width="868" alt="스크린샷 2022-12-12 오후 1 29 49" src="https://user-images.githubusercontent.com/96857599/206960982-156508d4-e832-46cc-b8bd-3207bbba320c.png">

 7. findAll 구현
<img width="634" alt="스크린샷 2022-12-12 오후 1 30 14" src="https://user-images.githubusercontent.com/96857599/206961024-1efa116f-b08a-45ed-b172-488f966b307f.png">
 8. SpringConfig 수정(JdbcTemplateMemberRepository를 memberRepository로서 스프링 빈에 등록)
<img width="620" alt="스크린샷 2022-12-12 오후 1 32 44" src="https://user-images.githubusercontent.com/96857599/206961289-6ca65fdb-1a77-40a9-bf03-055023e8aae7.png">
 
 9. 스프링 통합 테스트코드 MemberServiceIntegrationTest를 실행 시켜본다.
 
 #### 오류 파악하기(테스트 코드의 중요성); 이대로 실행하게 되면 아래와 같은 오류가 발생한다.

 <img width="1463" alt="스크린샷 2022-12-12 오후 1 39 59" src="https://user-images.githubusercontent.com/96857599/206962062-f555b499-24d8-46ba-8a9f-4d360c2427ce.png">
이유를 보면 파라미터를 잘못 설정했다는 것을 알 수 있는데, findById를 구현할 때 마지막에 id를 빼먹고 테스트를 돌려서 그렇다. (중복회원가입에서 오류는 DB에 client1을 넣어둔 상태라 그렇다. 빼고 다시 실행한다.)
 - 문제의 코드
 <img width="890" alt="스크린샷 2022-12-12 오후 1 40 29" src="https://user-images.githubusercontent.com/96857599/206962272-3841a352-9658-4d3a-a06c-d5203451949a.png">
 - 올바른 코드
 <img width="892" alt="스크린샷 2022-12-12 오후 1 45 02" src="https://user-images.githubusercontent.com/96857599/206962571-ecf5a8db-1e94-4015-be7f-ea053ee2a997.png">
 - 성공
 <img width="1060" alt="스크린샷 2022-12-12 오후 1 46 43" src="https://user-images.githubusercontent.com/96857599/206962750-1dbb8115-c5a2-4782-9387-d019953742fd.png">

### JPA
1. build.gradle에 JPA, h2 데이터베이스 관련 라이브러리 추가
 <img width="629" alt="스크린샷 2022-12-12 오후 2 38 17" src="https://user-images.githubusercontent.com/96857599/206968517-c28ecb8b-81e5-4d26-9728-df88795c7c41.png">
2. resources/application.properties에 스프링부트 JPA 설정 추가
 <img width="427" alt="스크린샷 2022-12-12 오후 2 41 41" src="https://user-images.githubusercontent.com/96857599/206969095-3203adee-fe27-4a03-910e-447e6f673c84.png">
3. JPA 앤티티 매핑
 <img width="571" alt="스크린샷 2022-12-12 오후 2 49 10" src="https://user-images.githubusercontent.com/96857599/206969870-e3c3e25b-5434-4310-a4a1-002b023fc7d8.png">
4. repository에 JpaMemberRepository 생성
- 내부적으로 데이터 소스를 가지고 있어 데이터 통신이 가능하게 하도록 EntityManager 주입
 <img width="413" alt="스크린샷 2022-12-13 오후 1 35 30" src="https://user-images.githubusercontent.com/96857599/207227638-ff988e1c-d07b-4b95-9627-abad5ced016c.png">

 #### **💡TIP💡**  control + T를 누르면 설정 옵션을 선택할 수 있다.
<img width="736" alt="스크린샷 2022-12-13 오후 1 41 53" src="https://user-images.githubusercontent.com/96857599/207228429-9130cbe0-bdc6-4ee0-ab51-4691107c96a0.png">
<img width="669" alt="스크린샷 2022-12-13 오후 1 42 59" src="https://user-images.githubusercontent.com/96857599/207228569-5833a670-7717-40c5-8fcb-119a4ef9767f.png">

- save 구현
 <img width="314" alt="스크린샷 2022-12-13 오후 1 52 04" src="https://user-images.githubusercontent.com/96857599/207229633-283f98e0-3fc6-4016-80ea-ef7e0be1f554.png">

- findById 구현
 <img width="400" alt="스크린샷 2022-12-13 오후 1 52 15" src="https://user-images.githubusercontent.com/96857599/207229656-fbdb9147-8c16-452c-abe0-9c658b6a1e14.png">

- findByName 구현
 <img width="886" alt="스크린샷 2022-12-13 오후 1 52 38" src="https://user-images.githubusercontent.com/96857599/207229714-ecd4c019-d83c-4593-be8a-8345aaa2b73e.png">

- findAll 구현
 <img width="609" alt="스크린샷 2022-12-13 오후 1 52 53" src="https://user-images.githubusercontent.com/96857599/207229752-1345f760-5d58-43d4-9fe5-1e19776ea5dc.png">
 
- JPA를 사용할 때 데이터를 변경하고 저장하려면 @Transactional이 필요하다. memebrService 색션에 추가한다
 <img width="688" alt="스크린샷 2022-12-13 오후 1 57 01" src="https://user-images.githubusercontent.com/96857599/207230274-65c58313-c7a0-432d-9bae-a12240479904.png">
 
- spring 빈에 jpa 등록

<img width="733" alt="스크린샷 2022-12-13 오후 2 00 04" src="https://user-images.githubusercontent.com/96857599/207230631-e8642421-8996-471d-9403-69fe64c53453.png">

### 스프링 데이터 JPA(스프링 데이터 JPA는 JPA를 편리하게 사용하도록 도와주는 기술이다. 따라서 JPA를 먼저 학습한 후에 스프링 데이터 JPA를 학습해야 한다.)

1. repository에 SpringDataJpaMemberRepository 인터페이스를 생성하고, JpaRepository<Member, Long>, MemberRepository를 상속받는다.
<img width="886" alt="스크린샷 2022-12-13 오후 9 57 08" src="https://user-images.githubusercontent.com/96857599/207324095-205663fa-25d6-46be-8f32-0f191fd107f0.png">
JPQL로 select m from Member m where m.name = ? 라고 짠 것과 같다.

2. springConfig에서 스프링 설정을 변경해준다.
<img width="631" alt="스크린샷 2022-12-13 오후 9 56 54" src="https://user-images.githubusercontent.com/96857599/207324048-2bd25904-f7c5-424e-8049-21109608a2f2.png">

스프링 데이터 JPA 제공 클래스
<img width="522" alt="스크린샷 2022-12-13 오후 9 57 46" src="https://user-images.githubusercontent.com/96857599/207324212-0aee9774-f826-4344-a8d2-f648d7200aff.png">

### AOP:Aspect Oriented Programming

 AOP가 필요한 상황
 - 모든 메소드의 호출 시간을 측정하고 싶다면? 
 - 공통 관심 사항(cross-cutting concern) vs 핵심 관심 사항(core concern) 
 - 회원 가입 시간, 회원 조회 시간을 측정하고 싶다면?
 
 
 1. MemberService 회원 조회 시간 측정 추가
 <img width="983" alt="스크린샷 2022-12-13 오후 10 12 25" src="https://user-images.githubusercontent.com/96857599/207327186-6b133165-b45c-4d48-b59d-73a59b8a5c72.png">
<img width="502" alt="스크린샷 2022-12-13 오후 10 15 08" src="https://user-images.githubusercontent.com/96857599/207328191-d6444c12-4a90-4914-b668-2d0eedeafffb.png">
 <img width="723" alt="스크린샷 2022-12-13 오후 10 16 41" src="https://user-images.githubusercontent.com/96857599/207328040-77ecc32d-8198-4086-8cc2-a68f4c0a3373.png">
 
 - 이런 식으로 모든 메소드에 추가해야한다..
 #### 문제
- 회원가입, 회원 조회에 시간을 측정하는 기능은 핵심 관심 사항이 아니다.
- 시간을 측정하는 로직은 공통 관심 사항이다.
- 시간을 측정하는 로직과 핵심 비즈니스의 로직이 섞여서 유지보수가 어렵다.
- 시간을 측정하는 로직을 별도의 공통 로직으로 만들기 매우 어렵다.
- 시간을 측정하는 로직을 변경할 때 모든 로직을 찾아가면서 변경해야 한다.
<img width="577" alt="스크린샷 2022-12-13 오후 10 05 13" src="https://user-images.githubusercontent.com/96857599/207325736-0e863bd8-6834-4d73-8f8a-7de44f2d11b2.png">
 이를 AOP를 적용하면
 <img width="540" alt="스크린샷 2022-12-13 오후 10 23 32" src="https://user-images.githubusercontent.com/96857599/207330469-0b337bf5-db23-4537-ad71-e05b695ae9d3.png">
 
### AOP 적용
1. aop 패키지를 생성하고 TimeTraceAop 클래스를 생성한다.
 <img width="684" alt="스크린샷 2022-12-13 오후 10 31 31" src="https://user-images.githubusercontent.com/96857599/207334868-9a627281-475b-446a-ae15-affddccc5f24.png">
2-1. SpringConfig에 스프링 설정을 추가한다.
 <img width="348" alt="스크린샷 2022-12-13 오후 10 33 55" src="https://user-images.githubusercontent.com/96857599/207336265-a5a7f7be-8d7e-47b3-a710-10e9a196006b.png">
2-2. 또는 컴포넌트 스캔을 사용한다.(강의에선 컴포넌트 스)
 <img width="729" alt="스크린샷 2022-12-13 오후 10 37 40" src="https://user-images.githubusercontent.com/96857599/207338172-144579a3-2dcd-4a26-ac66-1db7bbedc827.png">
로그
<img width="743" alt="스크린샷 2022-12-13 오후 10 41 44" src="https://user-images.githubusercontent.com/96857599/207340494-db8cf90f-d977-4030-a798-78b05bc6ea4a.png">
<img width="551" alt="스크린샷 2022-12-13 오후 10 43 23" src="https://user-images.githubusercontent.com/96857599/207341881-1b27e428-22a5-4541-9fc1-e49a10f10e1e.png">
