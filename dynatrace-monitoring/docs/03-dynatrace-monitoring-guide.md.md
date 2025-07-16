# 📊 Dynatrace Monitoring Guide

This guide helps you verify that your Calendar & Calculator app running on EC2 is being monitored by Dynatrace OneAgent.

---

## ✅ Step 1: Verify Dynatrace OneAgent is Installed and Running

SSH into your EC2 instance and run:

```bash
sudo /opt/dynatrace/oneagent/agent/tools/oneagentctl --status
```

✅ Expected output:

```
OneAgent is running.
```

If the agent is not running, see the install guide (coming next).

---

## ✅ Step 2: Generate Traffic to the App

Use `curl` or visit in browser:

```bash
curl http://<ec2-ip>:3000/home
curl http://<ec2-ip>:3000/calc
```

Repeat these calls a few times to ensure Dynatrace receives traffic.

---

## ✅ Step 3: View Application in Dynatrace

1. Log in to your Dynatrace dashboard
2. Go to **"Transactions & services"** in the left panel
3. Look for a service named something like `calendar-app` or `node.js`
4. Click the service to view:

   * Response times
   * Request rates
   * Failure rates
   * Service flow
   * CPU/memory usage
   * Logs (if enabled)

---

## ✅ Step 4: Explore Additional Metrics

You can explore:

* **Host view**: See EC2 metrics like CPU, RAM, disk, and network
* **Process view**: Monitor the Node.js runtime behavior
* **Logs**: If log monitoring is enabled, see app logs in Dynatrace
* **User sessions**: If RUM is added (not covered here)

---

## ✅ Step 5: Restart PM2 App (Optional)

If Dynatrace didn’t detect the service initially, restart the app:

```bash
pm2 restart calendar-app
```

Then refresh the Dynatrace dashboard.

---

🚀 You now have real-time observability on your deployed Node.js app via Dynatrace!
