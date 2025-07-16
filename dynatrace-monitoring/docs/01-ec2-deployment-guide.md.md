# 🚀 EC2 Deployment Guide

This guide walks you through deploying the Calendar & Calculator Node.js app to an AWS EC2 instance using PM2.

---

## ✅ Step 1: Launch and SSH into Your EC2 Instance

1. Launch an EC2 instance (Ubuntu 22.04 preferred).
2. Make sure you allow port **3000** in your security group.
3. Connect to your instance using SSH:

```bash
ssh -i your-key.pem ubuntu@<your-ec2-ip>
```

Replace `your-key.pem` with the path to your PEM key file, and `<your-ec2-ip>` with your instance’s public IP address.

---

## ✅ Step 2: Install Node.js and Git

```bash
sudo apt update
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs git
```

Verify the installation:

```bash
node -v
npm -v
```

---

## ✅ Step 3: Clone the GitHub Repository

Using SSH:

```bash
git clone git@github.com:ezlearnacademy/calendar-calculator-app-with-dynatrace.git
cd calendar-calculator-app-with-dynatrace
```

Or using HTTPS:

```bash
git clone https://github.com/ezlearnacademy/calendar-calculator-app-with-dynatrace.git
cd calendar-calculator-app-with-dynatrace
```

---

## ✅ Step 4: Install Node Dependencies

```bash
npm install
```

---

## ✅ Step 5: Install PM2 and Start the App

```bash
sudo npm install -g pm2
pm2 start server.js --name calendar-app
pm2 save
pm2 startup
```

When you run `pm2 startup`, it will print a command (starting with `sudo env ...`). Copy and run that command to enable PM2 on startup.

---

## ✅ Step 6: Allow Port 3000 in Security Group

In the AWS console:

* Go to **Security Groups**
* Edit **Inbound Rules**
* Add:

  * **Type:** Custom TCP
  * **Port Range:** 3000
  * **Source:** 0.0.0.0/0 *(or restrict to your IP)*

---

## ✅ Step 7: Test the Application

Open your browser and go to:

```http
http://<your-ec2-ip>:3000
```

You should see the calendar and calculator app interface.

---

## ✅ Step 8: Useful PM2 Commands

```bash
pm2 list                      # Show all PM2 processes
pm2 restart calendar-app      # Restart the app
pm2 stop calendar-app         # Stop the app
pm2 delete calendar-app       # Remove the app
```

---

✅ Done! Your app is running and ready to be monitored with Dynatrace.

