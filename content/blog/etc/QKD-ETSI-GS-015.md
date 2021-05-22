---
title: QKD ETSI GS 015
date: 2000-00-01 01:38:03
category: "etc"
draft: false
---

# ETSI GS QKD015

- 업무에 필요한 주요 부분 번역
- SDN 입장에서 본 QKD 중심

## 주요 용어

**entity**

- 특정 기능을 제공하는 하드웨어, 소프트웨어, 펌웨어 셋

**QKD application**

- KMS의 **QKD-derived-key**를 사용하는 entity

- external application일수도 있고 QKD 시스템에서 실행되는 internal application일 수도 있다.
- external application은 **SAE**와 유사

**QKD interface**

- 고도로 추상화된 QKD system 인터페이스
- QKD Interface는 네트워크 뷰와 관련된 특징만을 정의한다. 이 attribute는 qkd를 관리하기 위해 sdn controller에 제공된다.

**QKD link**

- 한쌍의 **QKD module**을 연결한 active / passive 컴포너트
- 키분배를 가능하게 한다

- 대칭키의 보안은 이 link 컴포넌트에 의존하지 않는다.

**QKD module**

- 암호 계층에 포함된 하드웨어, 소프트웨어, 펌웨어 컴포넌트 셋
- 한개 이상의 **QKD protocol**을 실행한다.
- **QKD protocol**은 적어도 다른 하나의 **QKD module**로하여금 대칭키를 생성하게 할 수있다.

**QKD network**

- 두개이상의 **QKD node**로 이뤄진 네트워크

**QKD node**

같은 보안경계, 장소에 있는 **QKD module**의 세트

**QKD protocol**

- 양자나 일반 신호의 운영이다
- 두 그룹이 **QKDlink**의 양끝단에서 공유된 bit string 에대해 동의할 수 있게 한다.

**QKD system**

- **QKD Link**에 의해 연결된 한쌍의 **QKD module**
- **QKD Link**는 **Quantum Key distribution** 기능을 **QKD Protocol**을 사용하여 제공한다.

**quantum channel**

- 양자 신호를 전송하기 위한 커뮤니 케이션 채널

**Quantum Key Distribution**

- 양자 상태를 전송하는 과정

- 원격 party 간에 대칭키를 생성하기 위함이다.
- 양자 얽힘이나 전송된 양자 상태를 완벽 복제가 불가능함에 기반을 둔 보안체계가 수반된 프로토콜 사용한다.

**SDN agent**

- 하나 이상의 **QKD system**을 관리하는 개체
- **QKD System**은 각각의 **QDK interface에 ** 의해 관리된다.
- 보안위치 내의 QKD 의 자원정보를 추상화한다.
- QKD 자원은 QKD network에 대한 SDN Controller에 의해 제어되고 통신된다.

**SD-QKD node**

- QKD 자원정보의 논리적, 추상적 표현
- **SDN Agent**관점에서 본 **QKD node**

**Secure Application Entity(SAE)**

- KMS(Key Management System)으로부터 하나이상의 키를 요청하는 **entity**
- 하나이상의 Secure Application enitity들과 연계되어 실행되는 하나이상의 application들 위해 키를 요청한다.

**secure location**

- 외부로부터 접근이 보호되었다고 가정된 장소

## 축약어

**ACK** Acknowledgement

**API** Application Programming Interface

**CRUD** Create, Read, Update and Delete

**DoS** Denial of Service

**HSM** Hardware Security Module

**HTTP** Hypertext Transfer Protocol

**ID** IDentifier

**IETF** International Engineering Task Force

**JSON** JavaScript Object Notation

**NBI** North Bound Interface

**NMS** Network Management System

**PHYS** Physical link

**QKD** Quantum Key Distribution

**QoS** Quality of Service

**RFC** Request For Comments

**SAE** Secure Application Entity

**SDN** Software-Defined Networking

**SD-ONC** Software-Defined Optical Network Controller

**SD-QKD** Software-Defined Quantum Key Distribution

**SD-QNC** Software-Defined Quantum Network Controller

