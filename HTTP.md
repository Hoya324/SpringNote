2023.01.07 ~
# HTTPStudy

### REST API
1. 자원을 URL로 표현
2. 리소스에 대한 행위를 HTTP 메서드로 표현

## 인터넷 

### 인터넷 통신

<img width="701" alt="스크린샷 2023-01-11 오후 4 16 24" src="https://user-images.githubusercontent.com/96857599/211741641-5b47e13c-852e-49de-af5f-b8411e71898e.png">

- 클라이언트가 서버로 요청을 보내는 방식을 알기 위해서는 IP를 이해해야한다.


### IP(인터넷 프로토콜)

1. 클라이언트가 IP를 가진다.
2. 서버에도 IP를 가진다.
- IP의 역할:  
  1. 지정한 IP 주소(IP Address)에 데이터 전달.
  2. 패킷(Packet)이라는 통신 단위로 데이터 전달
3. 메세지를 그냥 전달하는 것이 아니라 IP 패킷이라는 규칙을 통해 전달한다.
<img width="702" alt="스크린샷 2023-01-11 오후 4 20 36" src="https://user-images.githubusercontent.com/96857599/211742421-3cc5f456-94e7-4fe2-91c6-8d1f7d830a56.png">
4. 클라이언트 패킷 전달. (출발, 목적 IP와 메세지를 전달한다.)
<img width="701" alt="스크린샷 2023-01-11 오후 4 22 13" src="https://user-images.githubusercontent.com/96857599/211742727-f8fc0d8d-4cbe-4d10-a9cd-b625f28d5c84.png">

5. 서버 패킷 전달. (출발, 목적 IP와 메세지를 전달한다.)
<img width="702" alt="스크린샷 2023-01-11 오후 4 22 25" src="https://user-images.githubusercontent.com/96857599/211742763-1eda14f4-a4ff-424c-96b7-711272a482da.png">

> 클라이언트 -> 서버의 노드와 서버 -> 클라이언트의 전달 노드가 다를 수 있다.

### IP 프로토콜의 한계
- 비연결성
  - 패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷 전송 (받을 대상의 컴퓨터가 꺼져있거나 받을 수 없는 상태여도 일단 보낸다는 뜻)
- 비신뢰성
  - 중간에 패킷이 사라지면?
  - 패킷이 순서대로 안 오면?
- 프로그램 구분
  - 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상이면? (노래를 들으면서 게임을 하는 상황이라면?)

- 대상이 서비스 불능, 패킷 전송
<img width="703" alt="스크린샷 2023-01-11 오후 4 26 56" src="https://user-images.githubusercontent.com/96857599/211743515-ce4288c6-f359-4625-984b-29bad4c84026.png">
- 대상이 서비스 불능, 패킷 전송
<img width="703" alt="스크린샷 2023-01-11 오후 4 27 15" src="https://user-images.githubusercontent.com/96857599/211743569-97bb6e17-65f5-4ad4-9e93-60d07d4b80f6.png">
- 패킷 소실
<img width="698" alt="스크린샷 2023-01-11 오후 4 27 36" src="https://user-images.githubusercontent.com/96857599/211743633-b5ff1ed6-adcd-43e5-9aec-9b9096ff4c43.png">
- 패킷 전달 순서 문제 발생
<img width="699" alt="스크린샷 2023-01-11 오후 4 27 52" src="https://user-images.githubusercontent.com/96857599/211743692-81ea297f-2b27-4f3f-bb70-4714e3a4011d.png">

-> 위와 같은 문제를 해결해주는 것이 TCP

### TCP<img width="694" alt="스크린샷 2023-01-17 오후 7 43 20" src="https://user-images.githubusercontent.com/96857599/212878572-2221f094-8e13-4ca9-bbcc-fff4d09e9f48.png">

<img width="574" alt="스크린샷 2023-01-17 오후 7 43 42" src="https://user-images.githubusercontent.com/96857599/212878676-2b5b280b-b738-48d6-b0ce-e818fb17f50d.png">

<img width="689" alt="스크린샷 2023-01-17 오후 7 44 05" src="https://user-images.githubusercontent.com/96857599/212878755-5b6a3efd-727c-4d6a-9f02-167593fd01cb.png">

1. IP 패킷 정보
<img width="686" alt="스크린샷 2023-01-17 오후 7 45 26" src="https://user-images.githubusercontent.com/96857599/212879032-e40e56cb-65ca-4523-8d41-9862bdfac803.png">
- 출발지 IP, 목적지 IP, 등으 가짐
- 패킷(packet:소포)

2. TCP/IP 패킷 정보
<img width="654" alt="스크린샷 2023-01-17 오후 7 47 59" src="https://user-images.githubusercontent.com/96857599/212879615-103b85b6-aa3b-40ea-81cd-76d5e1fa87fd.png">
- 출발지 PORT, 목적지 PORT 전송 제어, 순서, 검증 정보 등
- 순서 제어 문제 해결 
  
#### TCP 특징
전송 제어 프로토콜(Transmission Control Protocol)

- 연결지향 - TCP 3 way handshake (가상 연결) 
- 데이터 전달 보증
- 순서 보장

- 신뢰할 수 있는 프로토콜 
- 현재는 대부분 TCP 사용


1. TCP 3 way handshake
<img width="667" alt="스크린샷 2023-01-17 오후 7 51 01" src="https://user-images.githubusercontent.com/96857599/212880284-8c88b904-86ae-4102-a0a4-5bac8764789c.png">
- 상대가 접속이 가능한 상태인지 확인하고 응답을 보낼지 말지 결정함.
- 가상 연결 -> 물리적인 연결이 아닌, 논리적인 연결임.

2. 데이터 전달 보증
<img width="663" alt="스크린샷 2023-01-17 오후 7 51 34" src="https://user-images.githubusercontent.com/96857599/212880395-7eb440fd-3348-40a1-9c97-fb559a429ee3.png">

3. 순서 보장
<img width="654" alt="스크린샷 2023-01-17 오후 7 54 38" src="https://user-images.githubusercontent.com/96857599/212881042-423a0646-3af1-49a5-abd0-4905f1509b8c.png">
- 순서가 잘못된 경우 순서를 맞춰서 다시 보낼 수 있도록 함.
	-> TCP에 출발지 PORT, 목적지 PORT 전송 제어, 순서, 검증 정보 등이 있기 때문에 가능함.
	
#### UDP 특징
사용자 데이터그램 프로토콜(User Datagram Protocol)

<img width="666" alt="스크린샷 2023-01-17 오후 7 56 13" src="https://user-images.githubusercontent.com/96857599/212881363-becbfd4e-5fa0-42e0-ba8e-ac1e65e71c02.png">

- 하얀 도화지에 비유(기능이 거의 없음) 
- 연결지향 - TCP 3 way handshake X 
- 데이터 전달 보증 X
- 순서 보장 X
- 데이터 전달 및 순서가 보장되지 않지만, 단순하고 빠름
- 정리
	- IP와 거의 같다. +PORT +체크섬 정도만 추가
	- 애플리케이션에서 추가 작업 필요

UDP 사용 이유
- TCP는 데이터 양도 많고, 속도도 느림(3 way handshake) -> TCP는 변경하기 힘듦
- 더 최적화하기 위해 사용하기 좋음 -> 최근 각광 받기 시작

### PORT (항구)

<img width="640" alt="스크린샷 2023-01-17 오후 8 03 44" src="https://user-images.githubusercontent.com/96857599/212882852-49e18ea4-f1f3-427e-902a-e889271f52e0.png">


- 패킷 
<img width="666" alt="스크린샷 2023-01-17 오후 8 04 35" src="https://user-images.githubusercontent.com/96857599/212883005-46146082-9e8d-4cc4-a2f7-970759c2ad94.png">

<img width="664" alt="스크린샷 2023-01-17 오후 8 05 23" src="https://user-images.githubusercontent.com/96857599/212883172-69b975d2-3d46-4d73-af4f-cb60bebcd48d.png">
- 각 IP에서 요청을 보낼 때 패킷에 출발 PORT와 도착 PORT를 저장해서 보내게 됨
- 각 PORT에 맞게 요청-응답

비유
IP: 아파트
PORT: 호 수

<img width="670" alt="스크린샷 2023-01-17 오후 8 07 47" src="https://user-images.githubusercontent.com/96857599/212883604-7e4311e7-37ac-46ff-828c-905b775fc087.png">


### DNS

#### IP의 단점
1. 기억하기 어렵다.
2. 변경될 수 있다.

<img width="667" alt="스크린샷 2023-01-17 오후 8 08 15" src="https://user-images.githubusercontent.com/96857599/212883714-474563bc-bcfc-4c66-9274-97a66316302b.png">

<img width="642" alt="스크린샷 2023-01-17 오후 8 08 45" src="https://user-images.githubusercontent.com/96857599/212883814-94e8fad0-2437-43fb-91c1-b5f388d8d45c.png">

<img width="653" alt="스크린샷 2023-01-17 오후 8 08 32" src="https://user-images.githubusercontent.com/96857599/212883773-57e0e8b7-6652-4dc8-b51f-362588d592b3.png">

#### DNS
도메인 네임 시스템(Domain Name System)

- 전화번호부와 같은 느낌
- 도메인 명을 IP 주소로 변환

#### DNS 사용
1. 도메인을 구매 등으로 획득
2. 도메인 명을 IP와 연결
3. IP가 바뀌면 바뀐 IP를 도메인에 다시 연결
<img width="649" alt="스크린샷 2023-01-17 오후 8 10 55" src="https://user-images.githubusercontent.com/96857599/212884275-bdcd8875-50f3-445c-84a8-69321788bbc6.png">

## URI와 웹 브라우저 요청 

### URI(Uniform Resource Identifier)

- URI는 로케이터(locator), 이름(name) 또는 둘다 추가로 분류될 수 있다. 
	-> [1.1.3. URI, URL, and URN	](https://www.ietf.org/rfc/rfc3986.txt)
	
<img width="666" alt="스크린샷 2023-01-20 오전 11 57 59" src="https://user-images.githubusercontent.com/96857599/213608495-69db666b-bc08-4920-b757-66669540b41a.png">

<img width="690" alt="스크린샷 2023-01-20 오전 11 58 23" src="https://user-images.githubusercontent.com/96857599/213608537-2cbec6ba-8f9a-4f26-82a6-01cbc6a5d5bd.png">

#### 단어 뜻
- Uniform: 리소스 식별하는 통일된 방식
- Resource: 자원, URI로 식별할 수 있는 모든 것(제한 없음)
- Identifier: 다른 항목과 구분하는데 필요한 정보

- URL: Uniform Resource Locator 
- URN: Uniform Resource Name

-URL - Locator: 리소스가 있는 위치를 지정
- URN - Name: 리소스에 이름을 부여
- 위치는 변할 수 있지만, 이름은 변하지 않는다.
- urn:isbn:8960777331 (어떤 책의 isbn URN)
- URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음 
- 앞으로 URI를 URL과 같은 의미로 이야기하겠음

#### 전체 문법

- scheme://[userinfo@]host[:port][/path][?query][#fragment] 
- https://www.google.com:443/search?q=hello&hl=ko

- 프로토콜(https) 
- 호스트명(www.google.com) 
- 포트 번호(443)
- 패스(/search)
- 쿼리 파라미터(q=hello&hl=ko)


1. scheme
- **scheme:**//[userinfo@]host[:port][/path][?query][#fragment] 
- **https**://www.google.com:443/search?q=hello&hl=ko
- 주로 프로토콜 사용
- 프로토콜: 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙
	- 예) http, https, ftp 등등
- http는 80 포트, https는 443 포트를 주로 사용, 포트는 생략 가능 
- https는 http에 보안 추가 (HTTP Secure)



2. userinfo
- URL에 사용자정보를 포함해서 인증 
- 거의 사용하지 않음
- scheme://**[userinfo@]**host[:port][/path][?query][#fragment] 
- https://www.google.com:443/search?q=hello&hl=ko


3. host
- 호스트명
- 도메인명 또는 IP 주소를 직접 사용가능
- scheme://[userinfo@]**host**[:port][/path][?query][#fragment] 
- https://**www.google.com**:443/search?q=hello&hl=ko


4. port
- 포트(PORT)
- 접속 포트
- 일반적으로 생략, 생략시 http는 80, https는 443
- scheme://[userinfo@]host**[:port]**[/path][?query][#fragment] 
- https://www.google.com:**443**/search?q=hello&hl=ko


5. path
- 리소스 경로(path), 계층적 구조 
- 예)
	- /home/file1.jpg
	- /members
	- /members/100, /items/iphone12
