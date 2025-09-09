# AWS Instance Setup

This guide walks through creating an Ubuntu EC2 instance on AWS, connecting via SSH, and preparing the system for development or deployment.

---

## 1. Launch an EC2 Instance

1. Go to the **AWS Management Console** → **EC2** → **Launch Instance**.
    
2. Configure:
    
    - **Name**: `my-server` (or any project name).
        
    - **AMI**: Ubuntu Server 22.04 LTS (recommended).
        
    - **Instance type**: `t2.micro` (free tier) or larger if needed.
    
    - **Key pair**: Select an existing SSH key or create a new one (`.pem` file).
        
    - **Network settings**:
        
        - Allow inbound **SSH (22)**
            
        - Allow **HTTP (80)** and **HTTPS (443)**
            
        - Optional: allow **Custom TCP 3000** if you need direct Node.js access (not advised for production).
            
3. Click **Launch Instance**.
    
4. Once it’s running, find the **Public IPv4 address** of your instance.
    

---

## 2. Connect via SSH

From your local machine (Linux/Mac/WSL):

```bash
ssh -i your-key.pem ubuntu@<EC2_PUBLIC_IP>
```

---

## 3. Update the System

Always update fresh instances:

```bash
sudo apt update && sudo apt upgrade -y
```

Install some essentials:

```bash
sudo apt install -y build-essential curl git ufw
```

---

At this point, your AWS instance is live, secure, and updated, ready for software installation.
