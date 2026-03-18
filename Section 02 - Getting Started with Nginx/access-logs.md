### Documentation Referenced - Nginx Variables

https://nginx.org/en/docs/http/ngx_http_core_module.html#var_remote_addr

### Step 1 - Take Backup of Original Nginx Configuration
```sh
cd /etc/nginx
cp nginx.conf nginx.conf.bak
```

### Step 2 - Customize the Log Format
```sh
nano nginx.conf
```
```sh
log_format text_friendly 'User from IP $remote_addr connected at $time_local and made request on $request_uri using $http_user_agent and response code was $status';


access_log  /var/log/nginx/access.log text_friendly;
```
```sh
systemctl reload nginx
```
### Step 3 - Test
```sh
tail -f /var/log/nginx/access.log

curl <NGINX-SERVER-IP> [From Different System]
```

### Step 4 - Restore the Original Configuration File
```sh
cd /etc/nginx

cp nginx.conf.bak nginx.conf

systemctl reload nginx
```