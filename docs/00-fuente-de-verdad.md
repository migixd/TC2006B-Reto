# Fuente de verdad

## Proyecto

- Evento: XXV Olimpiada Mexicana de Informatica.
- Sede: Tec de Monterrey Campus Chihuahua.
- Competidores totales: 594.
- Maximo simultaneo: 330 participantes.
- Bloque asignado: `172.23.24.0/21`.
- DNS interno y servidor DHCP: `172.23.26.162`.

## Participantes

| Categoria | Cantidad |
| --- | ---: |
| Preparatoria | 132 |
| Secundaria | 198 |
| Primaria | 264 |
| Total | 594 |

## Requerimientos

- Separar concursantes, jueces, entrenadores, prensa, invitados,
  infraestructura y servidores.
- Proporcionar DHCP y DNS centralizados.
- Permitir salida a Internet segun las politicas de cada segmento.
- Representar solo equipos terminales suficientes para interpretar la topologia.
- Usar elementos visuales, etiquetas e interfaces en el diseno logico.
- Nombrar closets, racks, patch panels y TO con criterio TIA/EIA-606-B.

## Sustituciones Packet Tracer

| Propuesta | Sustituto en Packet Tracer | Justificacion |
| --- | --- | --- |
| Cisco Catalyst 9300, 48 puertos | Cisco Catalyst 2960-24TT | Es el modelo disponible mas cercano para representar acceso con VLAN y enlaces troncales. |

La sustitucion es solo para simulacion y no modifica la propuesta economica.

## Pendientes bloqueantes

- Migrar del esquema heredado `172.16.x.x` al bloque oficial `172.23.24.0/21`.
- Confirmar que todas las interfaces del `.pkt` tengan nombre, IP y estado.
- Capturar imagenes finales del modo Physical y del modo Logical.
- Incorporar evidencia documental del trabajo colaborativo.

