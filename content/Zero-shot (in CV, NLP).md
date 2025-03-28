자료: https://velog.io/@euisuk-chung/%EC%83%9D%EC%84%B1-AI%EC%9D%98-%ED%95%99%EC%8A%B5-%EB%B0%A9%EC%8B%9D-%EC%A0%9C%EB%A1%9C%EC%83%B7%EC%9B%90%EC%83%B7%ED%93%A8%EC%83%B7-%EB%9F%AC%EB%8B%9D

**목적**: 본적 없는 클래스에 대한 인식
**테스트 방법**: 본적 없는 **class**의 객체 사용

![Few-shot](https://velog.velcdn.com/images/euisuk-chung/post/60dd6da0-8d33-4d7d-9812-c109d5397d3d/image.png)
# 1. N-shot Learning이란
각 클래스에 대해 N개의 예시를 제공하여 학습시키는 방법

# 2. Zero-shot Learning 이란
모델이 학습과정에서 본 적 없는 새 '클래스'를 인식할 수 있도록 하는 학습방법

# 3. 설정 방법
*참고: [[LLM 학습시키기|LLM 학습 과정]]*

# 3.1 ZSL 학습
사용 이유: 분류를 학습시킬 데이터가 없음
접근법: 객체와 그 객체가 속한 클래스의 관계 (속성 / 연결 방식 / 논리) 학습
의사결정 프로세스: input의 속성과 클래스간의 관계를 바탕으로 분류 시도

# 3.1.1 GZSL (Generalized ZSL)
기존에 학습한 클래스에 속할 수도, 속하지 않을 수도 있는 제로샷 문제
난관: 학습한 클래스에 예측이 편향되는 것
**방법론**
	- 핵심: 클래스의 **레이블의 의미**에 대한 기본적인 이해 학습 필요
		- '새' 라는 레이블의 특징으로 -> 하늘을 날 수 있고 부리와 날개를 가지진 중소형 동물이다
			- 이런 느낌
	1. 임베딩 모델 활용하여 특징을 수치화
	2. 클래스 - 레이블을 다이렉트로 학습 시키는게 아니라 Feature/Attribute 기반으로 분류하도록 학습
	3. Multi-modal embedding integration(joint embedding space)
		1. Normalize embeddings of different modalitiies
		2. Project vectors to a shared (higher dimensional) semantic space (a.k.a. Joint embedding space)
		3. Multi-modal classifier를 제작 하는법 (text and image)
			- 같은 학습 데이터를 활용하여 text embedding 모델, image embedding 모델을 각각 학습시킨다


# 3.2 FSL / NSL 학습
사용 이유: 분류를 학습시킬 데이터가 불충분
접근법: 각 Class 당 N 개의 예시를 제공
의사결정 프로세스: 기존 데이터의 메타 학습, 유사도 측정 (RAG) 활용하여 분류 시도

※메타 학습: 학습을 학습하는 방법. 특히 소량의 데이터를 ==효율적으로 학습하는법==을 학습한다. ZSL, OSL, FSL 등에 유용