- scheme://[userinfo@]host[:port]**[/path]**[?query][#fragment] 
- https://www.google.com:443/**search**?q=hello&hl=ko


6. query
- key=value 형태
- ?로 시작, &로 추가 가능 ?keyA=valueA&keyB=valueB
- query parameter, query string 등으로 불림, 웹서버에 제공하는 파라미터, 문자 형태
- scheme://[userinfo@]host[:port][/path]**[?query]**[#fragment] 
- https://www.google.com:443/search**?q=hello&hl=ko**


7. fragment
- html 내부 북마크 등에 사용
- 서버에 전송하는 정보 아님
- 잘 사용하지 않음
- scheme://[userinfo@]host[:port][/path][?query]**[#fragment]**
- https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started.html**#getting-started-introducing-spring-boot**


### 웹 브라우저 요청 흐름

1. 구글에 검색할 때
<img width="641" alt="스크린샷 2023-01-22 오후 1 23 06" src="https://user-images.githubusercontent.com/96857599/213900514-e4273da3-80d4-473d-9529-e0b0eff4a688.png">

2. DNS 조회를 통해 구글 서버를 찾음
<img width="668" alt="스크린샷 2023-01-22 오후 1 22 29" src="https://user-images.githubusercontent.com/96857599/213900499-1e68042b-2b54-4e3d-ba62-3e224043f2b3.png">

3. HTTP 요청 메세지 
<img width="687" alt="스크린샷 2023-01-22 오후 1 24 24" src="https://user-images.githubusercontent.com/96857599/213900539-64db39e6-52c8-4754-85b7-0f8c945878d1.png">

4. HTTP 메시지 전송
<img width="677" alt="스크린샷 2023-01-22 오후 1 25 27" src="https://user-images.githubusercontent.com/96857599/213900560-32a41800-d3f0-4711-8abb-9cd5b04b959a.png">

1. 웹 브라우저가 HTTP 메시지 생성
2. SOCKET 라이브러리를 통해 전달
	- A: TCP/IP 연결(IP, PORT) -> TCP 3 way handshake (SYN, SYN+ACK, SYN)
	- B: 데이터 전달
3. TCP/IP 패킷 생성(port 정보 추가), HTTP 메시지 포함

<img width="672" alt="스크린샷 2023-01-22 오후 1 34 45" src="https://user-images.githubusercontent.com/96857599/213900787-99a5e781-1e83-4eb9-ab44-4cc802d05b8a.png">

- HTTP 메시지 추가
<img width="674" alt="스크린샷 2023-01-22 오후 1 35 30" src="https://user-images.githubusercontent.com/96857599/213900816-f8be61bf-dc70-4a23-b2b8-308b185dcc69.png">

4. 인터넷 망으로 전달
<img width="673" alt="스크린샷 2023-01-22 오후 1 35 40" src="https://user-images.githubusercontent.com/96857599/213900822-8500f69c-415e-4fd4-a0ff-5285f26edb23.png">

5. 구글 서버에서 TCP/IP 패킷을 벗기고, HTTP 메시지 확인
<img width="658" alt="스크린샷 2023-01-22 오후 1 36 01" src="https://user-images.githubusercontent.com/96857599/213900833-27bd8e2c-b26d-4c15-9278-cb7ff3278e88.png">

6. 구글 서버에서 HTTP 응답 메시지 생성
<img width="654" alt="스크린샷 2023-01-22 오후 1 37 25" src="https://user-images.githubusercontent.com/96857599/213900859-41d0efe7-55e3-458d-8857-bb50c3ad4157.png">

7. 응답 패킷을 전달
<img width="658" alt="스크린샷 2023-01-22 오후 1 38 11" src="https://user-images.githubusercontent.com/96857599/213900886-c1c9fdbd-60e2-447a-a37c-131bc52095f2.png">

8. 웹 브라우저에 도착 후 TCP/IP 패킷을 벗겨내고, HTTP 응답 메시지를 화면에 띄움
<img width="650" alt="스크린샷 2023-01-22 오후 1 39 55" src="https://user-images.githubusercontent.com/96857599/213900938-dedca144-75d7-43e9-b7e6-833977630854.png">
<img width="655" alt="스크린샷 2023-01-22 오후 1 40 08" src="https://user-images.githubusercontent.com/96857599/213900946-9912a4f8-e2ea-42a6-b863-0b17696bebeb.png">


## HTTP 기본

### 모든 것이 HTTP(HyperText Transfer Protocol)
HTTP 메시지에 모든 것을 전송

- HTML, TEXT
- IMAGE, 음성, 영상, 파일
- JSON, XML (API)
- 거의 모든 형태의 데이터 전송 가능
- 서버간에 데이터를 주고 받을 때도 대부분 HTTP 사용 
- 지금은 HTTP 시대!


#### HTTP 역사
- HTTP/0.9 1991년: GET 메서드만 지원, HTTP 헤더X
- HTTP/1.0 1996년: 메서드, 헤더 추가
- HTTP/1.1 1997년: 가장 많이 사용, 우리에게 가장 중요한 버전
	- RFC2068 (1997) -> RFC2616 (1999) -> RFC7230~7235 (2014) 
- HTTP/2 2015년: 성능 개선
- HTTP/3 진행중: TCP 대신에 UDP 사용, 성능 개선


#### 기반 프로토콜

- TCP: HTTP/1.1, HTTP/2
- UDP: HTTP/3
- 현재 HTTP/1.1 주로 사용
	- HTTP/2, HTTP/3 도 점점 증가
	
- 네이버 
<img width="1215" alt="스크린샷 2023-01-22 오후 1 51 19" src="https://user-images.githubusercontent.com/96857599/213901198-e75f99ed-ec89-4dfe-b547-695e16b99958.png">
- 구글에서 "hello" 검색
<img width="1215" alt="스크린샷 2023-01-22 오후 1 51 19" src="https://user-images.githubusercontent.com/96857599/213901198-e75f99ed-ec89-4dfe-b547-695e16b99958.png">

#### HTTP 특징

- 클라이언트 서버 구조
- 무상태 프로토콜(스테이스리스), 비연결성
- HTTP 메시지
- 단순함, 확장 가능

### 클라이언트 서버 구조

- Request Response 구조
- 클라이언트는 서버에 요청을 보내고, 응답을 대기 
- 서버가 요청에 대한 결과를 만들어서 응답

<img width="560" alt="스크린샷 2023-01-23 오후 11 09 37" src="https://user-images.githubusercontent.com/96857599/214060221-caf55dec-fc94-4541-b91c-3f01195e8dd9.png">

### 무상태 프로토콜
스테이스리스(Stateless)

- 서버가 클라이언트의 상태를 보존X 
- 장점: 서버 확장성 높음(스케일 아웃) 
- 단점: 클라이언트가 추가 데이터 전송

<img width="679" alt="스크린샷 2023-01-23 오후 11 22 16" src="https://user-images.githubusercontent.com/96857599/214063093-986b6174-ad6b-4f36-9674-77a558008296.png">
1. 상태 유지 - stateful
- 중간에 다른 점원으로 바뀌면 안된다. (중간에 다른 점원으로 바뀔 때 상태 정보를 다른 점원에게 미리 알려줘야 한다.)
- 서버가 클라이언트의 이전 상태를 유지, 보존해주는 것

<img width="655" alt="스크린샷 2023-01-23 오후 11 22 52" src="https://user-images.githubusercontent.com/96857599/214063209-3cf433bc-edf9-420e-a045-26ef0262ec9e.png">
2. 무상태 - stateless
- 중간에 다른 점원으로 바뀌어도 된다.
	- 갑자기 고객이 증가해도 점원을 대거 투입할 수 있다.
	- 갑자기 클라이언트 요청이 증가해도 서버를 대거 투입할 수 있다.
- 무상태는 응답 서버를 쉽게 바꿀 수 있다. -> 무한한 서버 증설 가능
- 고객이 필요한 데이터를 그때그때 전달할 수 있음

#### 상태 유지 - stateful
<img width="636" alt="스크린샷 2023-01-23 오후 11 25 36" src="https://user-images.githubusercontent.com/96857599/214063758-b85731d3-ee6e-4faf-a97b-b290ff2b575e.png">

- 서버 1이 고장나면 클라이언트A는 처음부터 다시 해야함.
<img width="639" alt="스크린샷 2023-01-23 오후 11 27 43" src="https://user-images.githubusercontent.com/96857599/214064205-f63b91d5-f959-4c55-bb24-3d8dca2fa4b8.png">

#### 무상태 - stateless
<img width="652" alt="스크린샷 2023-01-23 오후 11 28 08" src="https://user-images.githubusercontent.com/96857599/214064286-83d9dab0-9844-4337-b1f3-3aa74fea2cea.png">

- 그러나 Stateless는 처음부터 필요한 데이터를 함께 보내기 때문에 다른 서버에 그대로 연결하면 된다.
<img width="656" alt="스크린샷 2023-01-23 오후 11 28 55" src="https://user-images.githubusercontent.com/96857599/214064496-6e1d2cb4-933f-4f2d-a4e5-0b26e73c720f.png">

- 수평 확장 유리 -> 이벤트할 때 유용함
<img width="663" alt="스크린샷 2023-01-23 오후 11 29 39" src="https://user-images.githubusercontent.com/96857599/214064671-9a3d90ab-8447-4a89-b2bf-624bf61eb6a8.png">

#### Stateless 실무 한계
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

1. 연결을 유지하는 모델

- TCP/IP 연결의 경우 기본적으로 요청과 응답 후에 연결을 유지함.
<img width="645" alt="스크린샷 2023-01-23 오후 11 32 43" src="https://user-images.githubusercontent.com/96857599/214065410-d70fc9bb-b1e3-45f7-86e9-38dd3b02d1fc.png">

- 클라이언트2가 연결을 해도 클라이언트1과의 연결은 유지됨.
<img width="666" alt="스크린샷 2023-01-23 오후 11 34 17" src="https://user-images.githubusercontent.com/96857599/214065790-c5228e29-5bab-4079-931a-dd6e53fa9919.png">

- 클라이언트3을 연결할 때에도 클라이언트 1, 2의 연결은 유지되므로 서버 자원을 소모하게 됨.
<img width="647" alt="스크린샷 2023-01-23 오후 11 35 01" src="https://user-images.githubusercontent.com/96857599/214065964-e3e3ad16-c66c-4143-b8d6-288c72849eda.png">

- 재연결
<img width="646" alt="스크린샷 2023-01-23 오후 11 36 12" src="https://user-images.githubusercontent.com/96857599/214066263-be144b09-88aa-4cda-8b66-ef8ee0bb4b87.png">

2. 연결을 유지하지 않는 모델

- TCP/IP 연결 후 필요 없어진 연결은 끊어짐
<img width="650" alt="스크린샷 2023-01-23 오후 11 37 33" src="https://user-images.githubusercontent.com/96857599/214066574-092e97ae-95a3-4de3-9234-d560078fbe62.png">
<img width="651" alt="스크린샷 2023-01-23 오후 11 37 44" src="https://user-images.githubusercontent.com/96857599/214066613-87206e4b-931c-426a-82a7-2a0057406aaa.png">


- 필요할 때 연결하고, 응답후 끊어지면 서버의 자원을 최소한으로 사용함.
<img width="649" alt="스크린샷 2023-01-23 오후 11 38 35" src="https://user-images.githubusercontent.com/96857599/214066807-4af4fb47-7d07-456c-b213-69ecf0be2eaa.png">
<img width="643" alt="스크린샷 2023-01-23 오후 11 38 44" src="https://user-images.githubusercontent.com/96857599/214066854-da39d406-ce11-4105-905b-9e353a97d35a.png">
<img width="650" alt="스크린샷 2023-01-23 오후 11 38 56" src="https://user-images.githubusercontent.com/96857599/214066896-4885c753-b4fb-4b68-9f6b-a769f889167e.png">


#### 비 연결성
- HTTP는 기본이 연결을 유지하지 않는 모델 
- 일반적으로 초 단위의 이하의 빠른 속도로 응답
- 1시간 동안 수천명이 서비스를 사용해도 실제 서버에서 동시에 처리하는 요청은 수십개 이하로 매우 작음
	- 예) 웹 브라우저에서 계속 연속해서 검색 버튼을 누르지는 않는다. 
- 서버 자원을 매우 효율적으로 사용할 수 있음

#### 비 연결성의 한계와 극복

