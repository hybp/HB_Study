Persistence Context: Application 단에서 **DB에 저장될** Entity 객체의 수명(생성, 이동, 삭제)을 효율적으로 관리하기 위한 규칙 등 일련의 context

(DB에 저장되지 않을 애는 JPA로 관리되지 않음)

Java에서 persistence와 persistence context -> DB 의 작업을 해주는 라이브러리: **Hibernate**

Java에서 persistence context에 접근해 entity를 관리하는 도구: **EntityManager**

EntityManager를 생성하는 도구: EntityManagerFactory
![[Screenshot 2025-03-19 at 2.47.27 PM.png]]

EntityManagerFactory를 만드려면 DB에 대한 정보 필요 (Persistence에 대한 정보)

/resources/META-INF/ 위치에 persistence.xml 파일에 기록

persistence.xml 예시)
```xml
<?xml version="1.0" encoding="UTF-8"?>
<persistence version="2.2"
		xmlns="http://xmlns.jcp.org/xml/ns/persistence" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/persistence http://xmlns.jcp.org/xml/ns/persistence/persiste
	<persistence-unit name="memo">
		<class>com.sparta.entity.Memo</class>
		<properties>
			<property name="jakarta.persistence.jdbc.driver" value="com.mysql.cj.jdbc.Driver"/>
			<property name="jakarta.persistence.jdbc.user" value="root"/>
			<property name="jakarta.persistence.jdbc.password" value="{비밀번호}"/>
			<property name="jakarta.persistence.jdbc.url" value="jdbc:mysql://localhost:3306/memo"/>
			<property name="hibernate.hbm2ddl.auto" value="create" />
			<property name="hibernate.show_sql" value="true"/>
			<property name="hibernate.format_sql" value="true"/>
			<property name="hibernate.use_sql_comments" value="true"/>
		</properties>
	</persistence-unit>
</persistence>
```


EntityManagerFactory 생성 코드
```java
EntityManagerFactory emf = Persistence.createEntityManagerFactory("Entity Name");
EntityManager em = emf.createEntityManager();
```


[[Transaction (트랜잭션)]]

