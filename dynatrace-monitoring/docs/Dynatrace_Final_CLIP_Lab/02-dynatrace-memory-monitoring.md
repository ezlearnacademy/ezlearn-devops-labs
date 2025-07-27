# 🧠 Dynatrace Lab: Memory Monitoring for Tomcat App

This lab helps you set up memory monitoring for your Tomcat-hosted Java application running on EC2 and detect when memory usage gets high.

---

## ✅ Step 1: Confirm Dynatrace OneAgent Is Installed

SSH into your EC2 instance and run:

```bash
sudo /opt/dynatrace/oneagent/agent/tools/oneagentctl --status
```

✅ You should see:

```
OneAgent is running.
```

---

## ✅ Step 2: View Memory Metrics for Your EC2 Host

1. Go to your Dynatrace dashboard
2. Navigate to **Hosts** → Select your EC2 instance
3. Scroll to the **Memory** section

Key metrics:

* **Memory usage %**
* **Used memory (bytes)**
* **Page faults / Swap usage** (optional)

---

## ✅ Step 3: View Memory Usage for Tomcat Process

1. In the same host view, scroll to **Processes**
2. Find and click the `java` process (associated with Tomcat)
3. Review:

   * JVM heap usage
   * Non-heap memory
   * Garbage collection stats

---

## ✅ Step 4: Create a Memory Alert

1. Go to **Settings > Anomaly detection > Infrastructure**
2. Under **Memory**, click **Edit thresholds**
3. Set:

   * Trigger alert if memory usage is > 90%
   * Duration: 5 minutes
4. Save changes

Dynatrace will now alert you if memory is consistently high.

---

## ✅ Step 5: Optional Synthetic Stress Test

Use this optional tool to simulate memory pressure:

```bash
sudo apt install stress
stress --vm 1 --vm-bytes 512M --timeout 60
```

Monitor your dashboard and verify the alert triggers.

---

🎯 You’re now monitoring memory usage for your Tomcat service and host with automatic alerts in Dynatrace.
