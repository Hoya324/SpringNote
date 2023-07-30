Http에 대해 학습한다.
인터넷과 네트워크
http
http 메서드
http 상태코드
http 헤더
RestApi

> HTTP에 대한 내용을 정리한 글입니다.

# 인터넷 네트워크

## 인터넷 통신

![image](https://github.com/Hoya324/SpringNote/assets/96857599/6aaa0df4-661f-40cf-8c9e-6d98d263551b)

- 클라이언트가 서버로 요청을 보내는 방식을 알기 위해서는 IP를 이해해야한다.

## IP(인터넷 프로토콜)

### IP의 역할
- 지정한 IP 주소(IP Address)에 데이터 전달.
- 패킷(Packet)이라는 통신 단위로 데이터 전달

### IP를 통한 통신 과정
1. 클라이언트가 IP를 가진다.
2. 서버에도 IP를 가진다.
3. 메세지를 그냥 전달하는 것이 아니라 IP 패킷이라는 규칙을 통해 전달한다.

![image](https://github.com/Hoya324/SpringNote/assets/96857599/40ee9db2-c2d1-442b-9f3b-4233dd24cdd2)

4. 클라이언트 패킷 전달. (출발, 목적 IP와 메세지를 전달한다.)

![image](https://github.com/Hoya324/SpringNote/assets/96857599/86731f4c-cdb3-4c50-898d-4c31d79fcfda)

5. 서버 패킷 전달. (출발, 목적 IP와 메세지를 전달한다.)

![image](https://github.com/Hoya324/SpringNote/assets/96857599/45dccce3-0bfe-4ea9-b297-b99d6dfcb33a)

> 클라이언트 -> 서버의 노드와 서버 -> 클라이언트의 전달 노드가 다를 수 있다.
> 

### IP 프로토콜의 한계

**비연결성**
- 패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷 전송 (받을 대상의 컴퓨터가 꺼져있거나 받을 수 없는 상태여도 일단 보낸다는 뜻)

**비신뢰성**
- 통신 중간에 패킷의 소실 문제
- 패킷의 도달 순서가 달라지는 문제

**프로그램 구분**
- 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상일 때 발생하는 문제

> 이와 같은 IP 프로토콜의 한계를 보완해주는 것이 TCP.

## TCP

### 인터넷 프로토콜 스택의 4계층

<img width="358" alt="스크린샷 2023-07-29 오전 11 22 02" src="https://github.com/Hoya324/SpringNote/assets/96857599/fe6325b9-ee71-423e-964a-2bd68c93de8a">

### 프로토콜 계층

<img width="522" alt="스크린샷 2023-07-29 오전 11 22 40" src="https://github.com/Hoya324/SpringNote/assets/96857599/1fe46963-0a8b-4b44-bb90-2c13452e2741">

<img width="585" alt="스크린샷 2023-07-29 오전 11 22 53" src="https://github.com/Hoya324/SpringNote/assets/96857599/2ce6490d-9871-4cb4-a00f-4bc318733bd1">

### IP 패킷과 TCP/IP 패킷 정보의 차이

**IP 패킷 정보**
- 출발지 IP, 목적지 IP, 등을 가짐
- 패킷(packet:소포)

<img width="547" alt="스크린샷 2023-07-29 오전 11 25 39" src="https://github.com/Hoya324/SpringNote/assets/96857599/83be6ce3-9fe6-48fc-aedb-38429935e0d7">

**TCP/IP 패킷 정보**
- 출발지 PORT, 목적지 PORT 전송 제어, 순서, 검증 정보 등
- 순서 제어 문제 해결

<img width="541" alt="스크린샷 2023-07-29 오전 11 26 22" src="https://github.com/Hoya324/SpringNote/assets/96857599/3031d0c2-d704-4ff8-9b63-1715e4f53093">

### TCP(Transmission Control Protocol/전송 제어 프로토콜) 특징
- 연결지향 -> TCP 3 way handshake (가상 연결)
- 데이터 전달 보증
- 순서 보장
- 신뢰할 수 있는 프로토콜
- 현재는 대부분 TCP 사용

**1. TCP 3 way handshake**

<img width="599" alt="스크린샷 2023-07-29 오후 3 35 47" src="https://github.com/Hoya324/SpringNote/assets/96857599/a28c1480-a032-48d4-954d-3066586f28ee">

- 상대가 접속이 가능한 상태인지 확인하고 응답을 보낼지 말지 결정함.
- 가상 연결 -> 물리적인 연결이 아닌, 논리적인 연결임.

**2. 데이터 전달 보증**

<img width="513" alt="스크린샷 2023-07-29 오후 3 36 43" src="https://github.com/Hoya324/SpringNote/assets/96857599/6ab0da61-a9ea-4571-9d75-e9232be83767">

- 수신측에 TCP 세그먼트가 도착하면 수신 측은 송신 측에게 도착했다고 알림. 이것을 ACK라고 함.
- TCP 헤더에 ACK 관련 정보를 넣은 TCP 세그먼트를 반환함.

**3. 순서 보장**

<img width="519" alt="스크린샷 2023-07-29 오후 3 38 52" src="https://github.com/Hoya324/SpringNote/assets/96857599/ad63d0b6-9bf4-4e0e-afef-9b6b7825cfc9">

- 순서가 잘못된 경우 순서를 맞춰서 다시 보낼 수 있도록 함.
- TCP에 출발지 PORT, 목적지 PORT 전송 제어, 순서, 검증 정보 등이 있기 때문에 가능함.
- 데이터 순서를 보증하기 위해서 TCP 세그먼트에 **시퀀스(Sequence)번호**를 붙임.
- 시퀀스 번호도 TCP헤더에 기록되며, 해당 세그먼트가 가지고 있는 데이터가 전송 데이터 전체 중 몇 바이트째부터 시작하는 부분인지를 가리키고 있음.

## UDP(User Datagram Protocol/사용자 데이터그램 프로토콜)

- 하얀 도화지에 비유(기능이 거의 없음)
- 연결지향 - TCP 3 way handshake X
- 데이터 전달 보증 X
- 순서 보장 X
- 데이터 전달 및 순서가 보장되지 않지만, 단순하고 빠름 정리

### 정리
- IP와 거의 같다. PORT, 체크섬 정도만 추가
- 애플리케이션에서 추가 작업 필요

**UDP 사용 이유**
- TCP는 데이터 양도 많고, 속도도 느림(3 way handshake) -> TCP는 변경하기 힘듦
- 더 최적화하기 위해 사용하기 좋음 -> 최근 각광 받기 시작

## PORT

> 같은 IP 서버에 여러 작업을 연결하면 어떻게 구분할 수 있을까?

- 각 IP에서 요청을 보낼 때 패킷에 출발 PORT와 도착 PORT를 저장해서 보내게 됨
- 각 PORT에 맞게 요청-응답

>  비유 IP: 아파트 PORT: 호수

<img width="535" alt="스크린샷 2023-07-29 오후 3 46 44" src="https://github.com/Hoya324/SpringNote/assets/96857599/19479633-b182-45aa-ae15-1de2e74294f8">

### PORT 번호
- 0 ~ 65535 할당 가능
- 0 ~ 1023: 잘 알려진 포트, 사용하지 않는 것이 좋음
  - FTP - 20, 21
  - TELNET - 23
  - HTTP - 80
  - HTTPS - 443
 
## DNS(Domain Name System/도메인 네임 시스템)
- 전화번호부와 같은 느낌
- 도메인 명을 IP 주소로 변환

### IP의 단점
- 기억하기 어렵다.
- 변경될 수 있다.

### DNS 사용
- 도메인을 구매 등으로 획득
- 도메인 명을 IP와 연결
- IP가 바뀌면 바뀐 IP를 도메인에 다시 연결

<img width="598" alt="스크린샷 2023-07-29 오후 3 55 30" src="https://github.com/Hoya324/SpringNote/assets/96857599/51b296bd-c7b0-4979-83f0-1c62b5ac641a">

## HTTP

### HTTP 메시지에 모든 것을 전송
- HTML, TEXT
- IMAGE, 음성, 영상, 파일
- JSON, XML (API)
- 거의 모든 형태의 데이터 전송 가능
- 서버간에 데이터를 주고 받을 때도 대부분 HTTP 사용

### HTTP 역사
- HTTP/0.9 1991년: GET 메서드만 지원, HTTP 헤더X
- HTTP/1.0 1996년: 메서드, 헤더 추가
- HTTP/1.1 1997년: 가장 많이 사용, 우리에게 가장 중요한 버전
  - RFC2068 (1997) -> RFC2616 (1999) -> RFC7230~7235 (2014)
- HTTP/2 2015년: 성능 개선
- HTTP/3 진행중: TCP 대신에 UDP 사용, 성능 개선

### 기반 프로토콜
- TCP: HTTP/1.1, HTTP/2
- UDP: HTTP/3
- 현재 HTTP/1.1 주로 사용
  - HTTP/2, HTTP/3 도 점점 증가

### HTTP 특징
- 클라이언트 서버 구조
- 무상태 프로토콜(스테이스리스), 비연결성
- HTTP 메시지
- 단순함, 확장 가능

### 클라이언트 서버 구조
- Request Response 구조
- 클라이언트는 서버에 요청을 보내고, 응답을 대기
- 서버가 요청에 대한 결과를 만들어서 응답

<img width="487" alt="스크린샷 2023-07-29 오후 4 07 08" src="https://github.com/Hoya324/SpringNote/assets/96857599/33409fbd-3855-4bd0-b16f-1caaf5a61edc">

### 무상태(Stateless) 프로토콜
- 서버가 클라이언트의 상태를 보존X
- 장점: 서버 확장성 높음(스케일 아웃)
- 단점: 클라이언트가 추가 데이터 전송

**상태유지(Stateful) 예시**

고객: 이 노트북 얼마인가요? 
점원A: 100만원 입니다.

고객: 2개 구매하겠습니다.
점원B: ? 무엇을 2개 구매하시겠어요?

고객: 신용카드로 구매하겠습니다.
점원C: ? 무슨 제품을 몇 개 신용카드로 구매하시겠어요?

- 위의 예시처럼 상태유지의 경우 중간에 점원(서버)이 바뀐다면 문제가 발생한다.
- 즉, 중간에 서버에 장애가 생겨 서버를 교체해야한다면 문제가 생긴다.

**무상태(Stateless) 예시**

고객: 이 노트북 얼마인가요? 
점원A: 100만원 입니다.

고객: 노트북 2개 구매하겠습니다.
점원B: 노트북 2개는 200만원 입니다. 신용카드, 현금중에 어떤 걸로 구매 하시겠어요?

고객: 노트북 2개를 신용카드로 구매하겠습니다. 
점원C: 200만원 결제 완료되었습니다.

- 무상태의 경우 중간에 점원(서버)이 바뀌어도 된다.
- 즉, 중간에 서버에 장애가 생기더라도 아무 서버나 호출할 수 있다.

### Stateful, Stateless 차이 정리
- **상태 유지**: 중간에 다른 점원으로 바뀌면 안된다. 
(중간에 다른 점원으로 바뀔 때 상태 정보를 다른 점원에게 미리 알려줘야 한다.)
  - 서버가 클라이언트의 이전 상태를 유지, 보존해주는 것

- **무상태**: 중간에 다른 점원으로 바뀌어도 된다.
  - 갑자기 고객이 증가해도 점원을 대거 투입할 수 있다.
  - 갑자기 클라이언트 요청이 증가해도 서버를 대거 투입할 수 있다.
  - 무상태는 응답 서버를 쉽게 바꿀 수 있다. -> 무한한 서버 증설 가능

### Stateless 실무 한계
- 모든 것을 무상태로 설계 할 수 있는 경우도 있고 없는 경우도 있다.
- 무상태
  - 예) 로그인이 필요 없는 단순한 서비스 소개 화면
- 상태 유지
  - 예) 로그인
- 로그인한 사용자의 경우 로그인 했다는 상태를 서버에 유지
- 일반적으로 브라우저 쿠키와 서버 세션등을 사용해서
- 상태 유지 상태 유지는 최소한만 사용
- 데이터를 너무 많이 보냄

### 비 연결성(connectionless)

**연결을 유지하는 모델**
- TCP/IP 연결의 경우 기본적으로 요청과 응답 후에 연결을 유지함.

<img width="566" alt="스크린샷 2023-07-29 오후 4 28 05" src="https://github.com/Hoya324/SpringNote/assets/96857599/569fb34c-503f-451e-9d5d-94ab43b60b79">

- 클라이언트2가 연결을 해도 클라이언트1과의 연결은 유지됨.

<img width="576" alt="스크린샷 2023-07-29 오후 4 28 44" src="https://github.com/Hoya324/SpringNote/assets/96857599/c62f03b1-c41e-475c-81ad-bf622e7d4e94">

- 클라이언트3을 연결할 때에도 클라이언트 1, 2의 연결은 유지되므로 서버 자원을 소모하게 됨.

<img width="607" alt="스크린샷 2023-07-29 오후 4 29 39" src="https://github.com/Hoya324/SpringNote/assets/96857599/7a2e3cc8-1f01-49e2-b4ed-6dd4ec6145b3">

- 재연결

<img width="604" alt="스크린샷 2023-07-29 오후 4 29 50" src="https://github.com/Hoya324/SpringNote/assets/96857599/7424c216-c008-4c12-93f2-0e03fe5561dc">

**연결을 유지하지 않는 모델**

- TCP/IP 연결 후 필요 없어진 연결은 끊어짐

<img width="557" alt="스크린샷 2023-07-29 오후 4 30 30" src="https://github.com/Hoya324/SpringNote/assets/96857599/f14a6301-52d4-4344-a258-fe34f2861361">

- 필요할 때 연결하고, 응답후 끊어지면 서버의 자원을 최소한으로 사용함.

<img width="548" alt="스크린샷 2023-07-29 오후 4 30 43" src="https://github.com/Hoya324/SpringNote/assets/96857599/632037e1-b4b7-4cc8-8a86-32c7998e4a63">

<img width="554" alt="스크린샷 2023-07-29 오후 4 30 51" src="https://github.com/Hoya324/SpringNote/assets/96857599/b2920d01-de5b-457d-aa9c-5b9591eb3989">

<img width="594" alt="스크린샷 2023-07-29 오후 4 30 59" src="https://github.com/Hoya324/SpringNote/assets/96857599/35a20e63-8164-4e18-852b-cb51d6001f5c">

<img width="600" alt="스크린샷 2023-07-29 오후 4 31 07" src="https://github.com/Hoya324/SpringNote/assets/96857599/a19484ab-fa20-48f3-8cfe-d44ad262ee63">

**비 연결성**
- HTTP는 기본이 연결을 유지하지 않는 모델
- 일반적으로 초 단위의 이하의 빠른 속도로 응답
- 1시간 동안 수천명이 서비스를 사용해도 실제 서버에서 동시에 처리하는 요청은 수십개 이하로 매우 작음
  - 예) 웹 브라우저에서 계속 연속해서 검색 버튼을 누르지는 않는다.
- 서버 자원을 매우 효율적으로 사용할 수 있음

**비 연결성의 한계와 극복**
- 한계
  - TCP/IP 연결을 새로 맺어야 함 - 3 way handshake 시간 추가(연결, 종료 낭비)
  - 웹 브라우저로 사이트를 요청하면 HTML 뿐만 아니라 자바스크립트, css, 추가 이미지 등등 수 많은 자원이 함께 다운로드
- 극복
  - 지금은 HTTP 지속 연결(Persistent Connections)로 문제 해결
  - HTTP/2, HTTP/3에서 더 많은 최적화
 
<img width="548" alt="스크린샷 2023-07-29 오후 4 41 24" src="https://github.com/Hoya324/SpringNote/assets/96857599/d052f5e0-b39c-4df5-a858-7c94be737422">

<img width="561" alt="스크린샷 2023-07-29 오후 4 41 41" src="https://github.com/Hoya324/SpringNote/assets/96857599/a5cd82a4-a633-4bd4-b75c-3b21c3ff3154">

**스테이스리스를 기억하자**
- 서버 개발자들이 어려워하는 업무
- 정말 같은 시간에 딱 맞추어 발생하는 대용량 트래픽
  - 예) 선착순 이벤트, 명절 KTX 예약, 학과 수업 등록
  - 예) 저녁 6:00 선착순 1000명 치킨 할인 이벤트 -> 수만명 동시 요청
