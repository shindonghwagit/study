# 1.5 Internet Connections (인터넷 연결)

---

## 학습 목표

- 사용자와 조직을 인터넷에 연결하는 **다양한 접속 기술**을 구분할 수 있다
- **가정용과 기업용** 인터넷 연결 방식의 차이를 설명할 수 있다
- **컨버징 네트워크**의 개념과 장점을 설명할 수 있다

---

## 1. Internet Access Technologies (인터넷 접속 기술)

> 사용자와 조직을 인터넷에 연결하는 방법은 다양하다.

### 가정용 / 소규모 사무실

| 기술 | 설명 |
|------|------|
| **Broadband Cable** | 케이블 TV 선로를 이용한 인터넷 |
| **DSL** (Digital Subscriber Line) | 전화선을 이용한 브로드밴드 인터넷 |
| **Wireless WAN** | 무선 방식의 광역 인터넷 접속 |
| **Mobile Services** | LTE, 5G 등 이동통신망 이용 |

### 기업용

기업은 **IP 전화, 화상회의, 데이터센터 스토리지** 등을 지원하기 위해 더 빠른 연결이 필요하다.

| 기술 | 설명 |
|------|------|
| **Business DSL** | 기업용 고속 DSL |
| **Leased Lines** (전용선) | 특정 기업만 사용하는 독점 회선 |
| **Metro Ethernet** | 도시 규모의 이더넷 기반 고속 연결 |

---

## 2. Home and Small Office Internet Connections (가정 및 소규모 사무실)

| 연결 방식 | 설명 | 특징 |
|-----------|------|------|
| **Cable** | 케이블 TV 사업자가 제공 | 고대역폭, 항상 연결 유지 |
| **DSL** | 전화선을 통한 연결 | 고대역폭, 항상 연결 유지 |
| **Cellular** (셀룰러) | 휴대폰 네트워크(LTE/5G) 이용 | 이동 중에도 사용 가능 |
| **Satellite** (위성) | 위성을 통한 연결 | ISP가 없는 **농촌·오지** 지역에 유용 |
| **Dial-up Telephone** (전화 접속) | 모뎀을 이용한 전화선 연결 | 저렴하지만 속도 매우 느림 |

### 연결 흐름

```
[Home User]      ── DSL ──────────────────┐
[Teleworker]     ── Cable / Cellular ─────┤ ISP → Internet
[Small Office]   ── Satellite / Dial-up ──┘
```

### 속도 & 상황별 선택 가이드

```
빠름  ┌─ Cable / DSL   → 일반 가정, 소규모 사무실
      ├─ Cellular      → 이동 중인 재택근무자
      ├─ Satellite     → 오지·농촌 (ISP 없는 지역)
느림  └─ Dial-up       → 최후의 수단 (매우 저렴하지만 느림)
```

---

## 3. Businesses Internet Connections (기업용 인터넷 연결)

> 기업 비즈니스 연결은 다음을 요구할 수 있다:
> - **더 높은 대역폭** (higher bandwidth)
> - **전용 연결** (dedicated connections)
> - **관리형 서비스** (managed services)

| 연결 방식 | 설명 |
|-----------|------|
| **Dedicated Leased Line** (전용 임대 회선) | ISP 네트워크 내에 예약된 전용 회선으로 먼 거리의 사무소를 음성/데이터로 연결 |
| **Ethernet WAN** | LAN에서 쓰는 이더넷 기술을 **WAN 규모로 확장** (= Metro Ethernet) |
| **DSL** (기업용) | **SDSL(대칭형 DSL)** 등 다양한 형태 제공 → 업/다운 속도 대칭 |
| **Satellite** (위성) | **유선 연결이 불가능한 환경**에서 연결 수단 제공 |

### 가정용 vs 기업용 비교

```
가정용  →  Cable, DSL, Cellular, Satellite, Dial-up
              비용 낮음 / 속도·안정성 상대적으로 낮음

기업용  →  전용선, Ethernet WAN, Business DSL, Satellite
              비용 높음 / 속도·안정성 높음
```