한계
- TCP/IP 연결을 새로 맺어야 함 - 3 way handshake 시간 추가
- 웹 브라우저로 사이트를 요청하면 HTML 뿐만 아니라 자바스크립트, css, 추가 이미지 등등 수 많은 자원이 함께 다운로드
<img width="656" alt="스크린샷 2023-01-23 오후 11 43 07" src="https://user-images.githubusercontent.com/96857599/214067959-79be21db-da5c-45a6-9bca-df676ffcbfc7.png">
<img width="1215" alt="스크린샷 2023-01-23 오후 11 42 31" src="https://user-images.githubusercontent.com/96857599/214067834-cf60cc87-1b9a-4ed6-bc76-e21d8ce5c86f.png">

극복
- 지금은 HTTP 지속 연결(Persistent Connections)로 문제 해결 
- HTTP/2, HTTP/3에서 더 많은 최적화
<img width="655" alt="스크린샷 2023-01-23 오후 11 43 45" src="https://user-images.githubusercontent.com/96857599/214068114-7308d787-03e1-49c7-98eb-1a25156872a1.png">

#### 스테이스리스를 기억하자 
- 서버 개발자들이 어려워하는 업무
- 정말 같은 시간에 딱 맞추어 발생하는 대용량 트래픽
	- 예) 선착순 이벤트, 명절 KTX 예약, 학과 수업 등록
	- 예) 저녁 6:00 선착순 1000명 치킨 할인 이벤트 -> 수만명 동시 요청

-> 맨 첫 페이지에 html로만 이루어진 페이지를 두어 클라이언트들의 클릭을 분산시키는 방법이 있다.

### HTTP 메시지

- HTTP의 요청 메시지와 HTTP 응답 메시지는 다르다.
<img width="671" alt="스크린샷 2023-01-25 오후 3 03 36" src="https://user-images.githubusercontent.com/96857599/214492085-73ea6e10-4a4d-402e-afc1-4582d4fc1bdb.png">

- 요청 메시지도 본문을 가질 수 있다. (예시에서만 없는 것일 뿐이다. )
<img width="689" alt="스크린샷 2023-01-25 오후 3 04 46" src="https://user-images.githubusercontent.com/96857599/214492252-0ebd9dad-b5dd-4d39-9671-2666c0a6994a.png">

<img width="680" alt="스크린샷 2023-01-25 오후 3 06 20" src="https://user-images.githubusercontent.com/96857599/214492459-f68ef5fc-5be4-44c8-867d-cb0bd6facfce.png">

#### 시작 라인

1. 요청 메시지
<img width="660" alt="스크린샷 2023-01-25 오후 3 07 23" src="https://user-images.githubusercontent.com/96857599/214492620-ba9d371a-5ed0-4c70-9957-e46a9ba2672a.png">

1-1. 요청 메시지 - HTTP 메서드
<img width="666" alt="스크린샷 2023-01-25 오후 3 09 53" src="https://user-images.githubusercontent.com/96857599/214493043-8df61ffb-19d3-4736-9b2e-0e700156b0e3.png">

1-2. 요청 메시지 - 요청 대상
<img width="680" alt="스크린샷 2023-01-25 오후 3 11 13" src="https://user-images.githubusercontent.com/96857599/214493222-54c83965-4bd3-4c1f-a0fd-ab56c4a823ec.png">

1-3. 요청 메시지 - HTTP 버전
<img width="665" alt="스크린샷 2023-01-25 오후 3 12 33" src="https://user-images.githubusercontent.com/96857599/214493386-c17f3425-63ef-4f47-a6d7-4a85697a7315.png">

2. 응답 메시지
<img width="653" alt="스크린샷 2023-01-25 오후 3 13 06" src="https://user-images.githubusercontent.com/96857599/214493476-20c085db-97b1-4d1b-b3ff-2c801825e796.png">


#### HTTP 헤더
<img width="658" alt="스크린샷 2023-01-25 오후 3 15 27" src="https://user-images.githubusercontent.com/96857599/214493751-3fc9b71c-af45-4931-9653-e88e56c7af15.png">

1. 용도
<img width="677" alt="스크린샷 2023-01-25 오후 3 16 46" src="https://user-images.githubusercontent.com/96857599/214493932-0eb90cce-9eff-405a-a6aa-15113b5975a0.png">

#### HTTP 메시지 바디
<img width="671" alt="스크린샷 2023-01-25 오후 3 18 16" src="https://user-images.githubusercontent.com/96857599/214494137-e3840e8b-edee-4c9c-9c61-49b3e76bc612.png">

> 단순함 확장 가능

> HTTP는 단순하다. 스펙도 읽어볼만...
> HTTP 메시지도 매우 단순
> 크게 성공하는 표준 기술은 단순하지만 확장 가능한 기술

#### HTTP 정리

- HTTP 메시지에 모든 것을 전송
- HTTP 역사 HTTP/1.1을 기준으로 학습 클라이언트 서버 구조
- 무상태 프로토콜(스테이스리스)
- HTTP 메시지
- 단순함, 확장 가능
- 지금은 HTTP 시대


## HTTP 메서드
1. HTTP API를 만들어보자
2. HTTP 메서드 - GET, POST
3. HTTP 메서드 - PUT, PATCH, DELETE
4. HTTP 메서드의 속성

### HTTP API를 만들어보자(왜 메서드를 사용하게 )

#### 요구사항
- 회원 정보 관리 API를 만들어라.
	- 회원 목록 조회 
	- 회원 조회
	- 회원 등록
	- 회원 수정
	- 회원 삭제

#### API URI 설계
- URI(Uniform Resource Identifier)
	- 회원 목록 조회 /read-member-list 
	- 회원 조회 /read-member-by-id 
	- 회원 등록 /create-member
	- 회원 수정 /update-member
	- 회원 삭제 /delete-member
	
-> 이것은 좋은 URI 설계일까?
	- 가장 중요한 것은 리소스를 식별하는 것이다.
#### API URI 고민
- 리소스의 의미는 뭘까?
	- 회원을 등록하고 수정하고 조회하는게 리소스가 아니다!
	- 예) 미네랄을 캐라 -> 미네랄이 리소스
	- 회원이라는 개념 자체가 바로 리소스다.
- 리소스를 어떻게 식별하는게 좋을까? 
	- 회원을 등록하고 수정하고 조회하는 것을 모두 배제
	- 회원이라는 리소스만 식별하면 된다. -> 회원 리소스를 URI에 매핑

#### API URI 설계
- 리소스 식별, URI 계층 구조 활용
- 회원 목록 조회 /members
- 회원 조회 /members/{id} -> 어떻게 구분하지? 
- 회원 등록 /members/{id} -> 어떻게 구분하지? 
- 회원 수정 /members/{id} -> 어떻게 구분하지? 
- 회원 삭제 /members/{id} -> 어떻게 구분하지?

> 참고: 계층 구조상 상위를 컬렉션으로 보고 복수단어 사용 권장(member -> members)

#### 리소스와 행위를 분리
- 가장 중요한 것은 리소스를 식별하는 것

- URI는 리소스만 식별!
- 리소스와 해당 리소스를 대상으로 하는 행위을 분리
	- 리소스: 회원
	- 행위: 조회, 등록, 삭제, 변경
- 리소스는 명사, 행위는 동사 (미네랄을 캐라) 
- 행위(메서드)는 어떻게 구분?

### HTTP 메서드 - GET, POST
> Representation 설명 전
주요 메서드
- GET: 리소스 조회
- POST: 요청 데이터 처리, 주로 등록에 사용 
- PUT: 리소스를 대체, 해당 리소스가 없으면 생성 
- PATCH: 리소스 부분 변경
- DELETE: 리소스 삭제

기타 메서드
- HEAD: GET과 동일하지만 메시지 부분을 제외하고, 상태 줄과 헤더만 반환
- OPTIONS: 대상 리소스에 대한 통신 가능 옵션(메서드)을 설명(주로 CORS에서 사용) 
- CONNECT: 대상 자원으로 식별되는 서버에 대한 터널을 설정
- TRACE: 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행


#### GET
- 리소스 조회
- 서버에 전달하고 싶은 데이터는 query(쿼리 파라미터, 쿼리 스트링)를 통해서 전달
- 메시지 바디를 사용해서 데이터를 전달할 수 있지만, 지원하지 않는 곳이 많아서 권장하지 않음
<img width="344" alt="스크린샷 2023-01-25 오후 3 34 56" src="https://user-images.githubusercontent.com/96857599/214496518-7666bb93-a3f2-4813-9eeb-1195b690360b.png">


<img width="667" alt="스크린샷 2023-01-25 오후 3 38 32" src="https://user-images.githubusercontent.com/96857599/214497062-0c42dfdc-ede6-4b35-a3c3-6fe68842715c.png">
<img width="682" alt="스크린샷 2023-01-25 오후 3 39 08" src="https://user-images.githubusercontent.com/96857599/214497154-8e28821b-ba6f-4c10-96af-6e7c28be9814.png">
<img width="666" alt="스크린샷 2023-01-25 오후 3 39 22" src="https://user-images.githubusercontent.com/96857599/214497185-2ef24599-d299-47ea-a8fb-b91cc7caec0e.png">

#### POST (클라이언트 측에서 데이터를 전달하여 처리를 요청하는 것)
- 요청 데이터 처리
- 메시지 바디를 통해 서버로 요청 데이터 전달
- 서버는 요청 데이터를 처리
	- 메시지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행한다.
- 주로 전달된 데이터로 신규 리소스 등록, 프로세스 처리에 사용	
<img width="219" alt="스크린샷 2023-01-25 오후 3 42 52" src="https://user-images.githubusercontent.com/96857599/214497640-1ffc4e4d-d0fe-42c3-b1e3-1ebd8e78a04e.png">

- /members로 오면 전달된 데이터를 어떤 방식으로 처리할지 미리 약속함.
<img width="670" alt="스크린샷 2023-01-25 오후 3 43 05" src="https://user-images.githubusercontent.com/96857599/214497664-dac7aeb3-dc9d-422a-ad1c-b4e8b45e73e7.png">

- 신규 리소스 식별자 생성
<img width="655" alt="스크린샷 2023-01-25 오후 3 43 17" src="https://user-images.githubusercontent.com/96857599/214497695-4aa6eca8-812a-4b31-a10b-824de9a2078c.png">

- 응답 데이터
<img width="671" alt="스크린샷 2023-01-25 오후 3 44 27" src="https://user-images.githubusercontent.com/96857599/214497867-785a65e2-d32b-4d30-b959-0f3a4d909f80.png">

##### 요청 데이터를 어떻게 처리한다는 뜻일까? 
예시)
- 스펙: POST 메서드는 대상 리소스가 리소스의 고유 한 의미 체계에 따라 요청에 포함 된 표현을 처리하도록 요청합니다. (구글 번역) 
- 예를 들어 POST는 다음과 같은 기능에 사용됩니다.
	- HTML 양식에 입력 된 필드와 같은 데이터 블록을 데이터 처리 프로세스에 제공	
		- 예) HTML FORM에 입력한 정보로 회원 가입, 주문 등에서 사용
	- 게시판, 뉴스 그룹, 메일링 리스트, 블로그 또는 유사한 기사 그룹에 메시지 게시
		- 예) 게시판 글쓰기, 댓글 달기
	- 서버가 아직 식별하지 않은 새 리소스 생성
		- 예) 신규 주문 생성
	- 기존 자원에 데이터 추가
		- 예) 한 문서 끝에 내용 추가하기
- 정리: 이 리소스 URI에 POST 요청이 오면 요청 데이터를 어떻게 처리할지 리소스마다 따로 정해야 함 -> 정해진 것이 없음


#### 정리
1. 새 리소스 생성(등록)
	- 서버가 아직 식별하지 않은 새 리소스 생성
2. 요청 데이터 처리
	- 단순히 데이터를 생성하거나, 변경하는 것을 넘어서 프로세스를 처리해야 하는 경우
	- 예) 주문에서 결제완료 -> 배달시작 -> 배달완료 처럼 단순히 값 변경을 넘어 프로세스의 상태가 변경되는 경우 
	- POST의 결과로 새로운 리소스가 생성되지 않을 수도 있음
	- 예) POST /orders/{orderId}/start-delivery (컨트롤 URI)
3. 다른 메서드로 처리하기 애매한 경우
	- 예) JSON으로 조회 데이터를 넘겨야 하는데, GET 메서드를 사용하기 어려운 경우 
	- 애매하면 POST


### HTTP 메서드 - PUT, PATCH, DELETE

#### PUT
- 리소스를 완전히 대체
	- 리소스가 있으면 대체 
	- 리소스가 없으면 생성 
	- 쉽게 이야기해서 덮어버림
