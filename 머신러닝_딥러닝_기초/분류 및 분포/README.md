# 📊 분류 작업과 확률 분포 손실 (Classification & Loss)

모델이 내놓은 확률 분포와 실제 정답 사이의 거리를 측정하고 최적화하는 과정을 정리합니다.

---

### 1️⃣ 분류 문제의 두 가지 유형
학습하려는 정답의 선택지 개수에 따라 출력층 설계가 달라집니다.

* **이진 분류 (Binary Classification)**
    * **정의**: 두 가지 상태(Yes/No, 0/1) 중 하나를 예측합니다.
    * **출력**: 보통 2개의 노드를 출력하여 각각의 확률을 구하거나, 1개의 노드에 Sigmoid를 적용합니다.
* **다중 분류 (Multi-class Classification)**
    * **정의**: 세 가지 이상의 카테고리(품종 A, B, C) 중 하나를 예측합니다.
    * **출력**: 클래스 개수만큼 노드를 출력하며, `Softmax`를 통해 전체 합이 1이 되도록 변환합니다.



---

### 2️⃣ 확률 분포를 위한 손실 함수 (Loss Functions)
예측값(확률)이 정답과 얼마나 일치하는지 계산하는 도구입니다.

* **NLLLoss (Negative Log Likelihood Loss)**
    * **특징**: 모델이 정답이라고 예측한 확률에 로그를 취해 오차를 계산합니다.
    * **입력**: 모델의 `LogSoftmax` 결과값과 정답의 **인덱스(번호)**를 입력받습니다.
    * **역할**: "정답 번호에 해당하는 확률을 100%로 끌어올려라!"라고 명령합니다.

* **KL Divergence (Kullback-Leibler Divergence)**
    * **특징**: 두 확률 분포가 얼마나 '다른지' 측정하는 지표입니다.
    * **입력**: 모델의 예측 **분포**와 실제 정답의 **분포(One-hot)**를 모두 입력받습니다.
    * **역할**: "예측한 전체 확률 그래프 모양을 정답 그래프 모양과 똑같이 만들어라!"라고 명령합니다.



---

### 💻 실전 코드 (PyTorch)

붓꽃(Iris) 데이터를 예시로 한 핵심 구현 코드입니다.

```python
import torch
import torch.nn as nn
import torch.nn.functional as F

# 1. 다중 분류에서의 NLLLoss (인덱스 기반)
logits = torch.tensor([[0.1, 1.2, 3.0]]) # 모델 출력
target_idx = torch.tensor([2])           # 정답은 2번 품종
loss_nll = nn.NLLLoss()(F.log_softmax(logits, dim=1), target_idx)

# 2. 다중 분류에서의 KL Divergence (분포 기반)
target_dist = torch.tensor([[0.0, 0.0, 1.0]]) # 정답 분포 (One-hot)
loss_kl = nn.KLDivLoss(reduction='batchmean')(F.log_softmax(logits, dim=1), target_dist)

# 수학적으로 정답이 One-hot인 경우, NLLLoss와 KLDiv는 동일한 결과를 보입니다.
