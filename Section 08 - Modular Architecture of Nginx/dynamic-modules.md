### Base Requirement:

Nginx should be installed officially from Nginx Stable repository and not from Ubuntu repository.

https://github.com/zealvora/nginx-beginner-to-advanced/blob/main/Section%201%20-%20Setting%20Up%20Labs/install-nginx.md

### Step 1 - Install Packages
```sh
apt update

apt -y install build-essential libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev net-tools libgd-dev
```

### Step 2 - Download Nginx
```sh
wget https://nginx.org/download/nginx-1.28.2.tar.gz

tar -xzvf nginx-1.28.2.tar.gz

cd nginx-1.28.2
```

### Step 3 - Build  Process
```sh
./configure --with-compat --with-http_image_filter_module=dynamic
```
```sh
make modules
```
```sh
ls -l objs/
```

### Step 4 - Deploy the Module
```sh
mkdir -p /etc/nginx/modules

cp objs/ngx_http_image_filter_module.so /etc/nginx/modules/
```

### Step 5 - Add Configuration File
```sh
cd /etc/nginx/conf.d/

nano resize.conf
```
```sh
server {
    listen       80;
    server_name  localhost;
    root   /usr/share/nginx/html;

   location /resize {
      alias /usr/share/nginx/html;
      image_filter resize 200 200;
  }
}
```
```sh
nginx -t
```

### Step 6 - Load the Module

```sh
nano /etc/nginx/nginx.conf
```
```sh
load_module /etc/nginx/modules/ngx_http_image_filter_module.so;
```
```sh
nginx -t
```
```sh
systemctl nginx reload
```
```sh
nginx -V
```
### Step 7 - Download Image for Testing
```sh
cd /usr/share/nginx/html

wget https://kplabs.in/friend.jpg
```

From browser: Run `http://<server-ip>/resisze/friend.jpg`


