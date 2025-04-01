Java Persistence API

JDBC보다 더 상위개념

JDBC는 Non-invasive interface for DB

JPA는 Spring Entity의 객체와 DB Table을 Mapping 해주는 ORM(Object Relational Mapping) 도구의 Interface (명세서)

예시)![[Screenshot 2025-03-19 at 2.32.17 PM.png]]

![[Screenshot 2025-03-19 at 2.31.53 PM.png]]

## Managing Entity Data with DB **without JPA** (but with JDBC only)

Target Entity
```java
public class Memo {

private Long id;

private String username;

private String contents;

}
```

Process
1. Create DB
```sql
create table memo (
	id bigint not null auto_increment,
	 contents varchar(500) not null,
	 username varchar(255) not null,
	 primary key (id)
);
```
2. Write SQL codes and execute using JDBC
```java
String sql = "INSERT INTO memo (username, contents) VALUES (?, ?)";

String sql = "SELECT * FROM memo";
```

```java
jdbcTemplate.update(sql, "Robbie", "오늘 하루도 화이팅~");

jdbcTemplate.query(sql, ...);
```

3. Create entities based on the sql results
```java
@Override
public MemoResponseDto mapRow(ResultSet rs, int rowNum) throws SQLException {
	// SQL 의 결과로 받아온 Memo 데이터들을 MemoResponseDto 타입으로 변환해줄 메서드
	Long id = rs.getLong("id");
	String username = rs.getString("username");
	String contents = rs.getString("contents");
	
	return new MemoResponseDto(id, username, contents);

}
```

## Hibernate

JDBC interafce가 DB 개발사가 제작한 JDBC Driver에 의해 구현되듯이
JPA interface를 구현한 유명한 product : **Hibernate**

### 사용 방법

1. build.gradle에 Hibernate 추가

```groovy
implementation 'org.hibernate:hibernate-core:6.1.7.Final'

implementation 'mysql:mysql-connector-java:8.0.28'
```

2. Annotation 사용
```java
@Entity
public class Haha {
	@Id
	private Long id;
	
	@Column(name = "username", nullable = false, unique = true)
	private String username;
	///
	
}
```
	
	@Entity로 해놓으면 JPA가 관리하게됨
	
	@Entity, @Id, @Column 등 annotation으로 각종 configuration 설정

[[Persistence (영속성)]]


[[JPA Entity Relationships]]
