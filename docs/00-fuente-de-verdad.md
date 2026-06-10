# Fuente de verdad

## Proyecto

- Evento: XXV Olimpiada Mexicana de Informática.
- Sede: Tec de Monterrey Campus Chihuahua.
- Competidores totales: 594.
- Máximo simultáneo: 330 participantes.
- Jueces: 10.
- Entrenadores: 40.
- Reporteros: 32.
- Invitados estimados: aproximadamente 300.
- Bloque asignado: `172.23.24.0/21`.
- DNS interno y servidor DHCP propuesto: `172.23.28.226`.
- Edificios físicos: CIT, Edificio de Negocios y Edificio de Ingeniería.

El Reto 01 declara un total de 686 asistentes antes de invitados, pero el
desglose `594 + 10 + 40 + 32` suma 676. Para dimensionar la red se usan las
cantidades detalladas y el estimado adicional de invitados.

## Participantes

| Categoría | Cantidad |
| --- | ---: |
| Preparatoria | 132 |
| Secundaria | 198 |
| Primaria | 264 |
| Total | 594 |

## Solución operativa elegida

- Día 1 por la mañana: primaria, 264 participantes.
- Día 1 por la tarde: secundaria y preparatoria, 330 participantes.
- Día 2: preparatoria, 132 participantes.
- Espacios con equipo institucional: aulas 1223, 1224, 12102 y Laboratorio de
  Finanzas, con 130 equipos considerados en Reto 02.
- Sala de Congresos: hasta 198 equipos rentados simultáneos y cinco switches de
  48 puertos.
- Sala Borrego: invitados.
- Sala Consejo: prensa.
- Laboratorio de Inteligencia Artificial: jueces.
- Salon 7101: entrenadores.
- Primer piso CIT y Domo de Negocios: áreas de espera con infraestructura WiFi
  existente.

## Requerimientos

- Separar concursantes, jueces, entrenadores, prensa, invitados,
  infraestructura y servidores.
- Proporcionar DHCP y DNS centralizados.
- Permitir salida a Internet segun las políticas de cada segmento.
- Representar solo equipos terminales suficientes para interpretar la topología.
- Usar elementos visuales, etiquetas e interfaces en el diseño lógico.
- Nombrar closets, racks, patch panels y TO con criterio TIA/EIA-606-B.

## Sustituciones Packet Tracer

| Propuesta | Sustituto en Packet Tracer | Justificación |
| --- | --- | --- |
| Cisco Catalyst 9300, 48 puertos | Cisco Catalyst 2960-24TT | Es el modelo disponible más cercano para representar acceso con VLAN y enlaces troncales. |

La sustitución es solo para simulación y no modifica la propuesta económica.

Reto 02 no contempla routers nuevos en producción porque los servicios se
integran a la infraestructura institucional existente. Los routers de Packet
Tracer se conservan únicamente para simular enrutamiento, DHCP relay, NAT y
salida a Internet.

## Estado y pendientes

- La topología fue migrada al bloque oficial `172.23.24.0/21`.
- Se validaron DHCP, DNS, EIGRP, NAT, Internet, troncales y aislamiento.
- Los equipos fueron redistribuidos entre edificios, pisos y Wiring Closets.
- Falta revisar que todas las etiquetas visibles coincidan con el diseño final.
- Capturar imágenes finales del modo Physical y del modo Logical.
- Incorporar evidencia documental del trabajo colaborativo.
