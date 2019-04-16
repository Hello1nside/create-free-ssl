# How to create a Free SSL certificate?

#### 1. Install certbot
```html
  sudo yum install certbot
```

#### 2. Creating a certificate
You need to execute the command one time
```html
certbot certonly -d example.com,example.org,subdomain.example.com --webroot --webroot-path /srv/www/example.com/webroot -m yourname@gmail.com --agree-tos --no-eff-email
```

List of all parameters: https://certbot.eff.org/docs/using.html#certbot-command-line-options
If everything went well, in the console we will get info with the paths to the certificate files (fullchain.pem and privkey.pem).

#### 3. Nginx configs
Add it to the config

```html
   listen  ip_адрес_сервера:443 ssl;
   ssl_certificate     /etc/letsencrypt/live/example.com/fullchain.pem;
   ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;
```

#### 4. Reload nginx:
```html
sudo nginx -s reload
```

#### 5. Add certificate auto update:
Add to cron (for example, once a day):
```html
   0	11	*	*	*	root	certbot renew 2>&1 ; nginx -s reload 2>&1
```

# Useful information

#### 1. Update with pens (by default it is updated only if less than 30 days are left before the end):

```html
   sudo certbot renew
```

#### 2. View information about all installed certificates on the server (shows sites, paths with keys, time to end):

```html
   sudo certbot certificates
```
