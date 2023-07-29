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
