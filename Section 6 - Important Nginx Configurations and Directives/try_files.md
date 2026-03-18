
### Step 1 - Setup Base Nginx Configuration
```sh
cd /etc/nginx/conf.d

nano try-files.conf
```
```sh
server {
    listen       80;
    server_name  localhost;
    root         /usr/share/nginx/html;
    index        index.html index.htm;

    location / {
        try_files $uri $uri.html =404;
    }
}
```
```sh
systemctl reload nginx
```

### Step 2 - Create Basic Files
```sh
cd /usr/share/nginx/html

touch about.html

echo "This is About HTML File" > about.html
```

### Step 3 - Testing
```sh
curl localhost/about

curl localhost/test
```
