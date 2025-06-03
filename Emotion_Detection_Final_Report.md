# 감정 인식 딥러닝 프로젝트 최종보고서

---

## 1. 프로젝트 소개

본 프로젝트는 이미지 데이터를 활용하여 사람의 감정을 분류하는 딥러닝 기반 감정 인식 모델을 개발하는 것을 목표로 합니다. 다양한 CNN 구조와 전이학습 모델을 실험하여, 감정 분류의 정확도를 높이고 실제 응용 가능성을 탐색하였습니다.

---

## 2. 주제 선정 이유

감정 인식은 인간-컴퓨터 상호작용, 스마트 기기, 헬스케어 등 다양한 분야에서 활용도가 높습니다. 특히 비대면 환경이 늘어나면서, 표정 기반 감정 인식의 중요성이 커지고 있습니다. 이에 따라, 이미지 기반 감정 분류 모델의 성능을 실험적으로 비교하고자 본 주제를 선정하였습니다.

---

## 3. 데이터셋 소개
- **데이터 출처:** 본 프로젝트에서 사용한 감정 이미지 데이터셋은 Kaggle(https://www.kaggle.com/datasets/ananthu017/emotion-detection-fer)에서 다운로드하였으며, 원 데이터는 International Conference on Machine Learning (ICML 2013)에서 공개된 FER2013 데이터셋입니다.
- **데이터 구성:** 7개 감정 클래스(Angry, Disgust, Fear, Happy, Sad, Surprise, Neutral)
- **이미지 크기:** 64x64 크기의 해상도로 실험
- **데이터 분할:** Train/Validation/Test 세트로 분리
- **클래스 분포 이미지 (Train/Validation/Test 모두 비슷)**
![Class Distribution](class_distribution.png)

---

## 4. 전처리 과정

1. **이미지 리사이즈:** 64x64 크기로 실험
2. **Grayscale 변환:** 컬러와 흑백 이미지 모두 실험
3. **정규화:** 픽셀값 [0,1]로 스케일링
4. **데이터 증강:** RandomFlip, RandomRotation, RandomZoom, RandomContrast, RandomBrightness 등 적용
5. **클래스 분포 시각화 및 데이터 확인:** 클래스별 이미지 수, 샘플 이미지 확인

---

## 5. 모델 구조

### (1) CNN 기반 모델

- **기본 CNN:** Conv2D, MaxPooling2D, Dropout, BatchNormalization, Dense 레이어로 구성된 표준 CNN 모델
- **Stacked CNN:** Conv2D 레이어를 2개씩 쌓아 더 깊은 특징 추출
- **Grayscale/Color 실험:** 입력 채널 수에 따라 구조 조정

### (2) 전이학습 기반 모델
- **EfficientNetB0:** 사전학습 가중치 사용, 상위 레이어만 학습

---

## 6. 레퍼런스 및 개선점

- 기존 연구에서는 단순 CNN, ResNet 등 다양한 구조가 활용됨
- 본 프로젝트에서는 데이터 증강, 정규화, EarlyStopping, ReduceLROnPlateau 등 다양한 Regularization 기법을 적용하여 과적합 방지 및 성능 개선을 시도함
- 전이학습 모델(EfficientNet)과 자체 CNN 구조를 비교하여 실제 성능 차이를 분석

---

## 7. 프로젝트 결과

- **최종 테스트 정확도:**  
  - 기본 CNN(RGB): 약 61%
  - 기본 CNN(Grayscale): 약 60~62%  
  - Stacked CNN(Grayscale): 약 63%
  - EfficientNetB0: 25%
- **학습/검증 Loss 및 Accuracy 곡선, Confusion Matrix 등 시각화 자료**
### 기본 CNN(RGB) 모델 결과
- **혼동 행렬:**  
  ![Confusion Matrix](cnn_rgb_cm.png)

<br>
<br>

- **Loss/Accuracy 곡선:**  
  ![Loss/Accuracy](cnn_rgb.png)

<br>
<br>
<br>
<br>

### 기본 CNN(Grayscale) 모델 결과
- **혼동 행렬:**  
  ![Confusion Matrix](cnn_gray2_cm.png)

<br>
<br>

- **Loss/Accuracy 곡선:**  
  ![Loss/Accuracy](cnn_gray2.png)

<br>
<br>
<br>
<br>

### Stacked CNN(Grayscale) 모델 결과
- **혼동 행렬:**  
  ![Confusion Matrix](stacked_cnn_gray_cm.png)

<br>
<br>

- **Loss/Accuracy 곡선:**  
  ![Loss/Accuracy](stacked_cnn_gray.png)

<br>
<br>

- **주요 성과:**  
  - 데이터 증강 및 정규화가 과적합 방지에 효과적임
  - Happy, Neutral 클래스는 F1 Score가 높게 나왔으나, Fear, Disgust, Surprise 클래스는 F1 Score가 낮게 나타남.
  - 이는 데이터 불균형, 표정의 모호함, 클래스 간 유사성 등으로 인해 발생한 것으로 보임.

---

## 8. 추후 발전 방향

- 더 다양한 전이학습 모델(ResNet, ViT 등) 적용
- 하이퍼파라미터 자동 탐색(AutoML) 및 앙상블 기법 적용
- 실제 환경(웹캠, 실시간 영상 등)에서의 감정 인식 실험
- 데이터셋 확장 및 클래스 불균형 개선
- 표정 외 음성, 텍스트 등 멀티모달 감정 인식 연구로 확장

---