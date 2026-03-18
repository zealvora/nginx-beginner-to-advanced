### Step 1 - Add HTML File in Backend Server 
```sh
cd /usr/share/nginx/html
```
```sh
nano friend.html
```
```sh
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>kplabs.internal</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: #f8fafc;
      display: flex;
      justify-content: center;
      padding: 60px 20px;
      margin: 0;
    }

    .card {
      background: #fff;
      border: 1px solid #e2e8f0;
      border-radius: 16px;
      padding: 40px;
      max-width: 480px;
      width: 100%;
      box-shadow: 0 4px 24px rgba(0,0,0,0.07);
      text-align: center;
    }

    .badge {
      display: inline-block;
      font-size: 11px;
      font-weight: 700;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      background: #dcfce7;
      color: #15803d;
      border-radius: 20px;
      padding: 4px 12px;
      margin-bottom: 20px;
    }

    h1 {
      font-size: 22px;
      font-weight: 700;
      color: #0f172a;
      margin: 0 0 8px;
    }

    p.intro {
      font-size: 15px;
      color: #475569;
      margin: 0 0 28px;
      line-height: 1.6;
    }

    /* The image below is NOT stored on this server.
       It is served directly by Nginx from its static cache. */
    .img-wrapper {
      border-radius: 12px;
      overflow: hidden;
      border: 2px solid #e2e8f0;
      margin-bottom: 20px;
    }

    .img-wrapper img {
      width: 100%;
      height: auto;
      display: block;
    }

    .note {
      font-size: 12px;
      color: #94a3b8;
      line-height: 1.6;
      background: #f8fafc;
      border: 1px solid #e2e8f0;
      border-radius: 8px;
      padding: 12px;
      text-align: left;
    }

    .note strong {
      color: #64748b;
    }

    code {
      font-family: 'JetBrains Mono', 'Courier New', monospace;
      font-size: 11px;
      background: #f1f5f9;
      padding: 1px 5px;
      border-radius: 4px;
      color: #e11d48;
    }
  </style>
</head>
<body>
  <div class="card">

    <div class="badge">kplabs.internal</div>

    <h1>This is an Image</h1>

    <p class="intro">
      The text above was served by the <strong>App Server</strong>.<br/>
      The image below was served by <strong>Nginx</strong> directly from its static cache — the app server was never contacted for it.
    </p>

    <!--
      ┌─────────────────────────────────────────────────┐
      │  This <img> tag causes the browser to make a   │
      │  SECOND HTTP request to /images/friend.jpg.     │
      │                                                 │
      │  Nginx intercepts that request via:             │
      │    location /images/ { root /var/nginx/static } │
      │  and serves the file from its own disk.         │
      │  The app server is NEVER contacted.             │
      └─────────────────────────────────────────────────┘
    -->
    <div class="img-wrapper">
      <img src="/images/friend.jpg" alt="A man and his dog — friend.jpg"/>
    </div>

    <div class="note">
      <strong>How this page was assembled:</strong><br/>
      ① <code>GET /</code> → Nginx proxied to this App Server → returned this HTML<br/>
      ② Browser parsed HTML, found <code>&lt;img src="/images/friend.jpg"&gt;</code><br/>
      ③ <code>GET /images/friend.jpg</code> → Nginx served from static disk (no app contact)
    </div>

  </div>
</body>
</html>
```

### Step 2 - Configure Nginx Reverse Proxy for Static Assets
```sh
mkdir -p /var/nginx/static/images

cd /var/nginx/static/images

wget https://kplabs.in/friend.jpg
```
```sh
cd /etc/nginx/conf.d

mv default.conf default.conf.bak

nano static-assets.conf
```
```sh
server {
    listen       80;
    server_name  _;


    location / {
        proxy_pass http://<backend-server-ip>;
 }

    location /images {
        root /var/nginx/static;
   }
}
```
```sh
systemctl reload nginx
```
```sh
echo > /var/log/nginx/access.log

tail -f /var/log/nginx/access.log
```

