Spring 환경에서 DB는 JDBC로 컨트롤, Entity Object Relational Mapping은 JPA로 한다는 것을 배웠다.

그렇다면 DB의 수정은 어떻게 할까?
Key: **정합성, 무결성이 유지 되어야 한다**
	- 참고: [[데이터 정합성과 무결성]]

Java way: Transaction들 **지연 저장소**에 모아서 한번에 DB 처리

**Transaction**
여러 SQL을 묶어서 실행시키고 성공적으로 수행 되면 DB에 반영, 실패하면 되돌리는 프로세스

예시)
```sql
START TRANSACTION; # 트랜잭션을 시작합니다.

INSERT INTO memo (id, username, contents) VALUES (1,'Robbie', 'Robbie Memo');

INSERT INTO memo (id, username, contents) VALUES (2,'Robbert', 'Robbert Memo');

SELECT * FROM memo;

COMMIT; # 트랜잭션을 커밋합니다.

SELECT * FROM memo;
```

Persistence Context로 관리되는 객체는 지연저장소에서 모아서 마지막에 DB에 commit

관계도
![[Screenshot 2025-03-20 at 12.37.32 AM.png]]

실제 구현은 EntityManager의 EntityTransaction 사용

구현 예
```java
EntityTransaction et = em.getTransaction(); // EntityManager 에서EntityTransaction 을 가져옵니다.

et.begin(); // 트랜잭션을 시작합니다.

try { // DB 작업을 수행합니다.

	Memo memo = new Memo(); // 저장할 Entity 객체를 생성합니다.
	
	memo.setId(1L); // 식별자 값을 넣어줍니다.
	
	memo.setUsername("Robbie");
	
	memo.setContents("영속성 컨텍스트와 트랜잭션 이해하기");
	
	em.persist(memo); // EntityManager 사용하여 memo 객체를 영속성 컨텍스트에 저장합니다.
	
	et.commit(); // 오류가 발생하지 않고 정상적으로 수행되었다면 commit 을 호출합니다.

// commit 이 호출되면서 DB 에 수행한 DB 작업들이 반영됩니다.

} catch (Exception ex) {

	ex.printStackTrace();
	
	et.rollback(); // DB 작업 중 오류 발생 시 rollback 을 호출합니다.
	
	} finally {
	
		em.close(); // 사용한 EntityManager 를 종료합니다.
	
	}
	
	emf.close(); // 사용한 EntityManagerFactory 를 종료합니다.
}
```


### @Transactional 애너테이션
- ```@Transactional``` 해놓은 매서드가 호출되면 매서드 내의 모든 DB 연산이 하나의 트랜잭션으로 묶임.
- Method가 정상 수행되면 commit 하고 예외 발생 시 롤백
-  !!! 조회성 작업에 ```@Transactional(readOnly = true)``` 해놓으면 읽기 작업의 **최적화** 가능 !!!



[[영속성 컨텍스트]]

[[@Async 어노테이션]]
