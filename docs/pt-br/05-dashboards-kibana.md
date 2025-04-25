# Criação de Dashboards no Kibana – Visualizando Eventos de Segurança

Este guia explica como criar dashboards personalizados no Kibana para monitorar eventos de segurança coletados dos sistemas Windows e Ubuntu.

---

## 🎯 Objetivo

Construir dashboards visuais no Kibana para monitorar atividades do sistema, eventos de autenticação e comportamentos de endpoints com base nos logs coletados.

---

## 🧰 Requisitos

- Elastic Stack operacional (Elasticsearch + Kibana)
- Logs sendo recebidos corretamente (Winlogbeat, Sysmon, Filebeat)
- Acesso ao Kibana com usuário elastic ou permissões suficientes

---

## 🛠️ Etapa 1 – Acessar a Área de Dashboards

1. Abra o Kibana no navegador:

```
https://<ip-do-servidor-ubuntu>:5601
```

2. Faça login com suas credenciais do usuário `elastic`.
3. Navegue até **Analytics → Dashboards**.

---

## 🎨 Etapa 2 – Criar um Novo Dashboard

1. Clique em **Create dashboard**.
2. Clique em **Create new visualization**.
3. Escolha **Lens** (recomendado para maior flexibilidade).

---

## 📈 Etapa 3 – Exemplos de Visualizações

### Exemplo 1: Resultados de Autenticação – Ubuntu Server

- Padrão de índice: `filebeat-*`
- Tipo de visualização: Gráfico de Pizza
- Dimensões:
  - Fatias por: `event.outcome` (Success/Failure)
- Filtros:
  - `log.file.path` contém `/var/log/auth.log`

---

### Exemplo 2: Principais IDs de Eventos – Windows Server

- Padrão de índice: `winlogbeat-*`
- Tipo de visualização: Gráfico de Barras
- Eixo X: `event.code`
- Eixo Y: Contagem
- Filtros:
  - `host.name` correspondente ao seu Windows Server

---

### Exemplo 3: Criação de Processos – Windows 11

- Padrão de índice: `winlogbeat-*`
- Tipo de visualização: Tabela de Dados
- Campos:
  - `process.name`
  - `process.executable`
- Filtros:
  - `event.code` igual a `1`
  - `host.name` correspondente ao seu Windows 11 Client

---

## 📋 Etapa 4 – Boas Práticas para Dashboards

- Nomeie cada dashboard de forma clara (ex: **Windows Server – Monitoramento AD**, **Ubuntu Server – Logs de Autenticação**).
- Agrupe visualizações logicamente por sistema ou tipo de evento.
- Utilize filtros de tempo (Últimas 24 horas, Últimos 7 dias) para análises recentes.

---

## 🔥 Extra: Criar Pesquisas Salvas

Crie Saved Searches no Discover do Kibana para consultas comuns, como:
- Tentativas de login falhadas
- Autenticações de domínio bem-sucedidas
- Processos iniciados de caminhos suspeitos

---

## ✅ Próxima etapa

Revise seus dashboards regularmente e ajuste as visualizações conforme as tendências e eventos observados em seu ambiente de laboratório.
