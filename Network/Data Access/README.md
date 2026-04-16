# 3.7 Data Access (데이터 접근)

---

## 학습 목표

- **Network Layer(L3)** 와 **Data Link Layer(L2)** 주소의 역할 차이를 설명할 수 있다
- **IP 주소(L3)** 의 구조(Network portion / Host portion)를 설명할 수 있다
- **MAC 주소(L2)** 가 Hop마다 바뀌는 이유를 설명할 수 있다
- **같은 네트워크**와 **다른 네트워크(Remote)** 에서의 주소 사용 방식을 비교할 수 있다
- **Default Gateway(DGW)** 의 개념과 역할을 설명할 수 있다

---

## 1. Addresses (주소 개요)

> Data Link Layer와 Network Layer 모두 **출발지→목적지** 주소를 사용하여 데이터를 전달한다.

| 계층 | 주소 유형 | 역할 | 비고 |
|------|-----------|------|------|
| **Network Layer (L3)** | IP 주소 (논리적 주소) | 원본 출발지 → 최종 목적지까지 **IP Packet 전달** | 전체 경로에서 **변하지 않음** |
| **Data Link Layer (L2)** | MAC 주소 (물리적 주소) | 같은 네트워크 내 **NIC → NIC로 Frame 전달** | Hop마다 **바뀜** (ex) 아파트 드람) |

### 계층별 주소 역할 정리

```
Physical    → Timing and synchronization bits
Data Link   → Destination and source physical addresses   (MAC)
Network     → Destination and source logical addresses    (IP)
Transport   → Destination and source process number (ports)
Upper Layers → Encoded application data
```

---

## 2. Layer 3 Logical Address (IP 주소)

> IP Packet은 **Source IP**와 **Destination IP** 두 개의 IP 주소를 포함한다.

| 필드 | 설명 |
|------|------|
| **Source IP address** | 패킷을 보내는 장치(원본 출발지)의 IP 주소 |
| **Destination IP address** | 패킷을 받을 장치(최종 목적지)의 IP 주소 |

> 💡 이 두 주소는 **같은 링크**에 있을 수도 있고, **원격(remote)** 에 있을 수도 있다.

### IP 주소의 구조 (IPv4 기준)

> IP 주소는 두 부분으로 구성된다.

| 부분 | IPv4 명칭 | IPv6 명칭 | 설명 |
|------|-----------|-----------|------|
| **Network portion** | Network portion | Prefix | 가장 왼쪽 부분 → **어느 네트워크 그룹**인지 식별. 같은 LAN/WAN은 동일한 Network portion을 가짐 |
| **Host portion** | Host portion | Interface ID | 나머지 부분 → **그룹 내 특정 장치** 식별. 네트워크 내에서 유일(unique) |

### 예시

```
PC1         → 192.168.1.110   (Network: 192.168.1 / Host: 110)
Web Server  → 172.16.1.99     (Network: 172.16.1  / Host: 99)
→ Network portion이 다름 → 서로 다른 네트워크!
```

---

## 3. Devices on the Same Network (같은 네트워크)

> 출발지와 목적지가 **같은 네트워크**에 있으면 Network portion이 동일하다.

```
PC1        → 192.168.1.110   (Network: 192.168.1)
FTP Server → 192.168.1.9     (Network: 192.168.1)
→ 같은 네트워크 → 직접 통신 가능
```

### 같은 네트워크에서의 MAC 주소 (L2)

> 같은 Ethernet 네트워크에서는 **실제 목적지 NIC의 MAC 주소**를 Frame에 사용한다.

- MAC 주소는 Ethernet NIC에 **물리적으로 내장**된 로컬 주소
- **Source MAC** = 출발지 NIC의 MAC (링크 내 originator)
- **Destination MAC** = 목적지 NIC의 MAC (항상 같은 링크에 있어야 함)

```
L2 Frame Header          L3 IP Packet Header
┌──────────────────┬─────────────────────────────────────┐
│ Destination MAC  │ Source MAC  │ Source IP │ Dest IP   │ Data
│ CC-CC-CC-CC-CC-CC│ AA-AA-...-AA│ 192.168.1.110 │ 192.168.1.9 │
└──────────────────┴─────────────────────────────────────┘
```

---

## 4. Devices on a Remote Network (다른 네트워크 — Remote)

> 목적지가 **다른 네트워크(Remote)** 에 있으면 어떻게 되는가?
> → Network Layer(L3)와 Data Link Layer(L2) 모두 영향을 받는다.

### Default Gateway (DGW) 개념

> 💡 **Default Gateway (DGW)** = 자 모르겠으면 일단 나한테 봐

- DGW는 해당 LAN의 일부인 **라우터 인터페이스 IP 주소**
- 외부 네트워크(remote)로 가는 모든 트래픽의 **"문(door)" 또는 "관문(gateway)"**
- LAN 내 모든 장치는 반드시 DGW 주소를 알아야 함 → 모르면 LAN 내에서만 통신 가능
- PC1이 L2에서 DGW(Router)로 프레임을 전달하면, 그 이후 라우터가 실제 목적지까지 **라우팅 프로세스** 시작

