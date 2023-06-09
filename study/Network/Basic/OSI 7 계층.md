# OSI 7 계층
OSI(Open Systems Interconnection) 7계층은 네트워크에서 데이터가 전송되는 과정을 7개의 계층으로 나눈 모델입니다.
이 모델은 데이터 통신에 필요한 기술과 프로토콜을 표준화하여 서로 다른 시스템 간의 통신을 가능하게 합니다.

## 계층

### 1. 물리 계층 (Physical Layer)
- 주된 역할: 물리적인 매체를 통해 비트(bit)를 전송하는 역할
- 사용되는 프로토콜: IEEE 802.3 (이더넷)
- 예시: 케이블, 허브(Hub), 리피터(Repeater)

### 2. 데이터 링크 계층 (Data Link Layer)
- 주된 역할: 물리 계층에서 전송된 비트를 관리하고 논리적인 형태인 프레임(Frame)으로 분리 및 조립하며, 오류 검출과 수정을 담당
- 사용되는 프로토콜: 이더넷 (Ethernet), 토큰 링(Token Ring)
- 예시: 스위치(Switch), 브릿지(Bridge), 네트워크 인터페이스 카드(NIC)

### 3. 네트워크 계층 (Network Layer)
- 주된 역할: 라우팅(Routing)과 경로 설정 등의 기능을 수행하며, IP 주소 할당 및 전송 제어 등의 역할을 수행
- 사용되는 프로토콜: 인터넷 프로토콜(IP), 인터넷 제어 메시지 프로토콜(ICMP), 인터넷 그룹 관리 프로토콜(IGMP)
- 예시: 라우터(Router)

### 4. 전송 계층 (Transport Layer)
- 주된 역할: 포트(Port)를 이용하여 양 끝단의 응용 프로그램 간에 신뢰성 있는 데이터 전송을 위해 연결 설정, 해제, 오류 검사 및 복구 기능을 제공(TCP 또는 UDP 어느것으로 할지 결정한다. TCP는 신뢰성 있는 통신, UDP는 신뢰성은 없지만 빠른 통신)
- 사용되는 프로토콜: 전송 제어 프로토콜(TCP), 사용자 데이터그램 프로토콜(UDP)
- 예시: TCP, UDP

### 5. 세션 계층 (Session Layer)
- 주된 역할: 양 끝단 간의 세션(Session) 설정, 유지 및 종료를 관리하며, 데이터 교환에 대한 동기화를 담당(상대방에게 보낼 수 있는지 인증을 체크한다.)
- 사용되는 프로토콜: 세션 계층 프로토콜
- 예시: SSH, TLS/SSL

### 6. 표현 계층 (Presentation Layer)
- 주된 역할: 데이터의 형식 변환, 암호화, 복호화 등을 수행하여 응용 계층이 사용하기 적절한 형태로 데이터를 제공
- 사용되는 프로토콜: 암호화, 데이터 인코딩

### 7. 응용 계층 (Application layer)
- 주된 역할: 응용 계층은 사용자나 응용 프로그램이 네트워크에 접속하기 위해 사용
- 사용되는 프로토콜: HTTP, FTP, DNS, Telnet 등 다양한 프로토콜

## 💁‍♂️ 프로토콜이란?
```
프로토콜은 컴퓨터 네트워크에서 통신을 하기 위해 사전에 정해진 규칙의 모음입니다. 프로토콜은 네트워크상의 데이터 전송, 메시지 전달, 오류 검출 및 수정, 인증 등의 작업에 대한 규칙을 제공합니다.

프로토콜은 서로 다른 장치들이 통신할 수 있도록 하며, 이는 전 세계의 컴퓨터들이 서로 통신할 수 있도록 해주는 인터넷에서 특히 중요합니다.
예를 들어, HTTP 프로토콜은 웹 브라우저와 웹 서버 간의 통신에 사용되며, TCP/IP 프로토콜은 인터넷 전체에서 데이터 전송을 관리합니다.
```

## QnA
- OSI 7 계층을 알아야되는 이유
  - 네트워크의 동작 원리와 프로토콜의 역할을 이해하는 데 도움이 됩니다. 각 계층은 다른 계층과 어떻게 상호 작용하며, 데이터가 어떻게 처리되고 전송되는지 이해할 수 있습니다.
  - 각 계층은 독립적으로 동작하기 때문에, 문제가 발생하면 해당 계층에서 발생한 문제임을 빠르게 파악하고, 문제를 해결할 수 있습니다.
- OSI 7계층 예시
  - 빨간색 화살표대로 길찾기를 검색하면 아래로 내려가서 물리까지 온 후 다른 컴퓨터로 전송이 되서 역순으로 가게 됩니다.
  - 1~4계층은 데이터를 전달하는 것이 주 기능이고,
  - 5계층부터는 데이터를 송수신하는 양쪽 컴퓨터 내의 프로세스들 간의 통신 프로토콜이 주 기능이라고 보면 되겠다.
- ![](/study/assets/content_network_osi7.png)

## 참고
- [https://ssdragon.tistory.com/86](https://ssdragon.tistory.com/86)