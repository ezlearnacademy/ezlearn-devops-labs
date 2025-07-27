# 🔁 Dynatrace CLIP Lab: Synthetic Monitoring with Auto-Remediation

This lab walks you through setting up a **Closed-Loop Incident Process (CLIP)** using Dynatrace synthetic monitoring, webhook alerting, and automatic remediation on an EC2 instance.

Your target: **[http://ezlearn.mitechnology.org:8080](http://ezlearn.mitechnology.org:8080)** (a live Tomcat web app)

---

## ✅ Step 1: Deploy and Monitor Your App

Make sure your Tomcat-based Java web application is deployed and being monitored by Dynatrace (OneAgent installed).

For this lab, we’ll test:

```http
http://ezlearn.mitechnology.org:8080
```

---

## ✅ Step 2: Create Synthetic Monitor in Dynatrace

1. Go to **Synthetic Monitoring > Create a monitor**
2. Choose **HTTP monitor**
3. URL to monitor:

   ```
   http://ezlearn.mitechnology.org:8080
   ```
4. Set check frequency to **1 minute**
5. Add at least one location (e.g., AWS US-East)
6. Save and deploy

---

## ✅ Step 3: Create Auto-Remediation Webhook Receiver on EC2

### A. Create script: `restart-tomcat.sh`

```bash
#!/bin/bash
sudo systemctl restart tomcat
```

Make it executable:

```bash
chmod +x restart-tomcat.sh
```

### B. Create simple webhook listener: `webhook-server.js`

```js
const express = require('express');
const { exec } = require('child_process');
const app = express();
app.use(express.json());

app.post('/dynatrace-webhook', (req, res) => {
  console.log('Webhook received:', req.body);
  exec('./restart-tomcat.sh', (error, stdout, stderr) => {
    if (error) {
      console.error(`Error: ${error.message}`);
      return res.status(500).send('Failed');
    }
    console.log(`Output: ${stdout}`);
    res.send('Remediation triggered');
  });
});

app.listen(4000, () => console.log('Webhook server on port 4000'));
```

### C. Run the server

```bash
node webhook-server.js
```

Ensure port 4000 is open in your EC2 security group.

---

## ✅ Step 4: Configure Dynatrace Problem Notification

1. Go to **Settings > Integration > Problem notifications**
2. Click **Add notification**
3. Choose **Custom webhook**
4. URL:

```http
http://<your-ec2-ip>:4000/dynatrace-webhook
```

5. Use default payload or customize if needed
6. Save

---

## ✅ Step 5: Test the CLIP Flow

1. Stop Tomcat to simulate failure:

```bash
sudo systemctl stop tomcat
```

2. Wait for the synthetic monitor to detect failure
3. Dynatrace sends webhook to EC2
4. EC2 runs `restart-tomcat.sh`
5. Tomcat is restarted, Dynatrace closes problem automatically

---

🎉 You’ve successfully implemented a full CLIP: detection, alert, and auto-remediation!
