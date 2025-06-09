# 딥러닝을 활용한 반려동물 안구 질환 예측 AI
AI for Predicting Ocular Health in Pets using Deep Learning

본 프로젝트는 AI Hub의 반려동물 안구 이미지 데이터를 기반으로, 결막염과 유루증 여부를 자동으로 분류하는 딥러닝 모델을 개발합니다.  
ResNet-18 기반 CNN과 Grad-CAM 시각화 기법을 통해 설명 가능한 AI를 구현하였으며, 실제 보호자용 자가 진단 서비스로의 활용 가능성까지 고려하였습니다.

## 프로젝트 개요

- 대상 질환: 결막염(Conjunctivitis), 유루증(Tear Stain Disorder)
- 주요 기능:
  - 이미지 기반 질환 자동 예측
  - Grad-CAM 기반 예측 근거 시각화
  - 보호자 사용을 고려한 경량 구조 설계
- 기술 스택: PyTorch, Fastai, ResNet-18, Google Colab, Grad-CAM

## 데이터 구성

- 출처: [AI Hub 반려동물 안구 질환 이미지](https://www.aihub.or.kr/aihubdata/data/view.do?dataSetSn=562)
- 샘플 수: 클래스별 300장씩 총 600장 사용
- 전처리: 이미지 리사이즈(224x224), 증강, RGB 정규화, 이상치 제거

## 모델 구조 및 학습

- Backbone: ResNet-18 (pretrained)
- 손실 함수: CrossEntropyLoss
- 옵티마이저: Adam
- 학습 방식: fit_one_cycle() (fastai)
- 출력: Softmax 확률 기반 클래스 분류

## 예측 성능 요약

| 항목         | 내용                              |
|--------------|-----------------------------------|
| 전체 정확도   | 약 91.3%                          |
| 결막염 인식   | 충혈, 백태, 혼탁 부위에 높은 집중 |
| 유루증 인식   | 눈물자국, 습기 부위에 주목       |
| 정상 인식     | 맑고 균일한 구조 기반 판단        |

## 질환별 예시 및 Grad-CAM 시각화

### 결막염 안구 이미지

아래 이미지는 결막염 유무(Positive/Negative)에 따른 반려동물의 안구 상태를 비교한 예시입니다.  
Positive 클래스에서는 충혈, 백태, 혼탁 등 결막염의 특징이 시각적으로 뚜렷하게 나타나며,  
Negative 클래스는 맑고 윤기 있는 각막 구조를 보입니다.

![결막염 이미지 예시](https://github.com/eunju429/pet-ocular-disease-ai/blob/main/sample-eyes.png?raw=true)

### 결막염 이미지에 대한 Grad-CAM 시각화

아래 이미지는 결막염 안구에 대한 Grad-CAM 히트맵입니다.  
딥러닝 모델이 예측 시 주목한 영역을 시각적으로 나타내며, 붉은 계열은 높은 주목도를 의미합니다.

![결막염 Grad-CAM 히트맵](https://github.com/eunju429/pet-ocular-disease-ai/blob/main/heatmap.png?raw=true)

### 결막염 원본 vs Grad-CAM 결과 비교

원본 이미지와 Grad-CAM 결과를 나란히 비교하여,  
모델이 충혈, 백태, 혼탁 등 실제 질환 부위에 주목하고 있음을 확인할 수 있습니다.

![결막염 Overlay](https://github.com/eunju429/pet-ocular-disease-ai/blob/main/Grad-CAM1.png?raw=true)

---

### 유루증 안구 이미지

Positive는 눈 주변의 습기, 눈물자국, 갈색 착색이 관찰되며,  
Negative는 눈 주변이 건조하고 깔끔한 상태를 보입니다.

![유루증 이미지 예시](https://github.com/eunju429/pet-ocular-disease-ai/blob/main/sample-eyes1.png?raw=true)

### 유루증 이미지 Grad-CAM 시각화

Grad-CAM 결과를 통해 모델이 눈 주변의 습기, 눈물자국 등에 주목했음을 확인할 수 있습니다.

![유루증 Grad-CAM 결과](https://github.com/eunju429/pet-ocular-disease-ai/blob/main/Grad-CAM3.png?raw=true)

### 정상 안구 Grad-CAM 시각화

유루증이 없는 정상 이미지에 대한 Grad-CAM 결과입니다.  
주목 영역이 전체적으로 약하며, 명확한 질환 징후가 없음을 잘 반영하고 있습니다.

![정상 유루증 Grad-CAM 결과](https://github.com/eunju429/pet-ocular-disease-ai/blob/main/Grad-CAM2.png?raw=true)

---

## 전체 개발 흐름도

### 예측 모델 개발 전체 흐름

데이터 수집부터 전처리, 학습, 예측, 시각화, 해석까지의 전체 흐름을 요약한 다이어그램입니다.

![전체 모델 구조도](https://github.com/eunju429/pet-ocular-disease-ai/blob/main/flowchart.png?raw=true)

### 모델 학습 및 해석 세부 구조

각 처리 단계(전처리, 학습, 시각화)의 내부 절차를 세부적으로 표현한 흐름도입니다.

![세부 학습 구조도](https://github.com/eunju429/pet-ocular-disease-ai/blob/main/flowchart2.png?raw=true)

---

## 서비스 활용 방안

- 모바일 기반 자가진단 애플리케이션
- 동물병원 진료 보조 시스템
- 농촌·도서 지역 비대면 진단 플랫폼
- 반려동물 건강 모니터링 및 보험 연계 서비스

## 향후 고려사항

- 다양한 촬영 조건에 대한 일반화 성능 확보 필요
- 실제 사용자 이미지 기반 추가 학습 필요
- Grad-CAM 시각화와 전문가 판단 일치 여부 검증
- 결과 해석을 위한 안내 문구(예: "전문 진단 권장") 도입 필요
