# An6000
Configurações Iniciais


`list` - **Lista os comandos**

`config` - **Acessa o modo de configuração**

`card auth 1/x x` - **Colocamos o numero do slot a ser autorizado e o tipo de cartão.**

`card auto-auth` - **Autoriza todos os cartoes de uma vez.**

**Adicionando IP na porta Ethernet**

```
interface meth 1
ip address x.x.x.x mask x.x.x.x
```
**Para checar a configuração:**

```
show ip address
```

**Adicionar gerencia pelas interfaces de uplink***
```
manage-vlan GERENCIA svlan x cvlan x
manage-vlan ipv4 GERENCIA x.x.x.x/x
```

`port vlan 1001 tag 1/8 3` - **Exemplo slot 8 porta 3**

`show manage-vlan all`
```
static-route destionation-ip 0.0.0.0 mask 0.0.0.0 nexthop x.x.x.x
show statis-route running-config
snmp-agent trap-receiver add ip x.x.x.x security-name adsl v2c
show snmp-agent trap-receiver
snmp-time interval 3600 servip ipv4 10.111.0.254
show snmp-time
```