- 중요! 클라이언트가 리소스를 식별 
	- 클라이언트가 리소스 위치를 알고 URI 지정 -> 구체적인 리소스를 지정한다는 점에서 POST와의 차이를 보임
	- POST와 차이점
<img width="220" alt="스크린샷 2023-01-25 오후 4 00 16" src="https://user-images.githubusercontent.com/96857599/214500270-2a1615b4-a646-4936-8927-0af740a06efa.png">

1. 리소스가 있는 경우
<img width="651" alt="스크린샷 2023-01-25 오후 4 01 59" src="https://user-images.githubusercontent.com/96857599/214500520-bc288d20-7edc-4324-9ab1-5501efab6c38.png">
<img width="648" alt="스크린샷 2023-01-25 오후 4 02 06" src="https://user-images.githubusercontent.com/96857599/214500538-a376607d-27f5-4ea0-81c1-be506df86808.png">

2. 리소스가 없는 경우
<img width="663" alt="스크린샷 2023-01-25 오후 4 03 11" src="https://user-images.githubusercontent.com/96857599/214500685-79e508f2-77c7-42a6-b664-19a1693a6fd7.png">
<img width="649" alt="스크린샷 2023-01-25 오후 4 03 20" src="https://user-images.githubusercontent.com/96857599/214500703-da7aae37-a334-41e3-81dd-acfcede28bd2.png">

3. 주의! - 리소스를 완전히 대체한다. (갈아치우는 것)
<img width="666" alt="스크린샷 2023-01-25 오후 4 03 30" src="https://user-images.githubusercontent.com/96857599/214500724-6295c9c5-3ebb-4bc5-888c-c6f0b106da49.png">
<img width="663" alt="스크린샷 2023-01-25 오후 4 03 44" src="https://user-images.githubusercontent.com/96857599/214500752-2b432a15-8b62-4555-9315-f5272c90325a.png">

#### PATCH
- 리소스를 부분 변경하는 것
<img width="215" alt="스크린샷 2023-01-25 오후 4 05 51" src="https://user-images.githubusercontent.com/96857599/214501104-5dab1e0d-6bfd-41df-81be-4c1a6bbd2457.png">


<img width="671" alt="스크린샷 2023-01-25 오후 4 05 06" src="https://user-images.githubusercontent.com/96857599/214500982-249adc61-20a2-432e-b89d-bb7a59185063.png">
<img width="656" alt="스크린샷 2023-01-25 오후 4 05 18" src="https://user-images.githubusercontent.com/96857599/214501024-11699e8a-df0a-47b7-b368-4397b88b302b.png">

> 특정 HTTP가 PATCH를 못 받아들이는 경우 POST를 사용하면 됨

#### DELETE
- 리소스 제거
<img width="211" alt="스크린샷 2023-01-25 오후 4 06 04" src="https://user-images.githubusercontent.com/96857599/214501148-54856f4f-9fdf-4f2b-a4e7-d574e27a2baa.png">

<img width="663" alt="스크린샷 2023-01-25 오후 4 06 17" src="https://user-images.githubusercontent.com/96857599/214501175-8e60834e-d982-4c44-a9c8-7001899bdc83.png">
<img width="659" alt="스크린샷 2023-01-25 오후 4 06 37" src="https://user-images.githubusercontent.com/96857599/214501240-36fb84b6-7aee-49f1-aae4-4ae9c9b1e79c.png">

### HTTP 메서드의 속성
- 안전(Safe Methods) 
- 멱등(Idempotent Methods) 
- 캐시가능(Cacheable Methods)
<img width="556" alt="스크린샷 2023-01-25 오후 4 08 08" src="https://user-images.githubusercontent.com/96857599/214501482-8b55b874-38f0-455e-ac62-59749cd336f2.png">


#### 안전(Safe)
- 호출해도 리소스를 변경하지 않는다. (예- GET, HEAD)
- Q: 그래도 계속 호출해서, 로그 같은게 쌓여서 장애가 발생하면요? 
- A: 안전은 해당 리소스만 고려한다. 그런 부분까지 고려하지 않는다.

#### 멱등(Idempotent)
- f(f(x)) = f(x)
- 한 번 호출하든 두 번 호출하든 100번 호출하든 결과가 똑같다.
- 멱등 메서드
	- GET: 한 번 조회하든, 두 번 조회하든 같은 결과가 조회된다.
	- PUT: 결과를 대체한다. 따라서 같은 요청을 여러번 해도 최종 결과는 같다. 
	- DELETE: 결과를 삭제한다. 같은 요청을 여러번 해도 삭제된 결과는 똑같다. 
	- POST: 멱등이 아니다! 두 번 호출하면 같은 결제가 중복해서 발생할 수 있다.

- Q: 재요청 중간에 다른 곳에서 리소스를 변경해버리면?
	- 사용자1: GET -> username:A, age:20
	- 사용자2: PUT -> username:A, age:30
	- 사용자1: GET -> username:A, age:30 -> 사용자2의 영향으로 바뀐 데이터 조회
- A: 멱등은 외부 요인으로 중간에 리소스가 변경되는 것 까지는 고려하지는 않는다.
	
##### 활용
- 자동 복구 메커니즘
- 서버가 TIMEOUT 등으로 정상 응답을 못주었을 때, 클라이언트가 같은 요청을 다시 해 도 되는가? 판단 근거

#### 캐시가능(Cacheable) 
- 응답 결과 리소스를 캐시해서 사용해도 되는가? 
- GET, HEAD, POST, PATCH 캐시가능
- 실제로는 GET, HEAD 정조만 캐시로 사용(URL만 키로 고려하면 되기 때문에 간단함)
	- POST, PATCH는 본문 내용까지 캐시 키로 고려해야 하는데, 구현이 쉽지 않음

## HTTP 메서드 활용
- 클라이언트에서 서버로 데이터 전송 
- HTTP API 설계 예시

### 클라이언트에서 서버로 데이터 전송

#### 데이터 전달 방식은 크게 2가지

- 쿼리 파라미터를 통한 데이터 전송
	- GET
	- 주로 정렬 필터(검색어)
- 메시지 바디를 통한 데이터 전송
	- POST, PUT, PATCH
	- 회원 가입, 상품 주문, 리소스 등록, 리소스 변경

### 클라이언트에서 서버로 데이터 전송 - 4가지 상황
- 정적 데이터 조회
	- 이미지, 정적 텍스트 문서 
- 동적 데이터 조회
	- 주로 검색, 게시판 목록에서 정렬 필터(검색어) 
- HTML Form을 통한 데이터 전송
	- 회원 가입, 상품 주문, 데이터 변경 
- HTTP API를 통한 데이터 전송
	- 회원 가입, 상품 주문, 데이터 변경
	- 서버 to 서버, 앱 클라이언트, 웹 클라이언트(Ajax)

### 정적 데이터 조회
- 쿼리 파라미터 미사용
<img width="670" alt="스크린샷 2023-01-25 오후 4 24 15" src="https://user-images.githubusercontent.com/96857599/214503807-a2141b30-04ee-4a0a-848c-0deb84d655e2.png">

#### 정리
- 이미지, 정적 텍스트 문서
- 조회는 GET 사용
- 정적 데이터는 일반적으로 쿼리 파라미터 없이 리소스 경로로 단순하게 조회 가능

### 동적 데이터 조회
- 쿼리 파라미터 사용
<img width="665" alt="스크린샷 2023-01-25 오후 4 26 30" src="https://user-images.githubusercontent.com/96857599/214504112-f8b6f985-af9b-4bff-bd8a-e81449350c29.png">

#### 정리
- 주로 검색, 게시판 목록에서 정렬 필터(검색어)
- 조회 조건을 줄여주는 필터, 조회 결과를 정렬하는 정렬 조건에 주로 사용 
- 조회는 GET 사용
- GET은 쿼리 파라미터 사용해서 데이터를 전달

### HTML Form 데이터 전송
- POST 전송 -> 저장
<img width="657" alt="스크린샷 2023-01-25 오후 4 29 41" src="https://user-images.githubusercontent.com/96857599/214504655-4a7f2b49-3a38-4bb8-8334-65e5e01c8442.png">

- GET 전송 -> 저장
<img width="673" alt="스크린샷 2023-01-25 오후 4 32 36" src="https://user-images.githubusercontent.com/96857599/214505128-a78d8952-56d3-41e2-80ef-137df006c994.png">

- GET 전송 -> 조회
<img width="650" alt="스크린샷 2023-01-25 오후 4 33 15" src="https://user-images.githubusercontent.com/96857599/214505282-738e5174-e721-41b4-9337-2971d416d679.png">

- multipart/form-data (주로 바이너리 데이터를 전송할 때 사용)
<img width="665" alt="스크린샷 2023-01-25 오후 4 35 45" src="https://user-images.githubusercontent.com/96857599/214505698-59a6c15f-02fd-452a-993b-e54036564935.png">

#### 정리

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

> 참고: HTML Form 전송은 GET, POST만 지원


### HTTP API 데이터 전송
- IOS나 안드로이드 같은 모바일 기기에서 서버에 바로 데이터를 전송해야할 때
<img width="666" alt="스크린샷 2023-01-25 오후 4 40 16" src="https://user-images.githubusercontent.com/96857599/214506591-3d86dccf-87ac-4b60-bb03-257911ff6a4c.png">

#### 정리
- 서버 to 서버
	- 백엔드 시스템 통신 
- 앱 클라이언트
	- 아이폰, 안드로이드 
- 웹 클라이언트
-	 HTML에서 Form 전송 대신 자바 스크립트를 통한 통신에 사용(AJAX)
-	 예) React, VueJs 같은 웹 클라이언트와 API 통신 
- POST, PUT, PATCH: 메시지 바디를 통해 데이터 전송
- GET: 조회, 쿼리 파라미터로 데이터 전달
- Content-Type: application/json을 주로 사용 (사실상 표준)
	- TEXT, XML, JSON 등등 (요즘엔(2022년) JSON 많이 사용함)


### HTTP API 설계 예시

- HTTP API - 컬렉션
	- POST 기반 등록
	- 예) 회원 관리 API 제공
- HTTP API - 스토어
	- PUT 기반 등록
	- 예) 정적 컨텐츠 관리, 원격 파일 관리 
- HTML FORM 사용
	- 웹 페이지 회원 관리 
	- GET, POST만 지원

### 회원 관리 시스템
#### API 설계 - post 기반 등록

- 회원 목록 /members -> GET
- 회원 등록 /members -> POST
- 회원 조회 /members/{id} -> GET
- 회원 수정 /members/{id} -> PATCH(부분적인 수정이므로 가장 자주 씀), PUT(게시글 작성할 때), POST 
- 회원 삭제 /members/{id} -> DELETE



#### POST - 신규 자원 등록 특징

- 클라이언트는 등록될 리소스의 URI를 모른다.(서버가 만들어준다.)
	- 회원 등록 /members -> POST
	- POST /members
- ⭐️서버가 새로 등록된 리소스 URI를 생성해준다.
	- HTTP/1.1 201 Created
	- Location: /members/100
- ⭐️컬렉션(Collection)
	- 서버가 관리하는 리소스 디렉토리 
	- 서버가 리소스의 URI를 생성하고 관리 
	- 여기서 컬렉션은 /members


### 파일 관리 시스템
#### API 설계 - PUT 기반 등록

- 파일 목록 /files -> GET
- 파일 조회 /files/{filename} -> GET 
- 파일 등록 /files/{filename} -> PUT 
- 파일 삭제 /files/{filename} -> DELETE 
- 파일 대량 등록 /files -> POST


#### PUT - 신규자원등록특징

- 클라이언트가 리소스 URI를 알고 있어야 한다.
	- 파일 등록 /files/{filename} -> PUT
	- PUT /files/star.jpg
- ⭐️클라이언트가 직접 리소스의 URI를 지정한다.
- ⭐️스토어(Store)
	- 클라이언트가 관리하는 리소스 저장소 
	- 클라이언트가 리소스의 URI를 알고 관리 
	- 여기서 스토어는 /files
	
> 대부분 post 기반의 컬렉션을 사용한다.

### HTML FORM 사용

- HTML FORM은 GET, POST만 지원
- AJAX 같은 기술을 사용해서 해결 가능 -> 회원 API 참고 
- 여기서는 순수 HTML, HTML FORM 이야기
- GET, POST만 지원하므로 제약이 있음


- 회원 목록   /members -> GET
- 회원 등록 폼 /members/new -> GET
- 회원 등록   /members/new(오류시에 등록 폼과 경로를 맞추면 좋다) 또는 /members -> POST
- 회원 조회   /members/{id} -> GET
- 회원 수정 폼 /members/{id}/edit -> GET
- 회원 수정    /members/{id}/edit, /members/{id} -> POST
- 회원 삭제    /members/{id}/delete -> POST (DELETE 메서드를 사용하지 못하기 때문에 컨드롤 URI 사용)

