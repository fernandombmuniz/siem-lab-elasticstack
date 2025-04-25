# Erros e Soluções – Laboratório SIEM

Este documento lista os principais erros encontrados durante a configuração do laboratório SIEM e como cada um foi solucionado.

---

## 🎯 Objetivo

Fornecer uma referência clara dos procedimentos de troubleshooting aplicados durante a configuração do Elastic Stack, Beats e Windows/Linux.

---

## ❗ Lista de Erros

| Erro Encontrado | Causa Provável | Solução Aplicada |
|:----------------|:---------------|:-----------------|
| Erro no Detection Engine do Kibana ("Failed to retrieve detection engine privileges") | Falta da configuração da chave de criptografia no Kibana | Adicionado `xpack.encryptedSavedObjects.encryptionKey` no `/etc/kibana/kibana.yml` e reiniciado o Kibana |
| Logs do Sysmon não aparecendo no Kibana | Sysmon não instalado ou configurado incorretamente | Instalado o Sysmon com arquivo de configuração verificado (`sysmonconfig.xml`) |
| Filebeat não coletando `/var/log/auth.log` | Problema de permissão para leitura do auth.log | Ajustadas permissões de arquivo e confirmada a configuração do input do Filebeat |
| Windows 11 sem envio de logs via Winlogbeat | Serviço não iniciado corretamente ou configuração de output errada | Corrigido `winlogbeat.yml` e reiniciado o serviço |
| Problema de comunicação DNS/AD (cliente não ingressava no domínio) | Problemas de sincronização DNS no Active Directory | Forçada a sincronização com `repadmin /syncall /AdeP` e reiniciado o serviço DNS |

---

## 🔧 Dicas de Troubleshooting

- Sempre verifique o status dos serviços usando `systemctl` (Linux) ou `Get-Service` (Windows).
- Revise os logs em `/var/log/` (Linux) ou no diretório de instalação do Winlogbeat (Windows).
- Verifique a configuração de IPs e regras de firewall.

---

## ✅ Conclusão

Encontrar e resolver problemas foi uma etapa essencial para construir um ambiente SIEM funcional, seguro e realista. O troubleshooting aprimorou a resiliência técnica e a capacidade operacional do laboratório.
