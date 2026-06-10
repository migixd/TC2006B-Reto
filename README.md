# TC2006B Reto - Red OMI Campus Chihuahua

Documentacion SDD y archivos de trabajo para el diseno fisico y logico de red
de la XXV Olimpiada Mexicana de Informatica en Tec de Monterrey Campus
Chihuahua.

## Navegacion

- `AGENTS.md`: reglas para trabajar en el repositorio.
- `docs/README.md`: indice de la fuente de verdad.
- `configuracion/packet-tracer/`: comandos y orden para migrar la topologia.
- `entregables/ActReto03.pkt`: copia del archivo Packet Tracer de trabajo.
- `entregables/ActReto03-reporte-borrador.pdf`: reporte pendiente de capturas finales.
- `referencias/configuracion-heredada.rtf`: configuracion anterior para consulta.

## Estado critico

La copia `entregables/ActReto03.pkt` ya usa el bloque oficial
`172.23.24.0/21`. Se validaron DHCP, DNS, EIGRP, NAT, salida a Internet,
troncales y aislamiento de concursantes. La redistribucion fisica por edificios
y closets esta en progreso: todavia faltan conexiones y equipos terminales
representativos en varios espacios. Tambien quedan pendientes las capturas y la
integracion del reporte final.
