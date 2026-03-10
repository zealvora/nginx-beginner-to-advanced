
### Server Weight Configuration
```sh
cd /etc/nginx/conf.d
```
```sh
nano load-balancer.conf
```
```sh
upstream backend {
  server <server-1-ip-here> ;
  server <server-2-ip-here> weight=2;
}

server {
    listen       80;
    server_name  _;

    location / {
        proxy_pass http://backend;
 }
}
```
```sh
systemctl reload nginx
```
### Step 3 - Testing
```sh
curl localhost

curl localhost
```