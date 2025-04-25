# Errors and Fixes – SIEM Lab

This document lists the main errors encountered during the SIEM Lab setup and how each was resolved.

---

## 🎯 Objective

Provide a clear reference of troubleshooting steps taken during the Elastic Stack, Beats, and Windows/Linux configuration.

---

## ❗ Error List

| Error Encountered | Probable Cause | Solution Applied |
|:------------------|:---------------|:-----------------|
| Kibana Detection Engine error ("Failed to retrieve detection engine privileges") | Missing encryption key configuration in Kibana | Added `xpack.encryptedSavedObjects.encryptionKey` in `/etc/kibana/kibana.yml` and restarted Kibana |
| No Sysmon logs arriving in Kibana | Sysmon was not installed or improperly configured | Installed Sysmon with a verified configuration file (`sysmonconfig.xml`) |
| Filebeat not ingesting `/var/log/auth.log` | Permissions issue reading auth.log | Adjusted file permissions and confirmed Filebeat input configuration |
| Windows 11 not sending Winlogbeat logs | Service not properly started or misconfigured output | Corrected `winlogbeat.yml` output settings and restarted the service |
| Windows Server AD communication issue (client could not join domain) | DNS issues and AD replication problems | Forced AD DNS synchronization with `repadmin /syncall /AdeP` and restarted DNS service |

---

## 🔧 Troubleshooting Tips

- Always check service statuses using `systemctl` or `Get-Service`.
- Review logs located at `/var/log/` (Linux) or under Winlogbeat installation path (Windows).
- Verify correct IP addressing and firewall configurations.

---

## ✅ Conclusion

Encountering and resolving issues was a critical part of building a functional, secure, and realistic SIEM environment. Troubleshooting improved the technical resilience and operational readiness of the lab setup.
