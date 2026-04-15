# 3.1 The Rules (규칙)

> **Cisco Networking Academy** - Module 3: Protocols and Models

---

## 학습 목표

- 성공적인 통신에 필요한 **규칙의 유형**을 설명할 수 있다
- 모든 통신의 **3가지 기본 요소**를 설명할 수 있다
- 프로토콜이 고려해야 할 **4가지 요구사항**을 나열할 수 있다
- 네트워크 프로토콜의 **5가지 요구사항**을 설명할 수 있다
- **Message Encoding, Formatting, Size, Timing, Delivery Options**을 구분할 수 있다

---

## 1. Communications Fundamentals (통신의 기본)

> 네트워크는 크기와 복잡성(다라지다)이 다양하다.
> **연결만으로는 부족**하고, 장치들은 **"어떻게(여떻게)" 통신할지에 대해 서로 합의**해야 한다.

### 모든 통신의 3가지 요소 (통신 3요소)

| 요소 | 설명 |
|------|------|
| **Source** (출발지/송신자) | 메시지를 **보내는** 쪽 |
| **Destination** (목적지/수신자) | 메시지를 **받는** 쪽 |
| **Channel** (채널/미디어) | 통신이 이루어지는 **경로(전송 경로)** |

```
[Source] → Channel(Media) → [Destination]
 송신자        전송 경로        수신자
```

---

## 2. Communications Protocols (통신 프로토콜)

> 모든 통신은 **프로토콜에 의해 통제된다(관리)**.
> 프로토콜은 통신이 **따라야 하는(어따라야 할) 규칙**이다.
> 이 규칙들은 프로토콜에 따라 다양하게 달라진다.

```
사람 간 통신:
Message Source → Transmitter → Transmission Medium → Receiver → Message Destination

컴퓨터 간 통신:
Message Source → Transmitter → Transmission Medium → Receiver → Message Destination
```

---

## 3. Rule Establishment (규칙의 확립)

> 개인들은 대화를 관리하기 위해 **확립된 규칙이나 합의**를 사용해야 한다.

### 올바른 형식 vs 잘못된 형식 비교

| 구분 | 내용 |
|------|------|
| ❌ **잘못된 형식** | 규칙 없이 작성 → 띄어쓰기 오류, 다른 언어 혼용 → 이해 불가 |
| ✅ **올바른 형식** | 규칙을 따라 작성 → 누구나 쉽게 읽고 이해 가능 |

### Rule Establishment (Cont.) - 프로토콜이 고려해야 할 요구사항 (고려해야한다)

| 요구사항 | 설명 |
|----------|------|
| **An identified sender and receiver** | 송신자와 수신자 식별 |
| **Common language and grammar** | 공통 언어와 문법(공통) |
| **Speed and timing of delivery** | 전달 속도와 타이밍 |
| **Confirmation or acknowledgment** | 확인 또는 수신 확인(승인) |

---

## 4. Network Protocol Requirements (네트워크 프로토콜 요구사항)

> 공통 컴퓨터 프로토콜은 다음 요구사항들에 대해 **합의**해야 한다.

| 요구사항 | 설명 |
|----------|------|
| **Message encoding** | 메시지 인코딩 |
| **Message formatting and encapsulation** | 메시지 형식화(형식화)와 캡슐화(캡슐화) |
| **Message size** | 메시지 크기 |
| **Message timing** | 메시지 타이밍 |
| **Message delivery options** | 메시지 전달 옵션 |

---

## 5. Message Encoding (메시지 인코딩)

| 용어 | 설명 |
|------|------|
| **Encoding** (인코딩) | 정보를 **전송(전송) 가능한(가능한) 형태(형태)로 변환(변환)** 하는 과정 |
| **Decoding** (디코딩) | 인코딩의 반대 과정 → 받은 신호를 원래 정보로 해석 |

### 전송 흐름

```
[Message Source]
      ↓ Encoding
  [Encoder] → [Transmitter] → [Transmission Medium "Channel"]
                                         ↓
                              [Receiver] → [Decoder] → [Message Destination]
                                                Decoding
```

- 네트워크로 전송되는 메시지는 **비트(0과 1)로 변환(대변환이 비트로)**
- 비트는 **빛, 소리, 전기(전기) 신호의 패턴**으로 인코딩
- 목적지(목적지) 호스트는 신호를 **디코딩해서 메시지를 해석**

---

## 6. Message Formatting and Encapsulation (메시지 형식화와 캡슐화)

> 메시지를 보낼 때는 **특정 형식(형식)이나 구조(구조)** 를 사용해야 한다.
> 메시지 형식은 **메시지 유형**과 **전달에 사용되는 채널**에 따라 달라진다.

### 편지 봉투 vs IPv6 패킷 헤더 비교

| 편지 봉투 | 네트워크 패킷 |
|-----------|---------------|
| 보내는 사람 주소 | Source IP Address |
| 받는 사람 주소 | Destination IP Address |
| 우체국 규격 | 프로토콜 형식(헤더 구조) |

### IPv6 헤더 구조 (40 Bytes)

