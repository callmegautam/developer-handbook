# Nginx SSL Setup with Let’s Encrypt (Certbot)

Adding SSL/TLS to your Nginx server secures traffic with HTTPS. The easiest way is with [Let’s Encrypt](https://letsencrypt.org/) using **Certbot**.

---

## 1. Install Certbot

```bash
sudo apt install -y certbot python3-certbot-nginx
```

---

## 2. Request an SSL Certificate

Make sure your domain (e.g. `your-domain.com`) is already pointing to your server’s public IP (via DNS).

Then run:

```bash
sudo certbot --nginx -d your-domain.com -d www.your-domain.com
```

Certbot will:

- Edit your Nginx config.
    
- Obtain certificates from Let’s Encrypt.
    
- Reload Nginx automatically.

---

## 3. Verify HTTPS

Open `https://your-domain.com` in your browser — you should see the secure lock icon.

---

## 4. Auto-Renew Certificates

Let’s Encrypt certificates expire every 90 days. Certbot installs a systemd timer for auto-renewal, but you can test it:

```bash
sudo certbot renew --dry-run
```

---

## 5. (Optional) Redirect All HTTP → HTTPS

If not already set, edit your site config:

```nginx
server {
    listen 80;
    server_name your-domain.com www.your-domain.com;
    return 301 https://$host$request_uri;
}
```

Reload Nginx:

```bash
sudo systemctl reload nginx
```

---

Your Nginx server is now serving traffic securely over HTTPS with free, auto-renewing SSL certificates.
