## Documenation Referenced

https://github.com/owasp-modsecurity/ModSecurity/wiki/Reference-Manual-(v2.x)

### Rule 1 - REMOTE_ADDR (ipMatch)
```sh
nano /etc/nginx/modsecurity.conf
```
```sh
SecRule REMOTE_ADDR "@ipMatch 127.0.0.1" "id:100007,phase:1,deny,status:403,msg:'IP Blacklisted'"
```
```sh
systemctl restart nginx
```
```sh
curl 127.0.0.1
```
Now run `curl` command from different system (your laptop) or browser.


### Rule 2 - REQUEST_HEADERS (User-Agent)
```sh
nano /etc/nginx/modsecurity.conf
```
```sh
SecRule REQUEST_HEADERS:User-Agent "@contains curl" "id:100003,phase:1,deny,status:403,msg:'No Curl Requests'"
```
```sh
systemctl restart nginx
```
Testing
```sh
curl <IP-OF-SERVER>
```
Try opening from browser



