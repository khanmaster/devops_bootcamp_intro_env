# Nginx Reverse Proxy Solution

## Solution

See below for reverse proxy setup

```bash
# On virtual machine open default config
sudo vi /etc/nginx/sites-available/default
```

In this file you should see a location block. This is where we are going to point our request to port 80 onto so it points to http://localhost:3000. Add the code below to set the configuration.

```bash
server {
    listen 80;

    server_name _;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}

```

Lets now test that our new config has not introduced any errors.

```bash
sudo nginx -t
```

The last thing to do is to restart nginz.

```bash
sudo systemctl restart nginx
```

If everything is correct you should now be able to go to `http://development.local` and see our page as if you were accessing the local host.
