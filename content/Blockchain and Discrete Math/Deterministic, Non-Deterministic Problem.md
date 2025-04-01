Ref: https://gazelle-and-cs.tistory.com/64

Analogy: 갈림길이 있는 모험에서 보물을 찾을 때
![](https://blog.kakaocdn.net/dn/E5IbY/btqIlwJfrzc/HY4PqO50GKPsUdl0PZehM0/img.png)

Deterministic algorithm : 한번에 한 node를 verify 한 후 움직이면서 보물이 있는지 없는지 확인
- 따라서 Time complexity = number of steps로 deterministic

Non-deterministic algorithm : 분신술을 사용해서 탐험할 수 있음 (병렬적 처리) (with shared memory)
- Time complexity = 병렬 처리를 한 경우 걸리는 시간의 최댓값


## Reduction from Non-Deterministic to Deterministic
분신술의 행위를 정답으로 향하는 "Hint"를 주는 행위로 치환 할 수 있음
*Why? 병렬 처리를 하게 되면 정답으로 향하는 선택지가 무조건 포함이 되기 때문*

- Time complexity = 분기점에서 힌트를 준다면 걸리는 시간의 최댓값


이렇게 힌트를 사용해서 풀 수 있는 문제를 NP 문제라고 함
- NP 의 또 다른 정의로 "Polynomial time 안에 deterministic 하게 verify 할 수 있는 문제"라고 하는게 hint가 주어졌을 때 정답인지 확인하는거랑 같음

이렇게 Non-D 에서 D로 치환 할 수 있는 문제를 NP 문제라고 함


### Why Determinism?

왜 Deterministic 인지 아닌지를 구분 할 필요가 있는가? Deterministic의 장점이 무엇인가?
-> All computers are "Deterministic Turing Machines" that solve deterministic problems for sure.

[[P vs NP Problem]]
