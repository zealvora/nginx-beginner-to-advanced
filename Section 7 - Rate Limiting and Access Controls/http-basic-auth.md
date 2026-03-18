### Step 1 - Install Required Packages

```sh
apt install apache2-utils -y
```

### Step 2 - Create the Password File
```sh
htpasswd -c /etc/nginx/.htpasswd admin
```
The terminal will prompt you to enter and confirm a password.

### Step 3 - Configure Directory and Files
```sh
cd /usr/share/nginx/html
mkdir admin
cd admin
echo "This is Secret File" > secrets.txt
```

### Step 4- Configure Nginx
```sh
nano /etc/nginx/conf.d/auth.conf
```
```sh
server {
    listen       80;
    server_name  _;

    location /admin {
        root /usr/share/nginx/html;
        index secrets.txt;

        auth_basic "Restricted Access - Admins Only";
        auth_basic_user_file /etc/nginx/.htpasswd;
 }
}
```
```sh
systemctl reload nginx
```