-> 맨 첫 페이지에 html로만 이루어진 페이지를 두어 클라이언트들의 클릭을 분산시키는 방법이 있다.

## HTTP 메시지

<img width="607" alt="스크린샷 2023-07-29 오후 4 46 21" src="https://github.com/Hoya324/SpringNote/assets/96857599/2c9f8d60-0872-4a03-96f4-feddbda986c8">

### 시작 라인

<img width="276" alt="스크린샷 2023-07-29 오후 5 19 05" src="https://github.com/Hoya324/SpringNote/assets/96857599/da46f3f4-7ad5-44b6-9bed-45ccb3206d9c">

**요청 메시지**
- start-line = **request-line** / status-line
- **request-line** = method SP(공백) request-target SP HTTP-version CRLF(엔터)

- HTTP 메서드 (GET: 조회)
- 요청 대상 (/search?q=hello&hl=ko)
- HTTP Version

**요청 메시지 - HTTP 메서드**
- 종류: GET, POST, PUT, DELETE...
- 서버가 수행해야 할 동작 지정
  - GET: 리소스 조회
  - POST: 요청 내역 처리

**요청 메시지 - 요청 대상**
- absolute-path[?query]
- (절대경로[?쿼리]) 절대경로= "/" 로 시작하는 경로
- 참고: *, http://...?x=y 와 같이 다른 유형의 경로지정 방법도 있다.

