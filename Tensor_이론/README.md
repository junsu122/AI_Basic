# **머신러닝/딥러닝 WorkFlow**

> 1. **문제 정의 (Problem Definition)**
>    - 목표 설정: 무엇을 예측하거나 분류할 것인가? (예: 개/고양이 분류, 집값 예측)
>    - 유형 결정: 지도 학습(회귀, 분류), 비지도 학습, 강화 학습 중 선택
>
> 2. **데이터 수집 및 준비 (Data Collection)**
>    - 데이터셋 확보 (CSV, SQL, API, 크롤링 등)
>    - 판다스(pandas) 등을 사용하여 데이터를 불러오기
>    - torch 사용을 위한 Tensor 변환
>
> 3. **데이터 전처리 및 탐색 (EDA & Preprocessing)**
>    - EDA(탐색적 데이터 분석): 그래프를 통해 데이터 분포와 상관관계 파악
>    - 결측치 처리: 비어있는 값(NaN)을 평균값/최빈값 등으로 채우거나 삭제
>    - 특성 공학(Feature Engineering): One-hot encoding, Scaling/Normalization
>
> 4. **데이터 분할 (Data Splitting)**
>    - 학습용(Train)과 테스트용(Test) 분리 (보통 7:3 또는 8:2)
>    - `train_test_split` 사용 (Train: `shuffle=True`, Test: `shuffle=False`)
>
> 5. **모델 선택 및 훈련 (Model Selection & Training)**
>    - 적합한 알고리즘 선택 (Decision Tree, Random Forest, CNN 등)
>    - `model.fit(x_train, y_train)`으로 모델 학습
>
> 6. **모델 평가 (Evaluation)**
>    - 평가 지표 확인: Accuracy, Precision, Recall, MSE(회귀) 등
>
> 7. **모델 최적화 및 배포 (Hyperparameter Tuning & Deployment)**
>    - 하이퍼파라미터 튜닝: 학습률, 나무 깊이 등을 조절하여 성능 극대화
