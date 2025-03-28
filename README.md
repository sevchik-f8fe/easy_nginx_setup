# easy_nginx_setup

 ```
server {
        listen 443 ssl http2;
        root /var/www/html;

        index index.html index.htm index.nginx-debian.html index.js;

        server_name vanopoizonserver.ru;

        ssl_certificate /etc/ssl/vanopoizonserver.crt;
        ssl_certificate_key /etc/ssl/vanopoizonserver.key;
        ssl_session_cache shared:SSL:10m;
        ssl_session_timeout 10m;
        keepalive_timeout 70;

#       ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
#       ssl_prefer_server_ciphers on;

        ssl_stapling on;
        ssl_trusted_certificate /etc/ssl/ca.crt;

        proxy_http_version 1.1;
        proxy_pass_request_headers on;
        proxy_pass_request_body on;
        proxy_redirect off;
        proxy_connect_timeout       600;
        proxy_send_timeout          600;
        proxy_read_timeout          600;
        send_timeout                600;

        resolver 8.8.8.8;

        location / {
                add_header 'Access-Control-Allow-Origin' '*' always;
                add_header 'Access-Control-Allow-Methods' '*' always;
                add_header Access-Control-Allow-Headers 'Authorization, Origin, X-Requested-With, Content-Type, Accept' always;
                proxy_set_header Host $host;
                proxy_pass http://127.0.0.1:3000;
        }
}

```