**요청 메시지 - HTTP 버전**
- HTTP Version

**응답 메시지**
- start-line = request-line / **status-line**
- **status-line** = HTTP-version SP status-code SP reason-phrase CRLF

- HTTP 버전
- HTTP 상태 코드: 요청 성공, 실패를 나타냄
  - 200: 성공
  - 400: 클라이언트 요청 오류
  - 500: 서버 내부 오류
- 이유 문구: 사람이 이해할 수 있는 짧은 상태 코드 설명 글

### HTTP 헤더
- header-field = field-name ":" OWS field-value OWS (OWS: 띄어쓰기 허용)
- field-name은 대소문자 구문 없음

<img width="552" alt="스크린샷 2023-07-29 오후 5 18 44" src="https://github.com/Hoya324/SpringNote/assets/96857599/e030a0dd-477c-412c-8c86-533bc39f8361">

**용도**
- HTTP 전송에 필요한 모든 부가정보
- 예) 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트(브라우저) 정보, 서버 애플리케이션 정보, 캐시 관리 정보...
- 표준 헤더가 너무 많음
  - [List_of_HTTP_header_fields](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields)
- 필요시 임의의 헤더 추가 가능
  - helloworld: hihi

### HTTP 메시지 바디

<img width="278" alt="스크린샷 2023-07-29 오후 5 25 27" src="https://github.com/Hoya324/SpringNote/assets/96857599/da404465-98bf-4403-876a-4c37a7d5df30">

