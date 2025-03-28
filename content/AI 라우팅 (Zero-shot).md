자료: https://www.clova.ai/tech-blog/%EB%A7%A5%EB%9D%BD%EC%9D%84-%EC%9D%B4%ED%95%B4%ED%95%98%EB%8A%94-%EB%98%91%EB%98%91%ED%95%9C-ai-%EB%B6%84%EB%A5%98-%EC%97%94%EC%A7%84-llm-%EB%9D%BC%EC%9A%B0%ED%84%B0

맹점: 질문자의 의도 파악 -> 일을 처리 할 수 있는 툴로 정보 전달

# 1. 기존 NLU 의 한계
## 1.1 Context 이해 능력
원하는 기능을 Direct 하게 말하는게 아닌 context만 설명하면 못알아들음
ex) 환전하고 싶어요 O. 돈 좀 달러로 바꾸고 싶은데.. X.
분류는 가능, 고도의 ==의도 파악==은 어려움
## 1.2 리튜닝 여부
새 카테고리 즉시 추가 불가
추가 학습 ==데이터== 필요

AI 라우팅은 [[Zero-shot (in CV, NLP)]]기반으로 분류를 위해 재학습 불필요
