# Nginx Setup for Node.js Apps

[Nginx](https://nginx.org/) is a high-performance web server and reverse proxy. In a Node.js production setup, Nginx typically sits in front of your app to:

- Forward requests to your Node.js app (reverse proxy).
    
- Serve static files efficiently.
    
- Handle SSL/TLS (HTTPS).

---

## 1. Install Nginx

```bash
sudo apt install -y nginx
```

Enable and start it:

```bash
sudo systemctl enable nginx
sudo systemctl start nginx
```

Check status:

```bash
systemctl status nginx
```

---

## 2. Basic Reverse Proxy Configuration

Create a new config file for your app:

```bash
sudo nano /etc/nginx/sites-available/myapp
```

Example config:

```nginx
server {
    listen 80;
    server_name gautamsuthar.in;

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

---

## 3. Enable the Config

```bash
sudo ln -s /etc/nginx/sites-available/myapp /etc/nginx/sites-enabled/
sudo nginx -t     # Test syntax
sudo systemctl reload nginx
```

---

## 4. Verify

- Open your domain or server IP in the browser.
    
- Requests should pass through Nginx → Node.js app (running on port `3000` via PM2).

---

Nginx is now set up as a reverse proxy in front of your Node.js app.
