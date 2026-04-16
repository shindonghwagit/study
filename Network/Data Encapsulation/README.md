# 3.6 Data Encapsulation (데이터 캡슐화)

---

## 학습 목표

- **Segmenting**과 **Multiplexing**의 개념과 이점을 설명할 수 있다
- **PDU(Protocol Data Unit)** 의 계층별 이름을 설명할 수 있다
- **Encapsulation(캡슐화)** 과정을 단계별로 설명할 수 있다
- **De-encapsulation(역캡슐화)** 과정을 단계별로 설명할 수 있다
- **Sequencing**의 개념과 TCP의 역할을 설명할 수 있다

---

## 1. Segmenting Messages (메시지 분할)

> **Segmenting**: 큰 메시지를 **작은 단위로 쪼개는** 과정
> **Multiplexing**: 여러 개의 분할된 데이터 스트림을 **서로 엮어서(interleaving)** 함께 전송하는 과정

> 💡 **Multiplexing** = 자원 공유 + process 혼합 → 여러 프로세스의 데이터를 함께 전송

### Segmenting의 2가지 이점

| 이점 | 설명 |
|------|------|
| **Increases Speed** (속도 향상) | 대용량 데이터를 통신 링크를 독점하지 않고 전송 가능 |
| **Increases Efficiency** (효율 향상) | 전송 실패 시 **전체가 아닌 해당 Segment만** 재전송하면 됨 |

---

## 2. Protocol Data Units (PDU)

> **캡슐화(Encapsulation)**: 프로토콜이 데이터에 자신의 정보(헤더)를 추가하는 과정
> 각 단계마다 PDU는 새로운 기능을 반영하는 **다른 이름**을 가진다.

### PDU 계층별 이름 (Passing down the stack)

```
Application  →  Data        (Email Data, User Data)
Transport    →  Segment     (Transport header + Data)
Network      →  Packet      (Network header + Transport header + Data)
Data Link    →  Frame       (Frame header + Network header + Transport header + Data + Frame trailer)
Physical     →  Bits        (1100010101000101100101001010101001)
```

### PDU 구조 시각화

```
┌──────────────────────────────────────────┐
│                  Email Data              │  ← Data
├───────────┬──────────────────────────────┤
│ Transport │         Data                 │  ← Segment
│  header   │                              │
├─────────┬─┴──────────┬───────────────────┤
│ Network │  Transport │    Data           │  ← Packet
│ header  │   header   │                   │
├───────┬─┴──────────┬─┴──────────┬────────┤
│ Frame │  Network   │ Transport  │  Data  │ Frame │  ← Frame
│header │  header    │  header    │        │trailer│
└───────┴────────────┴────────────┴────────┴───────┘
  1100010101000101100101001010101001...              ← Bits
```

> 💡 PDU의 이름 규칙은 **TCP/IP 프로토콜 suite 기준**으로 명명한다.
> PDU 이름에 대한 **범용적인 명명 규칙은 없다** (no universal naming convention).

---

## 3. Encapsulation Example (캡슐화 예시)

> 캡슐화는 **Top-Down 방식**으로 진행된다.
> 위 계층이 처리를 완료하면 아래 계층으로 넘겨주고, 최종적으로 **Bit Stream**으로 전송된다.

### 캡슐화 단계

```
1. User Data (실제 이메일·웹 내용)
        ↓ Transport header 추가 (포트 번호 등)
2. TCP Segment
        ↓ Network header 추가 (IP 주소)
3. IP Packet
        ↓ Frame header + Frame trailer 추가
4. Ethernet Frame
        ↓ 물리 매체를 통해 전송
5. Bit Stream → [Ethernet | IP | TCP | Data] 형태로 전송!
```

### 핵심 원칙

- **Top-Down process** — Application → Transport → Network → Data Link → Physical 순서
- 각 계층은 자신의 처리를 완료한 뒤 **아래 계층으로 전달(pass down)**
- 마지막에는 반드시 **Bit Stream** 형태로 물리 매체에 실려 전송됨

---

## 4. De-encapsulation Example (역캡슐화 예시)