**용도**
- 실제 전송할 데이터
- HTML 문서, 이미지, 영상, JSON 등등 byte로 표현할 수 있는 모든 데이터 전송 가능

## HTTP 메서드

> HTTP API를 만들어보자(좋은 URI 설계는 무엇인가)

**요구사항**
- 회원 정보 관리 API를 만들어라.
	- 회원 목록 조회 
	- 회원 조회
	- 회원 등록
	- 회원 수정
	- 회원 삭제

### API URI 설계
- URI(Uniform Resource Identifier)
	- 회원 목록 조회 `/read-member-list`
	- 회원 조회 `/read-member-by-id` 
	- 회원 등록 `/create-member`
	- 회원 수정 `/update-member`
	- 회원 삭제 `/delete-member`
	
### 이것은 좋은 URI 설계일까?
- **가장 중요한 것은 리소스를 식별**하는 것이다.
 
### API URI(Uniform Resource Identifier) 고민
- 리소스의 의미는 뭘까?
	- 회원을 등록하고 수정하고 조회하는게 리소스가 아니다!
	- 예) 미네랄을 캐라 -> 미네랄이 리소스
	- 회원이라는 **개념 자체**가 바로 리소스다.
- **리소스를 어떻게 식별하는게 좋을까?**
	- 회원을 등록하고 수정하고 조회하는 것을 모두 배제
	- **회원이라는 리소스만 식별**하면 된다. -> 회원 리소스를 URI에 매핑

