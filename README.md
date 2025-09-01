# Persona-Personalized-Avatar-Synthesis-via-LoRA

[![Typing SVG](https://readme-typing-svg.demolab.com/?lines=my+personal+character)](https://git.io/typing-svg)

## 📌 Overview
- 프로젝트 소개
- 핵심 목표 및 사용 기술

## 📁 Project Structure
├── data/ # 학습 및 평가용 데이터
├── models/ # 학습된 LoRA 및 체크포인트
├── results/ # 생성된 이미지 예시
├── src/ # 학습 및 추론 코드
├── docs/ # 세부 문서 (TRAINING.md, DATASET.md 등)
└── README.md
- 디렉토리 및 파일 설명
- 주요 구성 요소

## 🧠 Model Architecture
- **Base Model**: Stable Diffusion v1.5  
- **Fine-tuning**: LoRA (Low-Rank Adaptation)  
- 파이프라인: 텍스트 프롬프트 → 토큰 임베딩 → UNet → 디코더 → 스타일 변환 결과 이미지

## 🖼️ Dataset
- 학습 이미지: 픽셀 아트 (~6,500장), 서양화 인물 그림 (~6,500장)  
- 포맷: PNG, 512×512 정규화  
- 전처리: Resize, Center Crop, Normalize  

## 🧪 Training
- 환경: Google Colab Pro (T4/A100 GPU)  
- 주요 파라미터:  
  - learning_rate: 5e-5  
  - batch_size: 2  
  - max_train_steps: 10,000  
- LoRA rank: 4 / 8 실험  

## 📤 Inference
- 추론 방법 및 실행법
- 이미지 업로드 → 생성까지의 전체 흐름
- 예시 이미지 포함 (Before/After)

## 🧩 Demo / Web UI
- 웹 앱 or 데모 링크
- 사용 방법 안내 (if applicable)

## 💡 Results
- 생성된 캐릭터 예시 이미지
- 다양한 스타일 비교
- 품질 평가 간단 언급 (FID, 주관 평가 등)

## 🧰 Installation
- 필수 패키지
- 설치 및 실행 명령어

## ⚙️ Usage
- 학습 명령어
- 추론 명령어
- 커맨드라인 파라미터 설명

## 🚀 Roadmap
- 기능 확장 계획
- LoRA 외의 fine-tuning 지원 계획 등

##
