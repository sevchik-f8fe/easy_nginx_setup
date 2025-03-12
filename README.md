# easy_nginx_setup

 ```
server {
        listen 443 ssl http2;
        server_name domain.ru;
        index index.js index.html index.htm index.nginx-debian.html;

        ssl_certificate /etc/ssl/domain.crt;
        ssl_certificate_key /etc/ssl/domain.key;
        ssl_session_cache shared:SSL:10m;
        ssl_session_timeout 10m;
        keepalive_timeout 70;

        ssl_stapling on;
        ssl_trusted_certificate /etc/ssl/ca.crt;
        proxy_http_version 1.1;
        proxy_pass_request_headers on;
        proxy_pass_request_body on;
        proxy_redirect off;
        resolver 8.8.8.8;

        location / {
                add_header Access-Control-Allow-Headers '*';
                add_header Access-Control-Allow-Methods '*';
                add_header Access-Control-Allow-Origin '*';

                proxy_set_header Host $host;
                proxy_pass http://127.0.0.1:3000;
        }
}
```
