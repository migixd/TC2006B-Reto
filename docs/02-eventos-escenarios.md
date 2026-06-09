# Eventos y escenarios

## Escenarios principales

| ID | Escenario | Condicion | Resultado esperado |
| --- | --- | --- | --- |
| E01 | Concurso de preparatoria | 132 concursantes conectados | Direccion DHCP, DNS y acceso autorizado estables. |
| E02 | Concurso simultaneo maximo | 330 concursantes conectados | La red `/23` conserva capacidad suficiente. |
| E03 | Operacion de jueces | Juez conectado a VLAN Jueces | Accede a servicios autorizados y a Internet. |
| E04 | Cobertura de prensa | Reportero conectado a VLAN Prensa | Tiene Internet sin acceso a concursantes. |
| E05 | Invitado | Invitado conectado a VLAN Invitados | Tiene Internet y permanece aislado. |
| E06 | Administracion | Personal autorizado en Infraestructura | Puede administrar equipos segun politica. |
| E07 | Falla DHCP | DHCP-DNS-OMI no responde | Se detecta, registra y escala la falla. |
| E08 | Intento lateral | Invitado intenta llegar a Concursantes | El trafico es bloqueado. |

## Colores sugeridos

| Segmento | Color |
| --- | --- |
| Concursantes | Amarillo |
| Jueces | Verde |
| Entrenadores | Naranja |
| Prensa | Azul |
| Invitados | Morado |
| Infraestructura | Gris |
| Servidores | Rojo |

