# Patch panels, wall mounts y colores

Esta guia completa el cableado estructurado sin alterar las configuraciones de
VLAN, direccionamiento o routing.

## Restriccion tecnica

Los switches `2960-24TT` de la topologia tienen interfaces Ethernet de cobre y
no tienen interfaces de fibra utilizables. Por ello:

- Los Copper Patch Panels se integran a los enlaces horizontales de terminales.
- Los Fiber Patch Panels representan el backbone entre closets.
- Los uplinks activos de los switches se conservan como estan.
- No se conecta un Fiber Patch Panel directamente a un `2960-24TT`.

## Backbone de fibra representativo

Conectar los Fiber Patch Panels entre si con cable `Fiber` sin retirar los
uplinks funcionales existentes.

| Panel origen | Puerto | Panel destino | Puerto | Etiqueta |
| --- | ---: | --- | ---: | --- |
| `CIT-P1-FPP-01` | 1 | `CIT-P3-FPP-01` | 1 | `TRK-CIT-P1-P3` |
| `CIT-P1-FPP-01` | 2 | `ENH-P1-FPP-01` | 1 | `TRK-CIT-ENH` |
| `ENH-P1-FPP-01` | 2 | `ENH-P2-FPP-01` | 1 | `TRK-ENH-P1-P2` |
| `CIT-P1-FPP-01` | 3 | `EIC-P1-FPP-01` | 1 | `TRK-CIT-EIC` |

Si Packet Tracer muestra nombres distintos a `1`, usar el primer puerto libre
del mismo tipo y conservar la etiqueta de la tabla.

## Cadena horizontal de cobre

Para cada terminal cableada que ya funciona:

```text
puerto actual del switch
  -> frente del Copper Patch Panel
  -> parte posterior del Copper Patch Panel
  -> parte posterior del Copper Wall Mount
  -> frente del Copper Wall Mount
  -> terminal
```

Usar `Copper Straight-Through` en toda la cadena. Mantener el mismo puerto del
switch que utilizaba el enlace directo.

Implementar primero una sola cadena piloto. Validar DHCP y ping antes de
repetirla.

## Asignacion de puertos de cobre

| Closet / panel | Puerto panel | Destino horizontal | Switch y puerto que debe conservarse |
| --- | ---: | --- | --- |
| `CIT-P3-PP-01` | 1 | `PC-CIT-CONG-01` | `SW-CIT-P3-CONG-01 Fa0/1` |
| `CIT-P3-PP-01` | 2 | `PC-CIT-CONG-02` | `SW-CIT-P3-CONG-02 Fa0/1` |
| `CIT-P3-PP-01` | 3 | `PC-CIT-CONG-03` | `SW-CIT-P3-CONG-03 Fa0/1` |
| `CIT-P3-PP-01` | 4 | `PC-CIT-CONG-04` | `SW-CIT-P3-CONG-04 Fa0/1` |
| `CIT-P3-PP-01` | 5 | `PC-CIT-CONG-05` | `SW-CIT-P3-CONG-05 Fa0/1` |
| `ENH-P2-PP-01` | 1 | `PC-ENH-1223` | `SW-ENH-P2-1223 Fa0/1` |
| `ENH-P2-PP-01` | 2 | `PC-ENH-1224` | `SW-ENH-P2-1224 Fa0/1` |
| `ENH-P2-PP-01` | 3 | `PC-ENH-FIN` | `SW-ENH-P2-FIN Fa0/1` |
| `EIC-P1-PP-01` | 1 | `PC-EIC-12102` | `SW-EIC-P1-12102 Fa0/1` |
| `EIC-P1-PP-01` | 2 | `PC-EIC-JUEZ` | Conservar su puerto actual |
| `CIT-P1-PP-01` | 1 | `PC-CIT-ENTRENADOR` | Conservar su puerto actual |
| `ENH-P1-PP-01` | 1 | `PC-ENH-PRENSA` | Conservar su puerto actual |
| `ENH-P1-PP-01` | 2 | `AP-ENH-P1-CONSEJO` | Conservar su puerto actual |
| `ENH-P1-PP-01` | 3 | `AP-ENH-P1-INVITADOS-01` | Conservar su puerto actual |
| `CIT-P1-PP-01` | 2 | `AP-CIT-P1-7101` | Conservar su puerto actual |
| `EIC-P1-PP-01` | 3 | `AP-EIC-P1-IA` | Conservar su puerto actual |

No pasar por patch panel los enlaces entre routers, entre switches, ni los
servidores ubicados dentro del mismo rack.

## Colores

Aplicar el color al cable desde la herramienta de color de cables de Packet
Tracer. El color es visual y no reemplaza el tipo correcto de cable.

| Color | Uso |
| --- | --- |
| Azul | Cableado horizontal de cobre hacia terminales y AP |
| Verde | Uplinks de la red de concursantes |
| Amarillo | Enlaces de Jueces, Entrenadores, Prensa e Invitados |
| Rojo | Router a router, transito y WAN |
| Morado | Servidores e infraestructura |
| Naranja | Backbone representado mediante Fiber Patch Panels |

## Secuencia segura

1. Guardar una copia del `.pkt`.
2. Colocar y nombrar todos los paneles.
3. Conectar los cuatro enlaces representativos de fibra.
4. Elegir `PC-ENH-FIN` como piloto de cobre.
5. Anotar el puerto actual del switch y eliminar solo su enlace directo.
6. Construir la cadena por `ENH-P2-PP-01` puerto 3 y su Copper Wall Mount.
7. Validar DHCP, gateway, DNS e Internet.
8. Repetir una terminal a la vez.
9. Aplicar colores al finalizar.

