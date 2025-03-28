Inversion of Control (SOLID 설계 원칙), Dependency Injection (디자인 패턴)

"스프링에서 DI 패턴을 사용하여 IoC 원칙을 구현하고 있다."

스프링에서 dependency 가 주입되는 과정

1. DI: 
	- Objects define their dependencies only through constructor arguments, arguments to a factory method, or object properties that are set after the object is constructed (or returned from a factory method

2. IoC Container & Beans
	- Spring's IoC container then injects the dependencies when creating the bean


이렇게 Dependency가 Inject 될 때 (Through Beans and constructors), 제어의 역전이 일어난다
참고: [[의존성과 의존성 주입]]


[[의존성과 의존성 주입]]
