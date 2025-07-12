# 💡 Bloom Effect Demo

## 📌 설명
- 밝은 영역 추출 후 Gaussian Blur를 적용하여 Bloom 효과 구현

## 📸 스크린샷


## 📁 구조
bloom-effect-demo/
├── src/
│ ├── main.cpp
│ ├── shader.hlsl
├── assets/
│ └── sample_texture.png
└── README.md

## 🧪 실습 내용 요약
- 색상 Threshold 처리 → 밝기 기준 픽셀 추출
- Gaussian Blur 적용 (5x5 커널)
- 최종 출력: 원본 + 블러이미지 합성

## 📖 배운 점
- 블러 커널의 크기에 따라 효과가 달라짐
- GPU에서 연산하는 흐름이 익숙하지 않아 초기 디버깅에 시간 소요

## 📌 다음 목표
- Bloom 외 다른 후처리 효과 시도해보기
