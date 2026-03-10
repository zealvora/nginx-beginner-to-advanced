
### Example 1 - Setting Rate Limit
```sh
cd /etc/nginx/conf.d
```
```sh
nano rate-limit.conf
```
```sh
limit_req_zone $binary_remote_addr zone=mylimit:10m rate=10r/s;

server {
    listen 80;
    server_name _;
    root /usr/share/nginx/html;
    index index.html;
    
    limit_req zone=mylimit;

}
```
```sh
systemctl reload nginx
```
Testing:
```sh
for i in $(seq 1 50); do curl -s -o /dev/null -w "%{http_code}\n" http://127.0.0.1/; done
```

### Example 2 - Rate Limit with Burst
```sh
server {
    listen 80;
    server_name _;
    root /usr/share/nginx/html;
    index index.html;
    limit_req zone=mylimit;
    limit_req zone=mylimit burst=10 nodelay;
            
}
```
```sh
systemctl reload nginx
```
Testing:
```sh
for i in $(seq 1 50); do curl -s -o /dev/null -w "%{http_code}\n" http://127.0.0.1/; done
```