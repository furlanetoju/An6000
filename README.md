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

**Como ver o sinal de todas as ONUs de uma vez na porta PON** `show onu optical-info`
```
VZP-2(config-if-pon-1/16/7)# show onu optical-info 
			  --------------  ONU OPTIC MODULE PAR INFO  --------------
ID  TYPE(KM)  TEMP('C)  VOLT(V)  CURR(mA)  SENDPW(Dbm)  RECVPW(Dbm)  OLT RECVPW(Dbm) In-UpThres(Dbm) In-DnThres(Dbm) Out-UpThres(Dbm) Out-DnThres(Dbm)
11  20        42.16      3.26    18.35      2.80        -33.97       -30.45            0.00            0.00            0.00             0.00            
12  20        51.00      3.27    22.78      2.37        -40.00       -33.01            0.00            0.00            0.00             0.00            
17  20        54.43      3.30    16.30      1.93        -35.22       -30.45            0.00            0.00            0.00             0.00            
18  20        46.15      3.26    11.13      2.35        -33.00       -30.96            0.00            0.00            0.00             0.00            
23  20        52.67      3.27    17.45      2.26        -33.01       -30.45            0.00            0.00            0.00             0.00            
28  20        47.72      3.33    14.80      2.09        -33.97       -31.54            0.00            0.00            0.00             0.00            
36  20        49.84      3.33    17.05      2.19        -33.97       -31.54            0.00            0.00            0.00             0.00            
39  20        36.25      3.28    15.77      3.21        -36.98       -33.97            0.00            0.00            0.00             0.00            
42  20        47.72      3.26    16.86      2.41        -33.97       -30.96            0.00            0.00            0.00             0.00            
43  20        40.39      3.26    16.20      2.89        -35.22       -30.00            0.00            0.00            0.00             0.00            
46  20        45.95      3.33    12.40      2.97        -35.22       -30.00            0.00            0.00            0.00             0.00            
52  20        51.75      3.29    22.33      3.13        -40.00       -33.97            0.00            0.00            0.00             0.00            
62  20        45.33      3.26    16.25      2.96        -36.98       -32.21            0.00            0.00            0.00             0.00            
65  20        48.22      3.32    14.50      3.03        -36.98       -32.21            0.00            0.00            0.00             0.00            
69  20        47.47      3.24    10.04      2.48        -33.00       -30.00            0.00            0.00            0.00             0.00            
73  20         0.00      0.00     0.00      2.40        -33.98       -30.96            0.00            0.00            0.00             0.00            
77  20        46.51      3.23    10.87      2.40        -33.00       -30.96            0.00            0.00            0.00             0.00            
78  20        45.69      3.27     8.55      2.08        -33.00       -32.21            0.00            0.00            0.00             0.00            
81  20        45.50      3.28    10.57      2.36        -33.00       -30.45            0.00            0.00            0.00             0.00            
90  20        42.51      3.26    14.15      2.85        -36.98       -33.01            0.00            0.00            0.00             0.00            
VZP-2(config-if-pon-1/16/7)#
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

**Como verificar as informações da wan de uma ONT**

```
VZP-1(config-if-pon-1/10/1)# show onu wan-info 15

--------------------------------------
wan_index: 1
wan_name: INTERNET_R_VID_2617
wan_vlan: 2617
wan_cos: 65535
connect_type: ROUTE 
wan_dsp: PPPOE 
qos_status: disable 
wan_status: up 
stack_mode: ipv4 
wan_ip: 100.64.19.250/255.255.255.255 
wan_gateway: 100.64.0.1 
wan_masterdns: 100.100.100.100 
wan_slavedns: 1.1.1.1 
ipv6-address: ::/0
ipv6-gateway: ::
wan_ipv6_master_dns: ::
wan_ipv6_slave_dns: ::
wan_ipv6_static_prefix: ::/0
onu mac: 90:55:DE:A3:06:03
--------------------------------------

```
**Como mudar usuário e senha web da ONT FiberHome via CLI**

```
VZP-1(config-if-pon-1/10/1)# onu web-cfg 15 index 1 web-user admin web-password Xxxxx1@ group admin 
Set OK!
```
