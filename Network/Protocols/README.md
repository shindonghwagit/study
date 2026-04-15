# 3.2 Protocols (프로토콜)

> **Cisco Networking Academy** - Module 3: Protocols and Models

---

## 학습 목표

- 네트워크 프로토콜의 **4가지 유형**을 설명할 수 있다
- 프로토콜의 **6가지 기능**을 구분하고 설명할 수 있다
- **HTTP, TCP, IP, Ethernet**의 역할을 계층 구조로 설명할 수 있다
- **캡슐화(Encapsulation)** 와 **역캡슐화(De-encapsulation)** 과정을 설명할 수 있다
- 계층별 **PDU 이름**을 설명할 수 있다

---

## 1. Network Protocol Overview (네트워크 프로토콜 개요)

> 네트워크 프로토콜은 **공통된 규칙의 집합**을 정의한다.

프로토콜은 장치에서 다음으로 구현될 수 있다:
- **Software** (소프트웨어)
- **Hardware** (하드웨어)
- **Both** (둘 다)

각 프로토콜은 고유한:
- **Function** (기능)
- **Format** (형태)
- **Rules** (규칙)

을 가진다.

### 프로토콜 유형 4가지

| 프로토콜 유형 | 설명 |
|--------------|------|
| **Network Communications** | 하나 이상의 네트워크에서 둘 이상의 장치가 통신할 수 있게 함 |
| **Network Security** | 인증(인증), 데이터 무결성(무결성), 데이터 암호화(암호화)를 제공하여 데이터 보안 |
| **Routing** (최적의 경로 선택) | 라우터가 경로 정보를 교환하고, 경로를 비교하여 **최적 경로 선택** |
| **Service Discovery** | 장치 또는 서비스의 **자동 감지**에 사용 |

> 💡 **Cell 네트워크로 부른다** → 기지국 → 기지국 → 서버 기지국에서 신호를 받아서 4 갈래로 가기 되면, 나들로 불리 동일하게 도달하게 이름 Hand Over라고 표현

---

## 2. Network Protocol Functions (네트워크 프로토콜 기능)

> 장치들은 통신하기 위해 **합의된(합의된) 프로토콜**을 사용한다.
> 프로토콜은 **하나 또는 여러 개의 기능**을 가질 수 있다.

### 계층별 프로토콜 분류 (필기)

```
Trans  →  TCP / UDP
NET    →  IP / IPX
Data   →  LLC, MAC (Media Access Control) → Ethernet, WiFi
Phy    →                                    LTE, 5G
```

### 프로토콜 6가지 기능

| 기능 | 설명 | 핵심 키워드 |
|------|------|-------------|
| **Addressing** | 송신자와 수신자 식별 | 식별 |
| **Reliability** (신뢰성) | 데이터의 **확실한(완벽) 전달** 보장 | 보장 |
| **Flow Control** | 데이터가 **효율적인 속도**로 흐르도록 보장 | 속도 조절 |
| **Sequencing** (순서 지정) | 전송된 각 데이터 조각에 **고유한 번호** 부여 → 고장 번호 2, 전송됨 2개, 순서 지정 (다시) | 번호 부여 |
| **Error Detection** | 전송 중 데이터가 **손상(손상)됐는지 확인** | 오류 감지 |
| **Application Interface** | 네트워크 애플리케이션 간 **프로세스-to-프로세스 통신** | 앱 간 통신 |

---

## 3. Protocol Interaction (프로토콜 상호작용)

> 네트워크는 **여러 개의 프로토콜**을 함께 사용한다.
> 각 프로토콜은 **고유한 기능과 형식**을 가진다.

### 프로토콜별 기능

| 프로토콜 | 기능 |
|----------|------|
| **HTTP** | 웹 서버(서버)와 웹 클라이언트(클라이언트)의 **상호작용 방식** 규정, 콘텐츠와 형식 정의 |
| **TCP** | 개별 통신 세션(세션) 관리, **확실한(세션)한 전달 보장**, 흐름 제어 관리 |
| **IP** | 송신자에서 수신자까지 **전 세계적으로 메시지 전달** |
| **Ethernet** | **같은 LAN 내**에서 NIC → NIC로 메시지 전달 → 네트워크 크기 작위하는 하드(같은 LAN 내에서 Datagram 전달) |

### 계층 구조

```
┌─────────────┐
│    HTTP     │  ← 웹 콘텐츠 형식·규칙 (Application)
├─────────────┤
│    TCP      │  ← 신뢰성·흐름 제어 (Transport)
├─────────────┤
│     IP      │  ← 주소 지정·경로 결정 (Network)
├─────────────┤
│  Ethernet   │  ← 같은 LAN 내 실제 전송 (Data Link)
└─────────────┘
```