### API URI 설계
**리소스 식별, URI 계층 구조 활용**

- **회원** 목록 조회 `/members`
- **회원** 조회 `/members/{id}` -> 어떻게 구분하지? 
- **회원** 등록 `/members/{id}` -> 어떻게 구분하지? 
- **회원** 수정 `/members/{id}` -> 어떻게 구분하지? 
- **회원** 삭제 `/members/{id}` -> 어떻게 구분하지?

> 참고: 계층 구조상 상위를 컬렉션으로 보고 복수단어 사용 권장(member -> members)

**리소스와 행위를 분리**
가장 중요한 것은 리소스를 식별하는 것

- **URI는 리소스만 식별!**
- **리소스**와 해당 리소스를 대상으로 하는 **행위**을 분리
	- 리소스: 회원
	- 행위: 조회, 등록, 삭제, 변경
- 리소스는 명사, 행위는 동사 (미네랄을 캐라) 
- 행위(메서드)는 어떻게 구분할까?

### HTTP 메서드 - GET, POST

> Representation 설명 전

**주요 메서드**
- GET: 리소스 조회
- POST: 요청 데이터 처리, 주로 등록에 사용 
- PUT: 리소스를 대체, 해당 리소스가 없으면 생성 
- PATCH: 리소스 부분 변경
- DELETE: 리소스 삭제

**기타 메서드**
- HEAD: GET과 동일하지만 메시지 부분을 제외하고, 상태 줄과 헤더만 반환
- OPTIONS: 대상 리소스에 대한 통신 가능 옵션(메서드)을 설명(주로 CORS에서 사용) 
- CONNECT: 대상 자원으로 식별되는 서버에 대한 터널을 설정
- TRACE: 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행


### GET

<img width="367" alt="스크린샷 2023-07-29 오후 5 36 03" src="https://github.com/Hoya324/SpringNote/assets/96857599/fd603fc4-a08f-4c91-981c-905f2a0b289c">

- 리소스 조회
- 서버에 전달하고 싶은 데이터는 query(쿼리 파라미터, 쿼리 스트링)를 통해서 전달
- 메시지 바디를 사용해서 데이터를 전달할 수 있지만, 지원하지 않는 곳이 많아서 권장하지 않음

**리소스 조회1 - 메시지 전달**

<img width="625" alt="스크린샷 2023-07-29 오후 5 36 36" src="https://github.com/Hoya324/SpringNote/assets/96857599/42797d07-9e02-4e1d-82f6-957403fce976">

**리소스 조회2 - 서버도착**

<img width="608" alt="스크린샷 2023-07-29 오후 5 36 54" src="https://github.com/Hoya324/SpringNote/assets/96857599/21b4a3de-d197-4018-8465-15e520b9d8e4">

**리소스 조회3 - 응답 데이터**

<img width="593" alt="스크린샷 2023-07-29 오후 5 37 09" src="https://github.com/Hoya324/SpringNote/assets/96857599/1496454e-50e3-425c-b378-fea1c8c470bd">

### POST

**클라이언트 측에서 데이터를 전달하여 처리를 요청하는 것**

<img width="247" alt="스크린샷 2023-07-29 오후 5 37 35" src="https://github.com/Hoya324/SpringNote/assets/96857599/11284cc0-8f73-4e81-8c4a-8cad28e56318">

- 요청 데이터 처리
- 메시지 바디를 통해 서버로 요청 데이터 전달
- 서버는 요청 데이터를 처리
  - 메시지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행한다.
- 주로 전달된 데이터로 신규 리소스 등록, 프로세스 처리에 사용

**메시지 등록 - `/members`로 오면 전달된 데이터를 어떤 방식으로 처리할지 미리 약속함.**

<img width="561" alt="스크린샷 2023-07-29 오후 5 39 44" src="https://github.com/Hoya324/SpringNote/assets/96857599/bae63814-29d7-48cd-a7c7-a209dba81274">

**신규 리소스 생성 - 신규 리소스 식별자 생성**

<img width="629" alt="스크린샷 2023-07-29 오후 5 40 43" src="https://github.com/Hoya324/SpringNote/assets/96857599/9ae0df40-284c-4dce-9512-220dc21a168e">

**응답 데이터**

<img width="611" alt="스크린샷 2023-07-29 오후 5 40 53" src="https://github.com/Hoya324/SpringNote/assets/96857599/9dd77a7f-b20c-4217-9b90-52acd56d561f">

