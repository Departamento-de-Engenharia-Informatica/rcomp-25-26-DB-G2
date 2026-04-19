# Terminal 5 (T5) Implementation Summary - Sprint 2
**Team:** 2DB
**Terminal:** 5
**Status:** Completed (Verified & Tested)

---

## 1. Physical Topology & Hardware Implementation
A estrutura física do Terminal 5 foi reestruturada seguindo o modelo hierárquico de rede, garantindo que o Intermediate Cross-Connect (IC) funcione como o centro de distribuição local e assegure a conectividade com o Main Cross-Connect (MC).

* **Switching Infrastructure**:
    * **Intermediate Cross-Connect (IC)**: O switch  atua como o ponto central de distribuição do terminal, agregando o tráfego dos switches de acesso.
    * **Horizontal Cross-Connect (HC1 & HC2)**: Switches de acesso dedicados para a terminação de dispositivos finais, garantindo a separação física de setores.
* **Cabling**:
    * **Trunking**: Todas as ligações inter-switch (HC1-IC, HC2-IC) e a ligação IC-Router configuradas em modo Trunk.
    * **Native VLAN**: Configurada a **VLAN 749** como Native VLAN em todos os troncos para garantir a segurança e a gestão eficiente do tráfego.
* **Wireless Implementation**:
    * Implementação de um Access Point (AP) operando na VLAN 763, permitindo a conectividade sem fios para dispositivos móveis no Terminal 5.

---

## 2. IP Backbone Summary
O Terminal 5 está integrado na infraestrutura de backbone do campus, permitindo a comunicação com os restantes terminais através de uma hierarquia de roteamento centralizada.

* **Backbone ID**: `10.51.0.5`
* **Gateway de Saída**: Configurado no Router T5 para assegurar o encaminhamento de pacotes para o core da rede do campus.

---

## 3. Layer 3 Configuration: IPv4 & Routing
A configuração de Layer 3 utiliza a metodologia **Router-on-a-Stick** para permitir o encaminhamento de tráfego entre as diferentes sub-redes (VLANs) do terminal.

* **Default Gateways**: Cada sub-interface no router utiliza o primeiro endereço IP utilizável da respetiva gama.

| Interface | VLAN ID | Descrição | Network Address | Mask |
| :--- | :--- | :--- | :--- | :--- |
| Fa0/1.749 | 749 | GESTAO | 10.51.2.0/24 | 255.255.255.0 |
| Fa0/1.762 | 762 | T5_USERS | 10.51.16.0/20 | 255.255.240.0 |
| Fa0/1.763 | 763 | T5_WIFI | 10.51.32.0/20 | 255.255.240.0 |
| Fa0/1.764 | 764 | T5_VOIP | 10.51.48.0/20 | 255.255.240.0 |
| Fa0/1.765 | 765 | T5_SERVERS | 10.51.64.0/20 | 255.255.240.0 |

---

## 4. Layer 2 Logical Setup & Management
* **VLAN Segmentation**: Implementação de segmentação lógica para isolar tráfego de utilizadores, voz, servidores e gestão administrativa.
* **Switch Management (VLAN 749)**:
    * Implementação de Interfaces Virtuais (SVI) em todos os switches para permitir a gestão remota, alinhada com a numeração sequencial do projeto:
        * **Switch IC**: `10.51.2.40`
        * **Switch HC1**: `10.51.2.41`
        * **Switch HC2**: `10.51.2.42`
    * Configuração de `ip default-gateway 10.51.2.1` para permitir a administração a partir de outras sub-redes.
* **VoIP Access**: Porta do telefone (HC2) configurada com `switchport voice vlan 764` para priorização de tráfego de voz.

---

## 5. Verification & Validation
A implementação foi validada através de uma matriz de testes de conectividade (ICMP), confirmando o pleno funcionamento do roteamento inter-VLAN e acesso aos recursos:

1. **Gateway Local**: Teste do PC0 para `10.51.16.1` - **Sucesso**.
2. **Inter-VLAN**: Comunicação entre PC0 (VLAN 762) e PC-Gestão (VLAN 749) - **Sucesso**.
3. **Acesso ao Servidor**: Teste de conectividade do PC-Gestão para o Servidor `10.51.64.2` - **Sucesso**.
4. **Gestão de Infraestrutura**: Ping do PC-Gestão para o Switch IC (`10.51.2.40`) - **Sucesso**.
5. **Convergência de Rede**: Verificação dos estados das portas Trunk e propagação de VLANs - **Operacional**.

---