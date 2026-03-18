### Quick Setup
```sh
docker run -dt --name edge-proxy --hostname edge-proxy  nginx:latest
docker run -dt --name reverse-proxy --hostname reverse-proxy  nginx:latest
docker run -dt --name app-01 --hostname app-01 nginx:latest
docker run -dt --name client --hostname client nginx:latest
```

### Edge Proxy Configuration
```sh
server {
    listen       80;
    server_name  _;

    location / {
         proxy_pass http://172.17.0.3;
         proxy_set_header X-Real-IP $remote_addr;
         proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

### Reverse Proxy Configuration
```sh
server {
    listen       80;
    server_name  _;

    location / {
         proxy_pass http://172.17.0.3;
         proxy_set_header X-Real-IP $remote_addr;
         proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```
```sh
systemctl restart nginx
```


### Application Nginx Server
```sh
nano /etc/nginx/nginx.conf
```
```sh
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_real_ip"' 'XFF: "$http_x_forwarded_for"';
```

```sh
systemctl restart nginx
```

### Test the Setup

From Client:
```sh
curl <edge-proxy-ip>
```
From Application Server:
```sh
tail -f /var/log/nginx/access.log
```

