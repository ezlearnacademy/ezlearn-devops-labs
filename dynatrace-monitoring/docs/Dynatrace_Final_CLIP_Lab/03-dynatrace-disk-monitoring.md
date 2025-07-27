# 💾 Dynatrace Lab: Disk Space Monitoring for EC2

This lab helps you set up disk space monitoring for your EC2 instance that hosts a Tomcat application. You’ll learn to detect and alert on low disk space conditions using Dynatrace.

---

## ✅ Step 1: Confirm OneAgent is Monitoring Disk

On your EC2 instance, run:

```bash
sudo /opt/dynatrace/oneagent/agent/tools/oneagentctl --status
```

✅ You should see that the OneAgent is active and monitoring the system.

---

## ✅ Step 2: View Disk Metrics in Dynatrace

1. Go to the Dynatrace UI
2. Navigate to **Hosts** > Click on your EC2 host
3. Scroll down to the **Disks** section

You’ll see metrics like:

* Disk used %
* Disk read/write throughput
* Mount points and partitions

---

## ✅ Step 3: Set Disk Usage Alert Thresholds

1. Go to **Settings > Anomaly detection > Infrastructure**
2. Under **Disk**, click **Edit thresholds**
3. Set:

   * Alert if disk usage is > 90%
   * Duration: 5 minutes
4. Save

This ensures you’ll be alerted before disk exhaustion becomes critical.

---

## ✅ Step 4: Optional Manual Test

To simulate disk pressure (optional):

```bash
fallocate -l 1G tempfile1
fallocate -l 1G tempfile2
```

This will create large files to quickly consume disk.

To clean up:

```bash
rm tempfile1 tempfile2
```

---

## ✅ Step 5: View and Respond to Disk Alerts

1. Go to **Problems** in Dynatrace
2. Look for a disk space problem (if triggered)
3. Review affected services, hosts, and impact

---

🎯 You’re now successfully monitoring disk usage with automated alerts using Dynatrace!
