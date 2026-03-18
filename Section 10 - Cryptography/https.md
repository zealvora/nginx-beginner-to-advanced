
### Step 1 - Install Base Packages
```sh
apt update && apt install -y certbot python3-certbot-nginx
```

### Step 2 - Setup Base Nginx Configuration
```sh
cd /etc/nginx/conf.d

nano secure.conf
```

```sh
server {
    listen       80;
    server_name  secure.kplabs.in;
    root   /usr/share/nginx/html;

    location / {
        index  index.html index.htm;
    }
}
```

### Step 3 - Obtain and Install the SSL Certificate
```sh
certbot --nginx -d secure.kplabs.in
```

### Step 4 - Testing
```sh
curl https://secure.kplabs.in
```
