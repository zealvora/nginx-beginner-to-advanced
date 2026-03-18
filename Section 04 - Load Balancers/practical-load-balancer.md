### Base Requirement 
```sh
Server 1 - Load Balancer (Nginx)
Server 2 - Backend Application Server 1 (Nginx)
Server 3 - Backend Application Server 2 (Nginx)
```
### Step 1 - Configure Index Files for Backend Servers

#### Backend Server 1
```sh
cd /usr/share/nginx/html
cp index.html index.html.bak
echo "This is Server 1" > index.html
```
#### Backend Server 2
```sh
cd /usr/share/nginx/html
cp index.html index.html.bak
echo "This is Server 2" > index.html
```

### Step 2 - Configure Nginx as Load Balancer
```sh
cd /etc/nginx/conf.d
mv default.conf default.conf.bak 
```
```sh
nano load-balancer.conf
```
```sh
upstream backend {
  server <server-1-ip-here>;
  server <server-2-ip-here>;
}

server {
    listen       80;
    server_name  _;

    location / {
        proxy_pass http://backend;
 }
}
```
```sh
systemctl reload nginx
```
### Step 3 - Testing
```sh
curl localhost

curl localhost
```