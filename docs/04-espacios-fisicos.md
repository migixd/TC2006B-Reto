# Espacios fisicos

## Jerarquia Physical Locations

Packet Tracer permite los niveles `Intercity > City > Building > Wiring
Closet`. Para representar el campus se usara:

```text
Chihuahua
└── Chihuahua Capital - ITESM Campus Chihuahua
    ├── CIT
    ├── Edificio de Negocios
    └── Edificio de Ingenieria
```

No existe un nivel adicional de campus entre `City` y `Building`; por eso el
nombre del campus se integra en el contenedor de ciudad.

## Edificios, pisos y espacios

| Edificio | Piso | Espacios atendidos |
| --- | ---: | --- |
| CIT | 1 | Areas del primer piso y Salon 7101 |
| CIT | 3 | Sala de Congresos |
| Edificio de Negocios | 1 | Sala Borrego, Sala Consejo y Domo de Negocios |
| Edificio de Negocios | 2 | Aula 1223, Aula 1224 y Laboratorio de Finanzas |
| Edificio de Ingenieria | 1 | Laboratorio de IA y Aula 12102 |

## Closets y racks propuestos

Los Wiring Closets representan cuartos de telecomunicaciones por piso o zona,
no cada salon individual.

| Edificio | Wiring Closet | Rack | Espacios atendidos |
| --- | --- | --- | --- |
| CIT | `Wiring Closet CIT-MDF-P1` | `Rack CIT-MDF-P1.1` | Nucleo, primer piso y Salon 7101 |
| CIT | `Wiring Closet CIT-IDF-P3` | `Rack CIT-IDF-P3.1` | Sala de Congresos |
| Edificio de Negocios | `Wiring Closet ENH-MDF-P1` | `Rack ENH-MDF-P1.1` | Sala Borrego, Sala Consejo y Domo |
| Edificio de Negocios | `Wiring Closet ENH-IDF-P2` | `Rack ENH-IDF-P2.1` | Aulas 1223, 1224 y Laboratorio de Finanzas |
| Edificio de Ingenieria | `Wiring Closet EIC-MDF-P1` | `Rack EIC-MDF-P1.1` | Laboratorio de IA y Aula 12102 |

El nucleo, routers de frontera, DHCP y distribucion principal se conservaran
temporalmente en `Wiring Closet CIT-P1` hasta validar la ubicacion final.

## Nomenclatura TIA/EIA-606-B propuesta

| Elemento | Patron | Ejemplo |
| --- | --- | --- |
| Patch panel | `<EDIFICIO>-P<PISO>-PP-<NN>` | `CIT-P3-PP-01` |
| Telecommunications Outlet | `<EDIFICIO>-<ESPACIO>-TO-<NN>` | `ENH-DOMO-TO-01` |
| Switch | `SW-<EDIFICIO>-P<PISO>-ACC-<NN>` | `SW-EIC-P1-ACC-01` |
| Enlace troncal | `TRK-<ORIGEN>-<DESTINO>` | `TRK-CIT-EIC` |

## Reglas de acomodo

- Colocar switches, patch panels y enlaces ordenadamente dentro de cada rack.
- Usar TO y patch panel solo para nodos considerados cableado estructurado.
- No modelar con TO cada computadora conectada directamente al switch del area.
- Etiquetar fibras existentes usadas entre edificios.
- Mantener nombres consistentes entre Physical y Logical.
- Mover y renombrar un grupo de dispositivos a la vez, guardando y validando
  conectividad despues de cada movimiento.

## Distribucion de switches de examen

| Closet | Switches |
| --- | --- |
| `CIT-IDF-P3` | `SW-CIT-P3-CONG-01` a `SW-CIT-P3-CONG-05` |
| `ENH-IDF-P2` | `SW-ENH-P2-1223`, `SW-ENH-P2-1224`, `SW-ENH-P2-FIN` |
| `EIC-MDF-P1` | `SW-EIC-P1-12102` |
| `CIT-MDF-P1` | `DIST-ALUMNOS` y dos switches de reserva |

Las areas Sala Borrego, Sala Consejo, Laboratorio de IA y Salon 7101 pertenecen
a las redes Invitados, Prensa, Jueces y Entrenadores respectivamente; no deben
conectarse a `DIST-ALUMNOS`.
