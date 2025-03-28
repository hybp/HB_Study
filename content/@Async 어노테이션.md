
Q1. private method 에서 동작 하는가
- private method에서 @Async 할 수 없음
- ++ @Async 뿐만 아니라 @Transactional 등 어노테이션 동작 안함
Q2. self-invocation이 가능한가
- 불가능



### 무엇을 하는가?
비동기 작업을 스레드 풀에서 처리하는게 아니라 새로운 스레드를 매번 생성해서 수행


### Spring Boot에서 사용법
1. Application에 @EnableAsync 추가
```java
@SpringBootApplication 
@EnableAsync 
public class Application { 
	public static void main(String[] args) { 
	
		SpringApplication.run(MyApplication.class, args); 
		
	} 
}
```

2. 비동기로 실행할 매서드에 @Async 어노테이션 추가
```java
@Service 
public class YourService { 

	@Async 
	public void asyncMethod() { 
		// 비동기 로직 
	} 
	
	///
}
```

### 주의 할 점
- @Async 메서드는 스레드를 **재사용하지 않는다**
	매번 새로운 스레드 사용
	+스레드가 잘 종료되는지 확인해야 함
	  (커넥션 같은게 계속 유지 되는지)
	  
- private method 안됨 (Annotation 공통 사항)

- self. 안됨 (self-invocation)
	- 같은 class의 @Async 메소드 호출하는거 Async 안됨
	  (inner method)
	![](https://miro.medium.com/v2/resize:fit:1400/1*xGua9KlgSUHVBD6NpA3BCQ.png)
	- @Async는 Bean의 **proxy** 밖에서 동작하는데 proxy 안에 있으면 동기 처리
	  
	- Spring에서 직접 @Async가 붙은 메소드를 Bean을 통해 direct하게 실행해줘야 하는데
	  inner method는 bean을 거치지 않고 실행되기 때문에 (먼저 호출 할 때 부른 existing bean 재활용)

- return 값 void 또는 ```CompletableFuture<>```


### 세부 설정하는법

방법 1. AsyncConfig 사용
```java
@Configuration 
public class AsyncConfig { 
	@Bean 
	public ThreadPoolTaskExecutor taskExecutor() { 
		ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor(); 
		
		executor.setCorePoolSize(10); // 코어 스레드 풀 크기 설정 (최솟값)
		executor.setMaxPoolSize(20); // 최대 스레드 풀 크기 설정 
		executor.setQueueCapacity(500); // 작업 큐 용량 설정 
		executor.setThreadNamePrefix("AsyncThread-"); // 스레드 이름 접두사 설정 
		
		// 작업이 완료된 후 스레드 풀이 종료될 때까지 대기할 시간 설정 (단위: 초) 
		executor.setAwaitTerminationSeconds(60); 
		executor.initialize(); 
		
		return executor; 
	} 
}
```

방법 2. application.yml 사용
```yaml
spring:
  task:
    execution:
      pool:
        core-size: 8
        max-size: 8
```


[[!!!비동기 처리 확인하는법]]

