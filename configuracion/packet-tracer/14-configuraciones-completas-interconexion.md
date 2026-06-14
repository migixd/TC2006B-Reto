# Configuraciones de equipos de interconexión

Estas configuraciones corresponden a la topología final `ActReto05-FINAL.pkt`.
Antes de pegar comandos, guardar una copia del archivo.

## Credenciales comunes solicitadas por la rúbrica

Aplicar este bloque en **Alumnos**, **Frontera**, `DIST-ALUMNOS`,
`SWDistribucionExternos` y cada switch de acceso. Este bloque se agrega para
cumplir la rúbrica; verificarlo en Packet Tracer antes de entregar.

```cisco
enable
configure terminal
enable secret OMI2026
service password-encryption
banner motd # ACCESO EXCLUSIVO PERSONAL AUTORIZADO OMI #

line console 0
 password ConsolaOMI
 login
 logging synchronous
 exit

line vty 0 4
 password VTYOMI
 login
 exit

end
write memory
```

## Router Alumnos

```cisco
enable
configure terminal
hostname Alumnos

interface GigabitEthernet0/0
 description LAN CONCURSANTES
 ip address 172.23.24.1 255.255.254.0
 ip helper-address 172.23.28.226
 no shutdown

interface GigabitEthernet0/1
 description TRANSITO A FRONTERA
 ip address 172.23.28.233 255.255.255.252
 no shutdown

router eigrp 777
 network 172.23.24.0 0.0.1.255
 network 172.23.28.232 0.0.0.3
 no auto-summary

ip route 0.0.0.0 0.0.0.0 172.23.28.234
end
write memory
```

## Router Frontera

```cisco
enable
configure terminal
hostname Frontera

interface GigabitEthernet0/0
 description TRANSITO A CONCURSANTES
 ip address 172.23.28.234 255.255.255.252
 ip nat inside
 no shutdown

interface GigabitEthernet0/1
 description TRONCAL SEGMENTOS OMI
 no ip address
 no shutdown

interface GigabitEthernet0/1.10
 description JUECES
 encapsulation dot1Q 10
 ip address 172.23.28.1 255.255.255.224
 ip helper-address 172.23.28.226
 ip nat inside

interface GigabitEthernet0/1.20
 description ENTRENADORES
 encapsulation dot1Q 20
 ip address 172.23.28.65 255.255.255.192
 ip helper-address 172.23.28.226
 ip nat inside

interface GigabitEthernet0/1.30
 description PRENSA
 encapsulation dot1Q 30
 ip address 172.23.28.129 255.255.255.192
 ip helper-address 172.23.28.226
 ip nat inside

interface GigabitEthernet0/1.40
 description INVITADOS
 encapsulation dot1Q 40
 ip address 172.23.26.1 255.255.254.0
 ip helper-address 172.23.28.226
 ip nat inside

interface GigabitEthernet0/1.60
 description INFRAESTRUCTURA
 encapsulation dot1Q 60
 ip address 172.23.28.193 255.255.255.224
 ip helper-address 172.23.28.226
 ip nat inside

interface GigabitEthernet0/1.70
 description SERVIDORES
 encapsulation dot1Q 70
 ip address 172.23.28.225 255.255.255.248
 ip nat inside

interface GigabitEthernet0/2
 description CAMPUS
 ip address 10.32.100.100 255.255.255.0
 ip nat outside
 no shutdown

router eigrp 777
 network 172.23.24.0 0.0.7.255
 no auto-summary

access-list 7 permit 172.23.24.0 0.0.7.255
ip nat inside source list 7 interface GigabitEthernet0/2 overload
ip route 0.0.0.0 0.0.0.0 10.32.100.1

ip access-list extended BLOQUEAR-CONCURSANTES
 deny ip 172.23.26.0 0.0.1.255 172.23.24.0 0.0.1.255
 deny ip 172.23.28.64 0.0.0.63 172.23.24.0 0.0.1.255
 deny ip 172.23.28.128 0.0.0.63 172.23.24.0 0.0.1.255
 permit ip any any

interface GigabitEthernet0/0
 ip access-group BLOQUEAR-CONCURSANTES out
end
write memory
```

## SWDistribucionExternos

```cisco
enable
configure terminal
hostname SWDistribucionExternos
vlan 10
 name JUECES
vlan 20
 name ENTRENADORES
vlan 30
 name PRENSA
vlan 40
 name INVITADOS
vlan 60
 name INFRAESTRUCTURA
vlan 70
 name SERVIDORES

interface range FastEthernet0/1 - 2
 switchport mode access
 switchport access vlan 30
 spanning-tree portfast
interface range FastEthernet0/10 - 11
 switchport mode access
 switchport access vlan 20
 spanning-tree portfast
interface FastEthernet0/15
 switchport mode access
 switchport access vlan 10
 spanning-tree portfast
interface range FastEthernet0/20 - 22
 switchport mode access
 switchport access vlan 40
 spanning-tree portfast
interface FastEthernet0/24
 switchport mode access
 switchport access vlan 70
 spanning-tree portfast
interface GigabitEthernet0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,60,70
end
write memory
```

