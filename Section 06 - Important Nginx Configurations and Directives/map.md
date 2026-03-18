### Step 1 - Setup  Nginx Configuration

```sh
cd /etc/nginx/conf.d

nano map.conf
```
```sh
map $http_user_agent $index_file {
    default          "desktop.html";
    ~*iPhone         "mobile.html";
    ~*Android        "mobile.html";
}

server {
    listen       80;
    server_name  localhost;
    root   /usr/share/nginx/html;

    location / {
        index $index_file;
    }
}
```

```sh
nginx -t

systemctl reload nginx
```
### Step 2 - Setup HTML Files
```sh
cd /usr/share/nginx/html

touch desktop.html mobile.html

echo "This is Desktop Website" > desktop.html

echo "This is Mobile Website" > mobile.html
```
### Step 3 - Testing

To test as an iPhone:
```sh
curl -H "User-Agent: iPhone" http://localhost
```
To test as an Android:
```sh
curl -H "User-Agent: Android" http://localhost
```
Test Without Mobile User Agent
```sh
curl  http://localhost
```

