# 🌟 Gaussian blur 정리

## 1. 개념
- 이미지를 부드럽게 만듦
- vs box blur -> 좀 더 원본유지, 선명
- 가우시안 필터의 주요 용도는 이미지의 노이즈를 줄이는 것
- 가중 가우시안 분포를 사용하여 픽셀 값을 평균화함으로써, 필터는 이미지를 효과적으로 흐릿하게 처리하여 고주파 노이즈를 줄임

## 2. 구현 과정
1. 주변 픽셀들의 색을 평균내서 자신의 픽셀 색 변경
2. 


## 3. 관련 코드 요약
```cpp
void Image::GaussianBlur5()
{
	std::vector<Vec4> pixelsBuffer(this->pixels.size());

	/*
	* 참고자료
	* https://en.wikipedia.org/wiki/Gaussian_filter
	* https://followtutorials.com/2013/03/gaussian-blurring-using-separable-kernel-in-c.html
	*/
	const float weights[5] = { 0.0545f, 0.2442f, 0.4026f, 0.2442f, 0.0545f };

	// 가로 방향 (x 방향)
#pragma omp parallel for
	for (int j = 0; j < this->height; j++)
	{
		for (int i = 0; i < this->width; i++)
		{
			// 주변 픽셀들의 색을 평균내어서 (i, j)에 있는 픽셀의 색을 변경
			// this->pixels로부터 읽어온 값들을 평균내어서 pixelsBuffer의 값들을 바꾸기

		}
	}

	// Swap
	std::swap(this->pixels, pixelsBuffer);

	// 세로 방향 (y 방향)
#pragma omp parallel for
	for (int j = 0; j < this->height; j++)
	{
		for (int i = 0; i < this->width; i++)
		{
			// 주변 픽셀들의 색을 평균내어서 (i, j)에 있는 픽셀의 색을 변경
			// this->pixels로부터 읽어온 값들을 평균내어서 pixelsBuffer의 값들을 바꾸기

		}
	}

	// Swap
	std::swap(this->pixels, pixelsBuffer);
}
