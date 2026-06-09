# Inventario de enlaces actuales

## Distribucion Alumnos

La etiqueta visual del equipo es `Distribucion Alumnos`, pero su hostname IOS
actual es `Switch`.

| Puerto local | Destino | Puerto remoto | Estado |
| --- | --- | --- | --- |
| `Gi0/1` | Router `Alumnos` | `Gi0/0` | Confirmado |
| `Fa0/1` | `SW-EIC-01` | `Fa0/24` | Confirmado |
| `Fa0/2` | `SW-DOMO-01` | `Fa0/24` | Confirmado |
| `Fa0/3` | `SW-DOMO-02` | `Fa0/24` | Confirmado |
| `Fa0/4` | `SW-PREPA-01` | `Fa0/24` | Confirmado |
| `Fa0/5` | `SW-MENLO-01` | `Fa0/24` | Confirmado |
| `Fa0/6` | `SW-MENLO-02` | `Fa0/24` | Confirmado |
| `Fa0/7` | `SW-MENLO-03` | `Fa0/24` | Confirmado |
| `Fa0/8` | `SW-MENLO-04` | `Fa0/24` | Confirmado |
| `Fa0/9` | `SW-MENLO-05` | `Fa0/24` | Confirmado |
| `Fa0/10` | `SW-PREPA-02` | `Fa0/24` | Confirmado |
| `Fa0/11` | `SW-MENLO-06` | `Fa0/24` | Confirmado |

Los puertos `Fa0/12-Fa0/24` y `Gi0/2` estan disponibles.

## Asignacion final por espacio

La topologia dispone exactamente de once switches de acceso para once espacios.
Se propone la siguiente reasignacion, conservando inicialmente los puertos
actuales:

| Puerto DIST-ALUMNOS | Switch actual | Ubicacion final | Hostname final |
| --- | --- | --- | --- |
| `Fa0/1` | `SW-EIC-01` | EIC-P1, Laboratorio de IA | `SW-EIC-P1-IA` |
| `Fa0/2` | `SW-DOMO-01` | ENH-P1, Domo de Negocios | `SW-ENH-P1-DOMO` |
| `Fa0/3` | `SW-DOMO-02` | ENH-P1, Sala Borrego | `SW-ENH-P1-BORREGO` |
| `Fa0/4` | `SW-PREPA-01` | CIT-P1, Salon 7101 | `SW-CIT-P1-7101` |
| `Fa0/5` | `SW-MENLO-01` | CIT-P3, Sala de Congresos 1 | `SW-CIT-P3-CONG-01` |
| `Fa0/6` | `SW-MENLO-02` | CIT-P3, Sala de Congresos 2 | `SW-CIT-P3-CONG-02` |
| `Fa0/7` | `SW-MENLO-03` | ENH-P1, Sala Consejo | `SW-ENH-P1-CONSEJO` |
| `Fa0/8` | `SW-MENLO-04` | ENH-P2, Aula 1223 | `SW-ENH-P2-1223` |
| `Fa0/9` | `SW-MENLO-05` | ENH-P2, Aula 1224 | `SW-ENH-P2-1224` |
| `Fa0/10` | `SW-PREPA-02` | EIC-P1, Aula 12102 | `SW-EIC-P1-12102` |
| `Fa0/11` | `SW-MENLO-06` | ENH-P2, Laboratorio de Finanzas | `SW-ENH-P2-FIN` |

Se asignan dos switches a Sala de Congresos porque es el espacio de mayor
capacidad. Los demas espacios reciben un switch de acceso.

## Hallazgo

Todos los switches de acceso anuncian el mismo Device ID CDP: `Switch`.
Antes de redistribuirlos deben recibir hostnames unicos. Cambiar el hostname no
afecta conexiones, VLAN ni direccionamiento.

## Hostnames temporales para identificar enlaces

| Etiqueta visual actual | Hostname temporal |
| --- | --- |
| Distribucion Alumnos | `DIST-ALUMNOS` |
| SWAlumnos DOMO1 | `SW-DOMO-01` |
| SWAlumnos DOMO2 | `SW-DOMO-02` |
| SWAlumnos EIC | `SW-EIC-01` |
| SWAlumnos Prepa 1 | `SW-PREPA-01` |
| SWAlumnos Prepa 2 | `SW-PREPA-02` |
| SWAlumnos Menlo 1 | `SW-MENLO-01` |
| SWAlumnos Menlo 2 | `SW-MENLO-02` |
| SWAlumnos Menlo 3 | `SW-MENLO-03` |
| SWAlumnos Menlo 4 | `SW-MENLO-04` |
| SWAlumnos Menlo 5 | `SW-MENLO-05` |
| SWAlumnos Menlo 6 | `SW-MENLO-06` |

Despues de cambiar los hostnames, esperar aproximadamente 60 segundos y
ejecutar en `DIST-ALUMNOS`:

```text
show cdp neighbors
```

La salida permitira completar la correspondencia exacta entre `Fa0/1-Fa0/11`
y cada switch.
