---
title: "[컴퓨터네트워크] 1장. Introduction"
date: 2020-08-15T15:34:30-04:00
classes: wide
categories:
  - Computer Network
tags:
  - Computer Network
  - CS
---

**Warning Notice:** 이 글은 **COMPUTER NETWORKING A TOP DOWN APPROACH - James F. Kurose, Keith W. Ross(Pearson)** 도서를 읽고 개인적인 학습을 위해서 정리한 내용입니다. 틀린 내용이 있을 수 있습니다. All material copyright 1996-2012  J.F Kurose and K.W. Ross, All Rights Reserved
{: .notice--warning}

컴퓨터 네트워크 과목에서는 한 컴퓨터에서 다른 컴퓨터로 데이터를 전송하고 수신하기 위한 방법과 컴퓨터와 네트워킹 장비들에서 일어나는 일들을 배운다. 1장에서는 컴퓨터 네트워크 과목을 학습하기에 앞서 이 과목에서 주로 공부하는 인터넷에 대한 개괄적인 내용을 살펴보고, 주요 용어들을 정리한다.

## 1.1 인터넷(Internet) 이란?

우리가 네이버나 구글과 같은 웹사이트를 이용하기 위해서는 먼저 인터넷 업체를 통해서 **모뎀과 공유기** 등을 설치하고, 해당 장치에 연결된 **랜선**을 본인의 **데스크탑**에 연결해야 함을 알고있다. 우리는 상식적으로 다른 컴퓨터와 통신하기 위해서 인터넷이 필요하다는 것과, 이러한 인터넷을 사용하기 위해서는 인터넷 케이블이나 모뎀과 같은 자원이 필요하다는 것을 안다. 또한 우리에게 보여지지 않은 이면에서 **다른 컴퓨터와 통신하기 위한 여러 구성요소**들이 필요함을 짐작할 수 있다.

### 1.1.1 Nuts and Bolts View

앞선 짐작을 토대로 인터넷을 정의하는 것을 `Nut and Bolt View` 라고 한다. 이 관점에서 인터넷은 **인터넷을 구성하는 하드웨어, 소프트웨어, 데이터 구성요소로 바라보는 관점**이다. 이러한 관점에서 인터넷은 전 세계에 존재하는 수십억 개의 컴퓨팅 장치를 연결하는 네트워크이다.

