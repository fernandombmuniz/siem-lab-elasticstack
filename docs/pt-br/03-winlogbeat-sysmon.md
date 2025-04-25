# Instalação do Winlogbeat e Sysmon – Windows Server e Windows 11

Este guia explica como configurar a coleta avançada de logs no Windows utilizando Sysmon e Winlogbeat, enviando eventos para o Elastic Stack.

---

## 🎯 Objetivo

Instalar o Sysmon para gerar eventos de segurança detalhados e configurar o Winlogbeat para coletar e encaminhar esses logs para o Elasticsearch.

---

## 🧰 Requisitos

- Windows Server (AD) e Windows 11 Client
- Acesso ao PowerShell como Administrador
- IP e porta do seu servidor Elastic Stack
- Downloads necessários:
  - [Sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)
  - [Winlogbeat](https://www.elastic.co/downloads/beats/winlogbeat)

---

## 🛠️ Etapa 1 – Instalar o Sysmon

1. Baixe o `Sysmon.zip` e extraia o conteúdo.
2. Faça o download de um arquivo de configuração recomendado (exemplo: [SwiftOnSecurity/sysmon-config](https://github.com/SwiftOnSecurity/sysmon-config)).
3. Abra o PowerShell como Administrador e execute:

```powershell
.\Sysmon64.exe -accepteula -i sysmonconfig.xml
```

> Substitua `sysmonconfig.xml` pelo caminho do seu arquivo de configuração.

Para verificar se o Sysmon foi instalado:

```powershell
Get-Service Sysmon
```

---

## 📦 Etapa 2 – Instalar o Winlogbeat

1. Baixe e extraia o Winlogbeat.
2. Execute o instalador via PowerShell:

```powershell
.\install-service-winlogbeat.ps1
```

---

## ⚙️ Etapa 3 – Configurar o Winlogbeat para enviar logs

Edite o arquivo `winlogbeat.yml` e atualize as seguintes seções:

### Saída para o Elasticsearch:

```yaml
output.elasticsearch:
  hosts: ["https://<ip-do-elastic>:9200"]
  username: "elastic"
  password: "<sua-senha>"
  ssl.verification_mode: none
```

> Substitua `<ip-do-elastic>` e `<sua-senha>` com os seus valores reais.

### Logs a serem coletados:

```yaml
winlogbeat.event_logs:
  - name: Security
  - name: System
  - name: Application
  - name: Microsoft-Windows-Sysmon/Operational
```

---

## 🚀 Etapa 4 – Iniciar o Winlogbeat

Após editar a configuração:

```powershell
Start-Service winlogbeat
```

Para verificar o status do serviço:

```powershell
Get-Service winlogbeat
```

Você deverá começar a ver os eventos chegando no Kibana (em Discover).

---

## 🛡️ Extra: Validar a geração de eventos do Sysmon

Realize atividades básicas como criação de arquivos, execuções de processos ou comandos no PowerShell.

No Kibana Discover:
- Índice: `winlogbeat-*`
- Campo: `event.code`
- Códigos comuns:
  - `1` – Criação de processo
  - `3` – Conexão de rede
  - `11` – Criação de arquivo

---

## ⚠️ Problemas comuns

- Verifique os logs do Winlogbeat em: `C:\Program Files\Winlogbeat\logs\winlogbeat`
- Confirme se a hora/data do sistema estão corretas
- Verifique as regras do Firewall do Windows
- Certifique-se de que a configuração de TLS e senha estão corretas

---

## ✅ Próxima etapa

Repita este processo em todas as máquinas Windows do laboratório e prossiga para criar visualizações personalizadas no Kibana.  
Próximo guia: [04 – Coleta de logs no Ubuntu com Filebeat](04-filebeat-ubuntu.md).