### 요청 데이터를 어떻게 처리한다는 뜻일까? 
예시)
- 스펙: **POST 메서드**는 대상 리소스가 리소스의 고유 한 의미 체계에 따라 **요청에 포함 된 표현을 처리**하도록 요청합니다. (구글 번역) 
- 예를 들어 POST는 다음과 같은 기능에 사용됩니다.
	- HTML 양식에 입력 된 필드와 같은 데이터 블록을 데이터 처리 프로세스에 제공	
		- 예) HTML FORM에 입력한 정보로 **회원 가입, 주문** 등에서 사용
	- 게시판, 뉴스 그룹, 메일링 리스트, 블로그 또는 유사한 기사 그룹에 메시지 게시
		- 예) **게시판 글쓰기, 댓글 달기**
	- 서버가 아직 식별하지 않은 새 리소스 생성
		- 예) **신규 주문 생성**
	- 기존 자원에 데이터 추가
		- 예) **한 문서 끝에 내용 추가**하기
- 정리
  - 이 리소스 URI에 POST 요청이 오면 요청 데이터를 어떻게 처리할지 리소스마다 따로 정해야 함 -> 정해진 것이 없음


### POST 정리
1. **새 리소스 생성(등록)**
	- 서버가 아직 식별하지 않은 새 리소스 생성
2. **요청 데이터 처리**
	- 단순히 데이터를 생성하거나, 변경하는 것을 넘어서 프로세스를 처리해야 하는 경우
	  - 예) 주문에서 결제완료 -> 배달시작 -> 배달완료 처럼 단순히 값 변경을 넘어 프로세스의 상태가 변경되는 경우 
	- POST의 결과로 새로운 리소스가 생성되지 않을 수도 있음
	  - 예) POST /orders/{orderId}/start-delivery (컨트롤 URI)
3. **다른 메서드로 처리하기 애매한 경우**
	- 예) JSON으로 조회 데이터를 넘겨야 하는데, GET 메서드를 사용하기 어려운 경우 
	- 애매하면 POST

### HTTP 메서드 - PUT, PATCH, DELETE

### PUT

<img width="239" alt="스크린샷 2023-07-29 오후 5 49 59" src="https://github.com/Hoya324/SpringNote/assets/96857599/c9974401-5330-40de-b18c-9f3bd89f3aef">

- **리소스를 완전히 대체**
	- 리소스가 있으면 대체 
	- 리소스가 없으면 생성 
	- 쉽게 이야기해서 덮어버림
- **중요! 클라이언트가 리소스를 식별**
	- 클라이언트가 리소스 위치를 알고 URI 지정 -> 구체적인 리소스를 지정한다는 점에서 POST와의 차이를 보임
	- POST와 차이점

### PATCH

<img width="222" alt="스크린샷 2023-07-29 오후 5 51 38" src="https://github.com/Hoya324/SpringNote/assets/96857599/a370f015-c83b-4e4d-a987-e4ddb294dbb8">

- 리소스를 부분 변경하는 것
- 특정 HTTP가 PATCH를 못 받아들이는 경우 POST를 사용하면 됨

### DELETE

<img width="222" alt="스크린샷 2023-07-29 오후 5 52 22" src="https://github.com/Hoya324/SpringNote/assets/96857599/3b642232-2db3-4fdf-9973-d36966fe6520">

- 리소스 제거

### HTTP 메서드의 속성
- **안전(Safe Methods)**
- **멱등(Idempotent Methods)**
- **캐시가능(Cacheable Methods)**

