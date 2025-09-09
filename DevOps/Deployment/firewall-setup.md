# Firewall Setup with UFW

[UFW (Uncomplicated Firewall)](https://help.ubuntu.com/community/UFW) is a simple way to manage firewall rules on Ubuntu. This guide covers allowing essential services like SSH, HTTP, and HTTPS, while securing your server.

---

## 1. Check UFW Status

```bash
sudo ufw status
```

- If it says `inactive`, UFW is not running yet.

---

## 2. Allow SSH

Always allow SSH **before enabling the firewall**, or you may lock yourself out:

```bash
sudo ufw allow OpenSSH
```

- Default SSH port is `22`.
    
- If you’re using a custom SSH port, replace `OpenSSH` with `port <your-port>`.

---

## 3. Allow HTTP and HTTPS

```bash
sudo ufw allow 'Nginx Full'
```

- `Nginx Full` allows both **HTTP (80)** and **HTTPS (443)**.
    
- If using Apache, you could use `sudo ufw allow 'Apache Full'` instead.

---

## 4. Enable UFW

```bash
sudo ufw enable
```

- You’ll be prompted: `Command may disrupt existing ssh connections. Proceed with operation (y|n)?` → type `y`.

Check status again:

```bash
sudo ufw status
```

You should see rules for **OpenSSH**, **80/tcp**, and **443/tcp**.

---

## 5. (Optional) Deny All Other Incoming Traffic

By default, UFW blocks all other incoming connections. You can explicitly enforce it:

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

---

Your server now has a basic firewall protecting it while allowing SSH, HTTP, and HTTPS traffic — essential for production readiness.
