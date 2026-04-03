# Network Components (네트워크 구성요소)

---

## 학습 목표

- **End Device**의 개념과 데이터 흐름에서의 역할을 설명할 수 있다
- **Intermediary Device**의 종류와 각각의 기능을 구분할 수 있다
- **Host Roles**에서 Client와 Server의 차이, 그리고 서버의 종류를 설명할 수 있다
- **Peer-to-Peer** 네트워크의 구조와 장단점을 비교할 수 있다
- **Network Media** 3가지 유형의 전송 방식 차이를 설명할 수 있다

---

## 1. End Devices (종단 장치)

**End Device**란 메시지가 **시작되거나 도착하는** 장치를 의미한다.

> 데이터는 End Device에서 출발 → 네트워크를 통해 흐름 → 다른 End Device에 도달

- 예시: PC, 노트북, IP 전화기, 서버, 프린터 등

### 네트워크 흐름 구조

```
[LAN - 출발지]  →  [Internetwork - 중간 경로]  →  [LAN - 도착지]
  (End Device)         (라우터들의 연결망)             (End Device)
```

> 메시지는 중간 네트워크에서 **대체 경로(alternate routes)** 를 선택할 수 있어,
> 특정 경로에 장애가 생겨도 우회 전송이 가능하다.

---

## 2. Intermediary Network Devices (중간 네트워크 장치)

**Intermediary Device**란 종단 장치들을 **서로 연결**해주는 중간 장비이다.

### 주요 역할

- **신호 재생성 및 재전송**: 약해진 신호를 증폭해 다음 장치로 전달
- **경로 정보 유지**: 네트워크 내 존재하는 경로를 파악하고 관리
- **오류/장애 알림**: 통신 문제 발생 시 다른 장치에 통보

### 장치 종류

| 장치 | 설명 |
|------|------|
| **Wireless Router** (무선 라우터) | Wi-Fi 신호 제공 + 라우팅 기능 |
| **LAN Switch** (스위치) | 같은 LAN 내 장치들을 연결 |
| **Router** (라우터) | 서로 다른 네트워크 간의 경로 결정 |
| **Multilayer Switch** (멀티레이어 스위치) | 스위치 + 라우터 기능을 동시에 수행 |
| **Firewall Appliance** (방화벽) | 보안 정책에 따라 트래픽 허용/차단 |

---

## 3. Host Roles (호스트 역할)

네트워크에 연결된 모든 컴퓨터는 **Host** 또는 **End Device**라고 부른다.

### Server (서버)

End Device에 **정보를 제공**하는 컴퓨터

| 서버 종류 | 설명 |
|-----------|------|
| **Email Server** | 이메일 서버 소프트웨어를 실행, 클라이언트는 이메일 앱으로 접근 |
| **Web Server** | 웹 서버 소프트웨어를 실행, 클라이언트는 브라우저로 접근 |
| **File Server** | 기업 및 사용자 파일 저장, 클라이언트 장치가 파일에 접근 |

### Client (클라이언트)

서버에 **요청을 보내 정보를 가져오는** 컴퓨터

- 웹 서버로부터 웹 페이지 요청
- 이메일 서버로부터 이메일 수신

### 요청-응답 구조

```
[Client]  →  요청(Request)  →  [Server]
[Client]  ←  응답(Response) ←  [Server]
```

---

## 4. Peer-to-Peer (P2P) 네트워크

**P2P 네트워크**에서는 하나의 장치가 **클라이언트이자 서버** 역할을 동시에 수행할 수 있다.

>  매우 소규모 네트워크에서만 권장되는 구조

```
[프린터] ── [PC A: "프린터 공유 가능"]    [PC B: "파일 공유 가능"]
               ↕ 클라이언트 & 서버              ↕ 클라이언트 & 서버
```

### 장단점 비교

| 장점 (Advantages) | 단점 (Disadvantages) |
|-------------------|----------------------|
| 설치 및 구성이 쉬움 (Easy to set up) | 중앙 집중식 관리 불가 (No centralized administration) |
| 구조가 단순함 (Less complex) | 보안이 취약함 (Not as secure) |
| 비용이 낮음 (Lower cost) | 확장성이 낮음 (Not scalable) |
| 파일 전송, 프린터 공유 등 간단한 작업에 적합 | 성능이 느릴 수 있음 (Slower performance) |

