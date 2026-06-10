# Fuente de verdad

## Proyecto

- Evento: XXV Olimpiada Mexicana de Informatica.
- Sede: Tec de Monterrey Campus Chihuahua.
- Competidores totales: 594.
- Maximo simultaneo: 330 participantes.
- Jueces: 10.
- Entrenadores: 40.
- Reporteros: 32.
- Invitados estimados: aproximadamente 300.
- Bloque asignado: `172.23.24.0/21`.
- DNS interno y servidor DHCP propuesto: `172.23.28.226`.
- Edificios fisicos: CIT, Edificio de Negocios y Edificio de Ingenieria.

El Reto 01 declara un total de 686 asistentes antes de invitados, pero el
desglose `594 + 10 + 40 + 32` suma 676. Para dimensionar la red se usan las
cantidades detalladas y el estimado adicional de invitados.

## Participantes

| Categoria | Cantidad |
| --- | ---: |
| Preparatoria | 132 |
| Secundaria | 198 |
| Primaria | 264 |
| Total | 594 |

## Solucion operativa elegida

- Dia 1 por la manana: primaria, 264 participantes.
- Dia 1 por la tarde: secundaria y preparatoria, 330 participantes.
- Dia 2: preparatoria, 132 participantes.
- Espacios con equipo institucional: aulas 1223, 1224, 12102 y Laboratorio de
  Finanzas, con 130 equipos considerados en Reto 02.
- Sala de Congresos: hasta 198 equipos rentados simultaneos y cinco switches de
  48 puertos.
- Sala Borrego: invitados.
- Sala Consejo: prensa.
- Laboratorio de Inteligencia Artificial: jueces.
- Salon 7101: entrenadores.
- Primer piso CIT y Domo de Negocios: areas de espera con infraestructura WiFi
  existente.

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

Reto 02 no contempla routers nuevos en produccion porque los servicios se
integran a la infraestructura institucional existente. Los routers de Packet
Tracer se conservan unicamente para simular enrutamiento, DHCP relay, NAT y
salida a Internet.

## Estado y pendientes

- La topologia fue migrada al bloque oficial `172.23.24.0/21`.
- Se validaron DHCP, DNS, EIGRP, NAT, Internet, troncales y aislamiento.
- Los equipos fueron redistribuidos entre edificios, pisos y Wiring Closets.
- Falta revisar que todas las etiquetas visibles coincidan con el diseno final.
- Capturar imagenes finales del modo Physical y del modo Logical.
- Incorporar evidencia documental del trabajo colaborativo.
