# AGENTS.md

Este paquete documenta el diseno fisico y logico de red para la XXV Olimpiada
Mexicana de Informatica (OMI) en Tec de Monterrey Campus Chihuahua.

Antes de modificar el diseno, leer `docs/README.md` y los documentos base.

## Reglas

- Escribir en espanol y mantener Markdown claro.
- No guardar datos personales ni sensibles.
- Documentar primero cualquier cambio de VLAN, subred, capacidad o permiso.
- Mantener trazabilidad entre la fuente de verdad, Packet Tracer y las pruebas.
- No afirmar que una configuracion esta implementada hasta validarla en el `.pkt`.

## Estado critico

La fuente de verdad y la copia final de Packet Tracer usan el bloque
`172.23.24.0/21`. La conectividad representativa y el aislamiento fueron
validados; faltan las capturas y la integracion del reporte final.
