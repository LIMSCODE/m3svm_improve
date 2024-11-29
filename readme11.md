QMS와 LEM: FashionMNIST 분류 모델
이 저장소는 QMS(Quadratic Multiform Separation) 모델과 **LEM(Loyalty Extraction Machine)**을 구현하여 FashionMNIST 데이터셋에 적용한 결과를 제공합니다. 또한 논문의 실험 결과와 재현된 결과를 비교하여 기록하였습니다.

1. QMS 모델
QMS 모델은 입력 데이터를 이차 함수와 선형 함수로 처리하여 점수를 계산하는 구조입니다.
이는 이차 다항식 분리를 기반으로 분류하는 논문의 핵심 아이디어를 반영한 것입니다.

2. LEM (Loyalty Extraction Machine)
LEM은 데이터 샘플의 예측 신뢰도를 평가하여 아래 세 가지 그룹으로 구분합니다:

강한 충성도(Strong Loyalty): 높은 신뢰도를 가진 샘플 (예: 확률 > 80%).
약한 충성도(Weak Loyalty): 낮은 신뢰도를 가진 샘플 (예: 확률 < 50%).
일반 충성도(Normal Loyalty): 두 범위 사이에 속하는 샘플.
LEM의 활용:
강한 충성도 샘플은 높은 예측 정확도를 보여, 빠르고 신뢰할 수 있는 분류가 가능합니다.
약한 충성도 샘플은 성능이 떨어지므로, 더 높은 해상도의 데이터 또는 추가 레이블 정보를 통해 보완할 수 있습니다.
3. 논문 실험 결과
논문에서는 QMS와 LEM을 FashionMNIST 데이터셋에 적용하여 아래와 같은 결과를 얻었습니다:

테스트 정확도(Test Accuracy): 88.63%
강한 충성도 샘플: 테스트 데이터의 약 69.67%, 예측 정확도 99.82%.
약한 충성도 샘플: 약 7.34%, 예측 정확도 51.09%.
일반 충성도 샘플: 약 22.99%, 예측 정확도 73.90%.
해석:
강한 충성도 샘플은 높은 정확도를 유지하며 모델의 신뢰성을 강조합니다.
약한 충성도 샘플은 성능이 떨어지므로, 추가적인 처리 필요성을 언급합니다.
4. 재현 결과
본 구현에서는 논문을 바탕으로 QMS와 LEM을 적용한 실험을 재현하였고, 결과적으로 92.25%의 테스트 정확도를 기록하며 논문 결과(88.63%)보다 높은 성능을 보였습니다.

학습 및 테스트 결과:
초기 학습 (QMS 모델만 사용):
plaintext
코드 복사
Epoch 1, Training Accuracy: 79.47%
Epoch 2, Training Accuracy: 84.06%
Epoch 3, Training Accuracy: 85.32%
Epoch 4, Training Accuracy: 86.52%
Epoch 5, Training Accuracy: 86.92%
Initial Test Accuracy: 84.06%
LEM 적용 후 재학습:
plaintext
코드 복사
Filtered Data: 10000 samples (Strong + Normal Loyalty)
Re-training model with filtered data...
Epoch 1, Filtered Training Accuracy: 83.20%
Epoch 2, Filtered Training Accuracy: 85.36%
Epoch 3, Filtered Training Accuracy: 87.36%
Epoch 4, Filtered Training Accuracy: 87.71%
Epoch 5, Filtered Training Accuracy: 88.44%
Test Accuracy After Re-training with Filtered Data: 92.25%
5. 주요 결론
QMS 모델은 FashionMNIST 데이터에서 높은 정확도를 기록하며, 특히 강한 충성도 샘플에서 높은 신뢰성을 보였습니다.
LEM 적용을 통해 약한 충성도 샘플을 제거하고, 강한 및 일반 충성도 샘플만으로 재학습하여 모델 성능을 크게 향상시켰습니다.
재현 실험에서 92.25%의 테스트 정확도를 달성하여, 논문 결과(88.63%)를 초과하는 성능을 보였습니다.
