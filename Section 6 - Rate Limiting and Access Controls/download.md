### Step 1 - Create 1 GB Test File
```sh
cd /usr/share/nginx/html

fallocate -l 1G testfile
```

### Step 2 - Restrict Download Speed
```sh
nano /etc/nginx/conf.d/default.conf 
```
```sh
limit_rate 500k;
```
```sh
systemctl reload nginx
```