**Problem**: 늘어가는 Technical Requirements, Business Logic Complexity

*\*Technical Requirements: 보안, 안정성, 확장성, 시스템 연동 등
예시) DB에 연결하는것; DB에서 transaction을 발생시켜 정보를 업데이트하는 일련의 프로세스 등

\*Business Logic Complexity: 회사가 성장하면서 하는 **일**이 더 커지고 복잡해짐
예시) 새로운 기능 필요, 사업 영역 확장, 지리적 확장 등

**Spring's 철학**: Technical 과 Business를 분리시키고 Technical 공수를 최소화 시키자


**Spring의 3가지 핵심**
- [[IoC & DI]] (제어의 역전 / Dependency Injection)
- AOP (관점 지향 프로그래밍)
- PSA (여러 format에 대한 서비스 추상화, Portable Service Abstraction)

비즈니스 로직의 변경이 발생 했을 때 method 안의 코드를 수정하지 **않는것**을 non-invasive 라고 함
[[PSA]]

예시)  **jdbc's update method**
Pojo:
```java
try { 
    Class.forName("com.mysql.jdbc.Driver"); 
    Connection con = DriverManager.getConnection(serverURL, id, pw);
    con.setAutoCommit(false); // transaction 유지를 위해 AutoCommit false
    
    String sql_1 = "insert into emp(empno, ename, age, deptno, mgr) values(1, '오라클', 22, 0423, 05)"; 
    String sql_2 = "insert into emp(empno, ename, age, deptno, mgr) values(2, 'mysql', 23, 0424, 06)"; 
    
    PreparedStatement pstmt_1 = con.prepareStatement(sql_1);
    pstmt.executeUpdate(); 
    PreparedStatement pstmt_2 = con.prepareStatement(sql_2);
    pstmt.executeUpdate(); 
    
    conn.commit(); 
} catch (ClassNotFoundException e) {
	    System.out.println("드라이버가 존재하지 않습니다"); 
} catch (SQLException e) { 
	e.printStackTrace(); 
	conn.rollback(); // rollback
} finally { 
	pstmt_1.close(); 
	pstmt_2.close(); 
	conn.close(); 
}
```

WIth JDBC:
```java
@Autowired 
private JdbcTemplate jdbcTemplate; 

@Transactional 
public void DBTest() { 
	String sql_1 = "insert into emp(empno, ename, age, deptno, mgr) values(1, '오라클', 22, 0423, 05)"; 
	String sql_2 = "insert into emp(empno, ename, age, deptno, mgr) values(2, 'mysql', 23, 0424, 06)"; 
	
	jdbcTemplate.update(sql_1); 
	jdbcTemplate.update(sql_2); 
}
```




[[영속성 컨텍스트]]
[[Version Updates]]
