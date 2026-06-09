# Servidor DHCP-DNS-OMI

## Interfaz

En **Desktop > IP Configuration**:

- IP: `172.23.26.162`
- Mascara: `255.255.255.248`
- Gateway: `172.23.26.161`
- DNS: `172.23.26.162`

## Pools DHCP

En **Services > DHCP**, activar el servicio y crear:

| Pool | Gateway | DNS | Inicio | Mascara | Maximo |
| --- | --- | --- | --- | --- | ---: |
| CONCURSANTES | `172.23.24.1` | `172.23.26.162` | `172.23.24.10` | `255.255.254.0` | 330 |
| JUECES | `172.23.26.1` | `172.23.26.162` | `172.23.26.10` | `255.255.255.224` | 20 |
| ENTRENADORES | `172.23.26.33` | `172.23.26.162` | `172.23.26.40` | `255.255.255.224` | 20 |
| PRENSA | `172.23.26.65` | `172.23.26.162` | `172.23.26.70` | `255.255.255.224` | 20 |
| INVITADOS | `172.23.26.97` | `172.23.26.162` | `172.23.26.100` | `255.255.255.224` | 20 |
| INFRAESTRUCTURA | `172.23.26.129` | `172.23.26.162` | `172.23.26.130` | `255.255.255.224` | 20 |

No crear pool para Servidores; sus direcciones deben ser estaticas.

## DNS

En **Services > DNS**, activar el servicio y agregar:

| Nombre | Direccion |
| --- | --- |
| `dhcp-dns-omi.local` | `172.23.26.162` |

