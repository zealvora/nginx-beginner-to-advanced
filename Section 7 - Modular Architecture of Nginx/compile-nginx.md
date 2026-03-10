### Documentation Link Referenced:

https://nginx.org/en/download.html

### Step 1 - Install Packages
```sh
apt update

apt -y install build-essential libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev net-tools
```
### Step 2 - Download Nginx
```sh
wget https://nginx.org/download/nginx-1.28.2.tar.gz

tar -xzvf nginx-1.28.2.tar.gz

cd nginx-1.28.2
```

### Step 3 - Create Nginx User and Group
```sh
useradd nginx
```
### Step 3 - Compilation Process
```sh
./configure --sbin-path=/usr/sbin/nginx \
            --conf-path=/etc/nginx/nginx.conf \
            --error-log-path=/var/log/nginx/error.log \
            --http-log-path=/var/log/nginx/access.log \
            --user=nginx \
            --group=nginx \
            --pid-path=/var/run/nginx.pid \
            --with-http_ssl_module
```
```sh
make 

make install

```
### Step 4 - Manage Nginx
```sh

/usr/sbin/nginx

/usr/sbin/nginx -s stop

```
### Step 5 - Create Systemd file
```sh
nano /usr/lib/systemd/system/nginx.service
```
```sh
[Unit]
Description=nginx - high performance web server
Documentation=https://nginx.org/en/docs/
After=network-online.target remote-fs.target nss-lookup.target
Wants=network-online.target

[Service]
Type=forking
PIDFile=/var/run/nginx.pid
Environment="CONFFILE=/etc/nginx/nginx.conf"
EnvironmentFile=-/etc/default/nginx
ExecStart=/usr/sbin/nginx -c ${CONFFILE}
ExecReload=/bin/sh -c "/bin/kill -s HUP $(/bin/cat /run/nginx.pid)"
ExecStop=/bin/sh -c "/bin/kill -s TERM $(/bin/cat /run/nginx.pid)"

[Install]
WantedBy=multi-user.target
```