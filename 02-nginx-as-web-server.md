Section 2: NGINX as a Web Server

Goal

Learn how to use NGINX to serve static content such as HTML, CSS, JavaScript, and images — a foundational skill for DevOps and Cloud Engineers.

---

 What is a Web Server?

A **web server** is software that serves static files (like `.html`, `.css`, `.js`, `.png`) over HTTP.  
When users visit your website, the web server responds with these files.

NGINX is one of the fastest and most popular web servers used for this purpose.

---

 Default Web Root in Linux

| Directory  |           

/etc/nginx/nginx.conf        Main configuration file
/etc/nginx/sites-available/  Stores virtual host (server block) configs
/etc/nginx/sites-enabled/    Symlinks to active site configs
/var/www/html                Default web root directory
/var/log/nginx/              Contains access and error logs

---

Anatomy of a Basic `server` Block

```nginx
server {
    listen 80;
    server_name localhost;

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

### Breakdown:
- `listen 80;` → Listens on HTTP port 80
- `server_name localhost;` → Domain or IP to respond to
- `root` → Path where NGINX looks for files
- `index` → Default file to serve (usually index.html)
- `location /` → URL path handling

---

## Common Errors & Fixes

| Error                             | Solution                                 |
|----------------------------------|------------------------------------------|
| 403 Forbidden                    | Check file permissions (use `chmod`/`chown`) |
| 404 Not Found                    | Ensure correct `root` or `alias`         |
| NGINX not reloading changes     | Use `sudo nginx -s reload` or restart NGINX |
| Port already in use             | Use `sudo lsof -i :80` to identify process |

---

##  Summary

- NGINX can serve static files efficiently.
- The `root` and `index` directives define where and what to serve.
- Use Docker volumes to serve files without touching the host filesystem.
- Always reload NGINX after making config changes.

---
