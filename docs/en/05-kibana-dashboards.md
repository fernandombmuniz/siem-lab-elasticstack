# Creating Dashboards in Kibana – Visualizing Security Events

This guide explains how to create custom dashboards in Kibana to monitor security events collected from Windows and Ubuntu systems.

---

## 🎯 Objective

Build visual dashboards in Kibana to monitor system activities, authentication events, and endpoint behaviors based on collected logs.

---

## 🧰 Requirements

- Elastic Stack operational (Elasticsearch + Kibana)
- Logs arriving correctly (Winlogbeat, Sysmon, Filebeat)
- Access to Kibana with elastic user or sufficient privileges

---

## 🛠️ Step 1 – Access Kibana Dashboards

1. Open Kibana on your browser:

```
https://<your-ubuntu-server-ip>:5601
```

2. Login with your `elastic` user credentials.
3. Navigate to **Analytics → Dashboards**.

---

## 🎨 Step 2 – Create a New Dashboard

1. Click on **Create dashboard**.
2. Click **Create new visualization**.
3. Choose **Lens** (recommended for flexible design).

---

## 📈 Step 3 – Examples of Visualizations

### Example 1: Authentication Results – Ubuntu Server

- Index pattern: `filebeat-*`
- Visualization type: Pie Chart
- Dimensions:
  - Slice by: `event.outcome` (Success/Failure)
- Filters:
  - `log.file.path` contains `/var/log/auth.log`

---

### Example 2: Top Event IDs – Windows Server

- Index pattern: `winlogbeat-*`
- Visualization type: Bar Chart
- X-axis: `event.code`
- Y-axis: Count
- Filters:
  - `host.name` matches your Windows Server

---

### Example 3: Sysmon Process Creations – Windows 11

- Index pattern: `winlogbeat-*`
- Visualization type: Data Table
- Fields:
  - `process.name`
  - `process.executable`
- Filters:
  - `event.code` equals `1`
  - `host.name` matches your Windows 11 Client

---

## 📋 Step 4 – Dashboard Best Practices

- Name each dashboard clearly (e.g., **Windows Server – AD Monitoring**, **Ubuntu Server – Authentication Logs**).
- Group visualizations logically by system or type of event.
- Use time filters (Last 24 hours, Last 7 days) to maintain focus.

---

## 🔥 Extra: Create Saved Searches

Create Saved Searches in Kibana Discover to quickly filter common queries, like:
- Failed logins
- Successful domain authentications
- Process creations from suspicious paths

---

## ✅ Next Step

Regularly review dashboards and adapt visualizations to reflect the security posture and event trends in your lab environment.
