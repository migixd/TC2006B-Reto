# Configuraciones completas de equipos de interconexión

Guía autocontenida para configurar desde cero los equipos OMI de la topología
de Cisco Packet Tracer. Cada bloque IOS incluye hostname, interfaces, VLAN,
enrutamiento o seguridad según corresponda, contraseñas y guardado.

## Credenciales

| Uso | Contraseña |
| --- | --- |
| Consola | `ConsolaOMI` |
| Modo privilegiado `enable` | `OMI2026` |
| Líneas VTY | `VTYOMI` |

## Router Alumnos

Conexiones:

- `Gi0/0` a `DIST-ALUMNOS Gi0/1`.
- `Gi0/1` a `Frontera Gi0/0`.

```cisco
enable
configure terminal
hostname Alumnos
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

interface GigabitEthernet0/0
 description LAN CONCURSANTES HACIA DIST-ALUMNOS
 ip address 172.23.24.1 255.255.254.0
 ip helper-address 172.23.28.226
 no shutdown
 exit

interface GigabitEthernet0/1
 description TRANSITO HACIA FRONTERA
 ip address 172.23.28.233 255.255.255.252
 no shutdown
 exit

router eigrp 777
 network 172.23.24.0 0.0.1.255
 network 172.23.28.232 0.0.0.3
 no auto-summary
 exit

ip route 0.0.0.0 0.0.0.0 172.23.28.234
end
write memory
```

## Router Frontera

Conexiones:

- `Gi0/0` a `Alumnos Gi0/1`.
- `Gi0/1` a `SWDistribucionExternos Gi0/1`.
- `Gi0/2` a `FronteraCampus Gi0/0`.

```cisco
enable
configure terminal
hostname Frontera
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

interface GigabitEthernet0/0
 description TRANSITO HACIA ALUMNOS
 ip address 172.23.28.234 255.255.255.252
 ip nat inside
 no shutdown
 exit

interface GigabitEthernet0/1
 description TRONCAL HACIA SWDistribucionExternos
 no ip address
 no shutdown
 exit

interface GigabitEthernet0/1.10
 description JUECES
 encapsulation dot1Q 10
 ip address 172.23.28.1 255.255.255.224
 ip helper-address 172.23.28.226
 ip nat inside
 exit

interface GigabitEthernet0/1.20
 description ENTRENADORES
 encapsulation dot1Q 20
 ip address 172.23.28.65 255.255.255.192
 ip helper-address 172.23.28.226
 ip nat inside
 exit

interface GigabitEthernet0/1.30
 description PRENSA
 encapsulation dot1Q 30
 ip address 172.23.28.129 255.255.255.192
 ip helper-address 172.23.28.226
 ip nat inside
 exit

interface GigabitEthernet0/1.40
 description INVITADOS
 encapsulation dot1Q 40
 ip address 172.23.26.1 255.255.254.0
 ip helper-address 172.23.28.226
 ip nat inside
 exit

interface GigabitEthernet0/1.60
 description INFRAESTRUCTURA
 encapsulation dot1Q 60
 ip address 172.23.28.193 255.255.255.224
 ip helper-address 172.23.28.226
 ip nat inside
 exit

interface GigabitEthernet0/1.70
 description SERVIDORES
 encapsulation dot1Q 70
 ip address 172.23.28.225 255.255.255.248
 ip nat inside
 exit

interface GigabitEthernet0/2
 description SALIDA HACIA CAMPUS
 ip address 10.32.100.100 255.255.255.0
 ip nat outside
 no shutdown
 exit

router eigrp 777
 network 172.23.24.0 0.0.7.255
 no auto-summary
 exit

access-list 7 permit 172.23.24.0 0.0.7.255
ip nat inside source list 7 interface GigabitEthernet0/2 overload
ip route 0.0.0.0 0.0.0.0 10.32.100.1

ip access-list extended BLOQUEAR-CONCURSANTES
 deny ip 172.23.26.0 0.0.1.255 172.23.24.0 0.0.1.255
 deny ip 172.23.28.64 0.0.0.63 172.23.24.0 0.0.1.255
 deny ip 172.23.28.128 0.0.0.63 172.23.24.0 0.0.1.255
 permit ip any any
 exit

interface GigabitEthernet0/0
 ip access-group BLOQUEAR-CONCURSANTES out
 exit

end
write memory
```

## SWDistribucionExternos

Mapa de puertos:

| Puerto | Destino | VLAN |
| --- | --- | ---: |
| `Fa0/1` | `SW-ENH-P1-PRENSA Fa0/24` | 30 |
| `Fa0/2` | `AP-ENH-P1-CONSEJO Port 0` | 30 |
| `Fa0/10` | `SW-CIT-P1-ENTRENADORES Fa0/24` | 20 |
| `Fa0/11` | `AP-CIT-P1-7101 Port 0` | 20 |
| `Fa0/15` | `SW-EIC-P1-JUECES Fa0/24` | 10 |
| `Fa0/20` | `AP-ENH-P1-INVITADOS-01 Port 0` | 40 |
| `Fa0/21-22` | AP adicionales de invitados | 40 |
| `Fa0/24` | `DHCP-DNS-OMI Fa0` | 70 |
| `Gi0/1` | `Frontera Gi0/1` | Troncal |

```cisco
enable
configure terminal
hostname SWDistribucionExternos
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
 exit

interface range FastEthernet0/10 - 11
 switchport mode access
 switchport access vlan 20
 spanning-tree portfast
 exit

interface FastEthernet0/15
 switchport mode access
 switchport access vlan 10
 spanning-tree portfast
 exit

interface range FastEthernet0/20 - 22
 switchport mode access
 switchport access vlan 40
 spanning-tree portfast
 exit

interface FastEthernet0/24
 switchport mode access
 switchport access vlan 70
 spanning-tree portfast
 exit

interface GigabitEthernet0/1
 description TRONCAL HACIA FRONTERA
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,60,70
 exit

end
write memory
```

## DIST-ALUMNOS

Mapa de puertos:

| Puerto | Destino |
| --- | --- |
| `Fa0/1` | `SW-CIT-P3-CONG-04 Fa0/24` |
| `Fa0/2` | `SW-CIT-P3-CONG-05 Fa0/24` |
| `Fa0/3` | `SW-ALUMNOS-RESERVA-01 Fa0/24` |
| `Fa0/4` | `SW-CIT-P3-CONG-03 Fa0/24` |
| `Fa0/5` | `SW-CIT-P3-CONG-01 Fa0/24` |
| `Fa0/6` | `SW-CIT-P3-CONG-02 Fa0/24` |
| `Fa0/7` | `SW-ALUMNOS-RESERVA-02 Fa0/24` |
| `Fa0/8` | `SW-ENH-P2-1223 Fa0/24` |
| `Fa0/9` | `SW-ENH-P2-1224 Fa0/24` |
| `Fa0/10` | `SW-EIC-P1-12102 Fa0/24` |
| `Fa0/11` | `SW-ENH-P2-FIN Fa0/24` |
| `Gi0/1` | `Alumnos Gi0/0` |

```cisco
enable
configure terminal
hostname DIST-ALUMNOS
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

interface range FastEthernet0/1 - 11
 switchport mode access
 switchport access vlan 1
 exit

interface GigabitEthernet0/1
 description HACIA ROUTER ALUMNOS
 switchport mode access
 switchport access vlan 1
 exit

end
write memory
```

## Switches de acceso para concursantes

En cada switch, `Fa0/24` es el uplink hacia `DIST-ALUMNOS`. Los puertos
`Fa0/1-23` son puertos de terminales concursantes en VLAN 1.

### SW-CIT-P3-CONG-01

```cisco
enable
configure terminal
hostname SW-CIT-P3-CONG-01
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
interface range FastEthernet0/1 - 23
 switchport mode access
 switchport access vlan 1
 spanning-tree portfast
 exit
interface FastEthernet0/24
 description UPLINK DIST-ALUMNOS FA0/5
 switchport mode access
 switchport access vlan 1
 exit
end
write memory
```

### SW-CIT-P3-CONG-02

```cisco
enable
configure terminal
hostname SW-CIT-P3-CONG-02
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
interface range FastEthernet0/1 - 23
 switchport mode access
 switchport access vlan 1
 spanning-tree portfast
 exit
interface FastEthernet0/24
 description UPLINK DIST-ALUMNOS FA0/6
 switchport mode access
 switchport access vlan 1
 exit
end
write memory
```

### SW-CIT-P3-CONG-03

```cisco
enable
configure terminal
hostname SW-CIT-P3-CONG-03
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
interface range FastEthernet0/1 - 23
 switchport mode access
 switchport access vlan 1
 spanning-tree portfast
 exit
interface FastEthernet0/24
 description UPLINK DIST-ALUMNOS FA0/4
 switchport mode access
 switchport access vlan 1
 exit
end
write memory
```