| 색상 | 필드 | 역할 |
|------|------|------|
| 🟢 초록 | Version, Flow Label | 패킷의 버전과 흐름 식별 |
| ⬜ 회색 | Traffic Class, Payload Length, Next Header, Hop Limit | 전송 제어 정보 + 우선순위 |
| 🟣 보라 | Source IP Address, Destination IP Address | 출발지/목적지 주소 **(꼭 필요)** |

---

## 7. Message Size (메시지 크기)

> 호스트 간 인코딩은 **전송 매체에 적합한(적합한) 형식**이어야 한다.

```
❌ 너무 큰 메시지 하나 전송  →  전송 실패 / 오류
✅ 작은 패킷 여러 개로 분할  →  전송 성공
```

> 💡 이게 바로 **Packet Switching(패킷 교환)** 의 핵심! 데이터를 잘게 쪼개서 전송하기 때문에 네트워크를 효율적으로 사용할 수 있다.

---

## 8. Message Timing (메시지 타이밍)

| 개념 | 설명 |
|------|------|
| **Flow Control** | 데이터 전송 속도 관리, 얼마나 많은 정보를 얼마나 빠르게 전달할지 정의 |
| **Response Timeout** | 목적지로부터 **응답(응답)이 없을 때** 얼마나 기다릴지 관리 |
| **Access Method** (접근 법) | **언제 메시지를 보낼 수 있는지** 결정 |

### Collision (충돌) 문제

> 두 개 이상의 장치가 **동시에 데이터를 전송**하면 메시지가 손상됨

| 방식 | 설명 |
|------|------|
| **Proactive (사전 예방)** | 충돌이 일어나기 **전에** 미리 방지 |
| **Reactive** | 충돌 발생 **후** 복구 방법 실행 |

---

## 9. Message Delivery Options (메시지 전달 옵션)

| 방식 | 설명 | 비고 |
|------|------|------|
| **Unicast** | **1:1 통신** (일대일) | 카카오톡 개인 메시지 |
| **Multicast** | **1:N (특정 다수)** (전체는 아님) | 유튜브 라이브, 그룹 채팅 |
| **Broadcast** | **1:전체** (모두에게) | 재난 문자 |

> ⚠️ **Broadcast는 IPv4에서만** 사용 가능, **IPv6에서는 지원 안 함**
> IPv6에서는 **Anycast**라는 추가 전달 옵션 사용

### Load Balancing Server와 Multicast

```
여러 서버 중 부하가 가장 적은 서버로 요청을 분산 → Load Balancing Server (L.B.S)
Multicast와 연관: 특정 대상에게만 선택적으로 전송
```

### 노드 아이콘으로 보는 전달 방식

```
🟤 빨간(주황) 원  →  Source (송신자)
🟢 초록 원        →  메시지를 받는 장치
🟡 노란 원        →  메시지를 받지 않는 장치

Unicast    🟤 ──→ 🟢 (나머지 🟡🟡 수신 안 함)
Multicast  🟤 ──→ 🟢🟢🟢 (선택된 일부만)
Broadcast  🟤 ──→ 🟢🟢🟢🟢 (전체 수신)
```

---

## 10. Class Activity - Design a Communications System

> **목표**: 프로토콜과 표준 기관이 네트워크 통신의 **상호운용성(상호운용성)을 가능하게 하는 역할(조건)** 을 설명할 수 있다.

| 용어 | 설명 |
|------|------|
| **Protocol** | 장치들이 통신할 때 따르는 약속된 규칙 |
| **Standards Organizations** | IEEE, IETF 등 프로토콜 표준을 정의·관리하는 기관 |
| **Interoperability (상호운용성)** | 서로 다른 제조사의 장비들이 **함께 동작**할 수 있는 능력 |

---

## 전체 개념 요약

```
3.1 The Rules
│
├── Communications Fundamentals
│   └── 3요소: Source / Channel / Destination
│
├── Communications Protocols
│   └── 모든 통신은 프로토콜(규칙)을 따라야 함
│
├── Rule Establishment
│   └── 프로토콜 요구사항: 송수신자 식별 / 공통 언어 / 속도·타이밍 / 확인
│
├── Network Protocol Requirements
│   └── Encoding / Formatting·Encapsulation / Size / Timing / Delivery Options
│
├── Message Encoding     → 정보를 전송 가능한 형태로 변환 (인코딩/디코딩)
├── Message Formatting   → 특정 형식 사용, IPv6 헤더 구조
├── Message Size         → 패킷으로 쪼개서 전송
├── Message Timing       → Flow Control / Timeout / Access Method / Collision
└── Message Delivery     → Unicast(1:1) / Multicast(1:N특정) / Broadcast(1:전체)
```

---

## 배운 점

- 단순히 연결되어 있다고 통신이 되는 것이 아니라, **"어떻게 통신할지"에 대한 합의(프로토콜)** 가 반드시 필요하다
- 메시지는 **인코딩 → 전송 → 디코딩** 과정을 거치며, 전송 매체에 맞는 형태로 변환된다
- **캡슐화**는 데이터에 헤더를 씌우는 과정이며, IPv6 헤더는 40바이트로 구성된다
- **Broadcast는 IPv4에서만** 사용되고, IPv6에서는 Anycast로 대체된다
- **충돌(Collision)** 을 방지하거나 복구하는 것이 Access Method의 핵심 역할이다

---

## 참고 자료

- **Cisco Networking Academy** - Module 3: Protocols and Models
