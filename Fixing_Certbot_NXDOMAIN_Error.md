# 🌐 Fixing Certbot NXDOMAIN Error for malricpharma.co.ke

When running:

```bash
sudo certbot --nginx -d malricpharma.co.ke
```

You might see this error:

```
DNS problem: NXDOMAIN looking up A/AAAA for malricpharma.co.ke
```

---

## 💥 What This Means

The domain `malricpharma.co.ke` is not found online or doesn't have DNS A/AAAA records pointing to your server.

---

## 🔍 What Certbot is Trying to Do

1. Certbot contacts Let's Encrypt to issue an SSL cert.
2. Let's Encrypt tries to look up DNS records for your domain.
3. If it can't find an A or AAAA record (IPv4 or IPv6), it gives the NXDOMAIN error.

---

## ✅ Step-by-Step Fix

### 1. **Check if the domain exists**

Run:
```bash
nslookup malricpharma.co.ke
```

If it says "NXDOMAIN" or "can't find", then your domain isn’t public yet.

---

### 2. **Add DNS Records**

Log into your domain registrar and make sure the following records exist:

- **A Record (IPv4)**:
  ```
  Host: @
  Type: A
  Value: [Your Server's Public IP]
  TTL: 300
  ```

- **AAAA Record (Optional - IPv6)**:
  ```
  Host: @
  Type: AAAA
  Value: [Your Server's IPv6]
  ```

- **Optional www subdomain**:
  ```
  Host: www
  Type: A
  Value: [Same IP]
  ```

---

### 3. **Wait for DNS Propagation**

DNS changes take a few minutes to hours.

Check with:
```bash
dig malricpharma.co.ke
```

Or use online tools like [https://dnschecker.org](https://dnschecker.org).

---

### 4. **Re-run Certbot**

Once DNS is working:
```bash
sudo certbot --nginx -d malricpharma.co.ke
```

It should now succeed.

---

## 👀 Bonus: Nginx Configuration

Make sure your Nginx server block includes:

```nginx
server {
    listen 80;
    server_name malricpharma.co.ke;
    ...
}
```

---

## 🧠 Summary

| Problem             | Fix                                      |
|---------------------|-------------------------------------------|
| No DNS record       | Add A/AAAA record pointing to your IP     |
| Wrong IP            | Update DNS to the correct server IP       |
| DNS not live yet    | Wait for propagation                      |
| Nginx not handling  | Add `server_name` to your Nginx config    |

---

This guide helps you resolve the Certbot NXDOMAIN error and successfully set up HTTPS using Let's Encrypt.
