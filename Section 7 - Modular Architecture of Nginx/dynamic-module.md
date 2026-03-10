### Base Requirement

A Fresh Ubuntu LTS server with no Nginx installed.

We will install Nginx from Ubuntu repository. 

### Step 1 - Download Module from Repository

```sh
sudo apt update && apt install nginx -y

sudo apt install libnginx-mod-http-image-filter

ls -l /usr/lib/nginx/modules/
```

### Step 2 - Ensure Module is Loaded
```sh
ls /etc/nginx/modules-enabled/

cat /etc/nginx/modules-enabled/50-mod-http-image-filter.conf
```
### Step 3 - Modify Nginx Configuration
```sh
nano /etc/nginx/sites-available/default
```
```sh
 location /resize/ {
    alias /var/www/html/;
    image_filter resize 200 200;
   }
```
```sh
nginx -t

systemctl reload nginx
```
### Step 4 - Download Image File 
```sh
cd /var/www/html

wget https://kplabs.in/friend.jpg
```
### Step 5 - Test the Setup

From browser:

```sh
http://your-server-ip/friend.jpg

http://your-server-ip/resize/friend.jpg
```