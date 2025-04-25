# Laboratório SIEM – Monitoramento de Segurança com Elastic Stack

![Elastic Stack](https://img.shields.io/badge/Elastic%20Stack-8.x-blue?logo=elastic)
![Winlogbeat](https://img.shields.io/badge/Winlogbeat-8.x-blue?logo=elastic)
![Filebeat](https://img.shields.io/badge/Filebeat-8.x-blue?logo=elastic)
![Sysmon](https://img.shields.io/badge/Sysmon-v14.16-blue?logo=windows)
![Ubuntu](https://img.shields.io/badge/Ubuntu-22.04-orange?logo=ubuntu)
![Windows Server](https://img.shields.io/badge/Windows%20Server-2019-blue?logo=windows)
![Windows 11](https://img.shields.io/badge/Windows-11-blue?logo=windows)
![Kibana Dashboards](https://img.shields.io/badge/Kibana-Dashboards-green?logo=kibana)
![Status](https://img.shields.io/badge/Status-Concluído-brightgreen)

📄 Leia este documento em: [English](README.md)

Este repositório documenta um projeto prático de construção de um laboratório SIEM (Gerenciamento de Informações e Eventos de Segurança) utilizando Elastic Stack (Elasticsearch + Kibana), Winlogbeat, Filebeat e Sysmon, em um ambiente com Windows Server, Windows 11 e Ubuntu Server.

---

## 🎯 Objetivo do Projeto

Criar um ambiente funcional de SIEM capaz de coletar, analisar e visualizar eventos de segurança em uma rede híbrida simulada.

---

## 🧰 Tecnologias Utilizadas

- Elastic Stack (Elasticsearch + Kibana)
- Winlogbeat e Filebeat
- Sysmon (coleta avançada de eventos do Windows)
- Ubuntu Server 22.04
- Windows Server 2019 (Active Directory + DNS)
- Windows 11 Client
- pfSense (planejado)

---

## 📚 Documentação

- [📖 Visão Geral do Projeto](docs/pt-br/00-visao-geral.md)
- [📂 Documentação Completa (PT-BR)](docs/pt-br/)
- [📂 Documentação Completa (EN)](docs/en/)

Cada seção detalha as implementações, configurações e processos de troubleshooting realizados.

---

## 🚀 Melhorias Futuras

- Integração com pfSense para monitoramento de logs de firewall
- Simulação de ataques utilizando Kali Linux
- Implementação do Wazuh como evolução do SIEM

---

> Projeto desenvolvido por [Fernando Montarroys](https://github.com/fernandombmuniz) para aprimoramento de habilidades práticas em cibersegurança e administração de sistemas.
