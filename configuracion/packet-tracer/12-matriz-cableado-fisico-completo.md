# Matriz completa de cableado fisico

Esta guia completa la representacion fisica sin reemplazar enlaces logicos que
ya funcionan. Antes de cada fase guardar una copia del `.pkt`.

## Reglas

- No desconectar un enlace que aparezca verde y funcional solo para cambiar su
  tipo o color.
- Mover equipos a su closet y rack asignado conservando el cable existente.
- Usar `Copper Straight-Through` para terminal/AP/servidor/router a switch.
- Usar `Copper Cross-Over` para switch a switch y router a router.
- Los paneles de fibra pueden permanecer como representacion etiquetada si
  insertarlos rompe la topologia funcional.
- Usar solo terminales representativas; no modelar los 594 concursantes.

## Procedimiento en Packet Tracer

Repetir este procedimiento por cada fase:

1. Guardar una copia incremental del archivo, por ejemplo
   `ActReto03-fisico-fase1.pkt`.
2. Abrir **Physical** y entrar a:
   `Chihuahua > Chihuahua Capital > ITESM Campus Chihuahua`.
3. Entrar al edificio y Wiring Closet indicados en la matriz.
4. Para reubicar un equipo existente, usar **Move Object**, seleccionar el
   equipo y colocarlo dentro del rack destino. No borrarlo ni crear un duplicado.
5. Para crear una conexion nueva, seleccionar **Connections** (rayo), elegir el
   cable indicado, seleccionar el primer equipo y puerto, y despues el segundo
   equipo y puerto.
6. Esperar a que los indicadores de enlace cambien a verde.
7. Cambiar a **Logical** y verificar que la topologia conserve sus enlaces.
8. Ejecutar las pruebas de la seccion de validacion antes de continuar.

Si Packet Tracer no permite arrastrar un equipo directamente entre edificios,
usar **Move Object** desde la barra superior. No utilizar **Delete**.

## Fase 1: equipos centrales en CIT-MDF-P1

Ubicar en `Rack CIT-MDF-P1.1`:

- `Frontera`
- `Alumnos`
- `DIST-ALUMNOS`
- `SWDistribucionExternos`
- `DHCP-DNS-OMI`
- `CampusCore`
- `FronteraCampus`

Mantener y comprobar:

| Origen | Puerto | Destino | Puerto | Cable |
| --- | --- | --- | --- | --- |
| `Alumnos` | `Gi0/0` | `DIST-ALUMNOS` | `Gi0/1` | Copper Straight-Through |
| `Alumnos` | `Gi0/1` | `Frontera` | `Gi0/0` | Copper Cross-Over |
| `Frontera` | `Gi0/1` | `SWDistribucionExternos` | `Gi0/1` | Copper Straight-Through |
| `Frontera` | `Gi0/2` | `FronteraCampus` | `Gi0/0` | Copper Cross-Over |
| `DHCP-DNS-OMI` | `Fa0` | `SWDistribucionExternos` | `Fa0/24` | Copper Straight-Through |

No reconectar estos enlaces si ya aparecen activos.

## Fase 2: concursantes

Todos los uplinks llegan desde `DIST-ALUMNOS` al puerto `Fa0/24` del switch de
acceso. Conservar las conexiones actuales.

| Closet destino | Switch | Puerto DIST-ALUMNOS | Puerto switch |
| --- | --- | --- | --- |
| `CIT-IDF-P3` | `SW-CIT-P3-CONG-04` | `Fa0/1` | `Fa0/24` |
| `CIT-IDF-P3` | `SW-CIT-P3-CONG-05` | `Fa0/2` | `Fa0/24` |
| `CIT-MDF-P1` | `SW-ALUMNOS-RESERVA-01` | `Fa0/3` | `Fa0/24` |
| `CIT-IDF-P3` | `SW-CIT-P3-CONG-03` | `Fa0/4` | `Fa0/24` |
| `CIT-IDF-P3` | `SW-CIT-P3-CONG-01` | `Fa0/5` | `Fa0/24` |
| `CIT-IDF-P3` | `SW-CIT-P3-CONG-02` | `Fa0/6` | `Fa0/24` |
| `CIT-MDF-P1` | `SW-ALUMNOS-RESERVA-02` | `Fa0/7` | `Fa0/24` |
| `ENH-IDF-P2` | `SW-ENH-P2-1223` | `Fa0/8` | `Fa0/24` |
| `ENH-IDF-P2` | `SW-ENH-P2-1224` | `Fa0/9` | `Fa0/24` |
| `EIC-MDF-P1` | `SW-EIC-P1-12102` | `Fa0/10` | `Fa0/24` |
| `ENH-IDF-P2` | `SW-ENH-P2-FIN` | `Fa0/11` | `Fa0/24` |

Cable funcional actual: `Copper Cross-Over`.

### Terminales representativas de concursantes

Agregar una PC por espacio y conectar con `Copper Straight-Through`:

| PC | Switch | Puerto switch |
| --- | --- | --- |
| `PC-CIT-CONG-01` | `SW-CIT-P3-CONG-01` | `Fa0/1` |
| `PC-CIT-CONG-02` | `SW-CIT-P3-CONG-02` | `Fa0/1` |
| `PC-CIT-CONG-03` | `SW-CIT-P3-CONG-03` | `Fa0/1` |
| `PC-CIT-CONG-04` | `SW-CIT-P3-CONG-04` | `Fa0/1` |
| `PC-CIT-CONG-05` | `SW-CIT-P3-CONG-05` | `Fa0/1` |
| `PC-ENH-1223` | `SW-ENH-P2-1223` | `Fa0/1` |
| `PC-ENH-1224` | `SW-ENH-P2-1224` | `Fa0/1` |
| `PC-ENH-FIN` | `SW-ENH-P2-FIN` | `Fa0/1` |
| `PC-EIC-12102` | `SW-EIC-P1-12102` | `Fa0/1` |

