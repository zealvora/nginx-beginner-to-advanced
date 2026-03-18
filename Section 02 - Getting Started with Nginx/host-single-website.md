### Step 1: Add Custom Server Block for kplabs.internal

```sh
cd /etc/nginx/conf.d/
touch kplabs.conf
nano kplabs.conf
```
```sh
server {
  listen 8080;
  server_name kplabs.internal;

  location / {
     root /usr/share/nginx/html/kplabs;
     index kplabs.html;
   }
}
```

### Step 2: Configure Root Folder and Index File for kplabs.internal
```sh
cd /usr/share/nginx/html/
mkdir kplabs
cd kplabs
echo "This is Kplabs Website" > kplabs.html
```
```sh
cd /etc/nginx/conf.d

mv default.conf default.conf.bak

systemctl restart nginx
```

### Step 3: Testing
```sh
nano /etc/hosts
```
```sh
127.0.0.1 kplabs.internal
```
```sh
curl kplabs.internal:8080
```

### Step 4: Revert the Changes

```sh
cd /etc/nginx/conf.d

rm kplabs.conf

mv default.conf.bak default.conf

systemctl restart nginx
```

