### 핵심 기능: Providing non-invasive interface for DB - App connection

DB를 바꾸게 되는 경우 JDBC Driver만 MySQL -> PostgreSQL 이런 식으로 바꿔주면 된다
   -대신 DB 개발사에서 드라이버를 만들어서 라이브러리로 제공해야 함 (Maven Repo 등)

### 추가 (JDBC Template): 각종 method 위한 일관된 interface 제공

예시)  DB update method**
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

WIth JDBC Template:
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
(설정은 application.yml에서)


[[데이터 정합성과 무결성]]