# Instalação do Filebeat e Coleta de Logs no Ubuntu

Este guia explica como configurar o Filebeat no Ubuntu Server para coletar logs importantes do sistema Linux e enviá-los para o Elastic Stack.

---

## 🎯 Objetivo

Instalar e configurar o Filebeat para coletar logs do `/var/log/auth.log`, entradas de syslog e monitorar eventos de autenticação do sistema.

---

## 🧰 Requisitos

- Ubuntu Server 22.04 (mesmo servidor que executa o Elastic Stack)
- Acesso root ou sudo
- Conexão com a internet
- Pacote Filebeat (do repositório Elastic)

---

## 🛠️ Etapa 1 – Instalar o Filebeat

Atualize os repositórios e instale o Filebeat:

```bash
sudo apt update
sudo apt install filebeat -y
```

---

## ⚙️ Etapa 2 – Configurar Inputs do Filebeat

Edite o arquivo de configuração:

```bash
sudo nano /etc/filebeat/filebeat.yml
```

Habilite e configure os seguintes inputs:

### Habilitar Input de Arquivos de Log:

```yaml
filebeat.inputs:
- type: filestream
  id: auth-log
  paths:
    - /var/log/auth.log
```

### Habilitar Syslog (opcional):

Para capturar dados de syslog de dispositivos ou serviços externos:

```yaml
filebeat.inputs:
- type: syslog
  protocol.udp:
    host: "0.0.0.0:514"
```

---

## 📦 Etapa 3 – Configurar Saída para o Elasticsearch

No mesmo `filebeat.yml`, configure a saída para seu servidor Elastic:

```yaml
output.elasticsearch:
  hosts: ["https://<ip-do-elastic>:9200"]
  username: "elastic"
  password: "<sua-senha>"
  ssl.verification_mode: none
```

> Substitua `<ip-do-elastic>` e `<sua-senha>` pelos seus valores reais.

---

## 🚀 Etapa 4 – Habilitar e Iniciar o Filebeat

Habilite e inicie o serviço do Filebeat:

```bash
sudo systemctl enable filebeat
sudo systemctl start filebeat
```

Verifique o status:

```bash
sudo systemctl status filebeat
```

---

## 🛡️ Extra: Validar a Ingestão dos Logs

No Kibana, vá em **Discover** e filtre por:
- Índice: `filebeat-*`
- Exemplos de campos: `event.dataset`, `log.file.path`

Verifique se aparecem entradas do `/var/log/auth.log`.

---

## ⚠️ Problemas comuns

- Verifique os logs do Filebeat:

```bash
sudo journalctl -u filebeat
```

- Confirme permissões de leitura no `/var/log/auth.log`
- Valide a conectividade com o Elasticsearch

---

## ✅ Próxima etapa

Continue personalizando dashboards no Kibana para visualizar eventos do sistema Linux.