> 💡 **SDSL**: 일반 DSL은 다운로드 속도 > 업로드 속도인데, SDSL은 **업/다운 속도가 동일**해서 서버 운영이 많은 기업에 적합!

---

## 4. The Converging Network (컨버징 네트워크)

### 과거 - 통합 이전

> 컨버징 네트워크 이전에는, 조직이 **전화·영상·데이터**를 위해 **각각 별도의 케이블**을 설치해야 했다.
> 각 네트워크는 신호를 전달하기 위해 **서로 다른 기술, 규칙, 표준**을 사용했다.

| 네트워크 | 방식 | 특징 |
|----------|------|------|
| **Computer Networks** | Packet Switched | 데이터 전송 |
| **Telephone Networks** | **Circuit Switched** (전용 회선) | A→B 전용 채널 점유, C는 B를 통해 선 연결 |
| **Broadcast Networks** | 방송 신호 | 영상·방송 |

```
문제점:
데이터  → 데이터 전용 케이블 → 데이터 표준
전화    → 전화 전용 케이블   → 전화 표준 (Circuit Switched)
영상    → 영상 전용 케이블   → 방송 표준

= 인프라 3배, 비용 3배, 관리 복잡도 3배
```

### 현재 - Converging Network (통합 네트워크)

> **데이터·음성·영상을 하나의 네트워크 인프라로 통합**하여 전송

- 하나의 링크에서 **data, voice, video** 모두 전송 가능
- **동일한 규칙과 표준** 사용 → 관리 단순화
- **One Network - Multiple Devices** 구조

```
과거:
  PC      → 데이터 전용 망
  전화기  → 전화 전용 망 (Circuit Switched)
  TV      → 방송 전용 망

현재 (Converging):
  PC     ┐
  전화기 ┼── 하나의 네트워크 ──→ data + voice + video 동시 전송
  TV     ┘
```

> 💡 우리가 지금 쓰는 **인터넷 전화(VoIP), IPTV, 인터넷**이 모두 같은 회선 하나로 오는 게 바로 이 개념이야!

---

## 전체 개념 요약

```
Internet Connections
│
├── Internet Access Technologies
│   ├── 가정용  → Cable, DSL, Wireless WAN, Mobile
│   └── 기업용  → Business DSL, 전용선, Metro Ethernet
│
├── Home & Small Office Connections
│   ├── Cable     → 케이블 TV 선로 활용
│   ├── DSL       → 전화선 활용
│   ├── Cellular  → LTE/5G
│   ├── Satellite → 오지·농촌 특화
│   └── Dial-up   → 저렴하지만 느림
│
├── Business Connections
│   ├── Dedicated Leased Line → 전용 회선 (고신뢰)
│   ├── Ethernet WAN          → LAN 기술 WAN 확장
│   ├── Business DSL (SDSL)   → 업/다운 대칭
│   └── Satellite             → 유선 불가 환경
│
└── Converging Network
    ├── 과거 → 전화/데이터/영상 각각 별도 망
    │         Circuit Switched 방식 (전용 회선 점유)
    └── 현재 → 하나의 망으로 통합
               data + voice + video 동시 전송
```

---

## 배운 점

- 인터넷 연결 방식은 **사용 환경(가정/기업/오지)** 에 따라 최적의 방식이 다르다
- 기업은 단순한 속도뿐만 아니라 **전용성·안정성·관리성**까지 요구하기 때문에 더 비싼 연결 방식을 사용한다
- **Circuit Switched(전화망)** 는 A→B 전용 회선을 점유하는 방식이라 비효율적이었고, 이를 해결한 것이 **Packet Switched** 방식이다
- **컨버징 네트워크**는 각각 분리되어 있던 전화/데이터/영상 망을 하나로 통합하여, 하나의 인프라로 모든 서비스를 제공하는 현대 네트워크의 핵심 개념이다

---

## 참고 자료

- **Cisco Networking Academy** - Internet Connections 강의 슬라이드
- Cisco CCNAv7: Introduction to Networks (Module 1.5)