# 🛡️ Voice Phishing Detection System
### BERT 기반 보이스피싱 탐지 및 근절을 위한 통합 대응 체계 구축 프로젝트

> **“지능화·고도화되는 보이스피싱 범죄에 대응하기 위해  
딥러닝 기반 자연어 처리 기술을 활용한 실시간 탐지 및 예방 시스템을 구축한다.”**
>
> *An intelligent voice phishing prevention system leveraging BERT-based NLP models  
to protect personal financial assets and minimize social damage.*

---

## 📌 Project Overview (프로젝트 개요)

본 프로젝트는 기술 발전과 함께 점점 정교해지는 **보이스피싱 범죄**에 효과적으로 대응하기 위한  
**지능형 보이스피싱 탐지 시스템** 구축을 목표로 한다.

특히, 딥러닝 기반 자연어 처리 모델인 **BERT(KoBERT)** 를 활용하여  
음성 통화에서 추출된 텍스트(STT)를 분석하고,  
보이스피싱 여부를 **정밀 분류**함으로써 **실시간 대응이 가능한 예방 체계**를 구현하고자 한다.

이를 통해 개인의 금융 자산 보호는 물론,  
보이스피싱으로 인한 **사회적·경제적 피해를 최소화**하는 데 기여하는 것을 목표로 한다.

---

## 📊 System Flowchart (시스템 흐름도)

<p align="center">
  <img src="./flowchart_real.png" width="60%">
</p>

---

## 📂 Data Composition & Challenges (데이터 구성 및 문제점)

### 🔹 데이터 구성
- **보이스피싱 데이터**
  - 금융감독원 공개 데이터 활용
  - 총 **546건**의 실제 보이스피싱 대화 데이터
- **일반 통화 데이터**
  - 일반 대화 데이터 **20,000건**
- CSV 형식 구성
  - `comment`: 통화 내용 텍스트
  - `label`: 보이스피싱(1) / 정상 통화(0)

### 🔹 문제점
- 공개된 보이스피싱 데이터의 **절대적 부족**
- 특정 유형(금융기관·수사기관 사칭)에 데이터 편중
- 모델 학습 시 **과적합(overfitting)** 발생 가능성

---

## 🧠 Problem Solving Strategy (문제 해결 전략)

### 1️⃣ 데이터 증강(Data Augmentation)
논문  
> *“Easy Data Augmentation Techniques for Boosting Performance on Text Classification Tasks”*  
의 아이디어를 기반으로 텍스트 증강 기법 적용

- **RD (Random Deletion)**
- **RS (Random Swap)**
- **GPT 기반 시나리오 생성**
  - 기존 데이터의 문맥을 유지한 추가 시나리오 생성
  - 전체 학습 데이터의 약 **10% 추가**

📈 결과  
- 보이스피싱 데이터  
  - **546건 → 1,482건**
- Validation loss 감소
- 과적합 현상 완화 확인

---

## 🏗️ System Architecture (시스템 설계)

### 🔹 전체 구조
- **Android Application**
  - 통화 음성 수집
  - STT(Speech-to-Text) 처리
  - 탐지 결과 시각화
  - 푸시 알림 및 진동 경고 제공

- **Backend Server**
  - **Spring Boot**
    - 사용자 정보 관리
    - 통화 기록 저장
    - FastAPI와 연동
  - **FastAPI**
    - KoBERT 기반 딥러닝 모델 추론
    - 보이스피싱 확률 반환

---

## 🤖 AI Model Design (인공지능 모델 설계)

### 🔹 모델 파이프라인
1. 음성 → STT 변환
2. 텍스트 입력
3. **KoBERT Tokenizer**를 통한 인코딩
4. **KoBERT Encoder**
5. **BiLSTM Layer**
   - 문맥 정보 강화
6. **Dense Layer + Sigmoid**
   - 보이스피싱 확률 출력

---

## 📊 Classifier Comparison (분류기 비교)

- 다양한 분류 모델 성능 비교 수행
- 데이터 증강 적용 전·후 성능 비교
- KoBERT + BiLSTM 구조가
  - 정확도
  - 안정성
  - 일반화 성능 측면에서 우수함을 확인

---

## 📱 Application Design (앱 설계)

- 실시간 탐지 결과 표시
- 보이스피싱 의심 시
  - **푸시 알림**
  - **진동 경고**
- 사용자가 즉각 인지하고 통화를 종료할 수 있도록 UX 설계

---

## ✅ Execution Results (실행 결과)

- 보이스피싱/정상 통화 분류 결과 시각화
- 실제 시나리오 기반 테스트에서
  - 높은 탐지 정확도 확인
- 사용자 관점에서 직관적인 경고 전달 가능

---

## 🚀 Future Work (향후 계획)

### 🔹 데이터 측면
- 실제 사용자 동의 기반 통화 데이터 확보
- 다양한 보이스피싱 유형 추가
  - 가족 사칭
  - 납치 협박
  - 로맨스 스캠 등

### 🔹 서비스 측면
- 통화 **중 실시간 탐지 기능** 고도화
- 경고 UX 개선 및 판단 근거 제공
- 사용자 피드백 기반 모델 개선 루프 구축

### 🔹 확장 계획
- Android → **iOS 확장**
- **Web API 제공**
  - 기업·기관 대상 서비스화 가능성 검토

---

## 👥 Team Information

**Capstone Design Project**  
TEAM _별이삼샾_

- 류성욱 (Team Leader)
- 어준석
- 김강환
- 김유찬
- 김의성

---

## 📞 Contact

- **Project Maintainer**: [kkhwan0822-collab](https://github.com/kkhwan0822-collab)
- **Issues & Collaboration**: GitHub Issues를 통해 문의 바랍니다.