- HTML FORM은 GET, POST만 지원 
- ⭐️컨트롤 URI -> 최대한 리소스라는 개념을 가지고 URI를 설계하고, 안 될 때 사용한다.
	- GET, POST만 지원하므로 제약이 있음
	- 이런 제약을 해결하기 위해 동사로 된 리소스 경로 사용 (조작하는 기능을 수행하기 때문)
	- POST의 /new, /edit, /delete가 컨트롤 URI
	- HTTP 메서드로 해결하기 애매한 경우 사용(HTTP API 포함)


### 정리

- HTTP API - 컬렉션
	- POST 기반 등록
	- 서버가 리소스 URI 결정 
- HTTP API - 스토어
	- PUT 기반 등록
	- 클라이언트가 리소스 URI 결정 
- HTML FORM 사용
	- 순수 HTML + HTML form 사용
	- GET, POST만 지원

#### [참고하면 좋은 URI 설계 개념](https://restfulapi.net/resource-naming)

- 문서(document)
	- 단일 개념(파일 하나, 객체 인스턴스, 데이터베이스 row)
	- 예) /members/100, /files/star.jpg 
- 컬렉션(collection)
	- 서버가 관리하는 리소스 디렉터리 
	- 서버가 리소스의 URI를 생성하고 관리 
	- 예) /members
- 스토어(store)
	- 클라이언트가 관리하는 자원 저장소 
	- 클라이언트가 리소스의 URI를 알고 관리 
	- 예) /files
- 컨트롤러(controller), 컨트롤 URI
	- 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스 실행 
	- 동사를 직접 사용
	- 예) /members/{id}/delete

## HTTP 상태코드

### HTTP 상태코드 소개
 
상태 코드 - 클라이언트가 보낸 요청의 처리 상태를 응답에서 알려주는 기능

- 1xx (Informational): 요청이 수신되어 처리중
- 2xx (Successful): 요청 정상 처리
- 3xx (Redirection): 요청을 완료하려면 추가 행동이 필요
- 4xx (Client Error): 클라이언트 오류, 잘못된 문법등으로 서버가 요청을 수행할 수 없음 
- 5xx (Server Error): 서버 오류, 서버가 정상 요청을 처리하지 못함

#### 만약 모르는 상태 코드가 나타나면?

- 클라이언트가 인식할 수 없는 상태코드를 서버가 반환하면? 
- 클라이언트는 상위 상태코드로 해석해서 처리
- 미래에 새로운 상태 코드가 추가되어도 클라이언트를 변경하지 않아도 됨 
- 예)
	- 299 ??? -> 2xx (Successful) 
	- 451 ??? -> 4xx (Client Error) 
	- 599 ??? -> 5xx (Server Error)


### 1xx (Informational)
-> 요청이 수신되어 처리중

- 거의 사용하지 않으므로 생랴

### 2xx - 성공
-> 클라이언트의 요청을 성공적으로 처리

- 프로젝트를 진행할 때, 200 또는 201까지만 정해두고 사용하느 경우가 많다. 
- 각 팀에서 범위를 정해서 사용하는 것이 좋다. (너무 양이 많기 때문)

#### 200 OK
<img width="709" alt="스크린샷 2023-02-04 오후 3 52 27" src="https://user-images.githubusercontent.com/96857599/216753550-d0e73950-4476-4d3e-92f5-66b594b1853d.png">

#### 201 Created 
- POST 요청이므로 서버에서 자원을 생성하고, 자원에 대한 URI도 관리
<img width="717" alt="스크린샷 2023-02-04 오후 3 52 47" src="https://user-images.githubusercontent.com/96857599/216753564-c2166c5c-fc81-4473-8815-1a10ab790a46.png">

#### 202 Accepted 
-> 요청이 접수되었으나 처리가 완료되지 않았음
- 배치 처리 같은 곳에서 사용
- 예) 요청 접수 후 1시간 뒤에 배치 프로세스가 요청을 처리함

#### 204 No Content
-> 서버가 요청을 성공적으로 수행했지만, 응답 페이로드 본문에 보낼 데이터가 없음

- 예) 웹 문서 편집기에서 save 버튼
- save 버튼의 결과로 아무 내용이 없어도 된다.
- save 버튼을 눌러도 같은 화면을 유지해야 한다.
- 결과 내용이 없어도 204 메시지(2xx)만으로 성공을 인식할 수 있다.

### 3xx - 리다이렉션
-> 요청을 완료하기 위해 유저 에이전트(웹 브라우저)의 추가 조치 필요

- 300 Multiple Choices 
- 301 Moved Permanently 
- 302 Found
- 303 See Other
- 304 Not Modified
- 307 Temporary Redirect 
- 308 Permanent Redirect

#### 리다이렉션 이해
- 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동 (리다이렉트)

- 기존에 /event를 사용하다가 경로를 /new-event로 바꿈
-> 문제점: 기존의 경로를 저장해두고 사용하던 클라이언트들은 /event를 타고 들어옴
- HTTP/1.1 301 Moved Permanently Location: /new-event 라고 응답이 들어옴
- Location 경로로 자동으로 URL이 변경돼서 서버에 다시 /new-event 페이지로 요청함
<img width="615" alt="스크린샷 2023-02-04 오후 4 02 10" src="https://user-images.githubusercontent.com/96857599/216753922-edddb8cb-a0be-4e8e-805d-5de9e621c9c5.png">

**종류**
- 영구 리다이렉션 - 특정 리소스의 URI가 영구적으로 이동
	- 예) /members -> /users
	- 예) /event -> /new-event 
- 일시 리다이렉션 - 일시적인 변경
	- 주문 완료 후 주문 내역 화면으로 이동
	- PRG: Post/Redirect/Get (굉장히 자주 사용하는 패턴)
- 특수 리다이렉션
	- 결과 대신 캐시를 사용

#### 영구 리다이렉션
-> 301, 308
- 리소스의 URI가 영구적으로 이동
- 원래의 URL를 사용X, 검색 엔진 등에서도 변경 인지
- 301 Moved Permanently (실무에서 자주 사용함)
	- 리다이렉트시 요처 메서드가 GET으로 변하고, 본문이 제거될 수 있음(MAY)
<img width="715" alt="스크린샷 2023-02-04 오후 4 32 08" src="https://user-images.githubusercontent.com/96857599/216755103-b5c21c33-a373-4133-9d88-cc3000283744.png">

- 308 Permanent Redirect
	- 301과 기능은 같음
	- 리다이렉트 시 요청 메서드와 본문 유지(처음 POST를 보내면 리다이렉트도 POST 유지)
<img width="730" alt="스크린샷 2023-02-04 오후 4 34 55" src="https://user-images.githubusercontent.com/96857599/216755225-b5225dd9-3ced-44f2-99fe-ebf0a2ec8859.png">


#### 일시적인 리다이렉션
-> 302, 307, 303
 
- 리소스의 URI가 일시적으로 변경
- 따라서 검색 엔진 등에서 URL을 변경하면 안됨
- 302 Found
	- 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음(MAY)
- 307 Temporary Redirect
	- 302와 기능은 같음
	- **리다이렉트시 요청 메서드와 본문 유지**(요청 메서드를 변경하면 안된다. MUST NOT)
- 303 See Other
	- 302와 기능은 같음
	- **리다이렉트시 요청 메서드가 GET으로 변경**
	
	

### PRG: Post/Redirect/Get
-> 일시적인 리다이렉션 - 예시


#### PRG 사용전
- POST로 주문후에 웹 브라우저를 새로고침하면? 
- 새로고침은 다시 요청
- 중복 주문이 될 수 있다.


<img width="764" alt="스크린샷 2023-02-04 오후 4 40 56" src="https://user-images.githubusercontent.com/96857599/216755455-a544ef9b-9778-4692-a3fd-0fc16ce52c49.png">

-> 서버 차원에서 중복되 주문번호를 제거하는 것이 맞지만, 클라이언트 차원에서도 한번 방지하는 것도 좋다.

#### PRG 사용
- POST로 주문후에 새로 고침으로 인한 중복 주문 방지 
- POST로 주문후에 주문 결과 화면을 GET 메서드로 리다이렉트 
- 새로고침해도 결과 화면을 GET으로 조회
- 중복 주문 대신에 결과 화면만 GET으로 다시 요청

<img width="745" alt="스크린샷 2023-02-04 오후 4 44 13" src="https://user-images.githubusercontent.com/96857599/216755577-b4df328a-9f59-4e07-b9a2-a6001f0cd8d5.png">

- 리다이렉션 302 Found 또는 303 See Other를 통해 메서드를 Get으로 변경

- PRG 이후 리다이렉트
- URL이 이미 POST -> GET으로 리다이렉트 됨
- 새로 고침 해도 GET으로 결과 화면만 조회


## 정리
> 그래서 뭘 써야 하나요?

#### 302, 307, 303

- 잠깐 정리
	- 302 Found -> GET으로 변할 수 있음
	- 307 Temporary Redirect -> 메서드가 변하면 안됨 
	- 303 See Other -> 메서드가 GET으로 변경
- 역사
	- 처음 302 스펙의 의도는 HTTP 메서드를 유지하는 것
	- 그런데 웹 브라우저들이 대부분 GET으로 바꾸어버림(일부는 다르게 동작)
	- 그래서 모호한 302를 대신하는 명확한 307, 303이 등장함(301 대응으로 308도 등장)
- 현실
	- 307, 303을 권장하지만 현실적으로 이미 많은 애플리케이션 라이브러리들이 302를 기본값으로 사용 
	- 자동 리다이렉션시에 GET으로 변해도 되면 그냥 302를 사용해도 큰 문제 없음

#### 기타 리다이렉션 -> 300, 304

- 300 Multiple Choices: 안쓴다. 
- 304 Not Modified
	- 캐시를 목적으로 사용
	- 클라이언트에게 리소스가 수정되지 않았음을 알려준다. 따라서 클라이언트는 로컬PC에 저장된 캐시를 재사용한다. (캐시로 리다이렉트 한다.)
	- 304 응답은 응답에 메시지 바디를 포함하면 안된다. (로컬 캐시를 사용해야 하므로) 
	- 조건부 GET, HEAD 요청시 사용


### 4xx - 클라이언트 오류, 5xx - 서버 오류

#### 4xx (Client Error)
-> 클라이언트 오류

- 클라이언트의 요청에 잘못된 문법등으로 서버가 요청을 수행할 수 없음
- 오류의 원인이 클라이언트에 있음
- ⭐️중요! 클라이언트가 이미 잘못된 요청, 데이터를 보내고 있기 때문에, 똑같은 재시도가 실패함

> 4xx과 5xx의 가장 큰 차이: 4xx는 클라이언트에 오류 원인이 있으므로 재시도가 실패하지만, 5xx은 서버에 어류 원인이 있으므로 서버의 데이터가 복구된다면 같은 클라이언트의 요청에도 성공할 가능성이 있음

#### 400 Bad Request
-> 클라이언트가 잘못된 요청을 해서 서버가 요청을 처리할 수 없음

- 요청 구문, 메시지 등등 오류
- 클라이언트는 요청 내용을 다시 검토하고, 보내야함
- 예) 요청 파라미터가 잘못되거나, API 스펙이 맞지 않을 때

=> 백엔드 개발자가 막아야함

#### 401 Unauthorized
-> 클라이언트가 해당 리소스에 대한 인증이 필요함

- 인증(Authentication) 되지 않음
- 401 오류 발생시 응답에 WWW-Authenticate 헤더와 함께 인증 방법을 설명 
- 참고

- 인증(Authentication): 본인이 누구인지 확인, (로그인)
- 인가(Authorization): 권한부여 (ADMIN 권한처럼 특정 리소스에 접근할 수 있는 권한, 인증이 있어야 인가가 있음)
- 오류 메시지가 Unauthorized 이지만 인증 되지 않음 (이름이 아쉬움)

#### 403 Forbidden
-> 서버가 요청을 이해했지만 승인을 거부함

- 주로 인증 자격 증명은 있지만, 접근 권한이 불충분한 경우
- 예) 어드민 등급이 아닌 사용자가 로그인은 했지만, 어드민 등급의 리소스에 접근하는 경우

#### 404 Not Found
-> 요청 리소스를 찾을 수 없음

- 요청 리소스가 서버에 없음
- 또는 클라이언트가 권한이 부족한 리소스에 접근할 때 해당 리소스를 숨기고 싶을 때


#### 5xx (Server Error)
-> 서버 오류

