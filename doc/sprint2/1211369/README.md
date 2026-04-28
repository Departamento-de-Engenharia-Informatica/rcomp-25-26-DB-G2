# Terminal 2 (1222215) Implementation Summary - Sprint 2
**Team:** 2DB
**Terminal:** 2
**Status:** Completed & Integrated (Multi-floor)

---

## 1. Physical Topology & Hardware Implementation
A estrutura física foi expandida para representar a infraestrutura completa do Terminal 2, abrangendo dois pisos e a ligação ao backbone do campus.

* **Switching Infrastructure**:
    * **Main Cross-Connect (MC)**: Switch `SW-T2-F1` (Piso 1) como nó central de distribuição.
    * **Floor 2 Extension**: Adicionado um switch **PT-Empty** para o Piso 2, povoado com módulos **NM-1CFE** (FastEthernet) para dispositivos e **NM-1CGE** (Gigabit) para o uplink.
    * **Backbone Placeholders**: Três switches representam a terminação física dos links de fibra para os Terminais 3, 4 e 5.
* **Cabling**:
    * **Inter-Switch Trunking**: Ligação entre o switch do Piso 2 e o MC configurada via porta Gigabit em modo **Trunk**.
    * **Router Link**: A porta **GigabitEthernet 4/1** do MC liga ao Router R-T2, configurada como Trunk para suportar a arquitetura **Router-on-a-Stick**.
* **Wireless Implementation**:
    * Expansão da rede Wi-Fi para o Piso 2 com um Access Point dedicado na VLAN 751.
    * Laptop configurado com módulo **WPC300N** e SSID correspondente.

---

## 2. Internet Connection & WAN Configuration
O Terminal 2 atua como o gateway de saída para o ISP da equipa.

* **WAN Interface**: Interface **FastEthernet 0/1** do Router R-T2 configurada com o IP **89.73.67.34/30**.
* **Routing**:
    * Rota estática padrão (`0.0.0.0/0`) apontando para o ISP em **89.73.67.33**.
    * Rota de retorno configurada no router do ISP para a rede interna `10.51.0.0/17`.

---

## 3. Layer 3 Configuration: IPv4 & Routing
Endereçamento centralizado no Router R-T2, servindo de gateway para todas as sub-redes do terminal.

| Interface | VLAN ID | Descrição | Gateway IP | Mask |
| :--- | :--- | :--- | :--- | :--- |
| Fa0/0.748 | 748 | Backbone | 10.51.0.2 | 255.255.255.0 |
| Fa0/0.750 | 750 | T2_USERS | 10.51.24.1 | 255.255.252.0 |
| Fa0/0.751 | 751 | T2_WIFI | 10.51.16.1 | 255.255.248.0 |
| Fa0/0.752 | 752 | T2_VOIP | 10.51.28.1 | 255.255.254.0 |
| Fa0/0.753 | 753 | T2_SERVERS | 10.51.30.1 | 255.255.255.128 |

---

## 4. Layer 2 Logical Setup & Management
* **VTP Hierarchy**:
    * **MC Switch**: Configurado como **VTP Server** (Domínio: `rc2526dbg2`).
    * **Floor 2 Switch**: Configurado como **VTP Client**, recebendo a base de dados de 18 VLANs automaticamente.
* **Native VLAN Standardization**: Toda a infraestrutura Trunk foi padronizada para utilizar a **VLAN 749** como Native VLAN para garantir a segurança e estabilidade do STP.

---

## 5. Troubleshooting & Integration Challenges
A integração do segundo piso revelou erros de configuração que foram sistematicamente resolvidos:

* **Native VLAN Mismatch**:
    * **Problema**: Mensagens de erro de inconsistência na porta **Gig 4/1** (ligada ao router) por estar na VLAN 1 enquanto o resto da rede usava a 749.
    * **Solução**: Sincronização de todos os Trunks para a Native VLAN 749 e ajuste do comando `encapsulation dot1Q 749 native` nas sub-interfaces do Router.
* **Inter-VLAN Routing Block**:
    * **Problema**: Comunicação bem-sucedida apenas entre dispositivos na mesma VLAN (Layer 2); pings para a Gateway (.1) falhavam.
    * **Causa**: Falta de configuração de IPs e Default Gateways nos novos dispositivos do Piso 2 e tabelas ARP vazias no router.
    * **Solução**: Atribuição estática de endereços na gama `10.51.x.x/20` e ativação administrativa (`no shutdown`) da interface física Fa0/0 do router.
* **STP Convergence**:
    * **Problema**: Portas bloqueadas (laranja) por inconsistência de VLAN nativa com os switches vizinhos (T3, T4, T5).
    * **Solução**: Padronização da Native VLAN 749 nos links de backbone e utilização de "Fast Forward Time" para convergência do Spanning Tree.

---

## 6. Final Verification Results
1. **Intra-VLAN Connectivity**: Ping PC-Piso1 para PC-Piso2 (VLAN 750) - **Sucesso**.
2. **Inter-VLAN Gateway**: Todos os dispositivos alcançam a Gateway `10.51.x.1` - **Sucesso**.
3. **Internal Server Access**: Acesso validado ao servidor na VLAN 753 (`10.51.30.1`) - **Sucesso**.
4. **Internet Uplink**: Pings para o Router ISP (`89.73.67.33`) a partir de qualquer sub-rede - **Sucesso**.