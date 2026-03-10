### Documentation Referenced in This Video

https://nginx.org/en/linux_packages.html

### Step 1: Install Nginx

```sh
sudo bash << 'EOF'
set -e

# 1. Install prerequisites
apt update
apt install -y curl gnupg2 ca-certificates lsb-release ubuntu-keyring

# 2. Add Nginx GPG key
curl https://nginx.org/keys/nginx_signing.key | gpg --dearmor \
    | tee /usr/share/keyrings/nginx-archive-keyring.gpg >/dev/null

# 3. Setup repository
echo "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] \
https://nginx.org/packages/ubuntu $(lsb_release -cs) nginx" \
    | tee /etc/apt/sources.list.d/nginx.list

# 4. Set Pin Priority
echo -e "Package: *\nPin: origin nginx.org\nPin: release o=nginx\nPin-Priority: 900\n" \
    | tee /etc/apt/preferences.d/99nginx

# 5. Update and install
apt update
apt install -y nginx
EOF
```

### Step 2 - Start Nginx

```sh
systemctl start nginx

systemctl status nginx
```

### Step 3 - Test

```sh
curl localhost
```