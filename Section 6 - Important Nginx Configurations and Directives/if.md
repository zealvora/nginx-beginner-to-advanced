Documentation Referenced:

https://nginx.org/en/docs/http/ngx_http_rewrite_module.html#if

### Step 1 - Setup  Nginx Configuration

```sh
cd /etc/nginx/conf.d

nano if.conf
```
```sh
server {
    listen       80;
    server_name  localhost;
    root   /usr/share/nginx/html;
    index index.html;
    
    if ($remote_addr = "127.0.0.1") {
        return 403;
    }
}
```


```sh
systemctl reload nginx
```

### Step 2 - Testing
```sh
curl 127.0.0.1
```

Open Server IP from Browser to Check if Website Loads