```
PC1 (192.168.1.110)  →  R1 (DGW: 192.168.1.1)  →  R2 (172.16.1.1)  →  Web Server (172.16.1.99)
```

---

## 5. Role of Data Link Layer Addresses (L2 주소의 역할)

### 같은 네트워크 (Same IP Network)

```
L2 Header                   L3 IP Packet
┌────────────────────────┬─────────────────────────────┐
│ Dest MAC  │ Source MAC │ Source IP    │ Dest IP      │ Data
│ CC-CC-..  │ AA-AA-..   │ 192.168.1.110│ 192.168.1.9  │
└────────────────────────┴─────────────────────────────┘
→ L2 Destination = 실제 목적지 (FTP Server) MAC
```

### 다른 네트워크 (Different IP Network)

> 최종 목적지가 Remote일 때, L3는 DGW의 IP를 L2에 알려준다.

**첫 번째 세그먼트 (PC1 → R1)**
```
L2 Header                        L3 IP Packet (변하지 않음!)
┌─────────────────────────────┬──────────────────────────────┐
│ Dest: 11-11-11-11-11-11(R1) │ Source: AA-AA-.. │ Source IP: 192.168.1.110 │ Dest IP: 172.16.1.99 │
└─────────────────────────────┴──────────────────────────────┘
→ L2 Destination = R1 (Default Gateway) MAC
→ L3 Destination = Web Server IP (그대로 유지!)
```

**두 번째 세그먼트 (R1 → R2)**
```
→ L2 Source: R1 exit interface MAC
→ L2 Destination: R2 MAC
→ L3 IP Packet: 변하지 않음 (192.168.1.110 → 172.16.1.99)
```

**세 번째 세그먼트 (R2 → Web Server)**
```
→ L2 Source: R2 exit interface MAC
→ L2 Destination: Web Server NIC MAC
→ L3 IP Packet: 변하지 않음 (192.168.1.110 → 172.16.1.99)
```

### 핵심 원칙 ⭐

| 계층 | Hop마다 변하는가? | 이유 |
|------|------------------|------|
| **L2 MAC 주소** | ✅ **변함** | 로컬(local) 주소 → 각 링크/세그먼트마다 새로운 Frame 생성 |
| **L3 IP 주소** | ❌ **변하지 않음** | 글로벌(global) 주소 → 최종 목적지는 동일하기 때문 |

```
PC1 → R1 → R2 → Web Server

L2 MAC:  [AA→11] → [11→22] → [22→AB]   ← Hop마다 바뀜
L3 IP:   [192.168.1.110 → 172.16.1.99] ← 처음부터 끝까지 동일
```

---

## 전체 개념 요약

```
3.7 Data Access
│
├── Addresses
│   ├── L3 (Network Layer) → IP 주소 → 원본~최종 목적지 전달
│   └── L2 (Data Link Layer) → MAC 주소 → NIC~NIC (같은 네트워크 내)
│
├── Layer 3 Logical Address (IP)
│   ├── Source IP    → 패킷 원본 출발지
│   ├── Destination IP → 패킷 최종 목적지
│   ├── Network portion → 어느 네트워크 그룹인지
│   └── Host portion    → 그룹 내 특정 장치
│
├── Same Network
│   ├── Network portion 동일
│   ├── L2 Destination = 실제 목적지 MAC
│   └── 직접 통신 가능
│
├── Remote Network
│   ├── Default Gateway (DGW) → LAN의 "문" 역할 라우터
│   ├── L2 Destination = DGW(Router) MAC  ← 로컬 주소라 Hop마다 바뀜
│   └── L3 Destination IP = Web Server    ← 글로벌 주소라 변하지 않음
│
└── 핵심 원칙
    ├── L2 MAC → Hop마다 변함 (로컬 주소)
    └── L3 IP  → 처음~끝 동일 (글로벌 주소)
```

---

## 배운 점

- **L2(MAC)** 는 같은 네트워크 내 NIC↔NIC 전달용, **L3(IP)** 는 원본→최종 목적지 전달용으로 역할이 다르다
- IP 주소는 **Network portion + Host portion** 으로 구성 — Network portion이 같으면 같은 네트워크
- **Default Gateway(DGW)** = 모르겠으면 일단 나한테 봐 → LAN 밖으로 나가는 유일한 출구 (라우터)
- **L2 MAC 주소는 Hop마다 바뀐다** — 각 링크에서 새로운 Frame을 만들기 때문
- **L3 IP 주소는 절대 바뀌지 않는다** — 원본 출발지와 최종 목적지는 전체 경로에서 동일
- Packet은 수정되지 않지만, Frame은 각 라우터를 거칠 때마다 새로 생성된다

---