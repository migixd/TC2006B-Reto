# TC2006B Reto - Red OMI Campus Chihuahua

Documentación SDD y archivos de trabajo para el diseño físico y lógico de red
de la XXV Olimpiada Mexicana de Informática en Tec de Monterrey Campus
Chihuahua.

## Navegación

- `AGENTS.md`: reglas para trabajar en el repositorio.
- `docs/README.md`: índice de la fuente de verdad.
- `configuracion/packet-tracer/`: comandos y orden para migrar la topología.
- `entregables/ActReto03.pkt`: respaldo del entregable físico anterior.
- `entregables/ActReto04-FINAL.pkt`: archivo Packet Tracer final.
- `entregables/ActReto03-reporte-borrador.pdf`: reporte pendiente de capturas finales.
- `referencias/configuracion-heredada.rtf`: configuración anterior para consulta.

## Estado crítico

El archivo `entregables/ActReto04-FINAL.pkt` contiene la topología lógica y el
acomodo físico final por edificios, Wiring Closets y racks. Incluye patch
panels, wall mounts, nomenclatura y código visual de cableado. La red utiliza el
bloque oficial `172.23.24.0/21`; se validaron DHCP, DNS, EIGRP, NAT, salida a
Internet, troncales y aislamiento de concursantes. Quedan pendientes las
capturas y la integración del reporte final.
