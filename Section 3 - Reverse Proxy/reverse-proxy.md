### Step 1 - Add Reverse Proxy Configuration
```sh
cd /etc/nginx/conf.d
mv default.conf default.conf.bak 
nano reverse-proxy.conf
```

```sh
server {
    listen       80;
    server_name  _;

    location / {
         proxy_pass http://172.17.0.3;
    }
}
```


```sh
systemctl restart nginx
```

### Step 2 - Test the Entire Setup
```sh
curl <IP-OF-REVERSE-PROXY>
OR
curl 127.0.0.1 
```