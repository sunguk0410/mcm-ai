# MCM AI Journey — AI

> 고객보다 한발 먼저 취향을 이해하고, 다음 방문까지 기억하는 Interactive Retail Experience
<img width="1920" height="1080" alt="12" src="https://github.com/user-attachments/assets/b76a8c64-bd3b-421e-a465-0646d13ae926" />


MCM HAUS 청담의 오프라인 쇼핑 경험을 개인화하기 위한 **AI Recommendation & Computer Vision 모듈**입니다.

매장 카메라를 통해 고객의 동선과 체류 정보를 수집하고, AR Fitting 과정에서 발생한 상품 선택·피팅·위시리스트 행동을 함께 활용하여 고객 맞춤형 상품을 추천합니다.

## 주요 기능

### Computer Vision

* 카메라 기반 고객 감지 및 Tracking
* 고객의 매장 내 위치 및 이동 경로 분석
* Zone 진입·이탈 및 체류 시간 측정
* Spatial Interaction 기반 고객 행동 분석
* 분석 결과를 Spring Backend로 전달

### Personalized Recommendation

* Zone 체류 데이터 기반 초기 관심도 계산
* 회원 Wishlist 반영
* AR 상품 선택·피팅·찜 행동 반영
* RecRec 기반 Next-item Recommendation
* 고객 행동 발생 시 추천 결과 갱신
* 이미 탐색한 상품을 제외하고 유사 상품 추천

### Avatar Look

* AR Fitting 과정에서 축적된 고객 행동 분석
* 여러 Category의 상품을 조합하여 최종 Look 생성
* Personalized Avatar 생성에 사용할 상품 조합 반환

## AI 흐름

```text
Store Camera
     ↓
Customer Tracking
     ↓
Zone Interaction
     ↓
Spring Backend
     ↓
Zone + Wishlist + AR Interaction
     ↓
AI Recommendation Server
     ↓
RecRec
     ↓
Personalized Recommendation
     ↓
Avatar Look
```

## 기술 스택

| 파트                      | 기술                                       |
| ----------------------- | ---------------------------------------- |
| **AI / Recommendation** | Python, PyTorch, RecRec, FastAPI         |
| **Computer Vision**     | YOLO, OpenCV, MediaPipe                  |
| **Data Processing**     | NumPy, Pandas, Scikit-learn              |
| **Image Processing**    | rembg, Pillow                            |
| **Infra / DevOps**      | Docker, AWS EC2, AWS ECR, GitHub Actions |
| **Integration**         | REST API, Spring Boot                    |

## 실행 방법

### Recommendation Server

```bash
cd mcm-recommendation
pip install -r requirements.txt
uvicorn src.main:app --host 0.0.0.0 --port 8000
```

### Camera

```bash
cd mcm-camera/vision
pip install -r requirements.txt
python main.py
```

## 프로젝트 구조

```text
mcm-ai/
├─ mcm-camera/
│  └─ vision/
│     ├─ main.py
│     ├─ customer_tracker.py
│     ├─ spatial_interaction.py
│     ├─ pickup_detector.py
│     └─ backend_client.py
│
└─ mcm-recommendation/
   ├─ src/
   │  ├─ main.py
   │  ├─ recrec.py
   │  ├─ inference.py
   │  ├─ preference.py
   │  ├─ affinity.py
   │  ├─ contrastive_refresh.py
   │  ├─ avatar_look.py
   │  └─ background_removal.py
   ├─ checkpoints/
   ├─ tests/
   ├─ Dockerfile
   └─ requirements.txt
```

## 서비스 연동

```text
Camera
  ↓
Spring Backend
  ↑
AR Frontend
  ↓
Spring Backend
  ↓
AI Recommendation Server
  ↓
Spring Backend
  ↓
AR Frontend / Digital Closet
```

AI 서버는 추천과 추론에 집중하고, Spring Backend는 고객 세션과 행동 데이터 및 상품 정보를 관리합니다.

## TEAM

| 역할              | 담당       |
| --------------- | -------- |
| Product Manager | 이영서, 김민주 |
| Designer        | 홍지영      |
| Frontend        | 박서연, 조연우 |
| Backend         | 강성욱      |
