### Step 1 - Create 1 GB Test File
```sh
cd /usr/share/nginx/html

fallocate -l 1G testfile
```

### Step 2 - Restrict Download Speed
```sh
nano /etc/nginx/conf.d/default.conf 
```
In Server Block with location /

```sh
limit_rate 500k;
```
```sh
systemctl reload nginx
```
Try downloading the file from browser / Download Accelerator like IDM

### Step 3 - Limit Number of Connections
```sh
nano /etc/nginx/conf.d/default.conf 
```

In HTTP Context (Outside of server {})

```sh
limit_conn_zone $binary_remote_addr zone=addr:10m;
```
In Server Block with location /
```sh
limit_conn addr 1;
```
```sh
systemctl reload nginx
```

Try downloading the file from browser / Download Accelerator like IDM
