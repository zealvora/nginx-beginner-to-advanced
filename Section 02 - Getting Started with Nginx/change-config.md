
### Step 1 - Demonstrating Mistake in Configuration File

```sh
nano /etc/nginx/nginx.conf
```

Remove `;` from any line in the configuration file
```sh
systemctl restart nginx
```
Very if Nginx responds to requests with `curl localhost`

Add the `;` again so configuration file is valid again
```sh
systemctl start nginx
```

### Step 2 - Recommended Approach Whenever Making Any Changes

Remove `;` from any line in the configuration file

```sh
nginx -t
```

Undo the change to have valid Nginx configuration for future practicals.