Si `Fa0/1` ya esta ocupado, usar el primer puerto libre entre `Fa0/2-Fa0/23`.
Configurar cada PC mediante DHCP.

## Fase 3: segmentos externos

Ubicar los equipos de acceso en el closet que atiende su espacio:

| Segmento | Closet | Equipo |
| --- | --- | --- |
| Jueces | `EIC-MDF-P1` | `SW-EIC-P1-JUECES` |
| Entrenadores | `CIT-MDF-P1` | `SW-CIT-P1-ENTRENADORES` y `AP-CIT-P1-7101` |
| Prensa | `ENH-MDF-P1` | `SW-ENH-P1-PRENSA` y `AP-ENH-P1-CONSEJO` |
| Invitados | `ENH-MDF-P1` | `AP-ENH-P1-INVITADOS-01` y AP representativos |

Conservar o construir los siguientes enlaces desde
`SWDistribucionExternos`:

| Puerto SWDistribucionExternos | Destino | Puerto destino | VLAN | Cable |
| --- | --- | --- | ---: | --- |
| `Fa0/1` | `SW-ENH-P1-PRENSA` | `Fa0/24` | 30 | Copper Cross-Over |
| `Fa0/2` | `AP-ENH-P1-CONSEJO` | `Port 0` | 30 | Copper Straight-Through |
| `Fa0/10` | `SW-CIT-P1-ENTRENADORES` | `Fa0/24` | 20 | Copper Cross-Over |
| `Fa0/11` | `AP-CIT-P1-7101` | `Port 0` | 20 | Copper Straight-Through |
| `Fa0/15` | `SW-EIC-P1-JUECES` | `Fa0/24` | 10 | Copper Cross-Over |
| `Fa0/20` | `AP-ENH-P1-INVITADOS-01` | `Port 0` | 40 | Copper Straight-Through |
| `Fa0/24` | `DHCP-DNS-OMI` | `Fa0` | 70 | Copper Straight-Through |

Los puertos `Fa0/21-Fa0/22` pueden usarse para AP representativos adicionales
de invitados/espera, siempre en VLAN 40.

### Terminales representativas externas

| Terminal | Equipo de acceso | Puerto / medio |
| --- | --- | --- |
| `PC-EIC-JUEZ` | `SW-EIC-P1-JUECES` | `Fa0/1`, Copper Straight-Through |
| `PC-CIT-ENTRENADOR` | `SW-CIT-P1-ENTRENADORES` | `Fa0/1`, Copper Straight-Through |
| `PC-ENH-PRENSA` | `SW-ENH-P1-PRENSA` | `Fa0/1`, Copper Straight-Through |
| `Laptop-ENH-INVITADO` | `AP-ENH-P1-INVITADOS-01` | Inalambrico |

Configurar todos mediante DHCP.

## Fase 4: Internet y servidores simulados

Mantener los equipos de Internet y servicios simulados separados de la red OMI.
No modificar sus puertos si las pruebas a `200.1.1.1` y DNS funcionan.

Como minimo comprobar:

| Origen | Destino esperado |
| --- | --- |
| `FronteraCampus` | Router `Internet` |
| Router `Internet` | Switch de servidores simulados |
| Switch de servidores simulados | Servidores `Concurso`, `NBA`, `CISCO` y `DNS` |

## Fase 5: patch panels, TO y etiquetas

Agregar como representacion:

| Closet | Copper Patch Panel | Fiber Patch Panel |
| --- | --- | --- |
| `CIT-MDF-P1` | `CIT-P1-CPP-01` y `CIT-P1-CPP-02` | `CIT-P1-FPP-01` |
| `CIT-IDF-P3` | `CIT-P3-CPP-01` | `CIT-P3-FPP-01` |
| `ENH-MDF-P1` | `ENH-P1-CPP-01` | `ENH-P1-FPP-01` |
| `ENH-IDF-P2` | `ENH-P2-CPP-01` | `ENH-P2-FPP-01` |
| `EIC-MDF-P1` | `EIC-P1-CPP-01` | `EIC-P1-FPP-01` |

Backbone etiquetado:

- `TRK-CIT-P1-P3`
- `TRK-CIT-ENH`
- `TRK-ENH-P1-P2`
- `TRK-CIT-EIC`

No insertar paneles en enlaces funcionales si Packet Tracer elimina
conectividad. Las conexiones directas de cada switch de area a sus PCs no
requieren TO segun las notas de la actividad.

## Validacion obligatoria

Antes de validar, esperar aproximadamente 30 segundos para que converjan STP,
CDP y EIGRP.

### DIST-ALUMNOS

```text
show cdp neighbors
show interfaces status
```

Los puertos `Fa0/1-Fa0/11` y `Gi0/1` deben aparecer conectados.

### SWDistribucionExternos

```text
show vlan brief
show interfaces trunk
show interfaces status
```

### Terminal por closet

```text
ipconfig /all
ping <gateway-del-segmento>
ping 172.23.28.226
ping 200.1.1.1
```

Probar al menos:

- `PC-CIT-CONG-01`
- `PC-ENH-1223`
- `PC-EIC-12102`
- `PC-EIC-JUEZ`
- `PC-CIT-ENTRENADOR`
- `PC-ENH-PRENSA`
- `Laptop-ENH-INVITADO`