> 역캡슐화는 **Bottom-Up 방식**으로 진행된다.
> 각 계층은 자신의 헤더를 **제거(strip off)** 하고 위 계층으로 올려 보낸다.

### 역캡슐화 단계

```
수신: 01010110101001011101101001001010... (Bit Stream)
        ↓
1. Bits        → 비트 신호 수신
        ↓ Frame header/trailer 제거
2. Frame       → Ethernet 헤더 분석·제거
        ↓ Network header 제거
3. Packet      → IP 헤더 분석·제거
        ↓ Transport header 제거
4. Segment     → TCP 헤더 분석·제거
        ↓
5. Data        → 실제 데이터 → 애플리케이션에서 처리!
```

### Encapsulation vs De-encapsulation 비교

| 구분 | 방향 | 과정 | 역할 |
|------|------|------|------|
| **Encapsulation** (캡슐화) | Top-Down ↓ | 헤더를 층층이 추가 | Web Server 측 (송신) |
| **De-encapsulation** (역캡슐화) | Bottom-Up ↑ | 헤더를 층층이 제거 | Web Client 측 (수신) |

---

## 5. Sequencing (순서 지정)

> **Sequencing**: Segment에 번호를 붙여 수신 측에서 **올바른 순서로 재조립**할 수 있게 하는 과정

- 여러 조각(Segment)에 **번호 레이블**을 붙임 → 도착 순서가 달라도 올바르게 재조립
- **TCP**가 각 개별 Segment의 Sequencing을 담당한다

### Sequencing 흐름

```
송신 측                             수신 측
[3][2][1] ──────────────────────→  [1][2][3] (재조립)
[3][2][1] ──────────────────────→  [1][2][3] (재조립)

Multiple pieces are labeled for easy direction and re-assembly.
Labeling provides for ordering and assembling the pieces when they arrive.
```

---

## 전체 개념 요약

```
3.6 Data Encapsulation
│
├── Segmenting Messages
│   ├── Segmenting  → 큰 데이터를 작은 단위로 분할
│   ├── Multiplexing → 여러 스트림을 interleaving해서 전송
│   ├── Increases Speed     → 링크 독점 없이 전송
│   └── Increases Efficiency → 실패 시 해당 Segment만 재전송
│
├── Protocol Data Units (PDU)
│   ├── Data    (Application)
│   ├── Segment (Transport)   ← Transport header + Data
│   ├── Packet  (Network)     ← Network header + ...
│   ├── Frame   (Data Link)   ← Frame header + ... + Frame trailer
│   └── Bits    (Physical)    ← 0과 1의 비트 스트림
│
├── Encapsulation (캡슐화)
│   ├── Top-Down 방식
│   ├── Data → Segment → Packet → Frame → Bits
│   └── 각 계층이 헤더를 추가하고 아래 계층으로 전달
│
├── De-encapsulation (역캡슐화)
│   ├── Bottom-Up 방식
│   ├── Bits → Frame → Packet → Segment → Data
│   └── 각 계층이 자신의 헤더를 제거하고 위 계층으로 전달
│
└── Sequencing
    ├── Segment에 번호를 붙여 재조립 순서 보장
    └── TCP가 Sequencing 담당
```

---

## 배운 점

- **Segmenting**은 단순히 데이터를 자르는 것, **Multiplexing**은 여러 프로세스의 분할 데이터를 **함께 섞어서** 전송하는 것이다
- PDU 이름은 **TCP/IP suite 기준** 으로 명명하며, 계층마다 다른 이름을 가진다: **Data → Segment → Packet → Frame → Bits**
- **캡슐화는 Top-Down**, **역캡슐화는 Bottom-Up** — 방향이 반대다
- 각 계층은 자신의 헤더만 보고 처리한 뒤, 상위 계층으로 넘긴다 (헤더를 strip off)
- **TCP**가 Segment에 번호를 붙여 순서를 보장한다 — 도착 순서가 달라도 올바르게 재조립 가능
- Segmenting의 핵심 이점: **속도(Speed)** + **효율(Efficiency)** — 실패 시 전체가 아닌 해당 조각만 재전송

---