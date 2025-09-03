# PixelPersona: From Photos to Pixel Art with LoRA

[![Typing SVG](https://readme-typing-svg.demolab.com/?lines=my+personal+character)](https://git.io/typing-svg)

## Overview

PixelPersona는 일반 사진을 픽셀 아트 스타일의 나만의 캐릭터로 변환하는 프로젝트입니다.

Pyxelate를 사용해 기본 픽셀 데이터셋을 만들고 baseline 모델을 학습합니다.

이후 Stable Diffusion v1.5 기반 LoRA(Lo-Rank Adaptation)를 적용하여 픽셀화 스타일을 학습합니다.

최종적으로 사용자가 업로드한 사진을 픽셀 아트 스타일 이미지로 변환할 수 있습니다.

## Model Architecture

### 실험 환경

Base Model: Stable Diffusion v1.5

Fine-tuning: LoRA (Low-Rank Adaptation, rank=4 / 8 실험)

### Pipeline:

1.텍스트 인코딩 (CLIP)
→ 입력 프롬프트를 임베딩 벡터로 변환

2.Latent 변환 (VAE Encoder)
→ 이미지를 잠재 공간(latent space)으로 압축

3.UNet + LoRA Fine-tuning
→ 픽셀화 스타일 학습 (베이스 디테일 유지)

4.VAE Decoder
→ 잠재 공간을 다시 이미지로 복원 → 최종 픽셀 아트 생성

## Dataset

Source: [CelebA subset-kaggle](https://www.kaggle.com/datasets/jessicali9530/celeba-dataset)

Pixelization: Pyxelate를 활용해 16-color pixel art 1000장의 데이터셋 생성
```
pyx = Pyx(factor=6, palette=32)
```
Format: PNG, 512×512 정규화

Preprocessing: Resize, CenterCrop, Normalize, Data Augmentation (flip, affine, color jitter 등)

### 예시:
<img width="614" height="316" alt="Image" src="https://github.com/user-attachments/assets/d1f699d7-8b43-4554-9b8e-17b99d52f238" />

## Training

Environment: Google Colab Pro (T4 / A100 GPU)

-Hyperparameters:

 learning_rate: 5e-5
 
 batch_size: 8
 
 epochs: 3
 
 LoRA rank: 4
 
 Optimizer: AdamW
 
 Loss: MSE (noise prediction, diffusion-style loss)
 <img width="922" height="472" alt="Image" src="https://github.com/user-attachments/assets/e8424295-bae2-476d-a611-7364fd3a624b" />

##  Inference
### Image → Image (사진 → 픽셀화)
```ruby
prompt = "pixel art portrait, 16-color style"
result = pipe(
    prompt=prompt,
    image=init_image,
    strength=0.5,         
    guidance_scale=7.5
).images[0]
```

## Results
<img width="798" height="361" alt="Image" src="https://github.com/user-attachments/assets/12575731-7676-478e-a68f-7579be366890" />


평가:

베이스 모델(SD)은 얼굴, 표정, 손, 옷 주름 등 기본적인 디테일을 이미 학습해 두었음.

LoRA는 이 위에 **픽셀화 스타일(네모칸, 단순화된 색 팔레트)**을 덧입히는 역할만 수행.

따라서 표정과 윤곽은 자연스럽게 유지되면서, 전체가 픽셀 아트 느낌으로 변환됨.


## Installation
```ruby
git clone https://github.com/yourname/PixelPersona.git
cd PixelPersona
pip install -r requirements.txt
```
```ruby
git add requirements.txt
git commit -m "Add requirements.txt"
git push origin main
```

### 필수 패키지:
torch, diffusers, transformers, accelerate
pyxelate, Pillow, matplotlib
peft (LoRA 지원)

## Roadmap
- 웹 페이지 만들어 실전 사용
- LoRA 외의 fine-tuning 지원 계획 

## References
- Pyxelate: [SUPER PIXELATE](https://github.com/sedthh/pyxelate)
- LoRA: Low-Rank Adaptation (arXiv:2106.09685)
- HuggingFace Diffusers: https://huggingface.co/docs/diffusers/index
