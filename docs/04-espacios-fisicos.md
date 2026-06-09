# Espacios fisicos

## Physical Locations

| Edificio | Wiring Closet | Rack |
| --- | --- | --- |
| CIT | Wiring Closet CIT | Rack CIT.1 |
| Edificio de Negocios | Wiring Closet ENEG | Rack ENEG.1 |
| Edificio de Ingenieria | Wiring Closet EING | Rack EING.1 |

## Nomenclatura TIA/EIA-606-B propuesta

| Elemento | Patron | Ejemplo |
| --- | --- | --- |
| Patch panel | `<EDIFICIO>-PP-<NN>` | `CIT-PP-01` |
| Telecommunications Outlet | `<EDIFICIO>-TO-<NN>` | `ENEG-TO-01` |
| Switch | `SW-<EDIFICIO>-<ROL>-<NN>` | `SW-EING-ACC-01` |
| Enlace troncal | `TRK-<ORIGEN>-<DESTINO>` | `TRK-CIT-EING` |

## Reglas de acomodo

- Colocar switches, patch panels y enlaces ordenadamente dentro de cada rack.
- Usar TO y patch panel solo para nodos considerados cableado estructurado.
- No modelar con TO cada computadora conectada directamente al switch del area.
- Etiquetar fibras existentes usadas entre edificios.
- Mantener nombres consistentes entre Physical y Logical.

