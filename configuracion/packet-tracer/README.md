# Configuracion Packet Tracer

Estos comandos migran la topologia existente al bloque oficial
`172.23.24.0/21`.

## Orden de aplicacion

1. Guardar un respaldo del `.pkt` funcional con direcciones `172.16.x.x`.
2. Ordenar y etiquetar la vista logica y fisica sin cambiar conexiones.
3. Configurar VLAN y puertos en `SWDistribucionExternos`.
4. Conectar y configurar el servidor unificado `DHCP-DNS-OMI`.
5. Migrar el router `Frontera`.
6. Migrar el router `Alumnos`.
7. Renovar DHCP en terminales y ejecutar todas las pruebas.

## Direccionamiento

| Segmento | VLAN | Red | Gateway |
| --- | ---: | --- | --- |
| Concursantes | Acceso en router Alumnos | `172.23.24.0/23` | `172.23.24.1` |
| Invitados | 40 | `172.23.26.0/23` | `172.23.26.1` |
| Jueces | 10 | `172.23.28.0/27` | `172.23.28.1` |
| Entrenadores | 20 | `172.23.28.64/26` | `172.23.28.65` |
| Prensa | 30 | `172.23.28.128/26` | `172.23.28.129` |
| Infraestructura | 60 | `172.23.28.192/27` | `172.23.28.193` |
| Servidores | 70 | `172.23.28.224/29` | `172.23.28.225` |
| Transito Alumnos-Frontera | No aplica | `172.23.28.232/30` | No aplica |

El servidor `DHCP-DNS-OMI` usa `172.23.28.226/29`, gateway
`172.23.28.225` y DNS `172.23.28.226`.

## Puertos de distribucion

| Puerto | Uso | VLAN |
| --- | --- | ---: |
| Fa0/1-2 | Prensa | 30 |
| Fa0/10-11 | Entrenadores | 20 |
| Fa0/15 | Jueces | 10 |
| Fa0/20-22 | Invitados y espera | 40 |
| Fa0/24 | Servidor DHCP-DNS-OMI | 70 |
| Gi0/1 | Troncal hacia Frontera | 10, 20, 30, 40, 60, 70 |

Si el servidor esta conectado a otro puerto, aplicar la configuracion de
`Fa0/24` al puerto real.

## Estado real

- La topologia final fue migrada al bloque `172.23.24.0/21`.
- `DHCP-DNS-OMI` es el unico servidor DHCP interno activo.
- Se validaron DHCP, DNS, EIGRP, NAT, Internet, troncales y aislamiento.
- El respaldo anterior a la migracion debe conservarse fuera del entregable.
- La secuencia detallada vive en `08-plan-final-implementacion.md`.
- El acomodo y cableado se documentan en `09-acomodo-cableado-visual.md`.
- Las politicas de aislamiento implementadas viven en `10-politicas-acceso.md`.

## Nota visual

Si el espacio logico aparece en blanco, usar el boton **Reset Zoom** identificado
con una lupa y la letra `R`. Despues seleccionar **Logical** y volver al cluster
`Root`.
