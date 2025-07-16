# 📂 Dynatrace Log Monitoring Setup

This guide walks you through enabling log monitoring for your Node.js app using Dynatrace on an EC2 instance.

---

## ✅ Step 1: Confirm Log Monitoring is Enabled in OneAgent

1. On your EC2 instance, run:

```bash
sudo /opt/dynatrace/oneagent/agent/tools/oneagentctl --list-configuration | grep log
```

2. If log monitoring is disabled, enable it with:

```bash
sudo /opt/dynatrace/oneagent/agent/tools/oneagentctl --set-app-log-content-access=true
```

3. Restart OneAgent:

```bash
sudo systemctl restart oneagent
```

---

## ✅ Step 2: Identify Your App Logs

By default, Node.js logs using `console.log()` go to the terminal. To persist logs:

### Option 1: PM2 Log Files

If you're using PM2:

```bash
pm2 logs calendar-app
```

PM2 stores logs here:

```bash
~/.pm2/logs/calendar-app-out.log
~/.pm2/logs/calendar-app-error.log
```

### Option 2: Custom Log Files

You can also configure your Node.js app to write logs to `/var/log/app.log` or another location.

---

## ✅ Step 3: Add Log Files to Dynatrace Monitoring

1. In Dynatrace, go to **Settings > Log Monitoring > Log sources**
2. Click **Add log path**
3. Add:

   ```
   /home/ubuntu/.pm2/logs/*.log
   ```

   Or another custom path
4. Save

---

## ✅ Step 4: View Logs in Dynatrace

1. Go to **Logs** in the left sidebar
2. Filter by your EC2 host or app name
3. Search logs using keywords, timestamps, or error types

---

## ✅ Step 5: Set Up Log Alerts (Optional)

You can create alerts when certain log patterns appear:

1. Go to **Settings > Log Monitoring > Log Events**
2. Define rules like:

   * Text contains: `Error` or `Exception`
   * Severity: High
3. Set actions like sending an email or alerting a team

---

📊 You now have full visibility into logs from your Node.js app through Dynatrace!
