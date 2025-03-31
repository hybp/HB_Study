Blocking I/O vs Non-blocking I/O

톰캣 8.0부터 NIO가 기본 채택

BIO는 deprecate 됐음

### About BIO Connector
자바의 I/O 사용
BIO는 연결을 받고 처리하는 동안 thread를 계속 사용
(동시성 Lock 같이)

### About NIO Connector
NIO 는 I/O가 아닌 Http11NioProtocol tkdyd
**Poller**라는 별도의 스레드가 Socket들의 커넥션 관리
- Socket들을 캐시로 들고 있다가 해당 socket의 data에 대한 처리가 가능한 순간에 thread 할당


참고: [[Connection 이란]]
