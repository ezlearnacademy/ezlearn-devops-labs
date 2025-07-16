# 🧠 Install Dynatrace OneAgent on EC2

This guide walks you through installing Dynatrace OneAgent on an Ubuntu EC2 instance so you can monitor your Node.js application.

---

## ✅ Step 1: Log in to Dynatrace

1. Go to your Dynatrace environment (e.g. `https://<your-env-id>.apps.dynatrace.com`)
2. In the left sidebar, click **"Deploy Dynatrace"** or **"Set up monitoring"**
3. Select **"Start installation"** under OneAgent

---

## ✅ Step 2: Select Linux as the Platform

Choose the **Linux** tab.

Dynatrace will give you a command like the one below:

```bash
wget -O Dynatrace-OneAgent.sh "https://<env-id>.live.dynatrace.com/api/v1/deployment/installer/agent/unix/default/latest?Api-Token=abc123&type=unix&arch=x86"
sudo /bin/sh Dynatrace-OneAgent.sh --set-monitoring-mode=fullstack
```

✅ Copy and save this command — it includes your download token.

---

## ✅ Step 3: SSH into EC2 and Run Installer

On your terminal:

```bash
ssh -i your-key.pem ubuntu@<your-ec2-ip>
```

Then paste and run the installer command from Step 2. Example:

```bash
wget -O Dynatrace-OneAgent.sh "https://..."
sudo /bin/sh Dynatrace-OneAgent.sh --set-monitoring-mode=fullstack
```

---

## ✅ Step 4: Verify OneAgent is Running

Run:

```bash
sudo /opt/dynatrace/oneagent/agent/tools/oneagentctl --status
```

✅ You should see:

```
OneAgent is running.
```

If not, re-check your token or installation logs.

---

## ✅ Step 5: Refresh Dynatrace Dashboard

1. Go back to your Dynatrace UI
2. Open **"Hosts"** → Your EC2 instance should now appear
3. Under **"Transactions & services"**, your app will show up once traffic starts hitting it

---

🎉 That’s it! You’ve successfully installed OneAgent and linked it to Dynatrace.
