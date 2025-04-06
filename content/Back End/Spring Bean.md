Spring은 Bean을 통해 객체를 생성하고 의존되는 객체들의 DI를 구현한다

※ DI 주입 시점: 서버가 실행될 때

Spring IoC: Bean들을 모아둔 컨테이너


## Spring에서 Bean을 사용하는 방법

**Component 표시를 해준다**
```java
@Component
public class MemoService {
    ...
}
```

![[Screenshot 2025-03-18 at 3.50.08 PM.png]]

(Controller, RestController, Service, Repository는 @Component 자동 포함)

## Bean들 IoC Container에 넣는 법

메인 앱.java에
@SppringBootApplication 해놓으면

이 인터페이스는 자동으로
@EnableAutoconfiguration
@ComponentScan 이 달려있어서 하위 폴더 Bean들 (Component들) 다 IoC에 집어넣음


## Bean들 주입 하는법 (의존이 필요한 부분에 DI 하는법)

1. ```@Autowired```
	```java
public class HahaService {
	@Autowired
	private HahaRepository hahaRepository;
}
```

2. Dependency 생성 Method 위치에 ```@Autowired```
```java
public class MemoService {
	
	private final MemoRepository memoRepository;
	
	@Autowired
	public MemoService(MemoRepository memoRepository) {
		this.memoRepository = memorep
	}
}
```

3. ```@RequiredArgsConstructor```
	```java
@RequiredArgsConstructor
public class MemoService {
	private final MemoRepository memoRepository;
}
```


## 같은 type Bean 여러개 등록하는법

The Problem)
```java
// 공통 타입
public interface Food {
	void eat();
}

// Bean 1
@Component
public class Chicken implements Food {

	@Override
	public void eat() {
		// Implementation
	}
	
}

// Bean 2
@Component
public class Pizza implements Food {

	@Override
	public void eat() {
		// Implementation
	}
	
}
```

이 때 강제로
```java
@SpringBootTest
public class BeanTest {
	@Autowired
	Food pizza;
	
	@Autowired
	Food chicken;
}
```

Autowire로 injection 하게되면 ![[Screenshot 2025-03-28 at 12.33.47 PM.png]]
에러 뜬다.

## 해결책 1: @Primary
대표적으로 쓰고싶은 거에 @Primary 해놓는다

## 해결책 2: @Qualifier

@Component 정의
```java
@Component
@Qualifier("pizza")
public class Pizza implements Food {

	@Override
	public void eat() {
		// Implementation
	}

}
```

사용 예
```java
@SpringBootTest
public class BeanTest {

	@Autowired
	@Qualifier("pizza")
	Food pizza;
}
```

[[Spring Bean vs Static Singleton]]
