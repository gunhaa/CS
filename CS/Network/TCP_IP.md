



# TCP/IP 모델
> TCP/IP 모델은 인터넷과 네트워크 통신을 위한 4계층 아키텍처로, 각각의 계층이 특정한 네트워크 기능을 담당한다.

![OSI7](images/OSI7_2.jfif)

## 계층별 역할
### 응용 계층 (Application Layer)

주요 프로토콜: HTTP, FTP, SMTP, DNS 등
사용자가 접근하는 응용 서비스가 위치한 계층으로, 데이터를 특정 응용 프로그램에서 사용할 수 있는 형태로 변환한다. OSI 모델의 응용 계층, 표현 계층, 세션 계층에 해당하는 역할을 통합하여 수행한다.

### 전송 계층 (Transport Layer)

주요 프로토콜: TCP, UDP
데이터의 신뢰성과 연결 설정을 관리하며, 상위 계층의 데이터를 하위 계층에 전달할 때 오류를 제어하고, 패킷의 순서를 보장한다. 전송을 위한 프로토콜로 TCP와 UDP를 제공한다.
OSI 모델의 전송 계층과 대응된다.

### 인터넷 계층 (Internet Layer)

주요 프로토콜: IP, ICMP, ARP
데이터가 목적지까지 전달될 경로를 결정하는 라우팅 역할을 수행하며, 네트워크 간 데이터 패킷 전송을 관리한다. 특히, IP는 데이터 전송을 위한 주소 지정과 경로 설정을 제공하며, ICMP는 네트워크 오류 메시지를 관리하고, ARP는 IP 주소를 MAC 주소로 변환한다.
OSI 모델의 네트워크 계층과 유사하다.

### 네트워크 인터페이스 계층 (Network Interface Layer)

주요 프로토콜: Ethernet, Wi-Fi
물리적 데이터 전송을 수행하는 계층으로, 데이터 링크 계층과 물리 계층의 역할을 통합하여 수행한다. 데이터가 실제 네트워크 매체(케이블, 무선)에서 전송될 수 있도록 변환하고, 네트워크 카드나 드라이버와 통신한다.
OSI 모델의 데이터 링크 계층과 물리 계층을 합친 역할을 한다.


## Recap 
> tcp는 보낼 준비를 하는 것이고, ip는 인캡슐레이션(캡슐화)해서 어디로 보낼지를 정하는 것을 추상화 한 것이다.