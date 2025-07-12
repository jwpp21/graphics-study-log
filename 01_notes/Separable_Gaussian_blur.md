# 🌟 Gaussian blur 정리

## 1. 개념
- 이미지를 부드럽게 만듦
- vs box blur -> 좀 더 원본유지, 선명
- 가우시안 필터의 주요 용도는 이미지의 노이즈를 줄이는 것
- 가중 가우시안 분포를 사용하여 픽셀 값을 평균화함으로써, 필터는 이미지를 효과적으로 흐릿하게 처리하여 고주파 노이즈를 줄임

## 2. 구현 과정
1. 1차원 Gaussian 커널을 생성한다. (예: 5x1 커널, σ = 1.0)
2. 수평 방향으로 블러 → 결과를 버퍼에 저장
3. 수직 방향으로 블러 → 최종 결과 이미지로 저장
4. Separable Kernel을 활용해 2차원 블러를 1차원 연산 2번으로 최적화한다.

## 3. 관련 코드 요약
```cpp
### 수평 blur
const float weights[5] = { 0.0545f, 0.2442f, 0.4026f, 0.2442f, 0.0545f };

#pragma omp parallel for
for (int y = 0; y < height; y++) {
    for (int x = 0; x < width; x++) {
        Vec4 sum = Vec4(0, 0, 0, 0);
        for (int k = -2; k <= 2; ++k) {
            int sampleX = std::clamp(x + k, 0, width - 1);
            sum += pixels[y * width + sampleX] * weights[k + 2];
        }
        pixelsBuffer[y * width + x] = sum;
    }
}
---
### 수직 blur
#pragma omp parallel for
for (int y = 0; y < height; y++) {
    for (int x = 0; x < width; x++) {
        Vec4 sum = Vec4(0, 0, 0, 0);
        for (int k = -2; k <= 2; ++k) {
            int sampleY = std::clamp(y + k, 0, height - 1);
            sum += pixelsBuffer[sampleY * width + x] * weights[k + 2];
        }
        pixels[y * width + x] = sum;
    }
}
### 코드 요약
| 요소             | 설명                           |
| -------------- | ---------------------------- |
| `weights[]`    | 1D 가우시안 커널 (σ ≈ 1.0 기준)      |
| `Vec4`         | RGBA 벡터 (float) 기반 픽셀 데이터    |
| `std::clamp()` | 이미지 경계 처리 (Out-of-bounds 방지) |
| `OpenMP 병렬 처리` | 반복문 병렬화로 성능 향상               |


## 느낀점

Separable Kernel 개념 덕분에 2D 커널 연산을 1D 연산 2번으로 나눌 수 있어 연산량이 크게 줄어든다.

경계 처리 방식(clamping vs zero-padding)에 따라 결과 이미지 품질이 확연히 다름.

커널 크기와 σ 값 조절로 흐림 정도를 정밀하게 조정 가능, 실시간 렌더링에도 적용 가능성을 느낌.

고사양 프로젝트에서는 GPU 쉐이더(HLSL/GLSL)를 활용한 스크린 스페이스 블러 방식으로 확장될 수 있음.

