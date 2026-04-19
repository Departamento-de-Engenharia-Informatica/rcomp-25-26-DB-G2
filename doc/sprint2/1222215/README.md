# Terminal 2 (1222215) Implementation Summary - Sprint 2
**Team:** 2DB
**Terminal:** 2
**Status:** Completed (Verified & Tested)

---

## 1. Physical Topology & Hardware Implementation
A estrutura física foi reconstruída e validada seguindo a hierarquia de cablagem estruturada, garantindo que o Main Cross-Connect (MC) funcione como o centro de distribuição do campus.

* **Switching Infrastructure**:
    * **Main Cross-Connect (MC)**: O switch `SW-T2-F1` atua como o ponto central da rede.
    * **Intermediate Cross-Connect (IC)**: Adicionado um switch de piso dedicado para o Terminal 2 para separar a distribuição dos dispositivos finais.
    * **Backbone Placeholders**: Três switches adicionais representam a ligação física aos Terminais 3, 4 e 5.
* **Cabling**:
    * **Trunking**: Todas as ligações inter-switch e a ligação Switch-Router configuradas em modo Trunk.
    * **Native VLAN**: Configurada a **VLAN 749** como Native VLAN em todos os troncos para segurança e gestão.
* **Wireless Implementation**:
    * O laptop foi atualizado com o módulo **WPC300N** após a mitigação de erros de simulação.
    * Ligação estabelecida via SSID no Access Point (AP), operando na VLAN 751.

---

## 2. Internet Connection & WAN Configuration
Como gateway principal do campus, o Terminal 2 simula um uplink funcional para o ISP.

* **Connectivity Chain**: ISP Router -> Cloud (DSL) -> Modem -> Router T2.
* **ISP Handshake**:
    * Interface WAN do Router T2 configurada com o IP **89.73.67.34/30**.
    * Implementada a **Static Default Route** (`0.0.0.0 0.0.0.0 89.73.67.33`).
* **Return Traffic**: Rota estática configurada no router do ISP para alcançar a rede interna `10.51.0.0/17`.

---

## 3. Layer 3 Configuration: IPv4 & Routing
A configuração de Layer 3 utiliza **Router-on-a-Stick** para permitir a comunicação entre sub-redes.

* **Default Gateways**: Cada sub-interface utiliza o primeiro endereço IP utilizável de cada gama.

| Interface | VLAN ID | Descrição | Network Address | Mask |
| :--- | :--- | :--- | :--- | :--- |
| Fa0/0.748 | 748 | Backbone | 10.51.0.0/24 | 255.255.255.0 |
| Fa0/0.750 | 750 | T2_USERS | 10.51.24.0/22 | 255.255.252.0 |
| Fa0/0.751 | 751 | T2_WIFI | 10.51.16.0/21 | 255.255.248.0 |
| Fa0/0.752 | 752 | T2_VOIP | 10.51.28.0/23 | 255.255.254.0 |
| Fa0/0.753 | 753 | T2_SERVERS | 10.51.30.0/25 | 255.255.255.128 |

---

## 4. Layer 2 Logical Setup & Management
* **VTP (VLAN Trunking Protocol)**:
    * MC Switch configurado como **VTP Server** (Domínio: `rc2526dbg2`).
    * Criadas as 18 VLANs obrigatórias (748 a 765) para propagação global.
* **Switch Management (VLAN 749)**:
    * Criada interface virtual (SVI) no switch MC com o IP **10.51.2.1/23**.
    * Rede isolada sem gateway para garantir segurança na gestão.
* **VoIP Access**: Porta do telefone configurada com `switchport voice vlan 752`.

---

## 5. Verification & Disaster Recovery
A implementação incluiu uma fase de recuperação total após falha crítica do Packet Tracer, validada pelos seguintes testes de ping:

1. **Gateway Local**: PC-USER para `10.51.24.1` - **Sucesso**.
2. **Inter-VLAN**: PC-USER para Server `10.51.30.10` - **Sucesso**.
3. **Gestão Interna**: PC-MGMT para Switch MC `10.51.2.1` - **Sucesso**.
4. **Link WAN**: PC-USER para Router Outside IP `89.73.67.34` - **Sucesso**.
5. **Acesso Internet**: PC-USER para ISP Router `89.73.67.33` - **Sucesso**.

---

#