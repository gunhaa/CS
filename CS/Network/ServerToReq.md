# 서버에서 요청이 보내지기까지

> 서버에 요청을 보낸 후 5000byte의 get 요청의 application 계층 -> TCP -> ip 계층에서 일어나는 흐름

## 어플리케이션 계층

- 애플리케이션 계층에서 HTTP GET 요청이 만들어진다
- 5000바이트 크기의 데이터가 하나의 HTTP 요청 본문에 있다

```plaintext
GET /some/resource HTTP/1.1
Host: example.com
<기타 HTTP 헤더 및 요청 본문..(5000bytes)>
```

## 전송 계층(TCP)

- TCP 세그먼트의 최대 크기는 MSS(최대 세그먼트 크기)에 따라 달라지며, 일반적으로 한 세그먼트의 크기는 1460바이트 이다. 이는 Ethernet 프레임 크기 1500바이트에서 IP 헤더(20바이트)와 TCP 헤더(20바이트)를 제외한 값이다.

## 네트워크 계층(IP)

- TCP 세그먼트는 IP 계층으로 전달되며, IPv4 패킷으로 캡슐화 된다.
- IP 패킷은 IP 헤더와 데이터로 구성된다.
- 헤더: IP 헤더에는 출발지 및 목적지 IP 주소, TTL(Time-to-Live), 프로토콜(이 경우 TCP) 등의 정보가 포함된다.
- 데이터: 이 부분은 TCP 세그먼트입니다. 즉, TCP 세그먼트가 IP 패킷의 데이터 부분에 들어간다.
- IP 패킷은 일반적으로 MTU(Maximum Transmission Unit) 제약으로 인해 한 번에 보내는 데이터 크기가 제한된다. Ethernet의 경우, 보통 1500바이트가 MTU 제한이다. 즉, 5000바이트의 데이터는 여러 개의 패킷으로 나뉘어 전송된다.

## 예시 전송

- 5000바이트의 GET 요청은 4개의 TCP 세그먼트로 나뉘어 전송된다. 각 세그먼트의 크기는 1460바이트 정도로 나누고, 나머지 데이터는 마지막 세그먼트로 보내진다.

### 첫 번째 TCP 세그먼트

- TCP 헤더(20바이트) + 데이터(1460바이트) = 1480바이트
- IP 헤더(20바이트) + TCP 세그먼트 = 1500바이트 (하나의 IPv4 패킷 크기)
### 두 번째 TCP 세그먼트

- TCP 헤더(20바이트) + 데이터(1460바이트) = 1480바이트
- IP 헤더(20바이트) + TCP 세그먼트 = 1500바이트 (하나의 IPv4 패킷 크기)

### 세 번째 TCP 세그먼트

- TCP 헤더(20바이트) + 데이터(1460바이트) = 1480바이트
- IP 헤더(20바이트) + TCP 세그먼트 = 1500바이트 (하나의 IPv4 패킷 크기)

### 네 번째 TCP 세그먼트

- TCP 헤더(20바이트) + 데이터(620바이트) = 640바이트
- IP 헤더(20바이트) + TCP 세그먼트 = 660바이트

## 데이터 전송 순서
- 각 TCP 세그먼트는 IP 계층에서 전송될 때 IPv4 패킷으로 캡슐화된다. 이때 IP 패킷은 라우터를 통해 최종 목적지 서버로 전송된다.
- 서버에 도달한 후, IP 계층에서는 해당 IP 패킷을 추출하고, TCP 계층에서 재조합한 후, 애플리케이션 계층에 전달하여 최종적으로 HTTP 요청을 처리한다.