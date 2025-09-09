# PM2 Setup

[PM2](https://pm2.keymetrics.io/) is a process manager for Node.js that keeps your app running in the background, restarts it if it crashes, and makes startup on reboot simple.

---

## 1. Install PM2

```bash
sudo npm install -g pm2
pm2 -v
```

---

## 2. Start a Node.js App

### Option A: Quick Start (direct command)

Run your app immediately with a one-liner:

```bash
pm2 start npm --name "myapp" -- start
```

- `--name "myapp"` assigns a friendly name.
    
- `-- start` tells PM2 to run the `npm start` script from your `package.json`.

This is fast and good for quick deployments.

---

### Option B: Using an Ecosystem File

For more control and repeatable configs, create an **ecosystem file**.  
If your project uses **CommonJS** (`.js`):

```bash
touch ecosystem.config.js
```

If your project uses **ESM** (`"type": "module"` in `package.json`):

```bash
touch ecosystem.config.mjs
```

Example (`ecosystem.config.js`):

```js
module.exports = {
  apps: [
        {
            name: "url-backend",
            script: "dist/index.js",
            instances: 1,
            autorestart: true,
            watch: false,
            env: {
                PORT: "3001",
            },
        },
    ],
};
```

Example (`ecosystem.config.mjs`):

```js
export default = {
  apps: [
        {
            name: "url-backend",
            script: "dist/index.js",
            instances: 1,
            autorestart: true,
            watch: false,
            env: {
                PORT: "3001",
            },
        },
    ],
};
```

Start with:

```bash
pm2 start ecosystem.config.js
```

---

## 3. Manage Processes

```bash
pm2 list           # Show all processes
pm2 status         # Detailed status
pm2 stop myapp     # Stop a process
pm2 restart myapp  # Restart a process
pm2 delete myapp   # Remove from PM2
```

View logs:

```bash
pm2 logs myapp
```

---

## 4. Enable Auto-Start on Reboot

```bash
pm2 startup systemd
pm2 save
```

---

PM2 can be as quick or as structured as you need, direct command for speed, ecosystem file for clarity and scaling.
