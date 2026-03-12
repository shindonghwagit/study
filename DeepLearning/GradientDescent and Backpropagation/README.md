# Gradient Descent & BackPropagation

> **Easy 딥러닝** 교재 기반 학습 정리  
> 발표자: 신동화 (순천향대학교)

---

## 학습 목표

- 손실 함수를 최소화하는 최적화 알고리즘인 **경사 하강법(Gradient Descent)** 의 원리를 이해한다
- Batch GD, SGD, Mini-Batch GD 세 가지 변형의 **동작 방식과 장단점**을 비교·설명할 수 있다
- **학습률(Learning Rate)** 과 **가중치 초기화(Weight Initialization)** 가 학습에 미치는 영향을 이해한다
- **역전파(BackPropagation)** 가 Chain Rule을 통해 각 가중치의 기울기를 어떻게 계산하는지 설명할 수 있다

---

## 1. Gradient Descent (경사 하강법)

초기 파라미터 θ에서 시작하여, 손실 함수 $J(\theta)$의 기울기(gradient)를 따라 **반복적으로 θ를 갱신**하며 손실을 줄여나가는 최적화 알고리즘이다.

**가중치 업데이트 수식**

$$
\theta_j := \theta_j - \alpha \frac{\partial J(\theta)}{\partial \theta_j}
$$

| 기호 | 의미 |
|------|------|
| $\theta_j$ | 업데이트 대상 파라미터 (가중치) |
| $\alpha$ | 학습률 (Learning Rate) |
| $\frac{\partial J(\theta)}{\partial \theta_j}$ | 손실 함수의 기울기 (Gradient) |

**핵심**: 기울기의 **반대 방향**으로 학습률만큼 이동하는 것을 반복하여 손실이 최소인 지점을 찾는다.

---

### 1.1 Learning Rate (학습률)

한 번의 업데이트에서 얼마나 이동할지를 결정하는 하이퍼파라미터이다.

| 상황 | 문제 |
|------|------|
| **α가 너무 작을 때** | 수렴 속도가 매우 느림, 학습 시간 과다 |
| **α가 너무 클 때** | 최소점을 지나쳐 발산(overshoot) 가능 |

적절한 학습률을 찾는 것이 안정적인 학습의 핵심이다.

---

### 1.2 Batch Gradient Descent

**전체 학습 데이터**를 모두 사용하여 기울기를 계산하고 θ를 갱신하는 방식이다.

**알고리즘 동작 과정**

1. 가중치를 평균 0, 분산 $\sigma^2$인 정규분포에서 랜덤 초기화
2. **전체 데이터**에 대한 손실의 기울기를 계산
3. 기울기 반대 방향으로 학습률만큼 가중치 갱신
4. 수렴할 때까지 반복

**수식**

$$
\theta := \theta - \alpha \cdot \frac{1}{N} \sum_{i=1}^{N} \nabla_\theta J_i(\theta)
$$

**장점**: 전체 데이터를 보고 업데이트하므로 **안정적으로 수렴**한다.

**문제점**
- 전체 데이터를 매번 계산하므로 대규모 데이터셋에서 **계산 속도가 매우 느리다**
- **Local Minimum에 빠질 수 있다** — 현재 위치에서 내려가는 방향만 보고 이동하기 때문에, 초깃값이 잘못 설정되면 Global Minimum이 아닌 Local Minimum에 수렴한다

---

### 1.3 Weight 초기화 (가중치 초기화)

파라미터의 초깃값이 최소점으로부터 멀리 떨어져 있을수록 **많은 업데이트가 필요**하기 때문에 적절한 초기화가 중요하다.

**부적절한 초기화의 문제 — 안정 조건**

각 층의 출력 분산이 입력 분산과 동일하게 유지되어야 신호가 안정적으로 전파된다. 핵심 조건은 다음과 같다:

$$
n_{in} \cdot \text{Var}(W) \approx 1
$$

