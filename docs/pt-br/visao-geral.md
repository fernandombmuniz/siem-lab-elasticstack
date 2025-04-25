# Visão Geral do Projeto – Laboratório SIEM com Elastic Stack

Este documento apresenta uma visão geral do projeto de Laboratório SIEM, incluindo seus objetivos, estrutura e componentes utilizados.

---

## 🎯 Objetivo do Projeto

Criar um laboratório funcional e seguro de SIEM (Gerenciamento de Informações e Eventos de Segurança) utilizando Elastic Stack e Beats, simulando a coleta de logs, monitoramento e detecção em um ambiente realista.

---

## 🧰 Tecnologias Utilizadas

- **Elastic Stack (Elasticsearch + Kibana)**
- **Winlogbeat** (Coleta de eventos do Windows)
- **Filebeat** (Coleta de logs do Linux)
- **Sysmon** (Geração de eventos avançados no Windows)
- **Ubuntu Server 22.04** (Servidor do Elastic Stack)
- **Windows Server 2019** (Serviços de Domínio Active Directory + DNS)
- **Windows 11 Client** (Endpoint membro do domínio)
- **pfSense** (Planejado – Firewall e coleta de logs de rede)

---

## 🛠️ Topologia do Laboratório

[Windows Server 2019]  →  [Ubuntu Server 22.04]  →  [Windows 11 Client]  
   (AD + DNS)              (Elastic Stack)           (Membro do Domínio)  

                             ↓  
               [Opcional: Firewall pfSense]

---

## 🔐 Recursos de Segurança Implementados

- Criptografia TLS entre os componentes do Elastic
- Autenticação de usuários no Kibana e Elasticsearch
- Objetos salvos criptografados com chave personalizada

---

## 📚 Estrutura da Documentação

| Documento | Finalidade |
|:----------|:-----------|
| `01-configuracao-lab.md` | Configuração das VMs e rede |
| `02-elastic-stack.md` | Instalação e segurança do Elastic Stack |
| `03-winlogbeat-sysmon.md` | Coleta de logs no Windows com Sysmon e Winlogbeat |
| `04-filebeat-ubuntu.md` | Coleta de logs no Linux com Filebeat |
| `05-dashboards-kibana.md` | Criação de dashboards para visualização |
| `erros-e-solucoes.md` | Problemas enfrentados e soluções aplicadas |

---

## 🚀 Melhorias Futuras

- Integrar o pfSense para monitoramento de logs de firewall
- Simular cenários de ataque usando Kali Linux
- Implementar o Wazuh como segunda fase do SIEM

---

## 🏆 Consideração Final

Este projeto demonstra habilidades práticas em cibersegurança, administração de sistemas, troubleshooting e monitoramento de segurança — competências essenciais para atuação em SOCs e equipes de segurança da informação.
