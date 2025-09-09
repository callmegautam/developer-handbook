# Node.js Installation on Ubuntu

This guide covers installing Node.js (LTS version) and npm on Ubuntu (AWS EC2 or any Ubuntu server).

---

## 1. Add NodeSource Repository

Node.js from Ubuntu’s default repos is often outdated. Use NodeSource for the latest LTS release:

```bash
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
```

---

## 2. Install Node.js & npm

```bash
sudo apt install -y nodejs
```

Verify installation:

```bash
node -v
npm -v
```

---

## 3. Install Build Tools (Optional, Recommended)

Some npm packages require compilation:

```bash
sudo apt install -y build-essential
```