**SKR** Secure Key generation Rate

**SSH** Secure Shell

**TLS** Transport Layer Security

**URI** Uniform Resource Identifier

**URL** Uniform Resource Locator

**UUID** Universally Unique Identifier

**XML** Extensible Markup Language

**YANG** Yet Another Next Generation

## Software-Defined Quantum Key Distribution

### intro

이 문서에서 정의된 파라미터, 모델링은 하나이상의 **QKD module을 SDN Controller로 연결하는 인터페이스 관리**와 관계되어 있다.

이 인터페이스와 더 나아간 통합을 위한 요구사항은 **YANG 모델과, 메인 기능의 유스케이스**로 기술 되어 있다.

이러한 구조적 디자인은 controller로 하여금 QKD 자원을 중심적으로 조율하게하여 link 당 키할당을 수요에 맞게 최적화하고, direct, virtual QKD link를 자동으로 생성되게 한다. (virtual QKD link에서 key는 한 hob에서 다음 hob으로 연결되어 첫 지점, 마지막 지점을 연결한다. )

Annex A 에 기술된 workflows는 다음과 같이 실행된다고 여겨진다.

- SDN 아키텍쳐에서 사용되는 모든 잘 accepted된 네트워크 관리 프로토콜을 사용 (내부구조는 YANG 정보 모델을 기반으로 함)

그러나, 다음은 현재 문서의 정의범위 밖이다.

- 어떤 특정한 프로토콜 / 자료구조 / 특정실행이, 현재 문서에 정의된 YANG 정보모델을 실행하는데 사용되었는지

이러한 명세는 시스템 디자인과 실행단계동안 유연한 상태로 남겨져있다.

추가적으로, YANG 모델은 QKD 기술의 기초 / 핵심 모델로 디자인 되었다(운영자의 관리 측면에서). 그러나 다른 실험과 확장에 대해서 닫혀있지 않다. YANG 은 새로운 가능성을 통합하기 위해 유연성을 제공한다. 현재 문서의 미래 개정은 추가적인 파라미터를 포함할 수 있다.

### SD-QKD NODE

SD-QKD node는 하나 이상의 QKD module(SDN Controller와 표준 프로토콜로 연결된)의 집합이다. node와 controller간의 연결은 정보로 하여금 QKD 도베인으로부터 제공될수 있게 하고 원격으로 QKD system의 행동이 key 집합을 생성, 삭제, 갱신할 수 있게 한다(양자 채널이나 멀티 홉을 통해).

SD-QKD Node가 준수해야하는것은 다음과 같다.

- QKD interfacerk controller에 제공된, **하나 이상의 qkd 모듈**로 구성되어야 한다.
- 여러개의 QKD module 일수도 있다. 여러개의 interface로 추상화된 하나의 single node를 생성한다.
- secure location에 위치하여야 한다.
- 하나의 secure location 은 하나이상의 SD-QKD node를 구성할 수 있다.
- SD-QKD node는 다른 키 집합으로부터의 key 를 가진 kms를 포함하여야 한다. kms 는 여러개의 logical key store을 이용하여 application 그룹을 구별한다.

- application 들을 위해 API를 통해 key store 에서 key를 가져갈때 하나의(single) 접근을 제공해야 한다.
- 적어도 하나의 SDN controller와 연결되어 있어야한다. 표준 프로토콜이나 탐색과 제어 또는 통계 조회가 가능한 메커니즘으로
- application 정보를 controller에 노출해야한다. 탐색 목적이나 더나은 QKD key 사용을 최적화하기 위함이다.
- QKD interface를 QKD system 정보와 함께 SDN controller에 노출해야하고, quantum channel을 생성하기위해 system의 몇몇 파라미터를 설정하도록 해야한다.
- key link 정보를 SD-QKD system에 노출해야한다.
- 고전적인 channel 요구사항을(node에 있는 각 시스템에 대한 ) 노출해야한다.

다음으로 정의된 모델링은 추상화된 QKD domain 뷰를 제공한다.

