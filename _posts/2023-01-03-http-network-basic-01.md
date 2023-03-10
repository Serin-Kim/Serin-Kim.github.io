---
layout: post
title: "그림으로 배우는 Http & Network Basic 제1장"
date: 2023-01-03 10:03:36 +0530
categories: Book Network
---

책을 읽고 정리합니다.

## 제1장 웹과 네트워크의 기본에 대해 알아보자

### 웹 페이지가 보여지는 법?

웹 브라우저는 주소 입력란에 지정된 URL에 의지해 웹 서버로부터 리소스라고 불리는 파일 등의 정보를 얻고 있다.

이때, 서버에 의뢰하는 웹 브라우저를 클라이언트라고 부른다.

클라이언트에서 서버까지 일련의 흐름을 결정하는 것은 웹에서 `HTTP(HyperText Transfer Protocol)`이라 불리는 프로토콜이다.

프로토콜은 '약속'을 의미한다. 즉, 웹은 HTTP라는 약속을 사용한 통신으로 이루어져 있다.

### 네트워크의 기본은 TCP/IP

인터넷을 포함하여 일반적으로 사용하고 있는 네트워크는 `TCP/IP`라는 프로토콜에서 움직인다. HTTP는 그 중 하나이다.

인터넷과 관련된 프로토콜들을 모은 것을 TCP/IP라고 한다.

### 계층으로 관리하는 TCP/IP

#### TCP/IP가 계층화된 이유?

계층화되어 있으면 사양이 바뀌었을 때 해당 계층만 변경하면 된다.

| 계층         | 설명                                                           | 예시                           |
| ------------ | -------------------------------------------------------------- | ------------------------------ |
| 애플리케이션 | 유저에게 제공되는 애플리케이션에서 사용하는 통신의 움직임 결정 | FTP, DNS, HTTP                 |
| 트랜스포트   | 네트워크로 접속되어 있는 2대의 컴퓨터 사이의 데이터 흐름 제공  | TCP, UDP                       |
| 네트워크     | 네트워크 상에서 패킷의 이동 경로 설정                          | -                              |
| 링크         | 하드웨어적인 면                                                | 디바이스 드라이버, NIC, 케이블 |

### TCP/IP 통신의 흐름

계층 순서대로 통신한다. 송신하는 측은 애플리케이션에서부터 내려가고, 수신하는 측은 애플리케이션 계층으로 올라간다.

- 송신측: 계층을 통과할 때마다 헤더를 추가
- 수신측: 계층을 통과할 때마다 헤더를 삭제

이렇게 정보를 감싸는 것을 `캡슐화`라고 한다.

![IMG_0343](https://user-images.githubusercontent.com/68533016/210309737-5e3ac668-f8e8-4dfc-8b84-1e0125c1b35b.jpg){: width="700" }

### HTTP와 관계가 깊은 프로토콜은 IP/TCP/DNS

#### 배송을 담당하는 IP

네트워크 층, IP != IP 주소

IP의 역할은 `개개의 패킷을 상대방에게 전달`하는 것이다. IP주소와 MAC 주소가 중요하다.

#### 통신은 ARP를 이용하여 MAC 주소에서 한다

IP 통신은 MAC 주소에 의존해서 한다. 여러 대의 컴퓨터와 네트워크 기기를 중계해 상대방에게 도착한다. 그렇게 다음으로 중계할 곳의 MAC 주소를 사용하여 목적지를 찾아가는 것이다. 이때, `ARP(Address Resolution Protocol)`이라는 프로토콜을 사용한다.

즉, ARP는 `주소를 해결하기 위한 프로토콜` 중 하나인데, 수신지의 IP 주소를 바탕으로 MAC주소를 조사할 수 있다.

#### 그 누구도 인터넷 전체를 파악할 수 없다; 라우팅

목적지까지 중계를 하는 도중에 컴퓨터와 라우터 등의 네트워크 기기는 목적지에 도착하기까지 대략적인 목적지만 알고 있다. 이 시스템을 `라우팅`이라고 부른다.

### 신뢰성을 담당하는 TCP

`TCP(Transfer Control Protocol)`는 트랜스포트 층에 해당하는데, `신뢰성 있는 바이트 스트림 서비스를 제공`한다. 바이트 스트림 서비스란 용량이 큰 데이터를 보내기 쉽게 TCP 세그먼트라고 불리는 단위 패킷으로 작게 분해하여 관리하는 것을 의미하고, 신뢰성 있는 서비스는 상대방에게 보내는 서비스를 의미한다.

결국 TCP는 `대용량의 데이터를 보내기 쉽게 작게 분해하여 상대에게 보내고, 정확하게 도착했는지 확인`하는 역할을 담당한다.

#### 상대에게 데이터를 확실하게 보내는 것이 일이다

상대에게 확실하게 데이터를 보내기 위해서 TCP는 `쓰리웨이 핸드셰이킹(three way handshaking)`이라는 방법을 사용한다. 이 방법은 패킷이 보내졌는지 여부를 상대에게서 확인한다.

1. 송신측에서 최초로 `SYN` 플래그로 상대에게 접속함과 동시에 패킷을 보냄
2. 수신측에서 `SYN/ACK` 플래그로 송신측에 접속함과 동시에 패킷을 수신한 사실을 전함
3. 송신측이 `ACK` 플래그를 보내 패킷 교환이 완료되었음을 전함

- SYN(synchronize)
- ACK(acknowledgment)

### 이름 해결을 위한 DNS

`DNS(Domain Name System)`은 HTTP와 같이 응용 계층 시스템에서 `도메인의 이름과 IP주소의 이름 확인`을 제공한다.

- 사람: "www.hackr.jp"과 같이 영어와 숫자로 컴퓨터의 이름을 지정
- 컴퓨터: 숫자를 나열

DNS는 도메인명에서 IP주소를 조사하거나 반대로 IP주소로부터 도메인명을 조사하는 서비스를 제공한다.

## Reference

- [그림으로 배우는 Http & Network Basic](http://www.yes24.com/Product/Goods/15894097)
- [TCP flags](https://www.howtouselinux.com/post/tcp-flags)
