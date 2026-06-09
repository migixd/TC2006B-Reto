# Acomodo, cableado y elementos visuales

## Vista logica

Ordenar de izquierda a derecha:

1. Concursantes agrupados por edificio y espacio.
2. `DIST-ALUMNOS`, router `Alumnos`, router `Frontera`.
3. `SWDistribucionExternos` y segmentos Jueces, Entrenadores, Prensa e Invitados.
4. Campus, Internet y servidores.

## Colores de zonas

| Segmento | Color de zona |
| --- | --- |
| Concursantes | Verde |
| Jueces | Turquesa |
| Entrenadores | Amarillo |
| Prensa | Magenta |
| Invitados y espera | Naranja |
| Campus/Internet/servidores | Morado |

## Tipos de cable funcionales

| Conexion | Cable Packet Tracer |
| --- | --- |
| PC, servidor o AP a switch | Copper Straight-Through |
| Router a switch | Copper Straight-Through |
| Switch de distribucion a switch de acceso | Copper Cross-Over |
| Router a router Ethernet | Copper Cross-Over |
| Backbone entre edificios/pisos | Fiber, cuando los equipos tengan puertos compatibles |

Packet Tracer determina el aspecto/color del cable segun su tipo. No sustituir
un enlace funcional solo para cambiar su color.

## Cableado estructurado representado

- Copper Patch Panels: distribución horizontal hacia espacios.
- Fiber Patch Panels: backbone entre MDF/IDF y edificios.
- Los paneles pueden permanecer como representación etiquetada si insertar el
  panel en el enlace rompe la topologia funcional.
- Los cables directos de un switch de área a sus PCs no requieren TO ni patch
  panel según las notas de la actividad.

## Backbone fisico documentado

```text
CIT-MDF-P1
├── fibra → CIT-IDF-P3
├── fibra → ENH-MDF-P1 → fibra → ENH-IDF-P2
└── fibra → EIC-MDF-P1
```

## Etiquetas de enlaces

| Enlace | Etiqueta |
| --- | --- |
| CIT MDF a CIT IDF | `TRK-CIT-P1-P3` |
| CIT a ENH | `TRK-CIT-ENH` |
| ENH P1 a ENH P2 | `TRK-ENH-P1-P2` |
| CIT a EIC | `TRK-CIT-EIC` |