![1](https://user-images.githubusercontent.com/31771548/90309031-98472100-df1f-11ea-80a4-ea440789cf15.png)

**Nuts and Bolts View** 에서 사용하는 주요 용어를 정리하면 다음과 같다.

- **호스트(Host), End System** : 인터넷과 연결된 PC, Server Computer, laptop, smartphone과 같은 기기들.
- **(데이터) 패킷** : 호스트 시스템에서 주고 받는 데이터들의 묶음
- **통신 링크(Communication link)** : 호스트나 네트워킹 장비가 데이터를 송수신할 때 사용하는 매개체. 케이블, 라디오 신호, 인공위성 같은 장비들이 있다.
- **라우터(Router), 패킷 스위치(Packet Switch)** : 통신 링크상에서 이동하는 데이터 패킷이 목적지 호스트 시스템까지 전달될 수 있도록 데이터 패킷의 전달 경로를 설정해주는 장비
- **대역폭(bandwidth)** : 호스트나 라우팅 장비 등에서 통신링크를 통해 단위 시간당 얼마만큼의 데이터를 전송할수 있는지를 나타내는 지표다. **초당 비트수(bps)** 로 표현한다.
- **ISP(Internet Service Provider)** : 통신링크와 패킷 스위치등을 설치하여 지역 또는 국가간 네트워크 연결을 제공하는 서비스 업체를 말한다.(SK Broadband, AT&T 등등)
- **Protocol** : 인터넷에서 호스트 시스템간 또는 네트워킹 장비간에 데이터를 교환하는 규칙을 말한다. 이 규칙에는 데이터를 송수신 하는 순서, 데이터를 표현하는 방법, 데이터 손실시 수행하는 작업등을 포함할 수 있다. 대표적으로 TCP/IP가 존재한다.
- **Network Edge** : 호스트와 같이 인터넷 네트워크 상에서 데이터 송수신의 최종 목적지가 되는 지점을 말한다.
- **Access Network** : end system을 다른 end system과 연결하는 경로상에서, 가장 첫번째로 만나게 되는 라우터(가장자리 라우터)까지의 네트워크를 의미한다.
- **Network core(back bone)** : access network를 연결하는 network 이다. 여러 라우팅 장비, 패킷 스위치, 통신 링크 등 ISP 업체들이 설치해놓은 장비들이 있는 영역이라고 할 수 있다.

### 1.1.2 Service view

인터넷을 정의하는 또다른 관점은 **Service view** 이다. 이 관점에서 인터넷은 네트워킹 프로그램이 다른 컴퓨터와 통신하기 위해서 사용하는 **infrastructure**를 의미한다. 이 인프라에는 한 어플리케이션이 다른 어플리케이션과 데이터를 주고받을 수 있도록 도와주는 **Programming interface(API)** 를 포함한다.

## 1.2 네트워크 코어 (Network Core)

![8](https://user-images.githubusercontent.com/31771548/90313292-64cbbd00-df46-11ea-9896-2b70330aba6e.png)

네트워크 코어와 관련된 개념들에 대해서 간략히 알아보자. 먼저 네트워크 코어에서 데이터를 송수신하는 2가지 방법에 대해서 알아본다.

### 1.2.1 패킷 교환 방식

![9](https://user-images.githubusercontent.com/31771548/90313306-96dd1f00-df46-11ea-9df2-d58e57cde6f1.png)

하나의 end system에서 다른 end system으로 데이터를 전송할 때 어플리케이션 레벨에서 메시지를 주고 받는다. 이 메시지는 서로간의 동작을 제어하는 컨트롤일 수도 있고, jpeg, mp3와 같은 파일을 포함할 수 있다. 송신 end system에서 메시지를 수신 end system으로 보내기 위해, 송신 시스템은 긴 애플리케이션 layer 메시지를 패킷(packet)이라고 하는 작은 단위로 나누다. 각 패킷은 통신링크와 패킷 스위치를 거치게 된다. 패킷은 링크의 최대 전송속도로 통신 링크상에서 전송된다. 따라서 R bit/sec를 갖는 통신링크 상에서 L bits의 패킷을 전송할때 총 L/R sec 의 시간이 소요된다.

#### 저장 후 전달

![10](https://user-images.githubusercontent.com/31771548/90313316-a5c3d180-df46-11ea-9dc9-aeedf2df203b.png)

대부분의 패킷 스위치는 패킷을 전달할 때 `저장-후-전달` 방식을 사용한다. 즉, 하나의 패킷에 있는 비트를 전송받으면 곧바로 다른 링크로 해당 비트를 전송할 수 있는 것이 아니라, 완전한 패킷이 스위치에 전송될때까지 기다린 다음 비트를 전송할 수 있음을 의미한다.  

패킷을 저장한 뒤 전송하는 과정에서 딜레이가 발생한다. R bit/sec의 bandwidth를 갖는 N개의 링크로 구성된 네트워크에서 길이 L bits의 패킷을 전송하는데 걸리는 지연시간은 다음과 같다.

$$
delay = N{L \over R}
$$

#### 큐잉 지연과 패킷 손실

패킷 스위치에는 여러 링크가 연결되어 있다. 패킷 스위치는 각 링크에 대해서 출력 버퍼(출력 큐)를 가지고 있다. 도착하는 패킷이 링크를 통해서 전송되려고 할때 해당 링크가 이미 다른 패킷을 전송하고 있다면 패킷은 출력 버퍼에 저장될 필요가 있다. 이 과정에서 `저장-후-전달`에 더하여 `큐잉 지연`이 발생한다.

![11](https://user-images.githubusercontent.com/31771548/90313318-a6f4fe80-df46-11ea-803c-6bd1ee6a3a05.png)

위 그림에서 짧은 기간동안 라우터에 도착하는 패킷의 전송 속도가 1.5Mbps를 초과하게 되면 패킷은 출력 버퍼에 큐잉된다.  
버퍼의 크기는 유한하기 때문에 만약 출력 버퍼가 가득찬 상황에서 해당 링크로 패킷이 도착하게 되면 해당 패킷 또는 버퍼에 있던 패킷이 손실될 수 있다(`패킷 손실`)

#### 전달 테이블과 라우팅 프로토콜

라우터에 접속된 여러 통신링크 중 하나에서 오는 패킷을 어떻게 목적지로 향하는 다른 통신링크로 전달하는 가에 대해서 알아보자.  
인터넷에 연결된 모든 end system은 IP 주소를 가지고 있다. 송신 end system에서 수신 end system으로 패킷을 전송할 때 수신 시스템에 대한 IP 주소를 패킷의 헤더에 포함시킨다. 패킷을 수신한 라우터는 헤더에 존재하는 IP 주소를 활용한다. IP 주소는 우편 주소처럼 계층이 존재(예를 들어 인천광역시 / 남구 / 인주대로)하는데, 라우터는 내부의 전달 테이블(forwarding table)을 가지고 있어서 특정 IP의 특정 계층에 대한 전달 링크를 맵핑하여 관리한다. 이를 통해 패킷을 적절한 링크로 다시 전송할 수 있다.  

![12](https://user-images.githubusercontent.com/31771548/90313319-a6f4fe80-df46-11ea-96ed-5b4bbc01d952.png)

여기서 다시 어떻게 라우터에 전달 테이블을 설정할 것인가에 대한 의문이 남는다. 인터넷은 자동으로 라우터에 전달 테이블을 설정하는 `라우팅 프로토콜`을 갖는다. 이는 나중에 알아본다.

### 1.2.2 회선 교환(Circuit Switch) 방식

#### 회선 교환(Circuit Switch)

![13](https://user-images.githubusercontent.com/31771548/90313320-a78d9500-df46-11ea-9a46-9cb539ca3cdc.png)

회선 교환 방식에서 두 개의 end system이 통신하기 위해서는 링크자원(버퍼, 링크 전송률)이 통신세션(session)간에 예약된다. 패킷 교환 방식은 링크 자원을 예약하지 않는다. 이러한 방식을 사용하는 대표적인 예가 `전화망`이다. 전화망을 통해 송신자와 수신자가 통화를 하려고 할때, 네트워크 스위치들은 해당 연결 상태를 유지해야 한다. 이러한 연결을 정보통신 용어로 `회선(Circuit)`이라고 한다. 네트워크가 회선을 설정할 때, 그 연결이 이루어지는 동안 네트워크 링크에 일정한 전송률을 예약한다. 주어진 전송속도가 송신자-수신자 연결을 위해 예약되므로, 송신자는 보장된 일정 전송률로 데이터를 보낼 수 있다.  
이와 달리 패킷 교환 방식에서는 송신자가 보낸 패킷이 전송될 때 링크의 자원(회선)을 예약하지 않는다. 패킷이 전송될 링크가 혼잡하다면 출력 버퍼에 패킷이 저장 될 수 있으며, 이 과정에서 지연이 발생한다. 따라서 보장된 속도로 패킷이 전송되지 않을 수 있다.

#### 패킷 교환 VS 회선 교환

![15](https://user-images.githubusercontent.com/31771548/90313322-a8262b80-df46-11ea-9086-0d7757c97793.png)

다음과 같은 예를 보자. 각 인터넷 사용자가 1 Mbps의 링크를 공유한다고 하자. 각 사용자는 활동시간과 비활동시간을 번갈아가며 나타내며 활동시간은 전체 시간의 10%이다. 활동시간에는 100kbps의 속도로 데이터를 생산해낸다고 하자.  
회선교환 방식은 링크의 자원을 예약해야하기 때문에 동시에 최대 10명의 사용자만이 인터넷을 사용할 수 있다. 회선이 연결되어 있는 동안 사용자가 사용을 하든 안하든 간에 해당 회선은 연결이 끝날때까지 유지되어야 하며 이는 자원낭비이다.  
패킷 교환 방식의 경우 만약 전체 사용자가 35명일 때 11명 이상의 사용자가 동시에 인터넷을 사용할 확률은 0.0004이다. 때문에 패킷 교환 방식은 회선 교환 방식에 비교해서 거의 동일한 수준의 딜레이를 발생시키면서 더 적은 비용으로 네트워크를 구성할 수 있으며 동시에 더 많은 사람들이 사용할 수 있게 된다.(패킷 교환 방식의 구축 비용이 더 적기 때문에)

### 1.3.3 네트워크의 네트워크

End system이 인터넷에 연결되기 위해서는 지역의 ISP와 연결되어있어야 한다(access ISP). 또한 이러한 access ISP끼리도 연결이 되어있어야 두 개의 end system이 패킷을 주고받을 수 있게 된다. 어떻게 access ISP과 연결되어질 것인가는 돈과 국제 관계가 고려되야함

- 실현 불가능한 구조 : 모든 access ISP가 서로 연결된 형태  
![16](https://user-images.githubusercontent.com/31771548/90313323-a8bec200-df46-11ea-923d-cccf8816aad3.png)
- 네트워크 구조 1 : 전세계의 access ISP에 대해 연결 서비스를 제공하는 글로벌 transit ISP  
![17](https://user-images.githubusercontent.com/31771548/90313324-a8bec200-df46-11ea-8f5f-953b35663eda.png)
access ISP가 고객, 글로벌 transit ISP가 서비스 제공자가 된다.
- 네트워크 구조 2 : 글로벌 transit ISP가 여러 곳 생겨서 경쟁이 일어난 형태  
![18](https://user-images.githubusercontent.com/31771548/90313325-a9575880-df46-11ea-9bcf-9774fb0d0aa3.png)
  - 시장 경쟁에 의한 서비스 요금 하락 덕분에, access ISP는 구조1보다 구조2를 더 선호하게 된다.
  - 이들 글로벌 ISP끼리도 연결이 되어 있어야 국제적으로 통신이 가능할 수 있다.
- 네트워크 구조 3 : 한 지역에 대한 서비스를 제공하는 지역 ISP가 추가된 형태  
![19](https://user-images.githubusercontent.com/31771548/90313326-a9575880-df46-11ea-9d30-6c00cd07310f.png)
- 네트워크 구조 4 : 멀티홈, PoP, IXP, 피어링와 같은 구조가 추가된 형태
- 네트워크 구조 5 : 구글과 같은 컨텐츠 제공자가 자신들만의 전세계적 네트워크를 구성하고, 이 네트워크가 자신들의 서비스만을 목적으로 사용되는 형태  
![20](https://user-images.githubusercontent.com/31771548/90313328-a9efef00-df46-11ea-9d75-0d001a7caa58.png)

종합해서 네트워크는 다음과 같은 계층구조를 가지게 되었다.  
![21](https://user-images.githubusercontent.com/31771548/90313329-aa888580-df46-11ea-9d73-b42980c01fe6.png)

> Content Provider Network : 구글과 같은 컨텐츠회사가 네트워크를 제공할 정도로 커져버린 형태


## 1.4 프로토콜 계층과 서비스 구조

인터넷과 같은 거대한 시스템은 그 구조가 계층적으로 이루어져 있는 것이 많다. 인터넷 시스템의 계층 구조를 살펴보기에 앞서, 항공 시스템의 계층구조를 살펴보면서 계층구조의 장점에 대해서 알아보자.

![26](https://user-images.githubusercontent.com/31771548/90312314-6d1ffa00-df3e-11ea-83f0-a4654f8a4a0f.png)

항공 시스템은 위와 같은 계층구조를 가진다.

1. 공항 항공사 카운터에서 티켓을 구매
2. 수하물 맡기기
3. 게이트를 통해서 비행기에 탑승
4. 활주로에서 이륙
5. 관제 센터의 안내에 따라서 목적지로 이동
6. ...

거대한 항공 시스템은 하나의 기업이나 부서가 구성하는 것이 아니라 각 계층별로 특화된 서비스를 제공하는 여러 기업이나 부서로 구성된다. 이러한 계층별 구분은 **한 서비스의 전문가들이 한 계층만을 전담하여 신경쓸 수 있기 때문에 각 계층의 서비스 수준을 높일 수 있으며 이는 전체적인 시스템의 성능 향상**으로 이어진다. 그리고 **전체 시스템의 구성요소를 훨씬 더 쉽게 파악**할 수 있게 해준다. 또한 **한 계층에서의 변화가 다른 계층에 영향을 주지 않도록 분리했기 때문에 시스템의 유지보수**가 훨씬 쉽다. 예를 들어 수하물을 싣는 장소가 변경되었다고 해서 비행기 이륙과정이 달라질 필요가 없는 것이다.

계층적으로 시스템을 구성하기 위해선 필수적으로 이루어져야 하는 것이 있다. 그것은 바로 **인접한 계층간에 서비스를 주고받는 규칙 또는 동일 계층이지만 다른 공간에 존재하는 이들간의 서비스를 주고 받는 규칙을 정하는 것**이다. 항공 시스템을 예를 들어보면, 비행기의 게이트를 담당하는 부서와 비행기 안에서 일하는 크루 간에는 비행기에 승객이 다 탔는지에 대한 정보를 주고 받는 방법이 있을 것이다. 이는 항공 시스템의 계층적 구조에서 인접한 계층간의 정보를 주고 받는 규칙이다. 또다른 예로는 비행기가 출발하는 공항에서 수하물을 싣는 부서는 도착하는 공항의 수하물 관련 부서 직원이 알아볼 수 있도록 수하물에 어떤 사람의 짐인지를 알려주는 정보를 부착할 것이고, 도착 공항 수하물 부서 직원은 이를 확인하는 작업을 할 것이다. 이는 항공 시스템의 계층적 구조에서 동일 계층이지만 서로 다른 공간에 존재하는 구성요소끼리의 규칙이다.

### 1.4.1 인터넷 네트워크 상 프로토콜 계층 구조

앞서 언급한 항공 시스템의 게층 구조가 인터넷 시스템의 계층 구조에도 적용된다.

![28](https://user-images.githubusercontent.com/31771548/90312713-a9a12500-df41-11ea-97a3-3c3bd91ab891.png)

인터넷 시스템은 5개의 계층 구조로 이루어져 있으며 이를 **인터넷 프로토콜 5계층** 이라고 한다. 이러한 인터넷의 계층 구조의 특징은 앞서 언급한대로, 

- 각 계층별로 구분하여 개발하여 계층별 전문화가 가능하고, 전체 시스템의 성능이 향상된다.
- 전체 시스템의 구성요소를 훨씬 쉽게 파악할 수 있게 해준다.
- 한 계층에서의 변화가 다른 계층에 영향을 주지 않기 때문에 유지보수가 쉬워진다.

**인터넷 프로토콜 5계층** 의 각각의 구성 요소는 다음과 같다.

#### 어플리케이션 계층

호스트 시스템에서 네트워킹을 하는 사용자의 프로그램들간의 규칙을 정하는 계층이다. 이 계층에서 네트워킹 프로그램들 간에 주고 받는 데이터를 **메시지** 라고 한다. 이 메시지는 서로의 동작을 제어하는 명령이 될 수도 있고, 이메일이나 sms와 같은 사용자 데이터일 수도 있다.  `HTTP`, `FTP` 와 같은 프로토콜이 여기에 해당된다.

#### 트랜스포트 계층

어플리케이션 계층으로부터 **메시지** 를 받아서 목적지에 존재하는 어플리케이션 계층으로 **메시지**를 전달하는 역할을 한다. 이 계층에서는 **메시지** 를 더 작은 조각으로 쪼개서 전달할 수 있다. 트랜스포트 계층간에 주고 받은 데이터의 단위는 **세그먼트** 라고 한다.

이 계층의 프로토콜에는 **TCP**, **UDP**가 있다. **TCP** 은 **연결 지향형 프로토콜**로 트랜스포트 계층간 데이터를 주고 받기 전 무조건 연결을 진행해야한다. 또한 데이터 전송의 **신뢰성을 보장하는 프로토콜**이다. 즉, TCP 를 이용해서 전송한 데이터는 무조건 목적지까지 도달하며, 어떠한 이유로 중간에 데이터가 손실되었다면 이를 파악하여 재전송을 할 수 있다.

그에 반해서 **UDP** 프로토콜은 **비연결 지향형 프로토콜**이다. 즉 데이터 송수신에 앞서 연결과정이 없으며, 데이터 전송의 신뢰성을 보장받지 못한다. 그러나 불필요한 연결과정과 신뢰성 보장 작업을 하지 않기 때문에 실시간 라이브 방송처럼 전송의 **정확성보다 빠르게 데이터를 전송하는 것이 목적인 용도**에서는 적절히 사용될 수 있다.

#### 네트워크 계층

트랜스포트 계층으로부터 **세그먼트** 를 받아서 이 세그먼트가 목적지 호스트의 트랜스포트까지 이동할 수 있도록 하는 역할을 한다. 더 정확히는 목적지 호스트까지 이동할 수 있는 **라우터**로 세그먼트를 전달한다. 이를 위해서 목적지 호스트로 이어질 수 있는 다음 라우터의 IP 주소를 세그먼트에 추가한다. 이렇게 이전 계층에서 전달받은 데이터에 새로운 정보를 추가한 것을 **헤더정보**라고 한다.(헤더 정보를 제외한 부분은 **데이터그램** 이라고 한다.) 네트워크 계층은 어플리케이션이 존재하는 호스트 시스템 뿐만 아니라, 네트워크 코어를 구성하는 **라우터** 라는 장비에도 존재한다. 네트워트 계층끼리 주고 받은 데이터의 단위는 **패킷** 이라고 한다. 이 계층에서의 대표적인 프로토콜에는 **IP 프로토콜**이 있다.

#### 링크 계층

통신 링크(Communication Link)로 연결된 호스트와 라우터 또는 라우터와 라우터간에 데이터를 전달해주는 역할을 한다. 이 계층에서의 프로토콜은 **이더넷** 등이 있다. 이 계층에서 주고 받는 데이터의 단위는 **프레임** 이라고 한다.

#### 물리 계층

통신 링크 상에서 실제적으로 프레임을 전달하는 물리적인 매개체에서 일어나는 일들을 처리한다. 이 계층에서는 비트단위로 데이터를 주고받는다. 데이터를 전달하는 물리적인 매체에 따라서 프로토콜이 달라진다.

**인터넷 프로토콜 5계층** 에 추가적으로 2개의 계층을 추가해서 인터넷 계층을 표현한 것이 **OSI 7계층** 이다. **프레젠테이션 계층**과 **세션 계층** 이 추가되었으며, 데이터의 보안과 표현 등을 처리하는 계층이다. 이들 계층은 어플리케이션 계층에서 추가적으로 구현될 수 있으며 이 계층을 구현할지 말지는 프로그래머의 선택에 달려있다.

### 캡슐화

앞서 각 계층을 소개할 때 각 계층에서는 상위 계층으로부터 전달받은 데이터에 각 계층에서 사용할 추가적인 정보를 붙일 수 있으며 이를 헤더정보라고 언급한바 있다. 이렇게 각 계층에서 사용할 추가적인 정보를 붙이는 것을 **캡슐화**라고 한다. 이 같은 캡슐화를 통해서 **각 계층에서는 해당 계층에서 추가한 정보만 사용하게 할 수 있고, 다른 계층에서 사용하는 정보에 접근하는 것을 방지**할 수 있다.
