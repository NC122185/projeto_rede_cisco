projeto_rede_cisco
Simulação de Rede Empresarial - Cisco Packet Tracer

Este repositório contém o desenho, simulação e configuração de uma infraestrutura de rede empresarial desenvolvida no Cisco Packet Tracer. O objetivo do projeto foi replicar um ambiente de produção real, focando-se na segmentação de tráfego, encaminhamento inter-VLAN, automação de endereçamento e resolução de nomes.

 🎯 Objetivos do Projeto
- Implementar segmentação de tráfego lógico para aumentar a segurança da infraestrutura.
- Configurar encaminhamento dinâmico entre diferentes sub-redes (Inter-VLAN Routing).
- Automatizar a atribuição de endereços de rede.
- Simular serviços essenciais de infraestrutura empresarial (DNS e servidores).

 🛠️ Arquitetura e Lógica da Rede

A topologia está estruturada em duas sub-redes lógicas isoladas através de **VLANs**, garantindo que o tráfego de servidores e de utilizadores comuns permaneça segmentado:

*   VLAN 10 - SERVERS (`192.168.10.0/24`)
       Servidor DNS:** IP Estático `192.168.10.10`
       PC Servidor (Ex: Ficheiros/Aplicações): IP Estático `192.168.10.21`
*   VLAN 20 - CLIENTES (`192.168.20.0/24`)
    *   PC Cliente (Posto de Trabalho): IP Estático `192.168.20.21`

### Equipamentos e Configurações Aplicadas:
Router Cisco 2911:** Configurado como o gateway central da infraestrutura. Implementação da técnica Router-on-a-Stick através de subinterfaces lógicas (`G0/0.10` e `G0/0.20`) para permitir a comunicação controlada entre as VLANs. Adicionalmente, foi configurado o serviço **DHCP** no router para automação de rede.
Switch Cisco 2960: Atuação como o nó central de comutação. Criação e associação de portas de acesso às respetivas VLANs (10 e 20) e configuração da porta de ligação ao router em modo **Trunk** (802.1Q).
Servidor DNS:Configuração de um registo do tipo A associando o nome de domínio `dc01.lab.local` ao IP `192.168.10.10`, simulando o comportamento de um *Domain Controller* de Active Directory.

---

## 🧪 Testes e Validação da Infraestrutura

Para homologar a topologia e garantir o correto funcionamento de todos os serviços, foram realizados com sucesso os seguintes testes de conectividade:

1.  **Testes de Conectividade ICMP (Ping):**
    *   PC Cliente $\rightarrow$ PC Servidor (`192.168.10.21`) — Sucesso (Validação do Inter-VLAN Routing).
    *   PC Servidor $\rightarrow$ PC Cliente (`192.168.20.21`) — Sucesso.
    *   PC Servidor $\rightarrow$ Gateways (`192.168.10.1` e `192.168.20.1`) — Sucesso.
2.  Resolução de Nomes (DNS Lookup):
    *   Execução do comando `nslookup dc01.lab.local` a partir do PC Cliente e PC Servidor com resposta fidedigna apontando para o IP `192.168.10.10`.


🚀 Próximos Passos
Este projeto cumpre a fase inicial de planeamento e simulação da infraestrutura de rede. A etapa seguinte consiste na transposição deste cenário para um ambiente real virtualizado em **VirtualBox**, com a implementação prática do Windows Server, configuração do domínio Active Directory, Unidades Organizacionais (OUs), utilizadores e diretivas de grupo (GPOs).

---

 📂 Como Testar o Projeto
1. Faça o download do ficheiro `.pkt` presente neste repositório.
2. Abra o ficheiro utilizando o software **Cisco Packet Tracer**.