- 서버 문제로 오류 발생
- 서버에 문제가 있기 때문에 재시도 하면 성공할 수도 있음(복구가 되거나 등등)

#### 500 Internal Server Error 
-> 서버 문제로 오류 발생, 애매하면 500 오류

- 서버 내부 문제로 오류 발생 
- 애매하면 500 오류

#### 503 Service Unavailable
-> 서비스 이용 불가
- 서버가 일시적인 과부하 또는 예정된 작업으로 잠시 요청을 처리할 수 없음 
- Retry-After 헤더 필드로 얼마뒤에 복구되는지 보낼 수도 있음



> 5xx는 정말 서버에 문제가 생겼을 때만 사용해야함. (로직에 문제가 있거나, 쿼리에 문제가 있거나, 데이터베이스에 문제가 생기는 경우 등등)


## HTTP 헤더1 - 일반 헤더

### HTTP 헤더 개요
<img width="659" alt="스크린샷 2023-02-04 오후 5 04 35" src="https://user-images.githubusercontent.com/96857599/216756347-5b241de8-3fd2-4f55-8977-1ce80ec4f9b5.png">
<img width="665" alt="스크린샷 2023-02-04 오후 5 04 44" src="https://user-images.githubusercontent.com/96857599/216756350-bdd8f0cd-2fb0-437a-884f-1edea48fdcb5.png">
<img width="662" alt="스크린샷 2023-02-04 오후 5 04 52" src="https://user-images.githubusercontent.com/96857599/216756358-9c9aae32-a5bd-4832-b25a-97f1107b07ac.png">
<img width="683" alt="스크린샷 2023-02-04 오후 5 05 03" src="https://user-images.githubusercontent.com/96857599/216756365-bd280ec5-5d61-43df-80e4-6da5b5aa7ded.png">

### 그런데
<img width="600" alt="스크린샷 2023-02-04 오후 5 07 51" src="https://user-images.githubusercontent.com/96857599/216756473-fa5b3f74-625e-49a0-9bea-b024c6f5d762.png">

#### RFC723x 변화
- 엔티티(Entity) -> 표현(Representation)
- Representation = representation Metadata + Representation Data
- 표현 = 표현 메타데이터 + 표현 데이터
<img width="683" alt="스크린샷 2023-02-04 오후 5 08 25" src="https://user-images.githubusercontent.com/96857599/216756490-98a0a244-4d36-4726-82cd-899aae3af729.png">

### 표현

<img width="669" alt="스크린샷 2023-02-04 오후 5 09 22" src="https://user-images.githubusercontent.com/96857599/216756534-dd0bba2c-8bc4-4f5b-87a7-acb8ad9e0225.png">
- Content-Type
	- application/json은 기본이 UTF-8임
<img width="669" alt="스크린샷 2023-02-04 오후 5 09 22" src="https://user-images.githubusercontent.com/96857599/216756534-dd0bba2c-8bc4-4f5b-87a7-acb8ad9e0225.png">
- Content-Encoding (압축할 때)
<img width="669" alt="스크린샷 2023-02-04 오후 5 14 23" src="https://user-images.githubusercontent.com/96857599/216756744-5d1092e8-7494-4d0c-be26-a4c9586f6ed0.png">
-> identity는 압축 안 하는 것임.

- Content-Language (표현 데이터의 자연어 표시)
<img width="671" alt="스크린샷 2023-02-04 오후 5 15 02" src="https://user-images.githubusercontent.com/96857599/216756769-61f8648c-a05b-4d59-b9f2-bbd9abf72dd9.png">
- Content-Length
<img width="673" alt="스크린샷 2023-02-04 오후 5 15 41" src="https://user-images.githubusercontent.com/96857599/216756786-80e6b274-5839-4bea-afbc-d3e8dc06e804.png">




### 콘텐츠 협상
-> 클라이언트가 (우선순위에 맞게) 선호하는 표현을 서버에게 요청

- Accept: 클라이언트가 선호하는 미디어 타입 전달 
- Accept-Charset: 클라이언트가 선호하는 문자 인코딩 
- Accept-Encoding: 클라이언트가 선호하는 압축 인코딩 
- Accept-Language: 클라이언트가 선호하는 자연 언어

- 협상 헤더는 요청시에만 사용

#### Accept-Language

- 클라이언트가 한국인지 아닌지 정보가 존재하지 않음

<img width="673" alt="스크린샷 2023-02-05 오후 3 23 30" src="https://user-images.githubusercontent.com/96857599/216804989-c548031f-82b2-42d3-8e50-1b1260803429.png">

- Accept-Language가 있으면 선호하는 언어가 한국어인 것을 HTTP Header로 처리할 수 있음.

<img width="662" alt="스크린샷 2023-02-05 오후 3 24 55" src="https://user-images.githubusercontent.com/96857599/216805042-28743a7c-d6f1-4f15-83c7-f44bc023794c.png">

- 복잡한 예시 (한국어를 희망하는 클라이언트가 독일어와 영어를 지원하는 서버에서 기본 설정인 독일어보단 영어르 희망함.)

<img width="669" alt="스크린샷 2023-02-05 오후 3 26 25" src="https://user-images.githubusercontent.com/96857599/216805081-40ba3b41-151e-4488-b4f0-dc1af8ddf2d9.png">

- 협상과 우선순위 1
<img width="670" alt="스크린샷 2023-02-05 오후 3 28 25" src="https://user-images.githubusercontent.com/96857599/216805127-68a72832-7a57-40c6-b742-5af0e4308aba.png">
- 영어로 보내게 됨
<img width="667" alt="스크린샷 2023-02-05 오후 3 29 42" src="https://user-images.githubusercontent.com/96857599/216805164-f7de4577-1352-4c1c-abae-163b5b596cf4.png">

- 크롬에서 확인
<img width="1215" alt="스크린샷 2023-02-05 오후 3 31 46" src="https://user-images.githubusercontent.com/96857599/216805218-fa47f56e-7629-435b-b6c1-a04126ed20fe.png">


- 협상과 우선순위 2
<img width="636" alt="스크린샷 2023-02-05 오후 3 32 28" src="https://user-images.githubusercontent.com/96857599/216805229-4dcf1bfb-cec7-488c-9ace-7713e778d96b.png">

- 협상과 우선순위 3
<img width="645" alt="스크린샷 2023-02-05 오후 3 33 08" src="https://user-images.githubusercontent.com/96857599/216805252-fe88b010-7c13-4d2a-9af0-7c623d935368.png">


### 전송 방식

#### 단순 전송
- 컨텐츠에 대한 길이를 알 때 사용
<img width="658" alt="스크린샷 2023-02-05 오후 3 35 40" src="https://user-images.githubusercontent.com/96857599/216805324-c1e30596-2a68-4eff-8697-375e6406bb0d.png">

#### 압축 전송
- Content-Encoding을 꼭 입력해야함
<img width="660" alt="스크린샷 2023-02-05 오후 3 36 33" src="https://user-images.githubusercontent.com/96857599/216805341-01cff00f-192d-4fa5-b925-274fd74dbdfa.png">

#### 분할 전송
- Content-Length를 보내면 안 됨. (예상이 되지 않음, 청크들마다 길이가 나옴.)
<img width="665" alt="스크린샷 2023-02-05 오후 3 37 12" src="https://user-images.githubusercontent.com/96857599/216805362-03992e25-0c7e-4515-bae4-59454b818550.png">

<img width="653" alt="스크린샷 2023-02-05 오후 3 37 35" src="https://user-images.githubusercontent.com/96857599/216805370-ebcaef31-db7a-45d7-8a26-1c79e97f3242.png">

#### 범위 전송
- 중간에 끊기면 처음부터 다시 받지 않도록 범위를 설정할 수 있음.
<img width="653" alt="스크린샷 2023-02-05 오후 3 40 51" src="https://user-images.githubusercontent.com/96857599/216805474-859554b5-e68d-4381-8bdc-619377c4aecd.png">


### 일반 전송
- From: 유저 에이전트의 이메일 정보
- Referer: 이전 웹 페이지 주소
- User-Agent: 유저 에이전트 애플리케이션 정보
- Server: 요청을 처리하는 오리진 서버의 소프트웨어 정보 
- Date: 메시지가 생성된 날짜

#### From
-> 유저 에이전트의 이메일 정보

- 일반적으로 잘 사용되지 않음 
- 검색 엔진 같은 곳에서, 주로 사용 
- 요청에서 사용

#### Referer
-> 이전 웹 페이지 주소
- 현재 요청된 페이지의 이전 웹 페이지 주소
- A -> B로 이동하는 경우 B를 요청할 때 Referer: A 를 포함해서 요청 
- Referer를 사용해서 유입 경로 분석 가능
- 요청에서 사용
- 참고: referer는 단어 referrer의 오타


- 이전의 웹 페이지를 알려줌.
<img width="923" alt="스크린샷 2023-02-05 오후 3 42 57" src="https://user-images.githubusercontent.com/96857599/216805528-093d0a49-856a-4895-bc33-e5a86b9ef681.png">
<img width="923" alt="스크린샷 2023-02-05 오후 3 43 39" src="https://user-images.githubusercontent.com/96857599/216805554-05e54af8-451d-4c83-bcd0-a0fee6e0f9df.png">


#### User-Agent
-> 유저 에이전트 애플리케이션 정보

- user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/ 537.36 (KHTML, like Gecko) Chrome/86.0.4240.183 Safari/537.36
- 클리이언트의 애플리케이션 정보(웹 브라우저 정보, 등등) 
- 통계 정보
- 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능 
- 요청에서 사용

 
<img width="1304" alt="스크린샷 2023-02-05 오후 3 45 15" src="https://user-images.githubusercontent.com/96857599/216805603-2ee9c5fa-4964-475c-ba13-4eb505e757c8.png">


#### Server
-> 요청을 처리하는 ORIGIN 서버(프록시 서버가 아닌 클라이언트의 응답을 해주는 서버)의 소프트웨어 정보


- Server: Apache/2.2.22 (Debian) 
- server: nginx
- 응답에서 사용

#### Date
-> 메시지가 발생한 날짜와 시간

- Date: Tue, 15 Nov 1994 08:12:31 GMT
- 응답에서 사용


### 특별한 정보

- Host: 요청한 호스트 정보(도메인)
- Location: 페이지 리다이렉션
- Allow: 허용 가능한 HTTP 메서드
- Retry-After: 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간


#### ⭐️Host (필수 헤더)
-> 요청한 호스트 정보(도메인)

<img width="672" alt="스크린샷 2023-02-05 오후 3 50 17" src="https://user-images.githubusercontent.com/96857599/216805750-8ff15981-a0c4-477c-a643-5f59bdaf93d3.png">

- 같은 IP를 공유하는 여러 도메인이 있다.
<img width="664" alt="스크린샷 2023-02-05 오후 3 51 07" src="https://user-images.githubusercontent.com/96857599/216805783-e99d765a-cd25-4d5d-97e2-de43c628543e.png">

- Host가 없으면, 어느 도메인으로 가야할지 알 수 없다.
<img width="657" alt="스크린샷 2023-02-05 오후 3 51 22" src="https://user-images.githubusercontent.com/96857599/216805793-224029ad-f8cd-43a5-bc73-a25193057293.png">

- Host 정보 필수
<img width="641" alt="스크린샷 2023-02-05 오후 3 52 19" src="https://user-images.githubusercontent.com/96857599/216805829-a96fadc8-27f5-4aa1-9f12-f994b733bdbc.png">


#### Location
-> 페이지 리다이렉션
- 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동 (리다이렉트)
- 응답코드 3xx에서 설명
- 201 (Created): Location 값은 요청에 의해 생성된 리소스 URI
- 3xx (Redirection): Location 값은 요청을 자동으로 리디렉션하기 위한 대상 리소스를 가리킴


#### Allow
-> 허용 가능한 HTTP 메서드

- 405 (Method Not Allowed) 에서 응답에 포함해야함 
- Allow: GET, HEAD, PUT


#### Retry-After
-> 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간

- 503 (Service Unavailable): 서비스가 언제까지 불능인지 알려줄 수 있음 
- Retry-After: Fri, 31 Dec 1999 23:59:59 GMT (날짜 표기) 
- Retry-After: 120 (초단위 표기)


### 인증
- Authorization: 클라이언트 인증 정보를 서버에 전달 
- WWW-Authenticate: 리소스 접근시 필요한 인증 방법 정의

#### Authorization
-> 클라이언트 인증 정보를 서버에 전달

- Authorization: Basic xxxxxxxxxxxxxxxx

