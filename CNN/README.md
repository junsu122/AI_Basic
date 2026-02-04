# 🏎️ Vehicle vs ✈️ Airplane Classifier (CNN with Regularization)

이 프로젝트는 **CNN(Convolutional Neural Networks)**을 활용하여 자동차(Automobile)와 비행기(Airplane)를 분류하는 모델을 구현하고, 모델의 성능 향상을 위한 다양한 **과적합 방지(Regularization)** 기법을 적용한 예제입니다.

---

## 1. 프로젝트 개요
본 프로젝트는 이미지 데이터에서 특징(Feature)을 추출하여 물체의 종류를 판별합니다. 특히 조명 변화나 배경 노이즈에 강건한(Robust) 모델을 만들기 위해 **Batch Normalization**과 **Dropout** 등 기계공학적 제어 개념과 유사한 튜닝 기법을 적용하였습니다.



---

## 2. 주요 적용 기술 (Overfitting Tuning)

### ✅ Batch Normalization (배치 정규화)
* **역할:** 각 레이어의 출력값을 일정한 분포로 정규화합니다.
* **효과:** 학습 속도를 높이고 가중치 초기화 의존도를 낮춥니다. 시스템의 진동을 억제하는 **댐퍼(Damper)**와 같은 역할을 수행하여 학습의 안정성을 보장합니다.

### ✅ Dropout (드롭아웃)
* **역할:** 학습 시 무작위로 뉴런의 연결을 해제합니다.
* **효과:** 특정 뉴런에 대한 의존도를 낮추어 모델의 **범용성(Generalization)**을 확보합니다.

### ✅ Data Augmentation (데이터 증강)
* **역할:** 좌우 반전(Horizontal Flip) 등의 변환을 통해 학습 데이터를 풍부하게 만듭니다.
* **효과:** 물체의 기하학적 특징이 변해도 동일한 물체로 인식하는 **불변성(Invariance)**을 학습시킵니다.

---

## 3. 모델 구조 (Architecture)

| 단계 | 레이어 (Layer) | 구성 (Configuration) | 주요 역할 |
| :--- | :--- | :--- | :--- |
| **추출 1** | Convolution | 3x3 Kernel, 32 Filters | 기본적인 형태(Edge, Color) 추출 |
| **안정화** | Batch Norm | 32 Channels | 데이터 분포 정규화 (과적합 방지) |
| **압축** | Max Pooling | 2x2, Stride 2 | 주요 특징 강조 및 연산량 감소 |
| **규제** | Dropout | Rate: 0.3 ~ 0.5 | 뉴런 간 의존성 제거 |
| **판단** | Fully Connected | 256 Nodes | 추출된 특징 기반 최종 분류 |

---

## 4. 학습 및 성능 지표
학습 시 기록된 **Loss(손실)**와 **Accuracy(정확도)** 곡선을 통해 모델의 상태를 진단합니다.



* **Acc vs Val_Acc:** 두 곡선의 간격이 좁을수록 모델이 훈련 데이터를 외우지 않고 실전에 강한 상태임을 의미합니다.
* **Softmax Probability:** 최종 출력단에 Softmax를 적용하여 각 클래스에 대한 예측 확률(신뢰도)을 산출합니다.

---

## 5. 결론 및 고찰
이미지 데이터를 2차원 신호로 간주하고, CNN 필터를 통해 고차원적인 기하학적 형상을 분석하였습니다. 이는 전통적인 모멘트(Moment) 기반의 중심점 추적 방식보다 복잡한 환경에서 훨씬 강력한 성능을 보여줍니다.
