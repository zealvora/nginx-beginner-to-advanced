## Testing Default Configuration of Max Fails and Fail Timeout

### Step 1 - In Load Balancer Nginx Server

Terminal Tab 2
```sh
echo > /var/log/nginx/error.log

tail -f /var/log/nginx/error.log
```
Terminal Tab 1

### Step 2 - Stop Server-1 Nginx and Run TCPDUMP

Server-1 Terminal Tab
```sh
systemctl stop nginx

tcpdump -i eth0 port 80
```
### Step 3 - Start Sending Requests from Load Balancer

Terminal Tab 1 of Load Balancer Server
```sh
curl localhost

curl localhost
```

Verify if you see new entry in tcpdump command.

Also verify if you see new entry in the error.log file opened in Step 1.

## Set Custom Configuration for Max Fails and Fail Timeout

### Step 1 - Add custom configuration

```sh
nano /etc/nginx/conf.d/load-balancer.conf
```
```sh
upstream backend {
  server <server-1-ip-here> max_fails=3 fail_timeout=60s;
  server <server-2-ip-here> max_fails=3 fail_timeout=60s;
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
nginx -t

systemctl reload nginx
```

### Step 2 - Test and Monitor Error Log Files

Terminal Tab-1
```sh
echo > /var/log/nginx/error.log

tail -f /var/log/nginx/error.log
```
Terminal Tab-2
```sh
curl localhost

curl localhost

curl localhost
```