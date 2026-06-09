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
| CIT | `Wiring Closet CIT-P1` | `Rack CIT-P1.1` | Primer piso y Salon 7101 |
| CIT | `Wiring Closet CIT-P3` | `Rack CIT-P3.1` | Sala de Congresos |
| Edificio de Negocios | `Wiring Closet ENEG-P1` | `Rack ENEG-P1.1` | Sala Borrego, Sala Consejo y Domo |
| Edificio de Negocios | `Wiring Closet ENEG-P2` | `Rack ENEG-P2.1` | Aulas 1223, 1224 y Laboratorio de Finanzas |
| Edificio de Ingenieria | `Wiring Closet EING-P1` | `Rack EING-P1.1` | Laboratorio de IA y Aula 12102 |

El nucleo, routers de frontera, DHCP y distribucion principal se conservaran
temporalmente en `Wiring Closet CIT-P1` hasta validar la ubicacion final.

## Nomenclatura TIA/EIA-606-B propuesta

| Elemento | Patron | Ejemplo |
| --- | --- | --- |
| Patch panel | `<EDIFICIO>-P<PISO>-PP-<NN>` | `CIT-P3-PP-01` |
| Telecommunications Outlet | `<EDIFICIO>-<ESPACIO>-TO-<NN>` | `ENEG-DOMO-TO-01` |
| Switch | `SW-<EDIFICIO>-P<PISO>-ACC-<NN>` | `SW-EING-P1-ACC-01` |
| Enlace troncal | `TRK-<ORIGEN>-<DESTINO>` | `TRK-CIT-EING` |

## Reglas de acomodo

- Colocar switches, patch panels y enlaces ordenadamente dentro de cada rack.
- Usar TO y patch panel solo para nodos considerados cableado estructurado.
- No modelar con TO cada computadora conectada directamente al switch del area.
- Etiquetar fibras existentes usadas entre edificios.
- Mantener nombres consistentes entre Physical y Logical.
- Mover y renombrar un grupo de dispositivos a la vez, guardando y validando
  conectividad despues de cada movimiento.

## Distribucion pendiente

Los switches heredados (`SWAlumnos DOMO`, `SWAlumnos Menlo`, `SWAlumnos EIC` y
`SWAlumnos Prepa`) deben reasignarse y renombrarse de acuerdo con los espacios
anteriores. La asignacion exacta se confirmara antes de moverlos para no romper
la topologia funcional.
