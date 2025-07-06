---
title: Fixing GitHub SSH Error When Cloning Repo
date: 2025-07-06
description: Step-by-step guide to fix GitHub SSH authentication errors when cloning repositories, including SSH key generation, GitHub setup, and troubleshooting tips.
tags:
  [
    GitHub,
    SSH,
    Git,
    Error Fix,
    Authentication,
    Repository,
    Cloning,
    Troubleshooting,
  ]
---

# 🛠️ Fixing GitHub SSH Error When Cloning Repo

## 🧾 Error Message

When you try to clone a private repo:

```bash
git clone git@github.com:Starnoh254/PostgresBackup.git
```

And get this error:

```
ERROR: Repository not found.
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

---

## 🧠 What It Means

1. ✅ The repo **might not exist** (check for typos in the repo name or owner).
2. 🔐 You **might not have access** (e.g. trying to clone a private repo you don't own or have access to).
3. ❌ Your machine has **not shared its SSH public key with GitHub**, so GitHub blocks the connection.

---

## 🔑 Do You Add a Private or Public Key to GitHub?

- ❌ **Never** add the **private key** (`id_rsa`) to GitHub.
- ✅ You must add the **public key** (`id_rsa.pub`) to your GitHub account.

---

## ✅ Step-by-Step Fix

### 1. Check if You Already Have an SSH Key

```bash
ls ~/.ssh
```

Look for:

- `id_rsa` → private key
- `id_rsa.pub` → public key (this is the one you upload to GitHub)

If they don't exist, generate them 👇

---

### 2. Generate an SSH Key (if needed)

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

- Press `Enter` to accept the default location (`~/.ssh/id_rsa`)
- Leave the passphrase empty (or set one if you want extra security)

---

### 3. Add the Public Key to GitHub

```bash
cat ~/.ssh/id_rsa.pub
```

Copy the entire output (starts with `ssh-rsa`...).

Then go to GitHub:

1. Visit: [https://github.com/settings/keys](https://github.com/settings/keys)
2. Click **"New SSH key"**
3. Title: `VPS Key` (or any name)
4. Paste the copied key into the field
5. Click **Add SSH key**

---

### 4. Test SSH Authentication

```bash
ssh -T git@github.com
```

Expected response:

```
Hi Starnoh254! You've successfully authenticated, but GitHub does not provide shell access.
```

✅ This means your SSH key is working.

---

### 5. Clone the Repo Again

```bash
git clone git@github.com:Starnoh254/PostgresBackup.git
```

It should now work as expected 🎉

---

## 🧰 Bonus: Set Correct Permissions

Make sure your SSH files have the right permissions:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_rsa
chmod 644 ~/.ssh/id_rsa.pub
```

---

## 🧠 Final Tip

> If you're using a VPS and this is your first time setting up SSH, remember to do this **every time you start fresh on a new server**, since it won’t have your SSH keys set up by default.

---
