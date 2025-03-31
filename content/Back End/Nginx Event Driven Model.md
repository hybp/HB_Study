Master process와 worker processes로 이루어짐

**Master process**: 설정 파일을 읽고, 이에 맞게 worker process 생성
(주로 cpu 코어 갯수만큼 생성 (context switching 최소화))

이런 구조를 event driven model 이라고 함

**Worker process**: 실제 요청 처리

![[Screenshot 2025-03-28 at 2.33.20 PM.png]]

### Worker process
Master 에서 배정해준 listen socket을 통해 client와 연결하고 keep-alive 시간동안 유지
아무 요청 없을 경우 새로운 커넥션 형성

이런 형성, 제거, 새 요청 처리 작업들을 '**이벤트**'라고 한다

worker process는 하나의 스레드로 이벤트 꺼내서 처리


요청들은 OS 커널이 queue 형식으로 worker process에 전달
- queue에 담긴 상태에서 비동기 방식으로 대기

