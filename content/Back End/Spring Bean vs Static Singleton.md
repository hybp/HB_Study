처음 Bean의 개념을 접했을 때, 
> [!quote]다른 클래스에서 접근할 수 있게 dependency를 주입해주는거면 ```static``` 으로 접근성을 제공해줘도 되지 않나?

라는 생각이 들어서 조사를 해봤다.

미리 내리는 결론: 
- Status, dependency에 따라 기능이 바뀌면 Bean (e.g. 환율, 외부 API)
- Util성 으로 언제, 어디서든 같은 기능을 제공하면 Static (e.g. 수학 덧셈, 수학 절댓값)

static은 학부시절 OOP 수업에서 한번 배웠지만 여기에 다시 한번 정리하기로 한다
## static
### Where is it stored?
![[img1.daumcdn.png]]

static은 프로그램이 시작할 때 **Method Area**에 할당되고 프로그램이 종료될 때 해제된다.

(*\*Method Area is shared by **all threads** and stores : classes, interfaces, statics, methods, constants, variables)

Bean은 Spring의 ApplicationContext (Spring IoC container)에 의해 관리되며 Heap Area에 저장되고 주입된다.


### Why not good for state dependent methods?
static method는 프로그램이 시작할 때 메모리에 할당되기 때문에 class 내에서 같이 static으로 선언된 변수가 아니라면 static method에서 의존해서 사용할 수 없다. Dependency를 받을 수 없다.
-> 그래서 어느 시점, 공간에서도 동일한 기능을 perform 하는 기계적인 util성 기능에 사용하는 것이 좋다.