# Arquitectura de red

## Segmentacion

| VLAN | Segmento | Subred | Gateway propuesto | Hosts utiles |
| ---: | --- | --- | --- | ---: |
| Acceso en router Alumnos | Concursantes | `172.23.24.0/23` | `172.23.24.1` | 510 |
| 10 | Jueces | `172.23.26.0/27` | `172.23.26.1` | 30 |
| 20 | Entrenadores | `172.23.26.32/27` | `172.23.26.33` | 30 |
| 30 | Prensa | `172.23.26.64/27` | `172.23.26.65` | 30 |
| 40 | Invitados | `172.23.26.96/27` | `172.23.26.97` | 30 |
| 60 | Infraestructura | `172.23.26.128/27` | `172.23.26.129` | 30 |
| 70 | Servidores | `172.23.26.160/29` | `172.23.26.161` | 6 |
| No aplica | Transito Alumnos-Frontera | `172.23.26.168/30` | No aplica | 2 |

Servidor `DHCP-DNS-OMI`: `172.23.26.162/29`.

## Topologia propuesta

```mermaid
flowchart LR
  Internet --> Frontera["Router de frontera / NAT"]
  Frontera --> Core["Distribucion OMI"]
  Core --> CIT["Acceso CIT"]
  Core --> ENH["Acceso ENH"]
  Core --> EIC["Acceso EIC"]
  Core --> Servidor["DHCP-DNS-OMI"]
```

## Politicas minimas

| Origen | DNS/DHCP | Internet | Otros segmentos |
| --- | --- | --- | --- |
| Concursantes | Permitido | Segun evento | Denegado salvo servicios autorizados |
| Jueces | Permitido | Permitido | Acceso administrativo autorizado |
| Entrenadores | Permitido | Permitido | Denegado a concursantes |
| Prensa | Permitido | Permitido | Denegado |
| Invitados | Permitido | Permitido | Denegado |
| Infraestructura | Permitido | Restringido | Administracion autorizada |

## Nota de implementacion

La topologia validada conserva las VLAN existentes 10 a 40, pero aun usa
direcciones `172.16.x.x`. La configuracion de migracion corregida vive en
`configuracion/packet-tracer/` y adapta nombres, VLAN, pools DHCP,
subinterfaces, rutas y NAT a esta arquitectura.
