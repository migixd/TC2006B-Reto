# Configuracion Packet Tracer

Estos comandos migran la topologia existente al bloque oficial
`172.23.24.0/21`.

## Orden de aplicacion

1. Configurar `SWDistribucionExternos`.
2. Configurar switches de acceso: `Jueces`, `Entrenadores` y `Reporteros`.
3. Configurar router `Alumnos`.
4. Configurar router `Frontera`.
5. Configurar el servidor `DHCP-DNS-OMI`.
6. Renovar DHCP en las computadoras y ejecutar las pruebas.

## Direccionamiento

| Segmento | VLAN | Red | Gateway |
| --- | ---: | --- | --- |
| Concursantes | Acceso en router Alumnos | `172.23.24.0/23` | `172.23.24.1` |
| Jueces | 20 | `172.23.26.0/27` | `172.23.26.1` |
| Entrenadores | 30 | `172.23.26.32/27` | `172.23.26.33` |
| Prensa | 40 | `172.23.26.64/27` | `172.23.26.65` |
| Invitados | 50 | `172.23.26.96/27` | `172.23.26.97` |
| Infraestructura | 60 | `172.23.26.128/27` | `172.23.26.129` |
| Servidores | 70 | `172.23.26.160/29` | `172.23.26.161` |
| Transito Alumnos-Frontera | No aplica | `172.23.26.168/30` | No aplica |

El servidor `DHCP-DNS-OMI` usa `172.23.26.162/29`, gateway
`172.23.26.161` y DNS `172.23.26.162`.

## Puertos de distribucion

| Puerto | Uso | VLAN |
| --- | --- | ---: |
| Fa0/1-2 | Prensa | 40 |
| Fa0/10-11 | Entrenadores | 30 |
| Fa0/15 | Jueces | 20 |
| Fa0/20 | Invitados | 50 |
| Fa0/24 | Servidor DHCP-DNS-OMI | 70 |
| Gi0/1 | Troncal hacia Frontera | 20, 30, 40, 50, 60, 70 |

Si el servidor esta conectado a otro puerto, aplicar la configuracion de
`Fa0/24` al puerto real.

## Nota visual

Si el espacio logico aparece en blanco, usar el boton **Reset Zoom** identificado
con una lupa y la letra `R`. Despues seleccionar **Logical** y volver al cluster
`Root`.

