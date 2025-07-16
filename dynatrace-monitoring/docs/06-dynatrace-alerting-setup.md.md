# ⚠️ Dynatrace Alerting Setup Guide

This guide helps you configure alerts (problem notifications) in Dynatrace so you're notified when your Node.js app or EC2 instance runs into issues.

---

## ✅ Step 1: Go to Alerting Settings

1. Log into your Dynatrace dashboard
2. In the left sidebar, go to **Settings** → **Alerts** → **Problem notifications**
3. Click **Set up notifications**

---

## ✅ Step 2: Choose an Alert Channel

Choose how you want to be notified. Available channels:

* Email
* Microsoft Teams
* Slack
* Webhook (custom integrations)
* ServiceNow

Click **Add notification** and select your channel (e.g., Email)

---

## ✅ Step 3: Configure Email Alerts (Example)

If using email:

1. Select **Email**
2. Enter a name like:

   ```
   DevOps Alerts - Calendar App
   ```
3. Add one or more email addresses
4. Save

---

## ✅ Step 4: Set Up Alerting Rules (Management Zones or Tags)

You can narrow down what triggers alerts:

* **Entity tags**: Only alert if the problem is from services tagged `calendar-app` or `prod`
* **Management zones**: Apply rules to a specific zone (like `Training EC2 Hosts`)

Go to:

* **Settings** → **Anomaly detection** → choose service/host/process
* Configure thresholds or rely on automatic baseline detection

---

## ✅ Step 5: Test Your Alerts

You can generate a test alert:

```bash
sudo stress --cpu 2 --timeout 60
```

Or stop your app to see if Dynatrace detects the outage:

```bash
pm2 stop calendar-app
```

You should receive an email or Slack alert if everything is configured.

---

## ✅ Step 6: Monitor Open Problems

1. In Dynatrace, go to **Problems** from the sidebar
2. Click on a problem to view root cause, impact, and suggestions

---

🚀 You now have Dynatrace alerts set up to notify you in real-time when things go wrong!
