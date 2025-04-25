# Elastic Stack Installation and Security – Ubuntu Server

This guide explains how to install and secure Elasticsearch and Kibana on Ubuntu Server 22.04, which will serve as the core of our SIEM lab.

---

## 🎯 Objective

Install Elasticsearch and Kibana with basic security settings (TLS encryption and user authentication) to simulate a production environment.

---

## 🧰 Requirements

- Ubuntu Server 22.04 (updated)
- Root or sudo access
- Internet connection
- Elastic Stack version 8.x (tested with 8.12.x)

---

## 🛠️ Step 1 – Add Elastic APT Repository

Run the following commands to add Elastic's official repository and update the package list:

```bash
curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elastic-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/elastic-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list

sudo apt update
```

---

## 📦 Step 2 – Install Elasticsearch and Kibana

```bash
sudo apt install elasticsearch kibana -y
```

---

## 🔧 Step 3 – Enable and Start Services

Enable and start Elasticsearch and Kibana so they persist after reboots:

```bash
sudo systemctl enable elasticsearch
sudo systemctl start elasticsearch

sudo systemctl enable kibana
sudo systemctl start kibana
```

Check their status:

```bash
sudo systemctl status elasticsearch
sudo systemctl status kibana
```

---

## 🔐 Step 4 – Set Built-in Security

Elastic Stack 8.x comes with security features enabled by default. You must set the password for the `elastic` user.

Reset the password:

```bash
sudo /usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic
```

> Save this password securely — it is required to log into Kibana.

Optional (only if needed): create Kibana enrollment token:

```bash
sudo /usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana
```

---

## 🌐 Step 5 – Access Kibana

In your browser, go to:

```
https://<your-ubuntu-server-ip>:5601
```

Accept the self-signed certificate warning.

Login with:
- **Username**: `elastic`
- **Password**: (the one you generated)

---

## 🔒 Security Notes

Elastic Stack 8.x includes:
- TLS enabled by default
- Built-in user authentication
- Encrypted saved objects

If needed, set your encryption key in `/etc/kibana/kibana.yml`:

```yaml
xpack.encryptedSavedObjects.encryptionKey: "your-32-character-random-string"
```

Restart Kibana:

```bash
sudo systemctl restart kibana
```

---

## ⚠️ Common Issues

- **Kibana detection engine error**:  
  → Usually caused by missing `encryptionKey` in `kibana.yml`.

- **Services fail to start**:  
  → Check logs using:

```bash
sudo journalctl -u elasticsearch
sudo journalctl -u kibana
```

---

## ✅ Next Step

Continue to [03 – Winlogbeat and Sysmon on Windows](03-winlogbeat-sysmon.md) to start collecting Windows event logs.