### SW-CIT-P3-CONG-04

```cisco
enable
configure terminal
hostname SW-CIT-P3-CONG-04
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
interface range FastEthernet0/1 - 23
 switchport mode access
 switchport access vlan 1
 spanning-tree portfast
 exit
interface FastEthernet0/24
 description UPLINK DIST-ALUMNOS FA0/1
 switchport mode access
 switchport access vlan 1
 exit
end
write memory
```

### SW-CIT-P3-CONG-05

```cisco
enable
configure terminal
hostname SW-CIT-P3-CONG-05
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
interface range FastEthernet0/1 - 23
 switchport mode access
 switchport access vlan 1
 spanning-tree portfast
 exit
interface FastEthernet0/24
 description UPLINK DIST-ALUMNOS FA0/2
 switchport mode access
 switchport access vlan 1
 exit
end
write memory
```

### SW-ALUMNOS-RESERVA-01

```cisco
enable
configure terminal
hostname SW-ALUMNOS-RESERVA-01
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
interface range FastEthernet0/1 - 23
 switchport mode access
 switchport access vlan 1
 spanning-tree portfast
 exit
interface FastEthernet0/24
 description UPLINK DIST-ALUMNOS FA0/3
 switchport mode access
 switchport access vlan 1
 exit
end
write memory
```

### SW-ALUMNOS-RESERVA-02

```cisco
enable
configure terminal
hostname SW-ALUMNOS-RESERVA-02
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
interface range FastEthernet0/1 - 23
 switchport mode access
 switchport access vlan 1
 spanning-tree portfast
 exit
interface FastEthernet0/24
 description UPLINK DIST-ALUMNOS FA0/7
 switchport mode access
 switchport access vlan 1
 exit
end
write memory
```

### SW-ENH-P2-1223

```cisco
enable
configure terminal
hostname SW-ENH-P2-1223
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
interface range FastEthernet0/1 - 23
 switchport mode access
 switchport access vlan 1
 spanning-tree portfast
 exit
interface FastEthernet0/24
 description UPLINK DIST-ALUMNOS FA0/8
 switchport mode access
 switchport access vlan 1
 exit
end
write memory
```

### SW-ENH-P2-1224

```cisco
enable
configure terminal
hostname SW-ENH-P2-1224
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
interface range FastEthernet0/1 - 23
 switchport mode access
 switchport access vlan 1
 spanning-tree portfast
 exit
interface FastEthernet0/24
 description UPLINK DIST-ALUMNOS FA0/9
 switchport mode access
 switchport access vlan 1
 exit
end
write memory
```

### SW-EIC-P1-12102

```cisco
enable
configure terminal
hostname SW-EIC-P1-12102
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
interface range FastEthernet0/1 - 23
 switchport mode access
 switchport access vlan 1
 spanning-tree portfast
 exit
interface FastEthernet0/24
 description UPLINK DIST-ALUMNOS FA0/10
 switchport mode access
 switchport access vlan 1
 exit
end
write memory
```

### SW-ENH-P2-FIN

```cisco
enable
configure terminal
hostname SW-ENH-P2-FIN
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
interface range FastEthernet0/1 - 23
 switchport mode access
 switchport access vlan 1
 spanning-tree portfast
 exit
interface FastEthernet0/24
 description UPLINK DIST-ALUMNOS FA0/11
 switchport mode access
 switchport access vlan 1
 exit
end
write memory
```

## Switches de segmentos externos

### SW-EIC-P1-JUECES

`Fa0/24` conecta a `SWDistribucionExternos Fa0/15`. Los jueces se conectan por
cable a `Fa0/1-23`; no existe AP de jueces.

```cisco
enable
configure terminal
hostname SW-EIC-P1-JUECES
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
vlan 10
 name JUECES
interface range FastEthernet0/1 - 23
 switchport mode access
 switchport access vlan 10
 spanning-tree portfast
 exit
interface FastEthernet0/24
 description UPLINK SWDistribucionExternos FA0/15
 switchport mode access
 switchport access vlan 10
 exit
end
write memory
```

### SW-CIT-P1-ENTRENADORES

`Fa0/24` conecta a `SWDistribucionExternos Fa0/10`.

