---
title: How to Deploy a React (Vite) App with Nginx on a Subdomain
date: 2025-05-30
description: Step-by-step guide to deploying a React (Vite) app on a subdomain using Nginx, including prerequisites, configuration, and SSL setup.
tags: [React, Vite, Nginx, Deployment, Subdomain, SSL, DevOps]
---

# 🚀 How to Deploy a React (Vite) App with Nginx on a Subdomain

## 🎯 Goal:

Set up Nginx to serve a React (Vite) landing page when users visit:

```
staging.kenwpwa.co.ke
```

The React app is called:

```
KenWaPWA-landing-page1
```

---

## 🧰 Prerequisites:

* You’ve built the Vite app using:

  ```bash
  npm run build
  ```
* This creates a `dist/` folder with static files.
* The domain `staging.kenwpwa.co.ke` is already pointing to your VPS IP.
* You have Nginx installed:

  ```bash
  sudo apt install nginx
  ```

---

## 📁 Step 1: Move Your Build to a Web Directory

Put the built React files into a public directory:

```bash
sudo mkdir -p /var/www/staging.kenwpwa.co.ke
sudo cp -r /path/to/KenWaPWA-landing-page1/dist/* /var/www/staging.kenwpwa.co.ke/
```

---

## ⚙️ Step 2: Create a Server Block (Nginx Config)

Create a new file:

```bash
sudo nano /etc/nginx/sites-available/staging.kenwpwa.co.ke
```

Paste this config:

```nginx
server {
    listen 80;
    server_name staging.kenwpwa.co.ke;

    root /var/www/staging.kenwpwa.co.ke;
    index index.html;

    location / {
        try_files $uri /index.html;
    }
}
```

### 📎 Explanation:

* `server_name`: Tells Nginx which domain to respond to.
* `root`: Where your static files live.
* `try_files $uri /index.html;`: React uses client-side routing, so this makes sure all paths fallback to `index.html`.

---

## 🔗 Step 3: Enable the Config

Link the config to `sites-enabled`:

```bash
sudo ln -s /etc/nginx/sites-available/staging.kenwpwa.co.ke /etc/nginx/sites-enabled/
```

---

## ✅ Step 4: Test & Reload

Test Nginx:

```bash
sudo nginx -t
```

Reload if all is good:

```bash
sudo systemctl reload nginx
```

---

## 🔒 Optional: Add SSL with Let's Encrypt

Use Certbot to enable HTTPS:

```bash
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d staging.kenwpwa.co.ke
```

Done!

---

## 🧾 Summary Checklist for Deploying a React App:

1. `npm run build`
2. Copy `dist/` to `/var/www/yourdomain`
3. Create server block config under `sites-available/`
4. Symlink to `sites-enabled/`
5. Test and reload Nginx
6. (Optional) Add SSL with Certbot

---