---

## 4. TCP/IP Communication Process (TCP/IP 통신 과정)

### 핵심 개념

| 개념 | 설명 |
|------|------|
| **Encapsulation** (캡슐화) | 데이터를 보낼 때 **헤더를 층층이 씌우는** 과정 (웹 서버 측) |
| **De-encapsulation** (역캡슐화) | 받은 데이터에서 **헤더를 층층이 벗겨내는** 과정 (웹 클라이언트 측) |

### 계층별 PDU 이름 (필기)

```
Application  →  Data (Header + DATA) → BlackBox 형태 추구
Transport    →  Segment  (TCP/UDP)
Network      →  Packet   (IP)
Data Link    →  Frame    (MAC) → MTU (Maximum Transmission Unit)
                                  표준 Ethernet 기준: 1500 byte
Physical     →  Bit stream (0과 1)
```

> 💡 **포트 번호 (= Application address)**
> - 포트 번호: 어떤 앱(프로세스)인지 식별
> - 물리적 주소 → IP 주소
> - 논리적 주소 → MAC 주소
> - **1GB = 8Gb (Byte vs bit 구분 중요!)**
> - **Hop**: A → B → C 처럼 라우터를 하나씩 거치는 것

### 웹 서버 → 클라이언트 캡슐화 과정

```
1. User Data        → 실제 웹 페이지 내용
        ↓ TCP 헤더 추가 (trailer 포함)
2. TCP Segment      → 전송 제어 정보 추가
        ↓ IP 헤더 추가
3. IP Packet        → 출발지/목적지 IP 주소 추가
        ↓ Ethernet 헤더 추가
4. Ethernet Frame   → 물리적 전송 정보 추가
        ↓
[Ethernet | IP | TCP | Data] 형태로 전송!
```

### 웹 클라이언트 역캡슐화 과정

```
수신: [Ethernet | IP | TCP | Data]  (비트 신호로 수신)
        ↓ Ethernet 헤더 제거
        ↓ IP 헤더 제거
        ↓ TCP 헤더 제거
        ↓
User Data (실제 웹 페이지 내용) → 브라우저에 표시!
```

### 택배 비유

```
캡슐화 (포장)                역캡슐화 (개봉)
물건(Data)                   택배 차에서 내리기 (Ethernet 제거)
→ 박스에 넣기 (TCP Segment)  → 주소 라벨 확인 (IP 제거)
→ 주소 라벨 붙이기 (IP Packet)→ 박스 열기 (TCP 제거)
→ 택배 차에 싣기 (Frame)     → 물건 꺼내기 (Data 사용!)
→ 출발!
```

---

## 전체 개념 요약

```
3.2 Protocols
│
├── Network Protocol Overview (4가지 유형)
│   ├── Network Communications → 장치 간 통신
│   ├── Network Security       → 인증·무결성·암호화
│   ├── Routing                → 최적 경로 선택
│   └── Service Discovery      → 장치/서비스 자동 감지
│
├── Network Protocol Functions (6가지 기능)
│   ├── Addressing    → 송수신자 식별
│   ├── Reliability   → 전달 보장
│   ├── Flow Control  → 속도 관리
│   ├── Sequencing    → 순서 번호 부여
│   ├── Error Detection → 오류 감지
│   └── Application Interface → 앱 간 통신
│
├── Protocol Interaction
│   ├── HTTP     → 웹 콘텐츠 규칙
│   ├── TCP      → 신뢰성·세션 관리
│   ├── IP       → 전 세계 경로 결정
│   └── Ethernet → 같은 LAN 내 NIC↔NIC
│
└── TCP/IP Communication Process
    ├── 캡슐화   → Data → Segment → Packet → Frame → Bits
    ├── 역캡슐화 → Bits → Frame → Packet → Segment → Data
    └── PDU: Data / Segment / Packet / Frame / Bit stream
```

---

## 배운 점

- 프로토콜은 **소프트웨어, 하드웨어, 또는 둘 다**로 구현될 수 있으며, 각각 고유한 기능·형태·규칙을 가진다
- **Routing 프로토콜**은 단순히 경로를 찾는 게 아니라 여러 경로를 **비교해서 최적 경로를 선택**한다
- **캡슐화는 포장**, **역캡슐화는 개봉**으로 이해하면 쉽다. 계층마다 헤더가 추가/제거된다
- 각 계층의 PDU 이름이 다르다: **Data → Segment → Packet → Frame → Bits**
- **1GB = 8Gb** (Byte와 bit 혼동 주의), **포트 번호 = Application address**
- **MTU(Maximum Transmission Unit)**: 표준 Ethernet 기준 **1500 byte**

---

## 참고 자료

- **Cisco Networking Academy** - Module 3: Protocols and Models