![image](https://github.com/Hoya324/SpringNote/assets/96857599/f05d43e6-3131-443c-a53a-1367c6db4524)

### 안전(Safe)
- 호출해도 리소스를 변경하지 않는다. (예: GET, HEAD)
- Q: 그래도 계속 호출해서, 로그 같은게 쌓여서 장애가 발생하면요?
- A: 안전은 해당 리소스만 고려한다. 그런 부분까지 고려하지 않는다.

### 멱등(Idempotent)
- f(f(x)) = f(x)
- 한 번 호출하든 두 번 호출하든 100번 호출하든 결과가 똑같다.
- 멱등 메서드
	- **GET**: 한 번 조회하든, 두 번 조회하든 같은 결과가 조회된다.
	- **PUT**: 결과를 대체한다. 따라서 같은 요청을 여러번 해도 최종 결과는 같다. 
	- **DELETE**: 결과를 삭제한다. 같은 요청을 여러번 해도 삭제된 결과는 똑같다. 
	- **POST**: **멱등이 아니다!** 두 번 호출하면 같은 결제가 중복해서 발생할 수 있다.

- Q: 재요청 중간에 다른 곳에서 리소스를 변경해버리면?
	- 사용자1: GET -> username:A, age:20
	- 사용자2: PUT -> username:A, age:30
	- 사용자1: GET -> username:A, age:30 -> 사용자2의 영향으로 바뀐 데이터 조회
- **A: 멱등은 외부 요인으로 중간에 리소스가 변경되는 것 까지는 고려하지는 않는다.**

**활용**
- 자동 복구 메커니즘
- 서버가 TIMEOUT 등으로 정상 응답을 못 주었을 때, 클라이언트가 같은 요청을 다시 해도 되는가? 판단 근거

### 캐시가능(Cacheable) 
- 응답 결과 리소스를 캐시해서 사용해도 되는가? 
- GET, HEAD, POST, PATCH 캐시가능
- 실제로는 GET, HEAD 정도만 캐시로 사용(URL만 키로 고려하면 되기 때문에 간단함)
	- POST, PATCH는 본문 내용까지 캐시 키로 고려해야 하는데, 구현이 쉽지 않음

## HTTP 메서드 활용

### 클라이언트에서 서버로 데이터 전송

**데이터 전달 방식 2가지**
- **쿼리 파라미터를 통한 데이터 전송**
	- GET
	- 주로 정렬 필터(검색어)
- **메시지 바디를 통한 데이터 전송**
	- POST, PUT, PATCH
	- 회원 가입, 상품 주문, 리소스 등록, 리소스 변경

**4가지 상황**
- **정적 데이터 조회**
	- 이미지, 정적 텍스트 문서 
- **동적 데이터 조회**
	- 주로 검색, 게시판 목록에서 정렬 필터(검색어) 
- **HTML Form을 통한 데이터 전송**
	- 회원 가입, 상품 주문, 데이터 변경 
- **HTTP API를 통한 데이터 전송**
	- 회원 가입, 상품 주문, 데이터 변경
	- 서버 to 서버, 앱 클라이언트, 웹 클라이언트(Ajax)

### 정적 데이터 조회
- 쿼리 파라미터 미사용

<img width="627" alt="스크린샷 2023-07-30 오후 12 51 12" src="https://github.com/Hoya324/SpringNote/assets/96857599/e0dafca4-4372-4a2f-a08f-97fa6702f294">

**정리**
- 이미지, 정적 텍스트 문서
- 조회는 GET 사용
- 정적 데이터는 일반적으로 쿼리 파라미터 없이 리소스 경로로 단순하게 조회 가능

### 동적 데이터 조회
- 쿼리 파라미터 사용

<img width="519" alt="스크린샷 2023-07-30 오후 12 52 38" src="https://github.com/Hoya324/SpringNote/assets/96857599/eaaa0aae-0013-4ab6-9db0-61d29788b61d">

**정리**
- 주로 검색, 게시판 목록에서 정렬 필터(검색어)
- 조회 조건을 줄여주는 필터, 조회 결과를 정렬하는 정렬 조건에 주로 사용 
- 조회는 GET 사용
- GET은 쿼리 파라미터 사용해서 데이터를 전달

### HTML Form 데이터 전송
- POST 전송 -> 저장

<img width="546" alt="스크린샷 2023-07-30 오후 12 53 20" src="https://github.com/Hoya324/SpringNote/assets/96857599/00905558-0283-4418-bab1-911189d6917e">

- GET 전송 -> 저장

<img width="542" alt="스크린샷 2023-07-30 오후 12 53 35" src="https://github.com/Hoya324/SpringNote/assets/96857599/35dd84ef-f1d2-43b5-947d-d046d2598eeb">

- GET 전송 -> 조회

<img width="526" alt="스크린샷 2023-07-30 오후 12 53 51" src="https://github.com/Hoya324/SpringNote/assets/96857599/885220a4-b1c9-4cc5-8a60-d6ee6c8e816d">

> 주의! GET은 조회에만 사용!
> 
> 리소스 변경이 발생하는 곳에 사용하면 안됨!

- multipart/form-data (주로 바이너리 데이터를 전송할 때 사용)

<img width="643" alt="스크린샷 2023-07-30 오후 12 54 42" src="https://github.com/Hoya324/SpringNote/assets/96857599/1f85b67e-1db3-4dd2-9d31-bc5478d09cb2">

**정리**

- HTML Form submit시 POST 전송
	- 예) 회원 가입, 상품 주문, 데이터 변경
- Content-Type: application/x-www-form-urlencoded 사용
	- form의 내용을 메시지 바디를 통해서 전송(key=value, 쿼리 파라미터 형식)
	- 전송 데이터를 url encoding 처리
		- 예) abc김 -> abc%EA%B9%80 
- HTML Form은 GET 전송도 가능(쿼리 파라미터 방식으로 전송된다.)
- Content-Type: multipart/form-data
	- 파일 업로드 같은 바이너리 데이터 전송시 사용
	- 다른 종류의 여러 파일과 폼의 내용 함께 전송 가능(그래서 이름이 multipart) 

> 참고: HTML Form 전송은 **GET, POST만 지원**

### HTTP API 데이터 전송
- IOS나 안드로이드 같은 모바일 기기에서 서버에 바로 데이터를 전송해야할 때

<img width="535" alt="스크린샷 2023-07-30 오후 12 57 15" src="https://github.com/Hoya324/SpringNote/assets/96857599/f8a63f15-7ce3-4bba-95e9-69469880562f">

**정리**
- 서버 to 서버
	- 백엔드 시스템 통신 
- 앱 클라이언트
	- 아이폰, 안드로이드 
- 웹 클라이언트
	-	HTML에서 Form 전송 대신 자바 스크립트를 통한 통신에 사용(AJAX)
	-	예) React, VueJs 같은 웹 클라이언트와 API 통신 
