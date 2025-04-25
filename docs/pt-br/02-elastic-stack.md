# Instalação e Segurança do Elastic Stack – Ubuntu Server

Este guia explica como instalar e proteger o Elasticsearch e o Kibana no Ubuntu Server 22.04, que atuará como o núcleo do nosso laboratório SIEM.

---

## 🎯 Objetivo

Instalar o Elasticsearch e o Kibana com configurações básicas de segurança (criptografia TLS e autenticação), simulando um ambiente de produção.

---

## 🧰 Requisitos

- Ubuntu Server 22.04 atualizado
- Acesso root ou sudo
- Conexão com a internet
- Versão do Elastic Stack: 8.x (testado com 8.12.x)

---

## 🛠️ Etapa 1 – Adicionar o repositório APT da Elastic

Execute os comandos abaixo para adicionar o repositório oficial da Elastic e atualizar a lista de pacotes:

```bash
curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elastic-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/elastic-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list

sudo apt update
```

---

## 📦 Etapa 2 – Instalar o Elasticsearch e o Kibana

```bash
sudo apt install elasticsearch kibana -y
```

---

## 🔧 Etapa 3 – Ativar e iniciar os serviços

Habilite e inicie os serviços para que sejam executados automaticamente após reinicializações:

```bash
sudo systemctl enable elasticsearch
sudo systemctl start elasticsearch

sudo systemctl enable kibana
sudo systemctl start kibana
```

Verifique o status:

```bash
sudo systemctl status elasticsearch
sudo systemctl status kibana
```

---

## 🔐 Etapa 4 – Configurar segurança básica

O Elastic Stack 8.x já vem com segurança ativada por padrão. Você deve definir a senha do usuário `elastic`.

Redefina a senha:

```bash
sudo /usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic
```

> Salve essa senha com segurança. Você usará para acessar o Kibana.

Opcional: se for solicitado um token de registro do Kibana, gere com:

```bash
sudo /usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana
```

---

## 🌐 Etapa 5 – Acessar o Kibana

Abra o navegador e acesse:

```
https://<ip-do-servidor-ubuntu>:5601
```

Aceite o certificado autoassinado (TLS está ativado por padrão).

Credenciais:
- **Usuário**: `elastic`
- **Senha**: (a que você gerou anteriormente)

---

## 🔒 Detalhes de segurança

O Elastic Stack 8.x já inclui:
- Criptografia TLS ativada por padrão.
- Autenticação obrigatória.
- Proteção de objetos salvos via chave de criptografia.

Se necessário, configure manualmente a chave de criptografia no `/etc/kibana/kibana.yml`:

```yaml
xpack.encryptedSavedObjects.encryptionKey: "uma-string-aleatória-com-32-caracteres"
```

Depois reinicie o Kibana:

```bash
sudo systemctl restart kibana
```

---

## ⚠️ Problemas comuns

- **Erro: Detection engine do Kibana não carrega**  
  → Falta definir o `encryptionKey` no `kibana.yml`.

- **Serviço não inicia**  
  → Verifique os logs com:

```bash
sudo journalctl -u elasticsearch
sudo journalctl -u kibana
```

---
