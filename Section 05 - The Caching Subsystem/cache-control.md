### Step 1: Download Image File to Server
```sh
cd /usr/share/nginx/html

wget https://kplabs.in/friend.jpg 
```

### Step 2: Create Custom Conf File
```sh
cd /etc/nginx/conf.d
mv default.conf default.conf.bak
```
```sh
nano kplabs.conf
```
```sh
server {
    listen       80;
    server_name  localhost;
    root   /usr/share/nginx/html;
}
```
### Step 3 - Cache-Control: Public

```sh
location /friend.jpg {
    add_header Cache-Control "public, max-age=31536000";
}
```
```sh
systemctl reload nginx
```
```sh
curl -I localhost/friend.jpg
```

### Step 2 - Cache-Control No-Cache
```sh
location /friend.jpg {
    add_header Cache-Control "no-cache";
}
```
```sh
systemctl reload nginx
```
```sh
curl -I localhost/friend.jpg
```

### Step 3 - Cache-Control No-Store

cd /usr/share/nginx/html
cp friend.jpg dog.jpg

```sh
location  /dog.jpg {
    add_header Cache-Control "no-store";
}
```
```sh
systemctl reload nginx
```
```sh
curl -I localhost/dog.jpg
```

