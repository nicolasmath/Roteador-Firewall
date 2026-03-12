
![GitHub License](https://img.shields.io/github/license/nicolasmath/lab-redes-01)

# Segurança e Firewall

Alunos: Nicolas Lopes, Sara Oliveira

Professor: José de Assis

Data: 12/03/2026

---

Roteador DIR-853

Este documento descreve as funcionalidades de segurança e configurações de Firewall baseadas na interface do roteador AC1300 MU-MIMO.

## 1. Configurações de Host e Firewall

### Habilitar DMZ Host
A DMZ (Demilitarized Zone) permite expor um dispositivo da rede interna diretamente para a internet.
* **Funcionamento:** Todo o tráfego que chega da internet e não possui regra específica é direcionado para um único IP interno.
* **Exemplo:** Internet -> Roteador -> PC (192.168.0.10).
* **Risco:** O dispositivo fica vulnerável, pois as proteções padrão do firewall são ignoradas para este host.
* **Uso comum:** Servidores de jogos, consoles de videogame para obter NAT aberto, servidores de arquivos ou testes de rede.

### Habilitar SPI IPv4
O SPI (Stateful Packet Inspection) é um firewall que analisa o estado das conexões.
* **Função:** Verifica se os pacotes de dados pertencem a uma sessão ativa e legítima.
* **Operação:** Se um dispositivo interno solicita um site, o SPI permite o retorno. Se pacotes externos chegam sem terem sido solicitados, são bloqueados.
* **Importância:** É uma das camadas fundamentais de proteção contra acessos não autorizados.


### Habilitar Verificação Anti-Spoof
Protege a rede contra ataques de IP Spoofing.
* **Conceito:** Ocorre quando um invasor falsifica o endereço IP de origem para parecer que o tráfego vem de uma fonte confiável (como a própria rede interna).
* **Ação:** O firewall valida a procedência do pacote e bloqueia identidades falsificadas.
* **Objetivo:** Prevenir invasões e ataques de negação de serviço (DoS).

### Segurança Simples IPv6
Aplica regras de proteção básicas para o protocolo de nova geração.
* **Função:** Bloqueia tentativas de conexões externas não solicitadas voltadas para endereços IPv6 internos.
* **Contexto:** Diferente do IPv4, no IPv6 os dispositivos costumam ter IPs públicos reais, tornando o firewall essencial para evitar exposição direta.

### Filtro de Entrada IPv6
Mecanismo de controle de acesso granular para tráfego IPv6.
* **Operação:** Define quais tipos de conexões e protocolos podem atravessar a borda da rede.
* **Objetivo:** Proteger a integridade dos dispositivos internos e filtrar tráfego indesejado.

---

## 2. Application Layer Gateway (ALG)

As configurações de ALG ajudam o roteador a processar protocolos que normalmente apresentam dificuldades para atravessar o NAT (Network Address Translation).

### PPTP (Point-to-Point Tunneling Protocol)
* **Descrição:** Protocolo para criação de túneis VPN.
* **Papel do ALG:** Gerencia a porta 1723 e o protocolo GRE para permitir a conexão.
* **Status Atual:** Considerado legado e com vulnerabilidades de segurança conhecidas.

### IPsec (VPN)
* **Descrição:** Conjunto de protocolos para comunicações seguras e criptografadas.
* **Papel do ALG:** Auxilia na passagem de protocolos como ESP, AH e IKE pelo NAT.
* **Uso:** Amplamente utilizado para interligar redes corporativas e acessos remotos seguros.

### RTSP (Real Time Streaming Protocol)
* **Descrição:** Protocolo para controle de fluxos de dados multimídia.
* **Uso:** Utilizado por câmeras IP, servidores de streaming e sistemas de vigilância.
* **Papel do ALG:** Abre e gerencia portas dinâmicas necessárias para o fluxo de vídeo e áudio.

### SIP (Session Initiation Protocol)
* **Descrição:** Protocolo de sinalização para telefonia VoIP e videoconferência.
* **Função:** Gerencia o início, manutenção e término de chamadas.
* **Observação Técnica:** Embora o ALG vise ajudar, em muitos cenários de VoIP ele pode causar falhas na sinalização, sendo frequentemente desativado por administradores de rede.

---

## 3. Tabela Comparativa de Protocolos ALG

| Opção | Aplicação Principal | Nível de Segurança |
| :--- | :--- | :--- |
| PPTP | VPN Legada | Baixo |
| IPsec | VPN Moderna e Corporativa | Alto |
| RTSP | Streaming de Vídeo / Câmeras | N/A (Tráfego de Mídia) |
| SIP | Telefonia IP (VoIP) | N/A (Sinalização) |
