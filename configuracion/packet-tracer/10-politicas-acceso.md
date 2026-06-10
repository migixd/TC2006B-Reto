# Politicas de acceso implementadas

La ACL `BLOQUEAR-CONCURSANTES` esta aplicada de salida en
`Frontera GigabitEthernet0/0`. Bloquea el acceso de Invitados, Entrenadores y
Prensa a Concursantes, conservando DNS, Internet y el acceso autorizado de
Jueces.

## Matriz objetivo

| Origen | DHCP/DNS | Internet | Concursantes | Redes administrativas |
| --- | --- | --- | --- | --- |
| Concursantes | Permitido | Permitido | Mismo segmento | Denegado |
| Jueces | Permitido | Permitido | Permitido segun operacion | Permitido |
| Entrenadores | Permitido | Permitido | Denegado | Denegado |
| Prensa | Permitido | Permitido | Denegado | Denegado |
| Invitados | Permitido | Permitido | Denegado | Denegado |

## Configuracion aplicada

```cisco
ip access-list extended BLOQUEAR-CONCURSANTES
 deny ip 172.23.26.0 0.0.1.255 172.23.24.0 0.0.1.255
 deny ip 172.23.28.64 0.0.0.63 172.23.24.0 0.0.1.255
 deny ip 172.23.28.128 0.0.0.63 172.23.24.0 0.0.1.255
 permit ip any any

interface GigabitEthernet0/0
 ip access-group BLOQUEAR-CONCURSANTES out
```

## Pruebas validadas

- Invitados, Prensa y Entrenadores no alcanzan Concursantes.
- Jueces conserva acceso a Concursantes.
- Todos los segmentos representativos resuelven DNS y alcanzan Internet.
