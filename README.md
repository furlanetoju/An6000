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

**Configuração para mostrar tudo de uma vez no console, sem ter que ficar dando espaço ou enter**
```
VZP-2(config)# terminal length 512
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

**Visualizar versão de compilação da controladora**
```
diagnose
show debugversion
```
-------------------------------------------------------------------------------------------------------

**Autorizar uma ONU Bridge**

```
show discovery
interface pon 1/{slot}/{pon}
VZP-02(config-if-pon-1/1/1)# whitelist add phy-id {mac} type {model}
VZP-02(config-if-pon-1/1/1)# onu port vlan {onu-id} eth 1 service 1 tag priority 7 tpid 33024 vid {vlan} 
```
**Descobrir a ONU-ID number**
```
VZP-02(config-if-pon-1/1/1)# show online onuinfo | begin {mac}
```
**Exemplo de script**

```
show discovery
interface pon 1/1/1
VZP-02(config-if-pon-1/1/1)# whitelist add phy-id FHTT076f0af0 type 5506-01-A1
VZP-02(config-if-pon-1/1/1)# onu port vlan 1 eth 1 service 1 tag priority 7 tpid 33024 vid 101 

VZP-02(config)# show whitelist phy-id 1/1/1 FHTT076f0af0
VZP-02(config-if-pon-1/1/1)# show online onuinfo | begin FHTT076f0af0

```
**Como autorizar uma ONT**
```
show discovery
interface pon 1/{slot}/{pon}
onu wan-cfg {onu-id} index 1 mode internet type route {vlan} 7 nat enable qos disable vlanmode tag tvlan disable 0 0 dsp pppoe proxy disable {username} {password} {serve-name} auto entries 6 fe1 fe2 fe3 fe4 ssid1 ssid5
onu ipv6-wan-cfg {onu-id} ind 1 ip-stack-mode ipv4 ipv6-src-type dhcpv6 prefix-src-type delegate 
```

**Como ver sinal**
```
interface pon 1/{slot}/{pom}
show onu optical-info {onu-id}
```

**Evitar logout da OLT**
```
VZP-02(config)# idle-timeout 255
```

**Criar vlan de serviço via CLI**
```
VZP-02(config)# port vlan 2801 to 2816 tag 1/8 1
VZP-02(config)# port vlan 2801 to 2816 allslot
```
No exemplo acima, criamos da vlan `2801` a `2816` apontando para a porta master do nosso trunk, que no caso é `1/8 1`. Depois repetimos o comando, informando que vamos autorizar essa vlan em todos os cartões `allslot`

**Como localizar a ONU atraves do MAC do roteador**

```
VZP-02(config)# show mac-address port 1/16/15 | begin ec:ad:e0:d3:8d:cc
```

**Adicionar o profile na ONU**
```
onu bandwidth-profile {onu-id} profile-name {700M}
```
**Como verificar as ONUs online por slot e geral**
```
VZP-2(config)# show onu auth-and-online statistics level slot 

           Online/Auth  MDU(OL/AU)   SFU(OL/AU)   HGU(ON/AU)
------------------------------------------------------------
sytem    :  8588/9077       0/0       8588/9077       0/0    
------------------------------------------------------------
slot    1:  1460/1554       0/0       1460/1554       0/0    
------------------------------------------------------------
slot    3:  1332/1411       0/0       1332/1411       0/0    
------------------------------------------------------------
slot    6:  1407/1495       0/0       1407/1495       0/0    
------------------------------------------------------------
slot   12:  1312/1346       0/0       1312/1346       0/0    
------------------------------------------------------------
slot   14:  1579/1689       0/0       1579/1689       0/0    
------------------------------------------------------------
slot   16:  1498/1582       0/0       1498/1582       0/0    
------------------------------------------------------------
```