> 인증 방식이 여러가지 있기 때문에 value에는 각 인증에 맞는 값을 넣으면 됨

#### WWW-Authenticate
-> 리소스 접근시 필요한 인증 방법 정의

- 리소스 접근시 필요한 인증 방법 정의
- 401 Unauthorized 응답과 함께 사용 
- 401 오류가 나면, 아래와 같은 내용을 같이 클라이언트에게 제공하게 된다.
- WWW-Authenticate: Newauth realm="apps", type=1,
		    title="Login to \"apps\"", Basic realm="simple"
		    
		    
		    
		    
		    
### 쿠키
- Set-Cookie: 서버에서 클라이언트로 쿠키 전달(응답)
- Cookie: 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP 요청시 서버로 전달
		    title="Login to \"apps\"", Basic realm="simple"
		    
#### 쿠키 미사용

- 처음 welcome 페이지 접근
<img width="674" alt="스크린샷 2023-02-05 오후 4 00 41" src="https://user-images.githubusercontent.com/96857599/216806096-39745e98-c4a6-4d44-afbf-6b98b0958d9a.png">

- 로그인
<img width="663" alt="스크린샷 2023-02-05 오후 4 01 35" src="https://user-images.githubusercontent.com/96857599/216806124-be93a6b9-3f29-4ec7-961a-f951fdb432df.png">

- 로그인 이후 welcome 페이지 접근 (안녕하세요. 홍길동님을 기대했으나, 안녕하세요 손님이 다시 나옴)
<img width="664" alt="스크린샷 2023-02-05 오후 4 01 51" src="https://user-images.githubusercontent.com/96857599/216806135-65b6a3ad-693d-4a64-b7e2-4100b365d0af.png">


#### Stateless

- HTTP는 기본적으로 무상태(Stateless) 프로토콜이다.
- 클라이언트와 서버가 요청과 응답을 주고 받으면 연결이 끊어진다. 
- 클라이언트가 다시 요청하면 서버는 이전 요청을 기억하지 못한다. 
- 클라이언트와 서버는 서로 상태를 유지하지 않는다.

- 대안- 모든 요청에 사용자 정보 포함
<img width="653" alt="스크린샷 2023-02-05 오후 4 03 24" src="https://user-images.githubusercontent.com/96857599/216806208-0774fa3a-77f8-43a3-ab00-875117a2f783.png">

- 모든 링크에 사용자 정보를 포함하면, 보안상의 문제부터 여러 문제점이 발생함.
<img width="659" alt="스크린샷 2023-02-05 오후 4 05 35" src="https://user-images.githubusercontent.com/96857599/216806292-602de8e1-4ce8-45c3-86c0-b9916538c29c.png">

**모든 요청에 정보를 넘기는 문제**
- 모든 요청에 사용자 정보가 포함되도록 개발 해야함 
- 브라우저를 완전히 종료하고 다시 열면?

#### 쿠키를 사용하면 해결

- 로그인
- 웹브라우저 내부에 저장있는 쿠키 저장소에에 user=홍길동을 저장
<img width="667" alt="스크린샷 2023-02-05 오후 4 07 08" src="https://user-images.githubusercontent.com/96857599/216806346-06d29124-ae75-47e0-bac6-f632d466bff3.png">

- 로그인 이후 welcome 페이지 접근
- 웹브라우저는 쿠키 저장소를 무조건 확인함.
<img width="657" alt="스크린샷 2023-02-05 오후 4 08 34" src="https://user-images.githubusercontent.com/96857599/216806393-a8ca883d-93f5-413f-a812-4625031d3fc9.png">

- 모든 요청에 쿠키 정보 자동 포함
<img width="647" alt="스크린샷 2023-02-05 오후 4 09 45" src="https://user-images.githubusercontent.com/96857599/216806446-c2100900-bc0d-4c2b-b8c9-c260fbb32b33.png">

> 모든 요청에 쿠키 정보를 넣으면 보안상의 문제부터 여러 문제 초래

#### 쿠키

- 홍길동이라는 이름을 그대로 노출하면 보안에 문제가 생기므로, sessionId를 만들어서 해결한다.
- 예) set-cookie: **sessionId=abcde1234**; **expires**=Sat, 26-Dec-2020 00:00:00 GMT; **path**=/; **domain**=.google.com; **Secure**

- 사용처
	- 사용자 로그인 세션 관리
	- 광고 정보 트래킹
- 쿠키 정보는 항상 서버에 전송됨
	- 네트워크 트래픽 추가 유발 (문제점)
	-> 최소한의 정보만 사용(세션 id, 인증 토큰)
	- 서버에 전송하지 않고, 웹 브라우저 내부에 데이터를 저장하고 싶으면 웹 스토리지 (localStorage, sessionStorage) 참고
- 주의!
	- 보안에 민감한 데이터는 저장하면 안됨(주민번호, 신용카드 번호 등등)


#### 쿠키 - 생명주기
-> Expires, max-age

- Set-Cookie: expires=Sat, 26-Dec-2020 04:39:21 GMT
	- 만료일이 되면 쿠키 삭제
- Set-Cookie: max-age=3600 (3600초)
	- 0이나 음수를 지정하면 쿠키 삭제
- 세션 쿠키: 만료 날짜를 생략하면 브라우저 종료시 까지만 유지 
- 영속 쿠키: 만료 날짜를 입력하면 해당 날짜까지 유지

#### 쿠키 - 도메인
-> Domain


- 예) domain=example.org
- 명시: 명시한 문서 기준 도메인 + 서브 도메인 포함
	- domain=example.org를 지정해서 쿠키 생성
		- example.org는 물론이고
		- dev.example.org도 쿠키 접근 
- 생략: 현재 문서 기준 도메인만 적용
	- example.org 에서만 쿠키 접근
		- example.org 에서 쿠키를 생성하고 domain 지정을 생략
		- dev.example.org는 쿠키 미접근


#### 쿠키 - 경로
-> Path

- 예) path=/home
- 이 경로를 포함한 하위 경로 페이지만 쿠키 접근
- 일반적으로 path=/ 루트로 지정 
- 예)
	- path=/home 지정
	- /home -> 가능 
	- /home/level1 -> 가능 
	- /home/level1/level2 -> 가능 
	- /hello -> 불가능


#### 쿠키 - 보안
-> Secure, HttpOnly, SameSite


- Secure
	- 쿠키는 http, https를 구분하지 않고 전송
	- Secure를 적용하면 https인 경우에만 전송
- HttpOnly
	- XSS 공격 방지
	- 자바스크립트에서 접근 불가(document.cookie)
	- HTTP 전송에만 사용
- SameSite
	- XSRF 공격 방지
	- 요청 도메인과 쿠키에 설정된 도메인이 같은 경우만 쿠키 전송

[캐시와 쿠키의 차이](https://zorba91.tistory.com/163)
## HTTP 헤더2 - 캐시와 조건부 요청

### 캐시 기본 동작

#### 캐시가 없을 때
- 첫 번째 요청
<img width="654" alt="스크린샷 2023-02-05 오후 4 36 07" src="https://user-images.githubusercontent.com/96857599/216807278-6a835160-77c0-4cd3-94a4-f833eff30dfc.png">

<img width="662" alt="스크린샷 2023-02-05 오후 4 36 56" src="https://user-images.githubusercontent.com/96857599/216807302-e58ce802-140b-41a6-877b-4ac376ed30ef.png">

- 두 번째 요청
<img width="649" alt="스크린샷 2023-02-05 오후 4 37 03" src="https://user-images.githubusercontent.com/96857599/216807307-ad489795-7190-4991-8508-ca8824fece69.png">

<img width="650" alt="스크린샷 2023-02-05 오후 4 37 11" src="https://user-images.githubusercontent.com/96857599/216807313-c88e2967-d531-45b4-942a-e8bf01cc2239.png">


- 데이터가 변경되지 않아도 계속 네트워크를 통해서 데이터를 다운로드 받아야 한다. 
- 인터넷 네트워크는 매우 느리고 비싸다.
- 브라우저 로딩 속도가 느리다.
- 느린 사용자 경험

#### 캐시 적용
- 첫 번째 요청에서 캐시의 생명 주기를 설정하고 데이터를 저장해둠
<img width="673" alt="스크린샷 2023-02-05 오후 4 38 23" src="https://user-images.githubusercontent.com/96857599/216807348-b496c05f-b622-4de8-82ee-daa8a60eb693.png">

<img width="658" alt="스크린샷 2023-02-05 오후 4 39 35" src="https://user-images.githubusercontent.com/96857599/216807399-ae80c5e7-efa2-40ad-8b50-a9e4fe144016.png">

- 두 번째 요청에서 브라우저 캐시에 저장되어있는 데이터는 바로 응답함.
<img width="662" alt="스크린샷 2023-02-05 오후 4 40 07" src="https://user-images.githubusercontent.com/96857599/216807418-c52cae51-5590-4eaf-826f-282ca875c9a4.png">

<img width="645" alt="스크린샷 2023-02-05 오후 4 41 10" src="https://user-images.githubusercontent.com/96857599/216807451-fb25465f-a396-4e74-9239-f016c0dd6800.png">

- 캐시 덕분에 캐시 가능 시간동안 네트워크를 사용하지 않아도 된다. 
- 비싼 네트워크 사용량을 줄일 수 있다.
- 브라우저 로딩 속도가 매우 빠르다.
- 빠른 사용자 경험
 
- 세 번째 요청 -> 캐시 시간 초과
<img width="678" alt="스크린샷 2023-02-05 오후 4 41 46" src="https://user-images.githubusercontent.com/96857599/216807479-0ed2ed65-9ce0-403e-861e-ccba9fd74dbd.png">


<img width="643" alt="스크린샷 2023-02-05 오후 4 42 11" src="https://user-images.githubusercontent.com/96857599/216807494-726a8979-97e5-4a18-aa6d-c3795d4f6d1a.png">

- 캐시 유효 시간이 초과하면, 서버를 통해 데이터를 다시 조회하고, 캐시를 갱신한다. 
- 이때 다시 네트워크 다운로드가 발생한다.


> 캐시 유효 시간이 만료된 데이터가 다시 들어올 때, 같은 데이터더라도 다시 다운받게 된다. 시간, 용량이 아까운 상황..
> 이걸 해결하기 위한 매커니즘-> 검증 헤더와 조건부 요청


### 검증 헤더와 조건부 요청1

<img width="665" alt="스크린샷 2023-02-05 오후 4 44 58" src="https://user-images.githubusercontent.com/96857599/216807604-52ad5a5b-45aa-46d7-ad4f-c7035ad8e1ff.png">

-> 만약 데이터가 바뀌지 않았다면??
<img width="662" alt="스크린샷 2023-02-05 오후 4 45 35" src="https://user-images.githubusercontent.com/96857599/216807629-f6ede818-64ce-4573-b562-e823be812e35.png">



#### 검증 헤더 추가(최종 수정일 확인/UTC로 적어야함.)
<img width="665" alt="스크린샷 2023-02-05 오후 4 46 29" src="https://user-images.githubusercontent.com/96857599/216807652-daa1dabf-54c2-4f93-a7fb-316c8e3439d5.png">

- 캐시 유효시간 안에는 그대로 캐시 데이터 사용
<img width="657" alt="스크린샷 2023-02-05 오후 4 47 28" src="https://user-images.githubusercontent.com/96857599/216807698-2952bb74-3761-41a4-a583-18d89c566ae7.png">

- 두번째 요청-> 캐시 시간 초과

<img width="660" alt="스크린샷 2023-02-05 오후 4 48 30" src="https://user-images.githubusercontent.com/96857599/216807728-4c779cfa-f284-43f2-a14a-be835ccbce76.png">

<img width="659" alt="스크린샷 2023-02-05 오후 4 48 39" src="https://user-images.githubusercontent.com/96857599/216807734-e604370d-c5b4-4f6f-87f3-ba26ad6aaaec.png">

- 데이터의 최종 수정일을 확인함.
<img width="651" alt="스크린샷 2023-02-05 오후 4 49 44" src="https://user-images.githubusercontent.com/96857599/216807761-67b6d033-caa7-435b-a4c3-925a5125b255.png">
<img width="651" alt="스크린샷 2023-02-05 오후 4 50 09" src="https://user-images.githubusercontent.com/96857599/216807770-74b90722-886e-46f1-826c-77777d586a9e.png">

- 304 Not Modified를 내보낸다. 
- 단, HTTP Body가 없이 내보낸다.
<img width="674" alt="스크린샷 2023-02-05 오후 4 50 53" src="https://user-images.githubusercontent.com/96857599/216807793-a76a6fc3-5c0d-4d2b-a874-c6d3f933e141.png">

- 응답 결과를 재사용하고, 헤더 데이터를 갱신한다.
<img width="668" alt="스크린샷 2023-02-05 오후 4 52 55" src="https://user-images.githubusercontent.com/96857599/216807851-18ab963d-5dc4-4693-ad23-a8967f49cbb6.png">

#### 정리

- 캐시 유효 시간이 초과해도, 서버의 데이터가 갱신되지 않으면
- 304 Not Modified + 헤더 메타 정보만 응답(바디X)
- 클라이언트는 서버가 보낸 응답 헤더 정보로 캐시의 메타 정보를 갱신 
- 클라이언트는 캐시에 저장되어 있는 데이터 재활용
- 결과적으로 네트워크 다운로드가 발생하지만 용량이 적은 헤더 정보만 다운로드 
-  매우 실용적인 해결책

- 캐시에서 불러온 데이터인지 확인
<img width="1304" alt="스크린샷 2023-02-05 오후 4 57 44" src="https://user-images.githubusercontent.com/96857599/216808018-e2b7b56e-95c4-452b-acd1-784cfc525e7d.png">
<img width="1304" alt="스크린샷 2023-02-05 오후 4 57 51" src="https://user-images.githubusercontent.com/96857599/216808025-ae49b5b9-8e07-49b6-86c3-047a7d72d88f.png">

- 이미지를 더블클릭하고, 새로 고침해보면 304 Not Modified가 뜨게 되고, if-modified-since: Tue, 03 Mar 2020 20:15:00 GMT라는 조건부를 확인할 수 있다.
<img width="1104" alt="스크린샷 2023-02-05 오후 4 59 33" src="https://user-images.githubusercontent.com/96857599/216808075-819acda2-623c-4607-9828-13f4fe1e2811.png">

<img width="1104" alt="스크린샷 2023-02-05 오후 4 59 42" src="https://user-images.githubusercontent.com/96857599/216808080-7b6b1a7c-2cae-4e76-b887-53c7d1ff207e.png">



### 검증 헤더와 조건부 요청2

- 검증 헤더
	- 캐시 데이터와 서버 데이터가 같은지 검증하는 데이터
	- Last-Modified , ETag
- 조건부 요청 헤더
	- 검증 헤더로 조건에 따른 분기 
	- If-Modified-Since: Last-Modified 사용 
	- If-None-Match: ETag 사용
	- 조건이 만족하면 200 OK
	- 조건이 만족하지 않으면 304 Not Modified


#### 예시
- If-Modified-Since: 이후에 데이터가 수정되었으면?
	- 데이터 미변경 예시
		- 캐시: 2020년 11월 10일 10:00:00 vs 서버: 2020년 11월 10일 10:00:00 
		- 304 Not Modified, 헤더 데이터만 전송(BODY 미포함)
		- 전송 용량 0.1M (헤더 0.1M, 바디 1.0M)
	- 데이터 변경 예시
		- 캐시: 2020년 11월 10일 10:00:00 vs 서버: 2020년 11월 10일 11:00:00 
		- 200 OK, 모든 데이터 전송(BODY 포함)
		- 전송 용량 1.1M (헤더 0.1M, 바디 1.0M)

#### Last-Modified, If-Modified-Since 단점

- 1초 미만(0.x초) 단위로 캐시 조정이 불가능
- 날짜 기반의 로직 사용
- 데이터를 수정해서 날짜가 다르지만, 같은 데이터를 수정해서 데이터 결과가 똑같은 경우
- 서버에서 별도의 캐시 로직을 관리하고 싶은 경우
	- 예) 스페이스나 주석처럼 크게 영향이 없는 변경에서 캐시를 유지하고 싶은 경우
	-> ETag 사용