| 조건 | 결과 |
|------|------|
| $n_{in} \cdot \text{Var}(W) > 1$ | 활성값/기울기가 층을 거칠수록 **지수적으로 증가** → Exploding |
| $n_{in} \cdot \text{Var}(W) < 1$ | 활성값/기울기가 층을 거칠수록 **지수적으로 감소** → Vanishing |
| $n_{in} \cdot \text{Var}(W) = 1$ | 분산이 층 간에 유지되어 **안정적 학습** 가능 |

> **주의 — 활성화 함수에 따른 차이**: Sigmoid, tanh 같은 포화(saturating) 활성화 함수에서는 가중치가 너무 크면 입력이 포화 영역으로 밀려나 미분값이 0에 가까워지면서 오히려 **Vanishing Gradient**가 발생할 수 있다. 즉, "분산 과대 = 무조건 Exploding"이 아니며 활성화 함수의 특성을 함께 고려해야 한다.

**대표적인 초기화 방법**

| 방법 | 수식 | 적합한 활성화 함수 |
|------|------|-------------------|
| **LeCun 초기화** | $\text{Var}(W) = \dfrac{1}{n_{in}}$ | 일반적 사용, 가우시안 분포 기반 |
| **Xavier 초기화** | $\text{Var}(W) = \dfrac{2}{n_{in} + n_{out}}$ | Sigmoid, tanh |
| **Kaiming(He) 초기화** | $\text{Var}(W) = \dfrac{2}{n_{in}}$ | ReLU |

**공통 원리**: 모든 초기화 방법의 목표는 $n_{in} \cdot \text{Var}(W) \approx 1$을 만족시키는 것이다. 입력 노드 수($n_{in}$)가 클수록 분산을 작게 설정하여, 각 층의 출력 분산이 입력 분산과 동일하게 유지되도록 한다. Kaiming 초기화에서 분자가 2인 이유는 ReLU가 음수 입력을 0으로 만들어 분산이 절반으로 줄어드는 것을 보상하기 위함이다.

---

### 1.4 Stochastic Gradient Descent (SGD)

전체 데이터셋에서 **하나의 데이터**를 랜덤으로 샘플링하여 기울기를 계산하는 방식이다.

**알고리즘 동작 과정**

1. 가중치 랜덤 초기화
2. 단일 데이터 포인트 $i$ 하나를 랜덤 선택
3. 해당 샘플 하나에 대한 gradient 계산
4. 가중치 업데이트
5. 수렴할 때까지 반복

**수식**

$$
\theta := \theta - \alpha \cdot \nabla_\theta J_i(\theta)
$$

**장점**
- 학습 속도가 매우 빠르다
- 잦은 업데이트와 노이즈로 인해 **Local Minimum을 탈출**하여 더 나은 해를 찾을 가능성이 높다

**단점**
- Loss가 좋아졌다 나빠졌다를 반복하는 **불안정한 수렴** 양상을 보인다
- Global Minimum에 근사할 수 있어도 정확히 **수렴하지 못한다**

---

### 1.5 Mini-Batch Gradient Descent

전체 데이터를 **일정 크기(Batch Size)의 미니 배치**로 나누어, 각 배치마다 기울기를 계산하는 방식이다. Batch GD와 SGD의 절충안이다.

**알고리즘 동작 과정**

1. 가중치 랜덤 초기화
2. B개의 데이터로 이루어진 mini-batch 선택
3. 배치의 **평균 기울기** 계산
4. 가중치 업데이트
5. 수렴할 때까지 반복

**수식**

$$
\theta := \theta - \alpha \cdot \frac{1}{B} \sum_{i=1}^{B} \nabla_\theta J_i(\theta)
$$

**특징**: SGD에 비해 노이즈가 적고, Batch GD에 비해 계산이 빠르다. 단, **Batch Size를 적절히 설정**해야 한다.

---

### Gradient Descent 3가지 변형 비교

