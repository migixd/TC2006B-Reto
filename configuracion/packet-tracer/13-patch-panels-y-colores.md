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

## Fiber Patch Panels

Los Fiber Patch Panels se mantienen instalados, montados y etiquetados como
infraestructura disponible del campus. Sus puertos permanecen libres porque la
topologia logica actual no contiene enlaces de fibra y los uplinks funcionales
terminan en switches `2960-24TT` mediante cobre.

No conectar los Fiber Patch Panels entre si: hacerlo agregaria enlaces que no
existen en el diseno logico.

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
| `CIT-P3-CPP-01` | 1 | Primera terminal de Congreso | Conservar su puerto actual |
| `CIT-P3-CPP-01` | 2 | Segunda terminal de Congreso | Conservar su puerto actual |
| `CIT-P3-CPP-01` | 3 | Tercera terminal de Congreso | Conservar su puerto actual |
| `CIT-P3-CPP-01` | 4 | Cuarta terminal de Congreso | Conservar su puerto actual |
| `CIT-P3-CPP-01` | 5 | Quinta terminal de Congreso | Conservar su puerto actual |
| `ENH-P2-CPP-01` | 1 | Terminal representativa de Aula 1223 | Conservar su puerto actual |
| `ENH-P2-CPP-01` | 2 | Terminal representativa de Aula 1224 | Conservar su puerto actual |
| `ENH-P2-CPP-01` | 3 | Terminal representativa de Finanzas | Conservar su puerto actual |
| `EIC-P1-CPP-01` | 1 | Terminal representativa de Aula 12102 | Conservar su puerto actual |
| `EIC-P1-CPP-01` | 2 en adelante | Terminales de IA/Jueces | Conservar su puerto actual |
| `CIT-P1-CPP-02` | 1 en adelante | Terminales de Entrenadores/espera | Conservar su puerto actual |
| `ENH-P1-CPP-01` | 1 en adelante | Terminales/AP de Prensa e invitados | Conservar su puerto actual |

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
| Negro | Infraestructura externa o enlaces sin categoria del evento |

## Secuencia segura

1. Guardar una copia del `.pkt`.
2. Colocar y nombrar todos los paneles.
3. Dejar libres los puertos de los Fiber Patch Panels.
4. Elegir una terminal como piloto de cobre.
5. Anotar el puerto actual del switch y eliminar solo su enlace directo.
6. Construir la cadena por el Copper Patch Panel y su Copper Wall Mount.
7. Validar DHCP, gateway, DNS e Internet.
8. Repetir una terminal a la vez.
9. Aplicar colores al finalizar.