#### ETag, If-None-Match

- ETag(Entity Tag)
- 캐시용 데이터에 임의의 고유한 버전 이름을 달아둠
	- 예) ETag: "v1.0", ETag: "a2jiodwjekjl3"
- 데이터가 변경되면 이 이름을 바꾸어서 변경함(Hash를 다시 생성)
	- 예) ETag: "aaaaa" -> ETag: "bbbbb"
- 진짜 단순하게 ETag만 보내서 같으면 유지, 다르면 다시 받기!


#### 검증 헤더 추가
- 첫 번째 요청-> ETag 저장
<img width="677" alt="스크린샷 2023-02-05 오후 5 10 09" src="https://user-images.githubusercontent.com/96857599/216808454-55575757-5a13-4637-8bf3-9b81b5452e66.png">
<img width="662" alt="스크린샷 2023-02-05 오후 5 10 16" src="https://user-images.githubusercontent.com/96857599/216808461-dbf4d2ed-a40d-429a-a39d-b68500f137ca.png">


- 두 번째 요청 - 캐시 시간 초과
<img width="656" alt="스크린샷 2023-02-05 오후 5 10 25" src="https://user-images.githubusercontent.com/96857599/216808470-cc1038d2-b06f-4c3b-8eb7-d2fd230e262c.png">
- 요청한 이미지가 가진 ETag와 캐시가 가진 ETag와 동일함
<img width="663" alt="스크린샷 2023-02-05 오후 5 10 32" src="https://user-images.githubusercontent.com/96857599/216808476-b3ff3f59-0df1-498d-96a3-ae22c5918372.png">
<img width="655" alt="스크린샷 2023-02-05 오후 5 10 39" src="https://user-images.githubusercontent.com/96857599/216808481-48674c14-bb29-47b8-92f4-83340e6c8a26.png">
- 데이터가 수정되지 않음
<img width="653" alt="스크린샷 2023-02-05 오후 5 14 58" src="https://user-images.githubusercontent.com/96857599/216808633-bcc102a7-7aef-4bd6-985a-135cc94b866b.png">
- 실패(때문에 304 Not Modified가 뜸)
<img width="657" alt="스크린샷 2023-02-05 오후 5 10 55" src="https://user-images.githubusercontent.com/96857599/216808493-2e94b63b-7620-4382-a588-2e6b46335236.png">
- HTTP Body를 제외하고 전송
<img width="666" alt="스크린샷 2023-02-05 오후 5 11 27" src="https://user-images.githubusercontent.com/96857599/216808509-960c0f95-a6ba-4a33-83fb-e1a3515de6e3.png">
<img width="659" alt="스크린샷 2023-02-05 오후 5 11 34" src="https://user-images.githubusercontent.com/96857599/216808512-d663f38f-7aa2-4bc9-aca0-63bc0f41a66f.png">



#### 정리
- 진짜 단순하게 ETag만 서버에 보내서 같으면 유지, 다르면 다시 받기!
- 캐시 제어 로직을 서버에서 완전히 관리
- 클라이언트는 단순히 이 값을 서버에 제공(클라이언트는 캐시 메커니즘을 모름) 
- 예)
	- 서버는 배타 오픈 기간인 3일 동안 파일이 변경되어도 ETag를 동일하게 유지 
	- 애플리케이션 배포 주기에 맞추어 ETag 모두 갱신

### 캐시 제어 헤더
- Cache-Control: 캐시 제어 
- Pragma: 캐시 제어(하위 호환) 
- Expires: 캐시 유효 기간(하위 호환)

#### Cache-Control (가장 중요⭐️)
-> 캐시 지시어(directives)


- Cache-Control: max-age
	- 캐시 유효 시간, 초 단위
- Cache-Control: no-cache
	- 데이터는 캐시해도 되지만, 항상 원(origin) 서버에 검증하고 사용
- Cache-Control: no-store
	- 데이터에 민감한 정보가 있으므로 저장하면 안됨 (메모리에서 사용하고 최대한 빨리 삭제)

#### Pragma
-> 캐시 제어(하위 호환)

- Pragma: no-cache 
- HTTP 1.0 하위 호환


#### Expires
-> 캐시 만료일 지정(하위 호환)

- expires: Mon, 01 Jan 1990 00:00:00 GMT

- 캐시 만료일을 정확한 날짜로 지정
- HTTP 1.0 부터 사용
- 지금은 더 유연한 Cache-Control: max-age 권장 
- Cache-Control: max-age와 함께 사용하면 Expires는 무시

### 검증 헤더와 조건부 요청 헤더

- 검증 헤더 (Validator)
	- ETag: "v1.0", ETag: "asid93jkrh2l"
	- Last-Modified: Thu, 04 Jun 2020 07:19:24 GMT 
- 조건부 요청 헤더
	- If-Match, If-None-Match: ETag 값 사용
	- If-Modified-Since, If-Unmodified-Since: Last-Modified 값 사용


### 프록시 캐시

- 원 서버(origin) 직접 접근
-> 오래 걸림
<img width="670" alt="스크린샷 2023-02-05 오후 5 26 40" src="https://user-images.githubusercontent.com/96857599/216808994-25ed6d5b-78f3-48fe-951e-b563a4941c83.png">

#### 프록시 캐시 도입
- 첫 번째 요청
<img width="644" alt="스크린샷 2023-02-05 오후 5 27 09" src="https://user-images.githubusercontent.com/96857599/216809019-800ac708-a7d2-4d4d-a493-2e9090ef3fe8.png">

> 외국의 인기 없는 유튜브 영상을 보면 다운받는 로딩 속도가 느리지만, 한국의 인기 있는 영상을 보면 로딩 속도가 빠른 것이 프록시 캐시 서버 덕분이다.
<img width="661" alt="스크린샷 2023-02-05 오후 5 27 34" src="https://user-images.githubusercontent.com/96857599/216809043-f1ce65f1-21dc-47c1-88cc-f2610d8637d8.png">
<img width="665" alt="스크린샷 2023-02-05 오후 5 28 18" src="https://user-images.githubusercontent.com/96857599/216809067-c1e302c0-399b-47f7-8791-cd7aa8a0b537.png">

#### 캐시 지시어(directives) - 기타
- Cache-Control: public
	- 응답이 public 캐시에 저장되어도 됨 
- Cache-Control: private
	- 응답이 해당 사용자만을 위한 것임, private 캐시에 저장해야 함(기본값) 
- Cache-Control: s-maxage
	- 프록시 캐시에만 적용되는 max-age 
- Age: 60 (HTTP 헤더)
	- 오리진 서버에서 응답 후 프록시 캐시 내에 머문 시간(초)


### 캐시 무효화

#### Cache-Control
-> 확실한 캐시 무효화 응답(확실하게 캐시하지 않도록 만들어주는 것)

- Cache-Control: no-cache, no-store, must-revalidate 
- Pragma: no-cache
	- HTTP 1.0 하위 호환
> Pragma는 과거의 HTTP까지 호환하기 위해 사용한 것.


#### Cache-Control
-> 캐시 지시어(directives) - 확실한 캐시 무효화

- Cache-Control: no-cache
	- 데이터는 캐시해도 되지만, 항상 원 서버에 검증하고 사용(이름에 주의!) 
- Cache-Control: no-store
	- 데이터에 민감한 정보가 있으므로 저장하면 안됨(메모리에서 사용하고 최대한 빨리 삭제)
- Cache-Control: must-revalidate
	- 캐시 만료후 최초 조회시 원 서버에 검증해야함
	- 원 서버 접근 실패시 반드시 오류가 발생해야함 - 504(Gateway Timeout)
	- must-revalidate는 캐시 유효 시간이라면 캐시를 사용함
- Pragma: no-cache
	- HTTP 1.0 하위 호환


#### no-cache vs must-revalidate 
-> no-cache 기본 동작
<img width="661" alt="스크린샷 2023-02-05 오후 5 35 42" src="https://user-images.githubusercontent.com/96857599/216809423-8b457577-ab18-4b38-827d-58dfb6fd6ee6.png">
<img width="658" alt="스크린샷 2023-02-05 오후 5 36 28" src="https://user-images.githubusercontent.com/96857599/216809456-c826687d-bcce-4a96-9403-ebc65d3bce04.png">

- 만약, 순간적으로 네트워크가 단절되어 원 서버에 접근이 불가능하다면?
- Error or 200 OK (오류 보다는 오래된 데이타라도 보여주자)
<img width="657" alt="스크린샷 2023-02-05 오후 5 37 36" src="https://user-images.githubusercontent.com/96857599/216809498-a2ef795d-f7b6-4038-aeda-80da1ea7b223.png">

- must-revalidate는 문제가 생기면 오류가 발생하도록 함.
<img width="657" alt="스크린샷 2023-02-05 오후 5 38 35" src="https://user-images.githubusercontent.com/96857599/216809535-0d7f9ac6-ddb6-4246-9a4d-ec80509e30fe.png">



> RFC 7230 검색하면 더 자세한 HTTP에 대해 알 수 있다.