QKD system을 network element의 interface로 추상화할 수 있다.

이 네트워크 요소(SD-QKD node)는 이웃 노드, 중앙 컨트롤러와 end-to-end서비스나 key 연관(link) 을 생성하기 위해 통신할 수 있다.

충분한 QKD 시스템과 물리적 매체로 연결 가능할때 이러한 집합들은 direct quantum channel을 통해 생성된다.

다른 경우에, multi hob link 나 key 집합은 완전히 연결된 QKD network에 의해 생성된다.

또한, 제어 플레인에 의해 교환되는 정보는 중요하지 않다. key 정보는 드러나지 않는다.

그러므로, QKD network 의 SDN 패러다임의 도입은 어떤 추가적인 보안 위험을 함축해선 안된다.

특히 이 **모델의 목적**은 다음과 같다.

- 수요, 기능 및 네트워크의 상태에 따라 QKD 자원을 중앙집중식으로 관리 가능하게한다.
- 다른 QKD system들을 하나의 키 관리 하에 하나의 보안 경계로 묶는다. 더 나은 방식으로 수요를 탐지하고 필수적 연결이나 키 집합을 감지하기 위해서이다.
- 다음과 같은 복잡성을 감소시킨다.
  - 하나의 secure location에 있는 QKD modules들을 따로 운영하는것
  - QKD system에 대한 통계 처리
- 저수준의 파라미터와 QKD system과 기술의 행동에 관한 복잡성을 추상화한다.
- application의 Qos 정보와 각 링크의 생성률 정보에 기반한 모든 수요에 대처하는 QKD network에서, QKD link의 설정과 분배를 최적화한다.

### SD-QKD network & SD-QKD nodes

SD-QKD network는 SD-QKD 간의 연결로 묘사된다.

SD-QKD의 구성요소는 다음과 같다

- SD-QKD node capabilities

- QKD application

- QKD links(key association)

- QKD interfaces(systems)

## SD-QKD node capabilities

이 구조는 SDN controller에 기본적인 기능정보를 제공하기 위해 필수적인 parameter를 포함한다.

예시로는 다음이 있다.

- key 사용
- multihob 환경에서 node가 키를 사용가능한지

**다음 테이블이 전체적인 node의 기능만을 언급하고 있지만, 다른 서브 모듈들은 자신의 기능을 포함하여도 된다.**

### 테이블 1 : SD-QKD node capabilities

| Name                      | Type    | Details     | Description                                                                                       |
| ------------------------- | ------- | ----------- | ------------------------------------------------------------------------------------------------- |
| link_stats_support        | boolean | 기본값은 참 | 참이라면, 이 sd-qkd노드는 link와 관련된 통계 정보를 제공한다. (skr, link consumption, QBER)       |
| application_stats_support | boolean | ""          | 참이라면, 이 sd-qkd노드는 application 관련 통계정보를 제공한다. (application consumption, alerts) |
| key_relay_mode_enable     | boolean | ""          | QKD node의 key relay mode service 지원 여부                                                       |

## QKD interfaces

도입부에 기술되었듯이, QKD interface는 QKD system을 추상화한것이다. 이는 SD-QKD node의 부분으로 secure location에 포함되어 있다. 이 추상화는 SDN controller로 하여금 모든 QKD system 들을 식별하고 하나의 네트워크 요소로 집합 시키는것을 가능하게 한다.

상호 운용성(다른시스템과 제약없이 호환될 수 있는 성질) 이슈때문에 이 모델의 현재 버전은 디바이스, 벤더와 모델로서 기술된QKD technology 을 명시하고 있다. 현재 개발상태에서 다른 qkd module들과 매칭하는 것은 미작동 링크나 키생성 장애를 발생시킬 것이다.

### 테이블 2 : QKD interfaces

