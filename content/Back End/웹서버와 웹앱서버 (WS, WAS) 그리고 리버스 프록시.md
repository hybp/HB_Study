정적인 페이지는 Web Server
동적인 페이지는 Web App Server로 분리해 처리하게 되었다

WS는 클라이언트 요청을 처리하고 (Apache, Nginx)
WAS는 db transaction 등 다양한 로직을 처리하는 서버 (Spring)

원조 Apache의 한계 - 요청이 올 때마다 프로세스 할당 -> 많은 요청이 왔을 때 메모리 부족, CPU의 context switching overhead 증가


Spring Boot에서는 내장된 Tomcat 웹서버를 사용하지만 




[[리버스 프록시]]
