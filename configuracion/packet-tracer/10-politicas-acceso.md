# Politicas de acceso pendientes

La topologia heredada permite comunicacion entre todos los segmentos. Las ACL
de aislamiento deben aplicarse solo despues de terminar la migracion IP y
validar DHCP, DNS, EIGRP, NAT e Internet.

## Matriz objetivo

| Origen | DHCP/DNS | Internet | Concursantes | Redes administrativas |
| --- | --- | --- | --- | --- |
| Concursantes | Permitido | Permitido | Mismo segmento | Denegado |
| Jueces | Permitido | Permitido | Permitido segun operacion | Permitido |
| Entrenadores | Permitido | Permitido | Denegado | Denegado |
| Prensa | Permitido | Permitido | Denegado | Denegado |
| Invitados | Permitido | Permitido | Denegado | Denegado |

## Regla de implementacion

No usar una ACL generica que niegue todo el bloque `172.23.24.0/21` antes de
permitir explicitamente DNS, DHCP y cualquier servidor del concurso. La lista
exacta de servicios internos debe confirmarse antes de generar los comandos
finales.

## Pruebas requeridas

- Invitados no alcanzan `172.23.24.0/23`.
- Prensa no alcanza `172.23.24.0/23`.
- Entrenadores no alcanzan `172.23.24.0/23`.
- Jueces conserva los accesos autorizados.
- Todos los segmentos resuelven DNS y alcanzan Internet.

