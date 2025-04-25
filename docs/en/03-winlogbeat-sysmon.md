# Winlogbeat and Sysmon Installation – Windows Server and Windows 11

This guide explains how to configure advanced log collection in Windows using Sysmon and Winlogbeat, sending events to the Elastic Stack.

---

## 🎯 Objective

Install Sysmon to generate detailed event logs and configure Winlogbeat to collect and forward those logs to Elasticsearch.

---

## 🧰 Requirements

- Windows Server (AD) and Windows 11 Client
- Access to PowerShell as Administrator
- IP and port of your Elastic Stack server
- Downloaded:
  - [Sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)
  - [Winlogbeat](https://www.elastic.co/downloads/beats/winlogbeat)

---

## 🛠️ Step 1 – Install Sysmon

1. Download `Sysmon.zip` and extract it.
2. Download a recommended config file (e.g., from [SwiftOnSecurity/sysmon-config](https://github.com/SwiftOnSecurity/sysmon-config)).
3. Open PowerShell as Administrator and run:

```powershell
.\Sysmon64.exe -accepteula -i sysmonconfig.xml
```

> Replace `sysmonconfig.xml` with the path to your config file.

To verify installation:

```powershell
Get-Service Sysmon
```

---

## 📦 Step 2 – Install Winlogbeat

1. Download and extract Winlogbeat.
2. Run the PowerShell installer:

```powershell
.\install-service-winlogbeat.ps1
```

---

## ⚙️ Step 3 – Configure Winlogbeat to Send Logs

Edit the file `winlogbeat.yml` and update these sections:

### Elasticsearch Output:

```yaml
output.elasticsearch:
  hosts: ["https://<your-elastic-ip>:9200"]
  username: "elastic"
  password: "<your-password>"
  ssl.verification_mode: none
```

> Replace `<your-elastic-ip>` and `<your-password>` with your actual values.

### Event Logs to Collect:

```yaml
winlogbeat.event_logs:
  - name: Security
  - name: System
  - name: Application
  - name: Microsoft-Windows-Sysmon/Operational
```

---

## 🚀 Step 4 – Start Winlogbeat

After editing the config:

```powershell
Start-Service winlogbeat
```

To verify it's running:

```powershell
Get-Service winlogbeat
```

You should now see logs arriving in Kibana under `Discover`.

---

## 🛡️ Extra: Validate Sysmon Event Generation

Trigger basic activity like file creations, process executions, or PowerShell commands.

Search in Kibana Discover:
- Index: `winlogbeat-*`
- Field: `event.code`
- Common codes:
  - `1` – Process creation
  - `3` – Network connection
  - `11` – File created

---

## ⚠️ Troubleshooting

- Check logs at: `C:\Program Files\Winlogbeat\logs\winlogbeat`
- Ensure time/date on Windows is correct
- Check Windows Firewall rules
- Verify TLS and password are correct

---

## ✅ Next Step

Repeat this process for all Windows systems and proceed to create custom visualizations in Kibana. Next: [04 – Filebeat and Ubuntu logs](04-filebeat-ubuntu.md).