```cisco
enable
configure terminal
hostname SW-CIT-P1-ENTRENADORES
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
vlan 20
 name ENTRENADORES
interface range FastEthernet0/1 - 23
 switchport mode access
 switchport access vlan 20
 spanning-tree portfast
 exit
interface FastEthernet0/24
 description UPLINK SWDistribucionExternos FA0/10
 switchport mode access
 switchport access vlan 20
 exit
end
write memory
```

### SW-ENH-P1-PRENSA

`Fa0/24` conecta a `SWDistribucionExternos Fa0/1`.

```cisco
enable
configure terminal
hostname SW-ENH-P1-PRENSA
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
vlan 30
 name PRENSA
interface range FastEthernet0/1 - 23
 switchport mode access
 switchport access vlan 30
 spanning-tree portfast
 exit
interface FastEthernet0/24
 description UPLINK SWDistribucionExternos FA0/1
 switchport mode access
 switchport access vlan 30
 exit
end
write memory
```

## Access Points

### AP-CIT-P1-7101 - Entrenadores

1. Conectar `Port 0` a `SWDistribucionExternos Fa0/11` con
   `Copper Straight-Through`.
2. Abrir el AP y entrar a **Config > Wireless**.
3. Configurar `SSID: OMI-ENTRENADORES`.
4. Seleccionar `WPA2-PSK`.
5. Configurar la clave `EntrenaOMI2026`.
6. En cada laptop de entrenadores, seleccionar `OMI-ENTRENADORES`, escribir la
   clave y elegir DHCP.

### AP-ENH-P1-CONSEJO - Prensa

1. Conectar `Port 0` a `SWDistribucionExternos Fa0/2` con
   `Copper Straight-Through`.
2. Abrir el AP y entrar a **Config > Wireless**.
3. Configurar `SSID: OMI-PRENSA`.
4. Seleccionar `WPA2-PSK`.
5. Configurar la clave `PrensaOMI2026`.
6. En cada laptop de prensa, seleccionar `OMI-PRENSA`, escribir la clave y
   elegir DHCP.

### AP-ENH-P1-INVITADOS-01 - Invitados

1. Conectar `Port 0` a `SWDistribucionExternos Fa0/20` con
   `Copper Straight-Through`.
2. Abrir el AP y entrar a **Config > Wireless**.
3. Configurar `SSID: OMI-INVITADOS`.
4. Seleccionar `WPA2-PSK`.
5. Configurar la clave `InvitadosOMI2026`.
6. En cada laptop invitada, seleccionar `OMI-INVITADOS`, escribir la clave y
   elegir DHCP.

## Servidor DHCP-DNS-OMI

### Interfaz FastEthernet0

En **Desktop > IP Configuration > Static**:

| Campo | Valor |
| --- | --- |
| IP Address | `172.23.28.226` |
| Subnet Mask | `255.255.255.248` |
| Default Gateway | `172.23.28.225` |
| DNS Server | `172.23.28.226` |

Conectar `FastEthernet0` a `SWDistribucionExternos Fa0/24` con
`Copper Straight-Through`.

### DHCP

Entrar a **Services > DHCP**, seleccionar `On` y crear todos los pools:

| Pool | Gateway | DNS | Inicio | Máscara | Máximo |
| --- | --- | --- | --- | --- | ---: |
| CONCURSANTES | `172.23.24.1` | `172.23.28.226` | `172.23.24.10` | `255.255.254.0` | 330 |
| INVITADOS | `172.23.26.1` | `172.23.28.226` | `172.23.26.10` | `255.255.254.0` | 300 |
| JUECES | `172.23.28.1` | `172.23.28.226` | `172.23.28.10` | `255.255.255.224` | 20 |
| ENTRENADORES | `172.23.28.65` | `172.23.28.226` | `172.23.28.70` | `255.255.255.192` | 40 |
| PRENSA | `172.23.28.129` | `172.23.28.226` | `172.23.28.135` | `255.255.255.192` | 32 |
| INFRAESTRUCTURA | `172.23.28.193` | `172.23.28.226` | `172.23.28.200` | `255.255.255.224` | 20 |

### DNS

Entrar a **Services > DNS**, seleccionar `On` y agregar:

| Nombre | Dirección |
| --- | --- |
| `dhcp-dns-omi.local` | `172.23.28.226` |
| `servicios.omi.local` | `172.23.28.226` |
| `concurso.omi.local` | `200.1.1.50` |

### Página web interna

Entrar a **Services > HTTP**, seleccionar `HTTP: On`, editar `index.html` y
guardar:

```html
<html>
<head><title>Servicios OMI</title></head>
<body>
  <h1>Servicios internos de la XXV OMI</h1>
  <p>Servidor DHCP, DNS y servicios internos disponible.</p>
</body>
</html>
```

## Servidor Concurso

1. Abrir `Concurso` y entrar a **Desktop > IP Configuration > Static**.
2. Configurar `IP Address: 200.1.1.50`.
3. Configurar `Subnet Mask: 255.255.255.0`.
4. Configurar `Default Gateway: 200.1.1.1`.
5. Entrar a **Services > HTTP** y seleccionar `HTTP: On`.
6. Editar `index.html` y guardar:

```html
<html>
<head><title>XXV OMI</title></head>
<body>
  <h1>XXV Olimpiada Mexicana de Informática</h1>
  <p>Portal oficial del concurso.</p>
</body>
</html>
```

## Terminales

En cada PC o laptop cableada:

1. Abrir **Desktop > IP Configuration**.
2. Seleccionar `DHCP`.
3. Confirmar dirección, máscara, gateway y DNS del segmento.

Terminales concursantes y switch:

| Terminal | Switch | Puerto |
| --- | --- | --- |
| `PC-CIT-CONG-01` | `SW-CIT-P3-CONG-01` | `Fa0/1` |
| `PC-CIT-CONG-02` | `SW-CIT-P3-CONG-02` | `Fa0/1` |
| `PC-CIT-CONG-03` | `SW-CIT-P3-CONG-03` | `Fa0/1` |
| `PC-CIT-CONG-04` | `SW-CIT-P3-CONG-04` | `Fa0/1` |
| `PC-CIT-CONG-05` | `SW-CIT-P3-CONG-05` | `Fa0/1` |
| `PC-ALUMNOS-RESERVA-01` | `SW-ALUMNOS-RESERVA-01` | Primer puerto libre |
| `PC-ALUMNOS-RESERVA-02` | `SW-ALUMNOS-RESERVA-02` | Primer puerto libre |
| `PC-ENH-1223` | `SW-ENH-P2-1223` | `Fa0/1` |
| `PC-ENH-1224` | `SW-ENH-P2-1224` | `Fa0/1` |
| `PC-EIC-12102` | `SW-EIC-P1-12102` | `Fa0/1` |
| `PC-ENH-FIN` | `SW-ENH-P2-FIN` | `Fa0/1` |

Terminales externos:

| Terminal | Equipo de acceso | Puerto / medio |
| --- | --- | --- |
| `PC-EIC-JUEZ` | `SW-EIC-P1-JUECES` | `Fa0/1` |
| `PC-CIT-ENTRENADOR` | `SW-CIT-P1-ENTRENADORES` | `Fa0/1` |
| `PC-ENH-PRENSA` | `SW-ENH-P1-PRENSA` | `Fa0/1` |
| `Laptop-ENH-INVITADO` | `AP-ENH-P1-INVITADOS-01` | Inalámbrico |

## Verificación completa

### Alumnos

```cisco
show running-config
show ip interface brief
show ip route
show ip eigrp neighbors
ping 172.23.28.234
ping 172.23.28.226
```

### Frontera

Antes de revisar traducciones NAT, generar tráfico desde una PC interna hacia
`200.1.1.1` o `200.1.1.50`.

```cisco
show running-config
show ip interface brief
show ip route
show ip eigrp neighbors
show access-lists
show ip nat translations
show ip nat statistics
ping 172.23.28.233
ping 172.23.28.226
ping 10.32.100.1
```

### Switches

```cisco
show running-config
show vlan brief
show interfaces trunk
show interfaces status
show cdp neighbors
```

### Cada terminal

En **Desktop > Command Prompt**:

```text
ipconfig /all
ping <gateway-del-segmento>
ping 172.23.28.226
ping 200.1.1.1
ping 200.1.1.50
nslookup dhcp-dns-omi.local
nslookup servicios.omi.local
nslookup concurso.omi.local
```

En **Desktop > Web Browser**:

```text
http://servicios.omi.local
http://200.1.1.50
http://concurso.omi.local
```

Prueba de aislamiento desde Invitados, Entrenadores y Prensa:

```text
ping <IP-DE-UN-PC-CONCURSANTE>
```

El ping hacia concursantes debe fallar por la ACL
`BLOQUEAR-CONCURSANTES`. El acceso a DNS, páginas web e Internet debe responder.
