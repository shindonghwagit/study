# 1.8 Network Security (네트워크 보안)

---

## 학습 목표

- 네트워크 보안이 왜 필수적인지 설명할 수 있다
- **외부 위협(External Threats)** 과 **내부 위협(Internal Threats)** 의 종류를 구분할 수 있다
- 가정용/소규모 네트워크와 대규모 네트워크의 **보안 솔루션** 차이를 설명할 수 있다
- **ACL, IPS, VPN** 등 기업용 보안 장치의 역할을 설명할 수 있다

---

## 1. Security Threats (보안 위협)

> 네트워크 보안은 **네트워크 규모와 관계없이(규모에 상관없이)** 네트워킹의 **필수적인(중요의)** 부분이다.

- 보안을 구현할 때는 **데이터를 보호**하면서도 **네트워크에서 기대되는 QoS(서비스 품질)도 유지(QoS 흐름도 유지)** 해야 한다
- 네트워크 보안에는 데이터 보호와 위협 완화(완료)를 위해 **다양한 프로토콜, 기술, 장치, 도구, 기법**이 사용된다
- 위협은 **외부(외부)** 또는 **내부(내부)** 에서 발생할 수 있다

---

## 2. External Threats (외부 위협)

| 위협 | 설명 |
|------|------|
| **Viruses, Worms, Trojan Horses** | 악성 코드로 시스템 감염 |
| **Spyware and Adware** | 몰래 정보 수집 / 광고 강제 노출 |
| **Zero-day Attacks** | 보안 패치 나오기 전 날(0일), 패치 전의 취약점을 노린 공격 |
| **Threat Actor Attacks** | 해커의 공격 |
| **Denial of Service (DoS)** | 트래픽 폭주 → 서버 마비 (DOS) |
| **Data Interception and Theft** | 데이터 훔치기 |
| **Identity Theft** | 신분 도용 |

---

## 3. Internal Threats (내부 위협)

| 위협 | 설명 |
|------|------|
| **Lost or Stolen Devices** | 기기 분실·도난 |
| **Accidental Misuse by Employees** | 직원의 실수로 인한 오용 |
| **Malicious Employees** | 악의적인 직원 |

### 위협 방향 정리

```
External Threat  →  인터넷 외부에서 방화벽을 뚫고 침입 시도
                    (악성코드, 해킹, DoS, 데이터 도용 등)

Internal Threat  →  내부 네트워크 안에서 발생
                    (분실 기기, 직원 실수, 악의적 내부자)
```

> 💡 방화벽이 외부 위협을 막아도 **이미 내부에 감염된 장치(Compromised Host)** 가 있으면 내부 전체로 위협이 퍼질 수 있다 → 내부 보안도 외부 보안만큼 중요!

---

## 4. Security Solutions (보안 솔루션)

> 보안은 **여러 계층에 걸쳐(multiple layers)** 하나 이상의 보안 솔루션을 사용하여 구현되어야 한다.

### 가정용 / 소규모 사무실 보안

| 솔루션 | 설명 |
|--------|------|
| **Antivirus & Antispyware** | End Device에 설치 → 악성코드·스파이웨어 탐지 및 제거 |
| **Firewall Filtering** | 네트워크에 대한 **무단 접근 차단** |

### 대규모 네트워크 추가 보안 (Security Solutions Cont.)

| 솔루션 | 설명 |
|--------|------|
| **Dedicated Firewall System** (전용 방화벽) | 기업 전용 1차 차단 → 전용 방화벽 |
| **ACL** (Access Control List) | 누가 어디에 접근할 수 있는지 **접근 제어 룰 정의** |
| **IPS** (Intrusion Prevention System) | 공격을 **탐지하고 자동으로 차단** → 침입 방지 시스템 |
| **VPN** (Virtual Private Network) | 공용 인터넷에서 **암호화된 안전한 터널** 생성 → 가상 사설 망 |

### 심층 방어 구조 (Defense in Depth)

```
[Internet]
    ↓
[ACL]           ← 접근 허용/차단 규칙 적용
    ↓
[Firewall 🧱]   ← 외부 위협 1차 차단
    ↓
[IPS]           ← 침입 탐지 및 자동 차단
    ↓
[내부 네트워크]
    ↓
[Firewall 🧱]   ← 내부 구역 간 추가 차단
    ↓
[핵심 서버/자원]
```

> 💡 보안은 방어선을 **겹겹이 쌓는 구조(심층 방어)** 가 핵심이야!

---

### 핵심 마무리 문장

> *"네트워크 보안 공부는 **스위칭(이머닝)과 라우팅 인프라**에 대한 명확한 이해에서 시작된다."*

→ 보안을 제대로 이해하려면 **네트워크 기초(스위치, 라우터 동작 원리)** 를 먼저 알아야 한다!

---

## 전체 개념 요약

```
Network Security (1.8)
│
├── Security Threats (보안 위협)
│   ├── External (외부)
│   │   ├── Virus / Worm / Trojan  → 악성 코드
│   │   ├── Spyware / Adware       → 정보 수집·광고
│   │   ├── Zero-day               → 패치 전 취약점 공격
│   │   ├── Threat Actor           → 해커 공격
│   │   ├── DoS                    → 서버 마비
│   │   ├── Data Interception      → 데이터 도용
│   │   └── Identity Theft         → 신분 도용
│   │
│   └── Internal (내부)
│       ├── Lost/Stolen Devices    → 기기 분실
│       ├── Accidental Misuse      → 직원 실수
│       └── Malicious Employees   → 악의적 내부자
│
└── Security Solutions (보안 솔루션)
    ├── 가정용/소규모
    │   ├── Antivirus & Antispyware → End Device 설치
    │   └── Firewall Filtering      → 무단 접근 차단
    │
    └── 대규모 기업용 (추가)
        ├── Dedicated Firewall → 전용 방화벽 1차 차단
        ├── ACL               → 접근 제어 룰
        ├── IPS               → 침입 탐지·자동 차단
        └── VPN               → 암호화 터널 (가상 사설 망)
```

---

## 배운 점

- 네트워크 보안은 크기에 관계없이 **모든 네트워크에 필수**이며, 보안을 강화하면서도 **QoS를 함께 유지**해야 한다는 균형이 중요하다
- **Zero-day 공격**은 패치가 나오기 전에 이미 공격이 시작된다는 점에서 특히 위험하다
- **내부 위협**은 방화벽으로 막을 수 없는 경우가 많아 외부 위협만큼 심각하게 다뤄야 한다
- 대규모 네트워크에서는 **ACL → Firewall → IPS** 순서로 겹겹이 방어하는 **심층 방어(Defense in Depth)** 전략을 사용한다
- **VPN**은 공용 인터넷에서도 암호화된 터널을 만들어 안전한 통신을 가능하게 한다

---

## 참고 자료

- **Cisco Networking Academy** - Network Security 강의 슬라이드