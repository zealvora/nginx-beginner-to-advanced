### Step 1 - Configure Multiple Server Blocks for Websites

```sh
cd /etc/nginx/conf.d

nano websites.conf
```

```sh
server {
  listen 80;
  server_name kplabs.internal;

  location / {
     root /usr/share/nginx/html/kplabs;
     index kplabs.html;
   }
}

server {
  listen 80;
  server_name news.internal;

  location / {
     root /usr/share/nginx/html/news;
     index news.html;
   }
}
```

### Step 2 - Configure Website Contents and Folders

```sh
cd /usr/share/nginx/html/
mkdir kplabs
cd kplabs
echo "This is Kplabs Website" > kplabs.html
```

```sh
cd /usr/share/nginx/html/
mkdir news
cd news
echo "This is News Website" > news.html
```
```sh
systemctl restart nginx
```
### Step 3 - Testing
```sh
nano /etc/hosts
```
```sh
127.0.0.1 kplabs.internal
127.0.0.1 news.internal
```
```sh
curl kplabs.internal
curl news.internal
curl 127.0.0.1
```

### Step 4 - Add Default Server Option 
```sh
nano /etc/nginx/conf.d/websites.conf
```
Code Block for Reference:
```sh
server {
  listen 80 default_server;
  server_name kplabs.internal;

  location / {
     root /usr/share/nginx/html/kplabs;
     index kplabs.html;
   }
}
```

```sh
systemctl restart nginx
```

```sh
curl 127.0.0.1
```