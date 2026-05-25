# Static Website Deployment On Custome Port 81 using Nginx Webserver (Spotify Clone)

## Overview
This documentation provides a step-by-step guide to deploy a static website on an AWS EC2 instance using:
- Amazon Linux
- Nginx Web Server
- Custom Port: 81
- Static Website (Spotify Clone) Files

## System Architecture

![AD](<AD.png>) 

## Step 1: Launch EC2 Instance

1. Go to AWS Console → EC2
2. Click **Launch Instance** then give a name to instance
3. Choose:
   - AMI: Amazon Linux 
   - Instance Type: t3.micro (Free Tier)
4. Configure Security Group:
   - Allow SSH (22)
   - Allow Custom TCP (Port 81)
5. Launch and download key pair (.pem)

## Step 2: Connect to EC2

open git bash in your workspace where the .pem key is present

```bash
ssh -i your-key.pem ec2-user@your-public-ip
```

## Step 3: Install Nginx

```bash
sudo yum update
sudo yum install nginx -y
```

Start Nginx:
```bash
sudo systemctl start nginx
sudo systemctl enable nginx
sudo systemctl status nginx
```

## Step 4: Configure Nginx on Port 81

Edit config file:

```bash
sudo cd /etc/nginx/
sudo vim nginx.conf
```

Find:
```
listen       80;
```

Change to:
```
listen       81;
```

Save and restart the server:

```bash
sudo systemctl restart nginx
```

## Step 5: Move Your Spotify Clone Website Files into /html folder

Move your static website files (`index.html`, `style.css`, and `script.js`) into the Nginx web directory.

```bash
cd /usr/share/nginx/html

# Remove default Nginx files
sudo rm -rf *

# Create your HTML, CSS, and JS files
sudo vim index.html
sudo vim style.css
sudo vim script.js
```

Paste your Spotify Clone code into the respective files and save them.

Example project structure:

```bash
/usr/share/nginx/html/
│── index.html
│── style.css
└── script.js
```

## Step 6: Update Security Group

Ensure EC2 Security Group allows:
- Port 81 (Custom TCP)

## Step 7: Access Website

Open incognito tab in browser:
```
http://your-public-ip:81
```

![Output](<Screenshot 2026-04-29 135032.png>)
<br> 

## Conclusion

You have successfully deployed a static website (Spotify Clone)  on AWS EC2 using Nginx on a custom port (81).

---
