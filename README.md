# PixelPersona: From Photos to Pixel Art with LoRA

[![Typing SVG](https://readme-typing-svg.demolab.com/?lines=my+personal+character)](https://git.io/typing-svg)

## Overview

PixelPersona는 일반 사진을 픽셀 아트 스타일의 나만의 캐릭터로 변환하는 프로젝트입니다.

Pyxelate를 사용해 기본 픽셀 데이터셋을 만들고 baseline 모델을 학습합니다.

이후 Stable Diffusion v1.5 기반 LoRA(Lo-Rank Adaptation)를 적용하여 픽셀화 스타일을 학습합니다.

최종적으로 사용자가 업로드한 사진을 픽셀 아트 스타일 이미지로 변환할 수 있습니다.

## Model Architecture

Base Model: Stable Diffusion v1.5

Fine-tuning: LoRA (Low-Rank Adaptation, rank=4/8 실험)

Pipeline:

1. 텍스트 프롬프트 인코딩 (CLIP)

2. Latent space 변환 (VAE Encoder)

3. UNet + LoRA fine-tuning

4. VAE Decoder → 최종 픽셀 아트 이미지

## Dataset

Source: [CelebA subset-kaggle](https://www.kaggle.com/datasets/jessicali9530/celeba-dataset)

Pixelization: Pyxelate를 활용해 16-color pixel art 데이터셋 생성

Format: PNG, 512×512 정규화

Preprocessing: Resize, CenterCrop, Normalize, Data Augmentation (flip, affine, color jitter 등)
### 예시:

### Original	                    ### Pyxelate (Baseline)

## Training

Environment: Google Colab Pro (T4 / A100 GPU)

Hyperparameters:

learning_rate: 5e-5

batch_size: 2~8

epochs: 3

LoRA rank: 4, 8 (비교 실험)

Optimizer: AdamW

Loss: MSE (noise prediction, diffusion-style loss)

Loss Curve 예시:???

##  Inference
### Text → Image
```ruby
python src/inference.py \
  --prompt "pixel art portrait, 16-color style" \
  --output results/sample_t2i.png
```

### Image → Image (사진 → 픽셀화)
```ruby
python src/inference.py \
  --image data/sample.jpg \
  --prompt "pixel art portrait, 16-color style" \
  --strength 0.65 \
  --output results/sample_i2i.png
```

## Results

Baseline (Pyxelate) vs LoRA 학습 결과 비교

### Input	Pyxelate                  ### 	Pyxelate Baseline	             ###LoRA Output

	
	

평가:

Pyxelate: 단순화된 픽셀 변환, 디테일 손실

LoRA: 디테일 유지 + 픽셀풍 재현, 더 자연스러운 결과

정량 지표(FID) + 주관적 평가 병행


## Installation
```ruby
git clone https://github.com/yourname/PixelPersona.git
cd PixelPersona
pip install -r requirements.txt
```
### 필수 패키지:
torch, diffusers, transformers, accelerate

pyxelate, Pillow, matplotlib

peft (LoRA 지원)

## Roadmap
- 기능 확장 계획
- LoRA 외의 fine-tuning 지원 계획 등

## References
- Pyxelate: [PIXELATE](https://github.com/sedthh/pyxelate)
- LoRA: Low-Rank Adaptation (arXiv:2106.09685)
- HuggingFace Diffusers: https://huggingface.co/docs/diffusers/index
