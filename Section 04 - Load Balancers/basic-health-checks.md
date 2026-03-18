
### Step 1 - Verify Load Balancing to Both Backend Servers 

From Load-Balancer server
```sh
curl localhost

curl localhost
```
You should see traffic routed equally between Server-1 and Server -2

### Step 2 - Stop Sever 1 Nginx

Login to Server-1
```sh
systemctl stop nginx
```
### Step 3 - Verify Nginx Load Balancer Routing

Switch to load-balancer server tab
```sh
curl localhost

curl localhost
```
You should see all traffic directed to Server-2

### Step 4 - Stop Sever 2 Nginx

Login to Server-1
```sh
systemctl stop nginx
```
### Step 5 - Verify Nginx Load Balancer Routing

Switch to load-balancer server tab
```sh
curl localhost

curl localhost
```
You should see 502 timeout error message as both backends are stopped.

### Restore Configuration

Bring back Nginx in both Server-1 and Server-2 for next practicals.
```sh
systemctl start nginx
```