| Name                           | Type                                       | Details | Description                                                                                                                |
| ------------------------------ | ------------------------------------------ | ------- | -------------------------------------------------------------------------------------------------------------------------- |
| qkdi_id                        | ietf_yang_types:uuid                       | None    | interface id이다. **노드 안에서만** 고유 숫자로 기술되는데, **이 숫자는 SD-QKD node ID와 결합되면 전역적으로 고유해진다**. |
| capabilities                   | container                                  | None    | Capabilitiy of the QKD system(interface)                                                                                   |
| capabilities/ role_support     | etsi-qkdn-types: <br />QKD-ROLE-TYPES      | None    | QKD node의 key relay mode service 지원여부                                                                                 |
| capabilities/ wavelength_range | etsi-qkdn-types: <br />QKD-ROLE-TYPES      |         | 지원되는 wave length의 범위 (nm) (조정가능한 laser를 쓴다면 여러개 가능)                                                   |
| capablilities/ max_absorption  | uint32                                     |         | 지원되는 최대 흡수량(dB)                                                                                                   |
| model                          | string                                     |         | device model (vendor/ device)                                                                                              |
| type                           | etsi-qkdn-types:<br />QKD-TECHNOLOGY-TYPES |         | interface 타입 (QKD technology)                                                                                            |
| att_point                      | container                                  |         | 광 스위치와의 인터페이스 연결지점                                                                                          |
| att_point/ device              | string                                     |         | 인터페이스가 연결된 광스위치의 unique id                                                                                   |
| att_point/ port                | uint32                                     |         | 광스위치의 port id                                                                                                         |

## QKD Key Association Links

QKD key 연결 링크는 두개의 SD-QKD node 간의 논리적 키 연결이다. 이 링크는 두가지 타입이 있다.

- direct(physical)
  - 키가 생성된 직접적인 양자 채널
  - physical QKD link 는 한쌍의 QKD module에 의해 연결되어 있다.
- virtual
  - 키가 여러개의 SD-QKD node에 의해 전달된다.
  - end to end 연결
  - endpoint를 연결하는 직접적인 양자 채널이 없다.
  - end point 셋은 연결되어서 각각의 비밀 키는 생산되서 키를 재전달되어야한다.

모든 새로운 링크는 추적되고, 라벨링되고 다른 링크와 독립될 수 있어야한다.

virtual link들 또한 internal application으로 등록되어 있고, 다른 key 연결 링크의 QKD-derivedkey를 전소용도로 이용한다.

SDN Controller에 노출되는 정보는 최소한이 되어야하지만 배포된 link와 application에 대한 분석이나 최적화가 가능해야 한다. 다만 다른 중요한 정보는 SD-QKD node 보안 영역에 저장되어야한다.

### 테이블 3 : QKD key association link

