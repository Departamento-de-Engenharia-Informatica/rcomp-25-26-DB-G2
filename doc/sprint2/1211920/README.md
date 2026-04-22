# Terminal 5 (T5) Implementation Summary - Sprint 2
**Team:** 2DB
**Terminal:** 5
**Status:** Completed (Verified & Tested)

---

## 1. Physical Topology & Hardware Implementation
A estrutura física do Terminal 5 foi reestruturada seguindo o modelo hierárquico de rede, garantindo que o Intermediate Cross-Connect (IC) funcione como o centro de distribuição local e assegure a conectividade com o Main Cross-Connect (MC).

* **Switching Infrastructure**:
    * **Intermediate Cross-Connect (IC)**: O switch atua como o ponto central de distribuição do terminal, agregando o tráfego dos switches de acesso.
    * **Horizontal Cross-Connect (HC1 & HC2)**: Switches de acesso dedicados para a terminação de dispositivos finais, garantindo a separação física de setores.
* **Cabling**:
    * **Trunking**: Todas as ligações inter-switch (HC1 para IC, HC2 para IC) e a ligação do IC para o Router foram configuradas em modo Trunk (`switchport mode trunk`) para permitir a passagem de múltiplas VLANs.
* **Wireless Implementation**:
    * Implementação de um Access Point (AP) ligado diretamente ao IC (porta em modo Acesso), operando na VLAN 763 e permitindo a conectividade sem fios para dispositivos móveis no Terminal 5.

---

## 2. IP Backbone Summary
O Terminal 5 está integrado na infraestrutura de backbone do campus, permitindo a comunicação com os restantes terminais através de uma hierarquia de roteamento centralizada.

* **Backbone ID**: `10.51.0.5` configurado na interface de saída (FastEthernet0/0).
* **Gateway de Saída**: Configurada uma rota estática padrão (`ip route 0.0.0.0 0.0.0.0 10.51.0.2`) no Router T5 para assegurar o encaminhamento de pacotes desconhecidos para o core da rede do campus.

---

## 3. Layer 3 Configuration: IPv4 & Routing
A configuração de Layer 3 utiliza a metodologia **Router-on-a-Stick** para permitir o encaminhamento de tráfego entre as diferentes sub-redes (VLANs) do terminal, com o encapsulamento dot1Q aplicado nas sub-interfaces.

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
* **VLAN Segmentation**: Implementação de segmentação lógica em portas de acesso para isolar tráfego de utilizadores, voz, servidores e wi-fi.
* **Switch Management (VLAN 749)**:
    * Implementação de Interfaces Virtuais (SVI) na VLAN 749 em todos os switches para permitir a gestão remota:
        * **Switch IC**: `10.51.2.41`
        * **Switch HC1**: `10.51.2.42`
        * **Switch HC2**: `10.51.2.43`
    * Configuração do Default Gateway (`ip default-gateway 10.51.2.1`) em todos os switches para permitir a administração a partir de outras sub-redes.
* **VoIP Access**: Porta do telefone (no HC2) configurada com `switchport voice vlan 764` para priorização e correta separação lógica do tráfego de voz.

---

## 5. Verification & Validation
A implementação foi validada através de uma matriz de testes de conectividade (ICMP), confirmando o pleno funcionamento do roteamento inter-VLAN e acesso aos recursos:

1. **Gateway Local**: Teste de equipamentos finais para as respetivas sub-interfaces do Router - **Sucesso**.
2. **Inter-VLAN**: Comunicação entre equipamentos de diferentes VLANs (ex: Users para Gestão) - **Sucesso**.
3. **Acesso ao Servidor**: Teste de conectividade inter-VLANs para a gama `10.51.64.0/20` - **Sucesso**.
4. **Gestão de Infraestrutura**: Ping para os SVIs dos Switches (`10.51.2.41`, `.42` e `.43`) - **Sucesso**.
5. **Convergência de Rede**: Verificação dos estados das portas Trunk, Access e propagação correta das VLANs (Spanning-Tree PVST) - **Operacional**.