| 항목 | Batch GD | SGD | Mini-Batch GD |
|------|----------|-----|---------------|
| 데이터 사용량 | 전체 (N개) | 1개 | B개 (미니 배치) |
| 업데이트 빈도 | 1 epoch당 1회 | 1 epoch당 N회 | 1 epoch당 N/B회 |
| 수렴 안정성 | 매우 안정적 | 불안정 (노이즈 큼) | 중간 |
| 계산 속도 | 느림 | 빠름 | 중간 |
| Local Minimum 탈출 | 어려움 | 용이 | 중간 |

---

## 2. BackPropagation (역전파)

출력층에서 입력층 방향으로 **Chain Rule(연쇄 법칙)** 을 적용하여, 각 가중치에 대한 손실 함수의 편미분 값을 계산하고 가중치를 업데이트하는 방식이다.

**목표**: 손실 $L$을 줄이기 위해 각 가중치 $W$가 손실에 얼마나 기여했는지($\frac{\partial L}{\partial W}$)를 구하여 업데이트한다.

---

### 2.1 순전파(Forward Propagation)가 필요한 이유

역전파로 미분을 계산하려면 순전파에서 산출된 **중간 값들이 필요**하다.

**순전파 → 역전파 흐름**

1. **Forward**: 입력 $x$를 넣어 예측값 $\hat{y}$ 계산
2. **Loss**: 예측값과 실제값의 차이인 $L(\hat{y}, y)$ 계산
3. **Backward**: 순전파에서 저장한 중간 값들을 이용해 각 가중치에 대한 미분을 계산

---

### 2.2 Chain Rule (연쇄 법칙)

역전파의 핵심 도구이다. 합성 함수의 미분을 각 단계의 미분의 곱으로 분해한다.

**기본 원리**

$$
\frac{\partial L}{\partial W} = \frac{\partial L}{\partial \hat{y}} \cdot \frac{\partial \hat{y}}{\partial z} \cdot \frac{\partial z}{\partial W}
$$

**2-Layer 네트워크 예시**

입력 → (W1) → 은닉층 → (W2) → 출력 → 손실 $L$ 의 구조를 가정하면:

**W2에 대한 기울기** (출력층에 가까운 가중치)

$$
\frac{\partial L}{\partial W_2} = \frac{\partial L}{\partial \hat{y}} \cdot \frac{\partial \hat{y}}{\partial z_2} \cdot \frac{\partial z_2}{\partial W_2}
$$

**W1에 대한 기울기** (입력층에 가까운 가중치)

$$
\frac{\partial L}{\partial W_1} = \frac{\partial L}{\partial \hat{y}} \cdot \frac{\partial \hat{y}}{\partial z_2} \cdot \frac{\partial z_2}{\partial a_1} \cdot \frac{\partial a_1}{\partial z_1} \cdot \frac{\partial z_1}{\partial W_1}
$$

**핵심 관찰**: 입력층에 가까울수록 Chain이 길어지며, 이것이 **기울기 소실(Vanishing Gradient)** 문제의 원인이 된다. 각 단계의 미분값이 1보다 작으면 곱할수록 기울기가 급격히 줄어들기 때문이다.

---

## 배운 점

- Gradient Descent는 단일 알고리즘이 아니라, Batch → SGD → Mini-Batch로 **문제점을 보완하며 발전**해온 흐름이 있다. 각 변형이 "왜" 필요했는지를 이해하는 것이 핵심이다
- **학습률**과 **가중치 초기화**는 학습의 성패를 좌우하는 중요한 하이퍼파라미터이며, LeCun/Xavier/Kaiming 초기화는 모두 $n_{in}$이 클수록 분산을 줄인다는 **공통 원리**를 공유한다
- BackPropagation은 결국 **Chain Rule의 체계적 적용**이며, 순전파에서 저장한 중간 값을 활용해 효율적으로 기울기를 계산하는 방법이다
- Chain이 깊어질수록 기울기가 소실될 수 있다는 점에서 **가중치 초기화, 활성화 함수 선택, 네트워크 설계**가 모두 연결되어 있음을 체감했다

---

## 참고 자료

- **Easy 딥러닝** (교재)
- 발표 슬라이드: `Gradient_Descent_and_BackPropagation.pptx`