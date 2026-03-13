### Base Requirement

Fresh Ubuntu LTS Server

Nginx Installed From Ubuntu Repository
```sh
apt update && apt install nginx -y
```
### Step 1 - Install Mod Security

```sh
apt install libnginx-mod-http-modsecurity modsecurity-crs -y
```

### Step 2 - Configuring ModSecurity and Nginx
```sh
nano /etc/nginx/modsecurity.conf
```
Change `SecRuleEngine DetectionOnly` to `SecRuleEngine On`

Add two Rules
```sh
SecRule REQUEST_URI "@contains attack" "id:100001,phase:1,deny,status:403,log,msg:'Custom Rule Triggered: Blocked URI containing the word attack'"
```
```sh
SecRule REQUEST_BODY "@contains hacker" "id:100002,phase:2,deny,status:403,log,msg:'Custom Rule Triggered: Blocked Request Body containing the word hacker'"
```

### Step 3 - Configure Nginx 
```sh
cd /etc/nginx/sites-available/

mv default-modsecurity.conf default-modsecurity.conf.bak

mv default default.bak
```
```sh
nano default
```
Add following configuration


```sh
server {
        listen 8080;
        listen 80 default_server;
        listen [::]:80 default_server;
        modsecurity on;
        modsecurity_rules_file /etc/nginx/modsecurity.conf;
        root /var/www/html;
        index index.html index.htm index.nginx-debian.html;
        server_name _;

        location / {
          return 200 "It Works\n";
        }

        location /api {
           proxy_pass http://127.0.0.1:8080/;
   }
}
```
```sh
systemctl restart nginx
```

### Step 4 - Testing WAF Rules
```sh
curl -X POST -d "myfield=zeal" http://localhost/api

curl -X POST -d "myfield=hacker" http://localhost/api

curl localhost/attack

curl localhost/test
```