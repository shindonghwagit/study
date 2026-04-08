# Network Representations and Topologies (네트워크 표현과 토폴로지)

---

## 학습 목표

- 네트워크 다이어그램에서 사용하는 **심볼과 용어**를 이해한다
- **NIC, Physical Port, Interface**의 개념을 구분할 수 있다
- **Physical Topology**와 **Logical Topology**의 차이를 설명할 수 있다

---

## 1. Network Representations (네트워크 표현)

네트워크 다이어그램은 **토폴로지 다이어그램(Topology Diagram)** 이라고도 불리며,
네트워크 내 장치들을 **심볼(아이콘)** 로 표현한다.

### 주요 용어

| 용어 | 설명 |
|------|------|
| **NIC** (Network Interface Card) | 장치를 네트워크에 물리적으로 연결하는 하드웨어 카드 |
| **Physical Port** (물리적 포트) | 케이블을 직접 꽂는 장치의 물리적 연결 구멍 |
| **Interface** (인터페이스) | 네트워크 연결을 논리적으로 나타내는 개념 |

> **Note**: **Port**와 **Interface**는 같은 의미로 혼용되는 경우가 많다.

---

### 네트워크 심볼 표

#### End Devices (종단 장치)

| 심볼 이름 | 설명 |
|-----------|------|
| Desktop Computer | 일반 데스크탑 PC |
| Laptop | 노트북 |
| Printer | 프린터 |
| IP Phone | 인터넷 전화기 |
| Wireless Tablet | 무선 태블릿 |
| TelePresence Endpoint | 화상회의 단말 |

#### Intermediary Devices (중간 장치)

| 심볼 이름 | 설명 |
|-----------|------|
| Wireless Router | 무선 라우터 |
| LAN Switch | LAN 스위치 |
| Router | 라우터 |
| Multilayer Switch | 멀티레이어 스위치 |
| Firewall Appliance | 방화벽 |

#### Network Media (전송 매체)

| 표현 | 의미 |
|------|------|
| 물결선 (파란색) | Wireless Media (무선) |
| 실선 (검은색) | LAN Media (유선 LAN) |
| 번개선 (빨간색) | WAN Media (WAN 연결) |

---

## 2. Topology Diagrams (토폴로지 다이어그램)

토폴로지 다이어그램은 크게 두 가지로 나뉜다.

---

### Physical Topology (물리적 토폴로지)

> 중간 장치들의 **물리적 위치**와 **케이블 설치 현황**을 나타낸다

- 실제 장비가 **어느 방, 어느 랙, 어느 선반**에 있는지 표현
- 네트워크 설치 및 유지보수 시 활용
- 예시: `Web Server - Rack 2, Shelf 1`, `S1 - Rack 1, Shelf 3`

```
Physical Topology 예시

[Server Room: Rm 2158]         [Rm 2124]
  Web Server (Rack2/Shelf1)      S3 ── Class 1 (Rm 2125)
  Email Server (Rack2/Shelf2) ── R1
  File Server (Rack2/Shelf3)     S4 ── Class 2 (Rm 2126)
                                 S5 ── Class 3 (Rm 2127)
[IT Office: Rm 2159]
  S2
```

---

### Logical Topology (논리적 토폴로지)

> 장치들의 **포트 정보**와 네트워크의 **IP 주소 체계(주소 지정 방식)** 를 나타낸다

- 실제 물리 위치보다 **논리적 연결 관계**와 **IP 대역**에 집중
- 네트워크 설계 및 트러블슈팅 시 활용
- 예시: `S1 F0/1 ↔ R1 G0/0`, `Network 192.168.10.0`

```
Logical Topology 예시

Network 192.168.10.0
  Web Server  ── F0/1 ┐
  Email Server── F0/2 ┤── S1 ── G0/0 ── R1 ── G1/0 ── S3 (192.168.100.0)
  File Server ── F0/3 ┘         G0/1 ── S4 (192.168.101.0)
                                G1/2 ── S5 (192.168.102.0)
  S2 (192.168.11.0)
```

---

### Physical vs Logical 비교

| 구분 | Physical Topology | Logical Topology |
|------|-------------------|-----------------|
| **표현 내용** | 장비의 물리적 위치, 케이블 | 포트 번호, IP 주소 체계 |
| **주요 용도** | 설치, 유지보수 | 설계, 트러블슈팅 |
| **표시 정보** | 방 번호, 랙, 선반 | IP 대역, 인터페이스 이름 |

---

## 전체 개념 요약

```
Network Representations and Topologies
│
├── Network Representations (네트워크 표현)
│   ├── 토폴로지 다이어그램 = 심볼로 장치 표현
│   ├── NIC      → 물리적 네트워크 연결 카드
│   ├── Port     → 물리적 연결 구멍
│   └── Interface→ 논리적 연결 개념 (Port와 혼용)
│
└── Topology Diagrams (토폴로지 다이어그램)
    ├── Physical → 물리적 위치 & 케이블 설치
    └── Logical  → 포트 번호 & IP 주소 체계
```

---

## 배운 점

- 네트워크를 그림으로 표현할 때 **정해진 심볼**을 사용하며, 장치 종류마다 고유한 아이콘이 있다
- **Port와 Interface는 같은 의미**로 쓰이는 경우가 많아 혼동하지 않도록 주의해야 한다
- **Physical Topology**는 현장 설치 관점, **Logical Topology**는 네트워크 논리 설계 관점으로 서로 보완적으로 활용된다
- 실무에서는 두 토폴로지를 함께 보며 네트워크 전체 구조를 파악한다

---