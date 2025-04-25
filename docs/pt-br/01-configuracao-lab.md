 Configuração do Lab – SIEM com Elastic Stack

Este guia descreve a criação completa do ambiente virtualizado do projeto de laboratório SIEM, incluindo as máquinas virtuais (VMs) e suas respectivas funções.

---

## 🎯 Objetivo

Criar um ambiente controlado e virtualizado simulando uma rede real, com o objetivo de coletar, monitorar e detectar eventos de segurança usando o Elastic Stack e Beats.

---

## 🧰 Requisitos

- VMware Workstation (ou outra plataforma de virtualização)
- Mínimo de 16 GB de RAM (recomendado 24 GB)
- Pelo menos 120 GB de espaço em disco
- Conexão com a internet para baixar pacotes
- ISOs necessárias:
  - Ubuntu Server 22.04
  - Windows Server 2019
  - Windows 11 Pro
  - pfSense (opcional nesta fase)

---

## 🛠️ Topologia do Laboratório

[Windows Server 2019]  →  [Ubuntu Server 22.04]  →  [Windows 11 Client]  
   (AD + DNS)              (Elastic Stack)           (Membro do Domínio)  

                             ↓  
               [Opcional: Firewall pfSense]

Cada máquina irá enviar logs de eventos de segurança para o servidor Ubuntu com Elastic Stack instalado.

---

## 🖥️ Configuração das Máquinas Virtuais

### Ubuntu Server – Elastic Stack

- **Sistema**: Ubuntu Server 22.04 LTS
- **vCPU**: 2
- **RAM**: 6 GB
- **Disco**: 50 GB
- **Rede**: NAT ou Host-Only (com acesso à internet)
- **Função**: Servidor Elastic Stack (Elasticsearch + Kibana)

### Windows Server 2019 – Controlador de Domínio

- **Sistema**: Windows Server 2019 Standard
- **vCPU**: 2
- **RAM**: 4 GB
- **Disco**: 40 GB
- **Rede**: Mesma rede do Ubuntu Server
- **Função**: Active Directory (AD DS) + DNS

### Windows 11 – Estação Cliente

- **Sistema**: Windows 11 Pro
- **vCPU**: 2
- **RAM**: 4 GB
- **Disco**: 40 GB
- **Rede**: Mesma rede do controlador de domínio
- **Função**: Estação de trabalho membro do domínio, geração de logs

### pfSense (Opcional – Etapa Futuras)

- **Sistema**: pfSense última versão estável
- **vCPU**: 1
- **RAM**: 1 GB
- **Disco**: 20 GB
- **Rede**: Bridged ou segmento isolado
- **Função**: Firewall de rede e fonte de logs (syslog)

---

## 📋 Passos Iniciais

1. Instale o VMware Workstation (ou similar).
2. Crie as VMs conforme as especificações acima.
3. Instale o Ubuntu Server 22.04 e atualize os pacotes.
4. Instale o Windows Server 2019 e promova-o a controlador de domínio (AD DS + DNS).
5. Instale o Windows 11 e adicione-o ao domínio.
6. Verifique a comunicação entre todas as VMs com comandos `ping`.

---

## ⚡ Dicas e Boas Práticas

- Ative o VMware Tools (ou similar) para melhor desempenho das VMs.
- Defina IPs fixos — especialmente para o controlador de domínio.
- Use snapshots após configurações importantes para facilitar a recuperação.
- Comece com a rede NAT e integre o pfSense mais adiante.

---

## 🚀 Próximo Passo

Continue para o guia [02 – Instalação e Segurança do Elastic Stack](02-elastic-stack.md) para configurar o Elasticsearch e o Kibana.