서버에 Nginx를
1. 설치하고 (```sudo apt install nginx -y```)
2. 설정해서 (```/etc/nginx/nginx.conf```)
3. 실행하면 됨 (```(sudo) service nginx start / restart```) (ubuntu)
4. 확인 (```ps -ef | grep nginx```)

최초에 할 때만 설치하고 다음 부터는 

service nginx start 해주면 됨


### Config 예시

For load banacing
```nginx
http {
	upstream backend {
		server backend1.example.com;
		server backend2.example.com
	}
	server {
		location / {
			proxy_pass http://backend;
		}
	}
}
```

For IP control
```nginx
server {
	location / {
		allow 192.168.1.0/24
		allow 10.0.0.0/8;
		deny all;

		proxy_pass http://backend;
	}
}
```

Trippy
```nginx
# For more information on configuration, see:
#   * Official English Documentation: http://nginx.org/en/docs/
#   * Official Russian Documentation: http://nginx.org/ru/docs/

#user nginx;
#worker_processes auto;
#error_log /var/log/nginx/error.log notice;
#pid /run/nginx.pid;
  
events {
}

http {
    upstream spring-server {
        server localhost:8081;
        server localhost:8082;
    }

    # 실제 HTTP 서버를 설정하는 부분입니다.
    server {
        # listen 지시문은 서버가 80포트에서 들어오는 요청을 수신하도록 설정합니다.
        listen 80;
        include /etc/nginx/default.d/ *.conf;
        
        # 모든 경로에 대한 처리를 정의합니다. 프록시 서버로의 요청을 설정하는 부분입니다.
        location / {
            **proxy_set_header** X-Real-IP **$remote_addr**;
            **proxy_set_header** HOST **$http_host**;
            **proxy_set_header** X-Nginx-Proxy true;
            **proxy_set_header** X-Forwarded-For **$proxy_add_x_forwarded_for**;

            # proxy_pass는 실제 요청을 전달할 upstream 서버 그룹을 지정합니다.
            proxy_pass http://spring-server;
            
            # proxy_redirect는 프록시 응답의 리다이렉션을 설정하는 부분입니다.
            **proxy_redirect** off;
        }
    }
}
```



