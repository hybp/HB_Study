![Few-shot](https://velog.velcdn.com/images/euisuk-chung/post/631d744e-47cc-42f8-95b8-047d976773a6/image.png)
*이해를 위한 도표*

# 1. 사전학습
목적: 일반적인 패턴, 구조, 언어적 특성을 배양
데이터셋 양: Large Corpus
예시: BERT, GPT

# 2. 파인튜닝
목적: 특정 Task, 적은 양의 데이터에 적합하도록 조정
데이터셋 scope: 소량의 Domain focused
예시: 금융 특화 모델, 검색 특화 모델

# 3. 인퍼런스
학습된 모델을 새로운 데이터에 적용시켜 예측하는 단계
(따로 *학습*은 없음)

*※파인튜닝 단계에서 [[Zero-shot (in CV, NLP)|FSL, ZSL]]등을 학습시킬 수 있다*