---

## 5. Network Media (네트워크 미디어)

네트워크에서의 통신은 **미디어(Media)** 를 통해 전달된다.
미디어는 메시지를 출발지(source)에서 목적지(destination)까지 운반하는 **전송 매체**이다.

### 미디어 종류

| 미디어 유형 | 전송 방식 | 예시 |
|-------------|-----------|------|
| **Metal wires within cables** (구리선) | 전기 신호 (Electrical impulses) | UTP 케이블, 이더넷 케이블 |
| **Glass or plastic fibers within cables** (광섬유) | 빛의 펄스 (Pulses of light) | 광케이블 (Fiber-optic cable) |
| **Wireless transmission** (무선) | 전자기파의 특정 주파수 변조 (Modulation of electromagnetic waves) | Wi-Fi, 무선 IP 카메라 |

### 1) Copper (구리선)

- **전기 신호** 방식으로 데이터 전송
- 가장 보편적이고 저렴한 유선 매체
- 거리 제한 존재 & 전자기 간섭(EMI)에 취약
- 일반 가정/사무실 LAN 환경에 주로 사용

### 2) Fiber-optic (광섬유)

- **빛(광 펄스)** 방식으로 데이터 전송
- 고속·장거리 전송에 최적 (EMI 영향 없음)
- 구리선보다 비용이 높고 설치가 복잡
- 데이터센터, ISP 백본 망, 건물 간 연결에 사용

### 3) Wireless (무선)

- **전자기파(특정 주파수 변조)** 방식으로 데이터 전송
- 케이블 없이 이동하면서도 네트워크 접속 가능
- 보안 취약 & 장애물/간섭에 민감
- Wi-Fi, 무선 IP 카메라, 모바일 네트워크 등에 사용


### 미디어별 특성 한눈에 비교

```
구리선 (Copper)
  ├── 전송 방식: 전기 신호
  ├── 장점: 저렴, 설치 쉬움
  └── 단점: 거리 제한, EMI 취약

광섬유 (Fiber-optic)
  ├── 전송 방식: 빛(광 펄스)
  ├── 장점: 초고속, 장거리, EMI 없음
  └── 단점: 고비용, 복잡한 설치

무선 (Wireless)
  ├── 전송 방식: 전자기파
  ├── 장점: 이동성, 케이블 불필요
  └── 단점: 보안 취약, 간섭·장애물에 민감
```

> 실제 네트워크에서는 세 가지 미디어를 **상황에 맞게 혼합**하여 사용한다.
> 예: 건물 내부 → 구리선 / 건물 간 연결 → 광섬유 / 모바일 기기 → 무선

---

## 전체 개념 요약

```
네트워크 구성요소
├── End Devices (종단 장치)            → 데이터의 출발점 & 도착점
│
├── Intermediary Devices (중간 장치)   → 데이터 전달 & 경로 관리
│   ├── Wireless Router
│   ├── LAN Switch
│   ├── Router
│   ├── Multilayer Switch
│   └── Firewall Appliance
│
├── Host Roles (호스트 역할)
│   ├── Server → 정보 제공 (Email / Web / File)
│   ├── Client → 정보 요청
│   └── P2P    → 클라이언트 + 서버 동시 수행 (소규모 전용)
│
└── Network Media (전송 매체)
    ├── 구리선  → 전기 신호
    ├── 광섬유  → 빛 신호
    └── 무선    → 전자기파
```

---

## 배운 점

- 네트워크는 단순히 "연결"이 아니라, **장치-역할-매체**가 유기적으로 맞물린 구조임을 이해하게 되었다
- End Device와 Intermediary Device의 구분은, 데이터가 어디서 **생성/소비**되고 어디서 **중계**되는지를 명확히 한다
- P2P vs Client-Server 구조 비교를 통해, **규모와 보안 요구사항**에 따라 네트워크 설계가 달라짐을 알았다
- Network Media는 전송 환경(거리, 비용, 이동성)에 따라 적합한 매체를 선택해야 하며, 실제로는 세 가지를 혼합해서 사용한다

---