## DIST-ALUMNOS

No crear VLAN adicionales ni cambiar sus enlaces, porque actualmente distribuye
la LAN de concursantes directamente hacia `Alumnos Gi0/0`.

```cisco
enable
configure terminal
hostname DIST-ALUMNOS
interface GigabitEthernet0/1
 description ROUTER ALUMNOS GI0/0
interface range FastEthernet0/1 - 11
 description UPLINK SWITCH ACCESO CONCURSANTES
end
write memory
```

## Switches de concursantes

Aplicar el siguiente bloque individualmente y cambiar `<HOSTNAME>` por uno de
los nombres indicados:

- `SW-CIT-P3-CONG-01`
- `SW-CIT-P3-CONG-02`
- `SW-CIT-P3-CONG-03`
- `SW-CIT-P3-CONG-04`
- `SW-CIT-P3-CONG-05`
- `SW-ALUMNOS-RESERVA-01`
- `SW-ALUMNOS-RESERVA-02`
- `SW-ENH-P2-1223`
- `SW-ENH-P2-1224`
- `SW-EIC-P1-12102`
- `SW-ENH-P2-FIN`

```cisco
enable
configure terminal
hostname <HOSTNAME>
interface range FastEthernet0/1 - 23
 description TERMINALES CONCURSANTES
 switchport mode access
 spanning-tree portfast
interface FastEthernet0/24
 description UPLINK DIST-ALUMNOS
 switchport mode access
end
write memory
```

## SW-EIC-P1-JUECES

```cisco
enable
configure terminal
hostname SW-EIC-P1-JUECES
vlan 10
 name JUECES
interface range FastEthernet0/1 - 24
 switchport mode access
 switchport access vlan 10
 spanning-tree portfast
interface range GigabitEthernet0/1 - 2
 switchport mode access
 switchport access vlan 10
 spanning-tree portfast
end
write memory
```

## SW-CIT-P1-ENTRENADORES

```cisco
enable
configure terminal
hostname SW-CIT-P1-ENTRENADORES
vlan 20
 name ENTRENADORES
interface range FastEthernet0/1 - 24
 switchport mode access
 switchport access vlan 20
 spanning-tree portfast
interface range GigabitEthernet0/1 - 2
 switchport mode access
 switchport access vlan 20
 spanning-tree portfast
end
write memory
```

## SW-ENH-P1-PRENSA

```cisco
enable
configure terminal
hostname SW-ENH-P1-PRENSA
vlan 30
 name PRENSA
interface range FastEthernet0/1 - 24
 switchport mode access
 switchport access vlan 30
 spanning-tree portfast
interface range GigabitEthernet0/1 - 2
 switchport mode access
 switchport access vlan 30
 spanning-tree portfast
end
write memory
```

## Access Points

Los AP de Packet Tracer se configuran desde **Config**, no mediante CLI:

- AP de invitados: puerto cableado conectado a VLAN 40.
- AP de entrenadores: puerto cableado conectado a VLAN 20.
- AP de prensa: puerto cableado conectado a VLAN 30.
- Asignar SSID descriptivo y utilizar DHCP para los clientes inalámbricos.

## Servidor DHCP-DNS-OMI

- IP: `172.23.28.226`
- Máscara: `255.255.255.248`
- Gateway: `172.23.28.225`
- DNS: `172.23.28.226`
- DNS A: `dhcp-dns-omi.local` → `172.23.28.226`

Pools:

| Pool | Inicio | Máscara | Gateway | Máximo |
| --- | --- | --- | --- | ---: |
| CONCURSANTES | 172.23.24.10 | 255.255.254.0 | 172.23.24.1 | 330 |
| INVITADOS | 172.23.26.10 | 255.255.254.0 | 172.23.26.1 | 300 |
| JUECES | 172.23.28.10 | 255.255.255.224 | 172.23.28.1 | 20 |
| ENTRENADORES | 172.23.28.70 | 255.255.255.192 | 172.23.28.65 | 40 |
| PRENSA | 172.23.28.135 | 255.255.255.192 | 172.23.28.129 | 32 |
| INFRAESTRUCTURA | 172.23.28.200 | 255.255.255.224 | 172.23.28.193 | 20 |

## Equipos que no deben modificarse sin revisar su configuración

`CampusCore`, `FronteraCampus`, router Internet y los servidores externos
simulan la infraestructura institucional y la salida externa. Mantenerlos como
están mientras respondan correctamente las pruebas hacia `200.1.1.1`.

## Verificación

```cisco
show ip interface brief
show ip route
show ip eigrp neighbors
show ip nat translations
show ip nat statistics
show vlan brief
show interfaces trunk
show cdp neighbors
```
