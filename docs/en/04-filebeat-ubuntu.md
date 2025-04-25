# Filebeat Installation and Ubuntu Log Collection

This guide explains how to configure Filebeat on Ubuntu Server to collect important Linux system logs and send them to the Elastic Stack.

---

## 🎯 Objective

Install and configure Filebeat to collect logs from `/var/log/auth.log`, syslog entries, and monitor system authentication events.

---

## 🧰 Requirements

- Ubuntu Server 22.04 (same server running Elastic Stack)
- Root or sudo access
- Internet connection
- Filebeat package (from Elastic repository)

---

## 🛠️ Step 1 – Install Filebeat

Update the repositories and install Filebeat:

```bash
sudo apt update
sudo apt install filebeat -y
```

---

## ⚙️ Step 2 – Configure Filebeat Inputs

Edit the Filebeat configuration file:

```bash
sudo nano /etc/filebeat/filebeat.yml
```

Enable and configure these inputs:

### Enable Log Files Input:

```yaml
filebeat.inputs:
- type: filestream
  id: auth-log
  paths:
    - /var/log/auth.log
```

### Enable Syslog (optional):

To capture syslog data from external devices or services, you can also add:

```yaml
filebeat.inputs:
- type: syslog
  protocol.udp:
    host: "0.0.0.0:514"
```

---

## 📦 Step 3 – Configure Elasticsearch Output

In the same `filebeat.yml`, configure the output to your Elastic Stack server:

```yaml
output.elasticsearch:
  hosts: ["https://<your-elastic-ip>:9200"]
  username: "elastic"
  password: "<your-password>"
  ssl.verification_mode: none
```

> Replace `<your-elastic-ip>` and `<your-password>` with your actual values.

---

## 🚀 Step 4 – Enable and Start Filebeat

Enable and start the Filebeat service:

```bash
sudo systemctl enable filebeat
sudo systemctl start filebeat
```

Verify the status:

```bash
sudo systemctl status filebeat
```

---

## 🛡️ Extra: Validate Log Ingestion

On Kibana, go to **Discover** and filter by:
- Index: `filebeat-*`
- Field examples: `event.dataset`, `log.file.path`

Check if you see entries from `/var/log/auth.log`.

---

## ⚠️ Troubleshooting

- Check Filebeat logs:

```bash
sudo journalctl -u filebeat
```

- Confirm file permissions to read `/var/log/auth.log`
- Validate network connectivity to Elasticsearch

---

## ✅ Next Step

Continue to customize dashboards in Kibana to visualize Linux system events.
