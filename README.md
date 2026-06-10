# TC2006B Reto - Red OMI Campus Chihuahua

Documentación SDD y archivos de trabajo para el diseño físico y lógico de red
de la XXV Olimpiada Mexicana de Informática en Tec de Monterrey Campus
Chihuahua.

## Navegación

- `AGENTS.md`: reglas para trabajar en el repositorio.
- `docs/README.md`: índice de la fuente de verdad.
- `configuracion/packet-tracer/`: comandos y orden para migrar la topología.
- `entregables/ActReto03.pkt`: copia del archivo Packet Tracer de trabajo.
- `entregables/ActReto03-reporte-borrador.pdf`: reporte pendiente de capturas finales.
- `referencias/configuracion-heredada.rtf`: configuración anterior para consulta.

## Estado crítico

La copia `entregables/ActReto03.pkt` ya usa el bloque oficial
`172.23.24.0/21`. Se validaron DHCP, DNS, EIGRP, NAT, salida a Internet,
troncales y aislamiento de concursantes. La redistribución física por edificios
y closets está en progreso: todavía faltan conexiones y equipos terminales
representativos en varios espacios. También quedan pendientes las capturas y la
integración del reporte final.