- POST, PUT, PATCH: 메시지 바디를 통해 데이터 전송
- GET: 조회, 쿼리 파라미터로 데이터 전달
- Content-Type: application/json을 주로 사용 (사실상 표준)
	- TEXT, XML, JSON 등등 (요즘엔(2022년) JSON 많이 사용함)

### HTTP API 설계 예시

- **HTTP API - 컬렉션**
	- **POST 기반 등록**
	- 예) 회원 관리 API 제공
- **HTTP API - 스토어**
	- **PUT 기반 등록**
	- 예) 정적 컨텐츠 관리, 원격 파일 관리 
- **HTML FORM 사용**
	- 웹 페이지 회원 관리 
	- GET, POST만 지원


### 회원 관리 시스템

**API 설계 - post 기반 등록**
- **회원** 목록 /members -> **GET**
- **회원** 등록 /members -> **POST**
- **회원** 조회 /members/{id} -> **GET**
- **회원** 수정 /members/{id} -> **PATCH**(부분적인 수정이므로 가장 자주 씀), **PUT**(게시글 작성할 때), **POST** 
- **회원** 삭제 /members/{id} -> **DELETE**

**POST - 신규 자원 등록 특징**
- **클라이언트는 등록될 리소스의 URI를 모른다.(서버가 만들어준다.)**
	- 회원 등록 /members -> POST
	- POST /members
- ⭐️**서버가 새로 등록된 리소스 URI를 생성해준다.**
	- `HTTP/1.1 201 Created`<br>`Location: /members/100`
- ⭐️**컬렉션(Collection)**
	- 서버가 관리하는 리소스 디렉토리 
	- 서버가 리소스의 URI를 생성하고 관리 
	- 여기서 컬렉션은 /members

### 파일 관리 시스템

**API 설계 - PUT 기반 등록**
- **파일** 목록 /files -> **GET**
- **파일** 조회 /files/{filename} -> **GET** 
- **파일** 등록 /files/{filename} -> **PUT** 
- **파일** 삭제 /files/{filename} -> **DELETE** 
- **파일** 대량 등록 /files -> **POST**

**PUT - 신규 자원 등록 특징**

- 클라이언트가 리소스 URI를 알고 있어야 한다.
	- 파일 등록 /files/{filename} -> PUT
	- PUT **/files/star.jpg**
- ⭐️클라이언트가 직접 리소스의 URI를 지정한다.
- ⭐️**스토어(Store)**
	- 클라이언트가 관리하는 리소스 저장소 
	- 클라이언트가 리소스의 URI를 알고 관리 
	- 여기서 스토어는 /files
	
> 대부분 post 기반의 컬렉션을 사용한다.

### HTML FORM 사용

**설계 명세**
- HTML FORM은 **GET, POST만 지원**
- AJAX 같은 기술을 사용해서 해결 가능 -> 회원 API 참고 
- 여기서는 순수 HTML, HTML FORM 이야기
- GET, POST만 지원하므로 제약이 있음

**HTML FORM 사용 예시**
- **회원** 목록   /members -> **GET**
- **회원** 등록 폼 /members/new -> **GET**
- **회원** 등록   /members/new(오류시에 등록 폼과 경로를 맞추면 좋다), /members -> **POST**
- **회원** 조회   /members/{id} -> **GET**
- **회원** 수정 폼 /members/{id}/edit -> **GET**
- **회원** 수정    /members/{id}/edit, /members/{id} -> **POST**
- **회원** 삭제    /members/{id}/delete -> **POST** (DELETE 메서드를 사용하지 못하기 때문에 컨드롤 URI 사용)

**특징**
- HTML FORM은 GET, POST만 지원 
- ⭐️**컨트롤 URI** -> 최대한 리소스라는 개념을 가지고 URI를 설계하고, 안 될 때 사용한다.
	- GET, POST만 지원하므로 제약이 있음
	- 이런 제약을 해결하기 위해 동사로 된 리소스 경로 사용 (조작하는 기능을 수행하기 때문)
	- POST의 /new, /edit, /delete가 컨트롤 URI
	- HTTP 메서드로 해결하기 애매한 경우 사용(HTTP API 포함)


### 정리
- **HTTP API - 컬렉션**
	- **POST 기반 등록**
	- **서버가 리소스 URI 결정**
- **HTTP API - 스토어**
	- **PUT 기반 등록**
	- **클라이언트가 리소스 URI 결정**
- **HTML FORM 사용**
	- 순수 HTML + HTML form 사용
	- GET, POST만 지원

### [참고하면 좋은 URI 설계 개념](https://restfulapi.net/resource-naming)

- **문서(document)**
	- 단일 개념(파일 하나, 객체 인스턴스, 데이터베이스 row)
	- 예) /members/100, /files/star.jpg 
- **컬렉션(collection)**
	- 서버가 관리하는 리소스 디렉터리 
	- 서버가 리소스의 URI를 생성하고 관리 
	- 예) /members
- **스토어(store)**
	- 클라이언트가 관리하는 자원 저장소 
	- 클라이언트가 리소스의 URI를 알고 관리 
	- 예) /files
- **컨트롤러(controller), 컨트롤 URI**
	- 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스 실행 
	- 동사를 직접 사용
	- 예) /members/{id}/delete





