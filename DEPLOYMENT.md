# Deployment Instructions - whoisandrewfox.com

## Server Details
- **Server IP**: 66.228.35.159
- **Domain**: whoisandrewfox.com
- **DNS**: Cloudflare
- **Web Server**: Nginx on Linode

## 1. Cloudflare DNS Setup

Log into Cloudflare and add the following DNS records:

```
Type: A
Name: @
Content: 66.228.35.159
Proxy: Enabled (orange cloud)
TTL: Auto

Type: A
Name: www
Content: 66.228.35.159
Proxy: Enabled (orange cloud)
TTL: Auto
```

## 2. Server Deployment

SSH into the Linode server:
```bash
ssh root@66.228.35.159
```

Create the web directory:
```bash
mkdir -p /var/www/whoisandrewfox.com
```

Copy nginx configuration:
```bash
# From local machine:
scp nginx-whoisandrewfox.conf root@66.228.35.159:/etc/nginx/sites-available/whoisandrewfox.com
```

Enable the site:
```bash
# On server:
sudo ln -s /etc/nginx/sites-available/whoisandrewfox.com /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

## 3. Deploy Site Files

From your local machine:
```bash
cd ~/sites/whoisandrewfox.com
rsync -avz --exclude '.git' --exclude 'nginx-*.conf' --exclude '*.md' \
  ./ root@66.228.35.159:/var/www/whoisandrewfox.com/
```

## 4. SSL Certificate (Optional but Recommended)

On the server, install Let's Encrypt SSL:
```bash
sudo certbot --nginx -d whoisandrewfox.com -d www.whoisandrewfox.com
```

Certbot will automatically update the nginx configuration for HTTPS.

## 5. Update Workflow

After making local changes:
```bash
cd ~/sites/whoisandrewfox.com
git add .
git commit -m "Update portfolio"
git push
rsync -avz --exclude '.git' --exclude 'nginx-*.conf' --exclude '*.md' \
  ./ root@66.228.35.159:/var/www/whoisandrewfox.com/
```

## Verification

1. DNS propagation: `dig whoisandrewfox.com`
2. Site accessibility: Visit http://whoisandrewfox.com
3. Nginx status: `sudo systemctl status nginx`
4. Nginx logs: `sudo tail -f /var/log/nginx/whoisandrewfox.com-access.log`
