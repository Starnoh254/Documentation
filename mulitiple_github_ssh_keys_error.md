---
title: Managing Multiple GitHub SSH Keys & Accounts
date: 2025-07-06
description: Complete guide to managing multiple GitHub accounts on one machine using SSH config, including setup, troubleshooting, and best practices for avoiding authentication conflicts.
tags:
  [
    GitHub,
    SSH,
    Multiple Accounts,
    Authentication,
    Git,
    SSH Config,
    Troubleshooting,
  ]
---

# 🛠️ Managing Multiple GitHub SSH Keys & Accounts

## 📌 Problem

When using multiple GitHub accounts (e.g., **personal** and **work**) on the same machine, you might encounter issues like:

- `Permission denied (publickey)`
- Git using the wrong account
- Error when running: `ssh -T git@github.com`

This happens because Git/SSH doesn't know which key to use if multiple are available.

---

## 🧪 Reproducing the Issue

You might see this error:

```bash
$ ssh -T git@github.com
Hi someone_else! You've successfully authenticated, but GitHub does not provide shell access.
```

Or:

```bash
Permission denied (publickey).
```

This means Git used the **wrong SSH key** — often the first one it finds in `~/.ssh/`.

---

## ✅ Solution: Use SSH Config

Create or edit the `~/.ssh/config` file:

```bash
nano ~/.ssh/config
```

### Example Configuration

```ini
# Personal GitHub Account
Host github-personal
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_personal

# Work GitHub Account
Host github-work
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_work
```

Save and close the file.

---

## 🎯 How to Use

### Cloning Repos

Use the custom `Host` instead of `github.com`:

```bash
# For personal projects
git clone git@github-personal:YourUsername/repo.git

# For work projects
git clone git@github-work:WorkUsername/repo.git
```

This tells SSH which key to use.

---

## 🔍 Testing Which Key Is Used

Run:

```bash
ssh -T git@github-personal
```

or

```bash
ssh -T git@github-work
```

If everything is working, you’ll see:

```bash
Hi YourUsername! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## 🧼 Notes

- Do **not** use the default `git@github.com` for both accounts.
- Always reference `github-personal` or `github-work` in remote URLs.
- You can edit the `.git/config` in any project if you forget:

```ini
[remote "origin"]
  url = git@github-personal:YourUsername/repo.git
```

---

## 📁 Where to Put Your Keys

- `~/.ssh/id_rsa_personal`
- `~/.ssh/id_rsa_work`

Make sure to **add the public keys** (`.pub`) to the correct GitHub account under **Settings > SSH and GPG keys**.

---

## 🧠 Summary

| Task                   | Command / Tip                           |
| ---------------------- | --------------------------------------- |
| Test which key is used | `ssh -T git@github-work`                |
| Add key to GitHub      | Use the **public** key (`.pub`)         |
| Avoid key conflict     | Use `~/.ssh/config` and different hosts |
| Clone properly         | Use `git@github-work:User/repo.git`     |