| Name                                    | Type                                  | Details                                          | Description                                                                                                                                                      |
| --------------------------------------- | ------------------------------------- | ------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| link_id                                 | ietf_yang_types:uuid                  |                                                  | QKD link 의 unique id                                                                                                                                            |
| enable                                  | boolean                               | 기본값 참                                        | 해당 링크의 키생성 프로세스를 활성화 / 비활성화할지의 여부이다.                                                                                                  |
| local/qkd_node                          | ietf_yang_types:uuid                  |                                                  | local SD-QKD node의 unique id 이다                                                                                                                               |
| local/interface                         | uint32                                |                                                  | 키연결 링크를 생성할때 사용되는 interface 이다                                                                                                                   |
| remote/qkd_node                         | ietf_yang_types:uuid                  |                                                  | remote SD-QKD node의 unique id 이다.<br />**이 값은 key link가 요청이 도착하였을때 SDN controller에 의해 제공된다.**                                             |
| remote/interface                        | uint32                                |                                                  | link를 생성할때 사용되는 interface                                                                                                                               |
| type                                    | etsi-qkdn-types:<br />QKD-LINK-TYPES  |                                                  | Key Association Link type: **Virtual or Direct**                                                                                                                 |
| state                                   | etsi-qkdn-types: LINK-STATUS-TYPES    |                                                  | 링크의 상태                                                                                                                                                      |
| applications                            | List: ietf_yang_types:uuid            |                                                  | 링크로부터 key를 소비하는 application들                                                                                                                          |
| prev_hop                                | ietf_yang_types                       | (if type=VIRTUAK)                                | virtual key association link에서 이전 hop                                                                                                                        |
| next_hop                                | ietf_yang_types: uuid                 | (if type=VIRTUAK)                                | virtual key association link에서 next hop이다. 여러개의 sub paths가 있을 경우를 위해 리스트 형식으로 정의                                                        |
| bandwidth                               | uint32                                | (if type=VIRTUAK)                                | key association link를 위해서 필요한 대역폭(bps)<br />Physcal link의 대역폭을 남겨두기 위해 사용한다. internal application으로 virtual link를 지원하기 위함이다. |
| channel_att                             | uint8                                 | (if type=PHYS)                                   | 양자 채널에서 예상되는 감쇠계수(진폭에 세기가 줄어드는 정도), src node(QKD node) 와 dst node 사이에서                                                            |
| wavelength                              | etsi-qkdn-types:<br />wavelength      | (if type =PHYS)                                  | 양자 채널에서 사용될 대역폭(**설정정보**) interface가 조정 불가하다면, 이 설정은 우회가능하다.                                                                   |
| qkd_role                                | etsi-qkdn-types:<br />QKD-ROLE-TYPES  | (if type = PHYS)                                 | QKD module의 transmitter / receiver mode 이다. multi role이 지원되지 않느다면 무시된다 .                                                                         |
| Performance/ <br />expected_consumption | uint32                                | Config false                                     | 해당 링크에 연결된 모든 application의 대역폭을 합친 값이다                                                                                                       |
| Performance/<br />skr                   | uint32                                | Config false                                     | 해당 링크의 Secret key rate generation                                                                                                                           |
| Performance/<br />eskr                  | uint32                                | Config false                                     | Effective secret key rate generation of the key association link available after internal consumption                                                            |
| Performance/<br />phys_perf             | list                                  | (if type=PHYS)<br />Config false<br />Key "type" | physycal performance parameters의 리스트                                                                                                                         |
| Performance/<br />phys_perf/type        | etsi-qkdn-types:<br />PHYS-PERF-TYPES | (if type = PHYS)<br />Config false               | 컨트롤러에 노출될 physical 성능 값의 타입                                                                                                                        |
| Performance/<br />phys_perf/<br />value | uint32                                | (if type=PHYS)<br />config false                 | type으로 명시된 항목에 대응하는 숫자 값                                                                                                                          |

## QKD Applications

SD-QKD node의 관점에서 , QKD application은 해당 노드의 kms의 QKD-derived key를 요청하는 모든 개체로 정의된다. 이 application들은 external일수도 있고 internal 일수도 있다.

- external
  - end-user application, Hardware Security Module(HSM), virtual network function, an encryption card, security protocols, etc)
  - cm module / virtual network(018 service)에 사용하는 기능들
- internal
  - virtual link 생성을 위한 authentication에 사용되는 키들
  - forwarding module (virtual link를 구성하는 qkd module)

소프트웨어 관점에서, application은 특정 시간에 키를 사용하는 고정적으로 실행중인 인스턴스나 프로세스이다.

하나의 인스턴스나 프로세스는 서로다른 독립된 세션을 열어야한다.

SDN controller는 application 관리에 관하여 두가지 역할을 가진다.

- 들어오는 application을 등록하고, 구체적으로는 실제 요구에 맞게 QKD network의 사용을 최적화하기 위해 QoS 요구사항을 등록한다.
- QKD application들을 위해 대응하는 SD-QKD 원격 node를 찾는복잡성을 처리한다.

application들로 하여금 QKD network에 대해 알게하는 것(또는 그들의 local QKD node/system에 대한 정보를 교환하는 것)은 application 계층에 비바람직한 복잡성을 가져온다.

그러한 상황을 막기 위해서 SDN controller는 새로운 application이 등록되고, SD-QKD node가 주어진 application을 통해 대응하는 SD-QKD node를 찾기위해 접근할 수 있는 중앙저장소로서 동작한다.

