# 이정인 포트폴리오

## 1. 감기진료 건수 데이터와 기상청 데이터를 활용한 시간변화에 따른 기후와 감기 관계 분석 (2024.01 - 2024.02)
#### 목적
- 카메라를 통해 화분에서 자라는 식물을 실시간으로 캡처하고 분석하여 식물의 성장도를 파악하고 성장도에 따른 최적 환경을 제공해주는 스마트 화분 제품 개발 
#### 활용 기술
- 인공지능
  * TensorFlow, Keras, NumPy, ImageDataGenerator
- 애플리케이션
  * 리눅스 운영체제, FastApi, Firebase, HTML, Jinja2 
#### 분석 과정
- 시각화를 활용한 EDA 분석
  * 피어슨 상관 관계 계수를 히트맵 시각화 하여 컬럼간의 관계 분석
  * 감기 발생건수에 대한 각 기후데이터의 산점도 시각화를 통한 관계 분석
  * 년도, 월, 일 별 감기 발생건수와 기후 변화의 추이를 선그래프로 시각화 하여 분석 
- 모델을 활용한 회귀 분석
  * 특성 및 타겟 데이터 선정
  * 학습을 위한 특성 데이터 스케일링 전처리
  * 윈도우 슬라이딩 방식으로 10을 시간단위로 묶어 시계열 데이터 구성
  * 시계열 데이터 학습을 위한 keras LSTM 모델 모델링
  * 모델 학습 및 평가
#### 결과
- 월, 요일에 따른 감기 발생건수와 기후데이터가 특정한 패턴이 있음을 확인    
  (그래프 추가)
- 기후 시계열 데이터로 감기 발생건수의 회귀 예측 결과 높은 정확성으로 예측은 어렵지만 전반적인 경향성은 파악 할수 있음   
  * mape : 약 40%
  * R2 스코어 : 약 0.5
  (그래프 추가)


## 2. 비언어적 표현(포즈 및 표정)을 분석하여 소셜 인터랙션을 개선하는 서비스
#### 목적
- 카메라를 통해 포즈 및 표정을 실시간 감지하여 횟수를 카운팅하고, 각 항목별 가중치를 적용하여 소셜 인터렉션에 대한 최종 점수를 산출하는 서비스 개발
#### 활용 데이터
- 포즈 데이터: Mediapipe를 활용하여 33개 랜드마크 좌표 수집
  * 7가지 포즈 라벨: 다리 꼬기, 팔짱 끼기, 머리 넘기기, 턱 만지기, 입 가리고 웃기, 마시기, 먹기
- 표정 데이터: Kaggle ‘FER-2013’ 데이터셋 활용 (약 16만 장 이미지)
  * 7가지 표정 라벨: Happy, Sad, Neutral, Fear, Surprise, Disgust, Angry
- 불필요한 데이터 제거 및 품질 개선 수행
#### 활용 기술
- 인공지능
  * TensorFlow, Keras, OpenCV, NumPy, XGBoost, scikit-learn, ImageDataGenerator
- 디바이스
  * Raspberry Pi + 웹캠 연동
#### 개발 과정
- 얼굴 표정 인식 CNN 모델 개발
  * 약 16만장의 표정 이미지를 수집하고, 라벨별 데이터 개수 조절하여 데이터 불균형 해소
  * OpenCV를 사용하여 이미지 크기 조정, 정규화 등 전처리 작업을 수행
  * TensorFlow와 Keras를 활용하여 CNN 모델을 직접 구축하고 크롭된 표정 이미지의 라벨 분류 학습
- 포즈 인식 XGBoost 모델 개발
  * 이미지크롤링을 통해 약 3800장의 행동 이미지 수집하고, mediapipe를 활용하여 이미지 좌표 추출
  * XGBoost 모델으로 추출좌표의 라벨 분류 학습
- 디바이스 구현
  * 라즈베리파이 서버에서 카메라를 통해 입력된 이미지를 실시간 추론하는 프로세스 구현
#### 결과
- 포즈 인식 모델: XGBoost (Accuracy: 87.03%)
  * 포즈 인식에서 높은 정확도를 보였으며, 실시간 예측 성능이 우수하여 채택
- 표정 인식 모델: CNN (Accuracy: 40.67%)
  * 표정 인식에서는 이미지 기반의 CNN이 더 적합하여 선택
- 입력 데이터: Mediapipe를 통해 포즈 및 표정 좌표 추출
- 출력 데이터: 각 행동 및 표정별 횟수 카운트 → 가중치 반영 후 최종 점수 산출
- 시제품 개발
  * ![image](https://github.com/user-attachments/assets/352abbeb-5a13-408f-b46f-1def11bf87bc)

