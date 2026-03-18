### Step 1 - Setup  Nginx Configuration

```sh
cd /etc/nginx/conf.d

nano rewrite.conf
```
```sh
server {
    listen       80;
    server_name  localhost;
    root   /usr/share/nginx/html;

    location /myimages {
        rewrite ^/myimages(.*)$ /images$1;
    }
}
```

```sh
nginx -t

systemctl reload nginx
```
### Step 2 - Setup HTML Files
```sh
cd /usr/share/nginx/html

mkdir images

cd images 

wget https://kplabs.in/friend.jpg
```
### Step 3 - Testing

```sh
curl -I http://localhost/myimages/friend.jpg
```

From Browser: `http://<server-ip>/myimages/friend.jpg`