모든 application은 그것의 key manager가 어디에 위치한지 ip/ port 정보만 알뿐이다. 반면에 컨트롤 계층은 새로운 application을 동록하고 연결하는데 신경을 쓴다.

### 테이블 4 : QKD application

| Name                                | Type                                 | Details      | Description                                                                                                                                                                                         |
| ----------------------------------- | ------------------------------------ | ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| app_id                              | ietf_yang_types:uuid                 |              | 이 값은 QKD key association link로부터 키를 추출해가는 한쌍의 application을 고유하게 식별한다.                                                                                                      |
| Qos                                 | container                            |              | 요청되는 Quality of Service                                                                                                                                                                         |
| Qos/max_bandwidth                   | uint32                               |              | 이 application에서 허가되는 최대 대역 폭이다. 이 값을 초과하는 것은 local key store 에서 application으로 에러를 일으킬수 있다. 이 값은 아마 **내부적으로, 혹은 관리자에 의해 기본값으로 설정된다**. |
| Qos/min_bandwidth                   | uint32                               |              | 이 값은 **선택적인 파라미터 값**이다. application에 대한 최소 key rate를 요구할 수 있게 한다.                                                                                                       |
| Qos/jitter                          | uint32                               |              | 이 값은 최대 jitter 값을 명시하며, 빠른 키 재생성을 요구하는 application을 위한 delivery API에 의해 제공된다(msec). 이 값은 다른 Qos와 조화되어 충분히 넓은 Qos 정의를 제공할 수 있다.              |
| Qos/ttl                             | uint32                               |              | 이 값은 키가 사용되지 않고 key store에 저장될 수 있는 최대시간(seconds)를 명시한다.                                                                                                                 |
| Qos/clients_shared_path_enable      | boolean                              |              | 참이라면, 이 application의 여러 clients는 *service impact 를 감소시키기 위해서 키를 공유할것*이다.                                                                                                  |
| Qos/clients_shared_keys_required    | boolean                              |              | 참이라면 이 application의 여러 client들은 service impact를 감소시키기위해 키를 공유할 것이다.                                                                                                       |
| type                                | etsi-qkdn-types:<br />QKD-APP-TYPES  |              | 등록된 application의 타입이다. 모듈의 타입으로 정의된 이 값은 client이거나 internal일수 있다.                                                                                                       |
| server_app_id                       | inet: URI                            |              | server application의 id                                                                                                                                                                             |
| client_app_id                       | inet: URI                            |              | 대응하는 SD-QKD 노드의 kms와 연결된 client application의 id                                                                                                                                         |
| backing_link_id                     | Leaf-list:<br />ietf_yang_types:uuid |              | QKD key를 application들에 제공하는 key association llink의 id                                                                                                                                       |
| local_qkdn_id                       | ietf_yang_types: uuid                |              | local application에 key를 제공하는 local QKD node id                                                                                                                                                |
| remote_qkdn_id                      | ietf_yang_types:uuid                 |              | remote sdqkdnode의 id . unknown 상태라면 local SD-QKD 는 local aplication에 key를 제공할수 없다.                                                                                                    |
| priority                            | uint32                               | 기본값 0     | association / application의 우선순위. **이 값은 유저에 의해 정의 된다** 그러나 일반적으로 network 관리자에 의해 관리된다.                                                                           |
| creation_time                       | date-and-time                        | Config false | service가 생성된 날짜와 시간                                                                                                                                                                        |
| expiration_time                     | date and time                        |              | service가 만료된 날짜와 시간                                                                                                                                                                        |
| Statistics/statistic                | Container/list                       |              |                                                                                                                                                                                                     |
| Statistics/statistic/ end_time      | date-and-time                        | Config false | 통계의 끝 시간                                                                                                                                                                                      |
| Statistics/statistic/ start_time    | date-and-time                        | Config false | 통계의 시작 시간                                                                                                                                                                                    |
| Statistics/statistic/ consumed_bits | uint32                               |              | 주어진 기간동안 사용된 secret key의 양(bits)                                                                                                                                                        |
|                                     |                                      |              |                                                                                                                                                                                                     |
