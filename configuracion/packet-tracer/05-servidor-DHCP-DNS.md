# Servidor DHCP-DNS-OMI

## Interfaz

En **Desktop > IP Configuration**:

- IP: `172.23.28.226`
- Mascara: `255.255.255.248`
- Gateway: `172.23.28.225`
- DNS: `172.23.28.226`

## Pools DHCP

En **Services > DHCP**, activar el servicio y crear:

| Pool | Gateway | DNS | Inicio | Mascara | Maximo |
| --- | --- | --- | --- | --- | ---: |
| CONCURSANTES | `172.23.24.1` | `172.23.28.226` | `172.23.24.10` | `255.255.254.0` | 330 |
| INVITADOS | `172.23.26.1` | `172.23.28.226` | `172.23.26.10` | `255.255.254.0` | 300 |
| JUECES | `172.23.28.1` | `172.23.28.226` | `172.23.28.10` | `255.255.255.224` | 20 |
| ENTRENADORES | `172.23.28.65` | `172.23.28.226` | `172.23.28.70` | `255.255.255.192` | 40 |
| PRENSA | `172.23.28.129` | `172.23.28.226` | `172.23.28.135` | `255.255.255.192` | 32 |
| INFRAESTRUCTURA | `172.23.28.193` | `172.23.28.226` | `172.23.28.200` | `255.255.255.224` | 20 |

No crear pool para Servidores; sus direcciones deben ser estaticas.

## DNS

En **Services > DNS**, activar el servicio y agregar:

| Nombre | Direccion |
| --- | --- |
| `dhcp-dns-omi.local` | `172.23.28.226` |
