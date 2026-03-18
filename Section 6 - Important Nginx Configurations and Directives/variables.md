### Documentation Referenced:

https://nginx.org/en/docs/varindex.html

### Step 1 - Setup Base Nginx Configuration
```sh
cd /etc/nginx/conf.d

nano variables.conf
```

```sh
log_format custom_kplabs 'client_ip=$remote_addr ' 'server_ip=$server_addr ' 'method=$request_method ' 'uri=$uri ' 'raw_uri=$request_uri ' 'host=$host ' 'user_agent="$http_user_agent" ' 'bytes_in=$request_length ' 'bytes_out=$bytes_sent ' 'status=$status ' 'duration=${request_time}s';

server {
    listen       80;
    server_name  localhost;
    root   /usr/share/nginx/html;
    index  index.html index.htm;
    access_log /var/log/nginx/kplabs.log custom_kplabs;
}
```
```sh
nginx -t

systemctl reload nginx
```
### Step 2 - Testing
```sh
curl localhost/index.html

cat /var/log/nginx/kplabs.log
```