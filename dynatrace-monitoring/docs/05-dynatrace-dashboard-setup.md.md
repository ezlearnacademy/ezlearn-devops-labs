# 🌎 Dynatrace Dashboard Setup Guide

This guide walks you through creating a custom Dynatrace dashboard to visualize performance metrics for your EC2-hosted Node.js application.

---

## ✅ Step 1: Access Dashboards

1. Log into your Dynatrace environment
2. In the left sidebar, click **Dashboards**
3. Click **Create dashboard** and give it a name like:

   ```
   Calendar App Monitoring
   ```

---

## ✅ Step 2: Add Key Widgets

Click **Add tile** and choose the following widgets:

### 1. **CPU Usage (Host)**

* Category: **Host metrics**
* Metric: `CPU usage %`
* Filter: Select your EC2 instance

### 2. **Memory Usage (Host)**

* Metric: `Memory used %`
* Filter by your EC2 instance

### 3. **Response Time (Service)**

* Category: **Service metrics**
* Metric: `Response time`
* Filter: Select `calendar-app` or your Node.js service

### 4. **Request Count (Service)**

* Metric: `Request count`

### 5. **Error Rate (Service)**

* Metric: `Failure rate`

---

## ✅ Step 3: Customize Layout

* Resize and arrange tiles for readability
* Add sections: **Infrastructure**, **Service Metrics**, etc.
* Rename each tile clearly (e.g., "App Response Time", "Host CPU Usage")

---

## ✅ Step 4: Save and Share

* Click **Save** after adding all widgets
* To share: click **Share dashboard** → Copy link or grant access to specific users/teams

---

## ✅ Step 5: Add Dashboard to Favorites (Optional)

Pin your dashboard to the sidebar for quick access:

1. Click the three dots on the dashboard
2. Select **Pin to menu**

---

🚀 You now have a live dashboard giving you real-time visibility into your Node.js app and EC2 instance!
