# Actividad Reto 03: El diseno fisico de la red

## XXV Olimpiada Mexicana de Informatica

Tec de Monterrey Campus Chihuahua

**Integrantes**

- Mirka Giselle Gutierrez Uriarte - A01564135
- Paola Regina Lechuga Esparza - A01569279
- Ilse Paola Cruz Fernandez - A01562692

Curso: Interconexion de dispositivos, Grupo 301  
Profesor: Mtro. Faustino Bejarano Romero  
Fecha: 9 de junio de 2026

## Objetivo

Representar en Packet Tracer el diseno fisico y logico de la red para la XXV
OMI, incluyendo segmentacion, dispositivos, cableado estructurado, etiquetas y
elementos visuales que faciliten su interpretacion.

## Diseno fisico

El diseno considera los edificios CIT, Edificio de Negocios y Edificio de
Ingenieria. Cada edificio cuenta con Wiring Closet y rack identificado. Los
patch panels, TO y enlaces estructurados siguen una nomenclatura consistente
basada en TIA/EIA-606-B.

**Insertar aqui la captura final del modo Physical de Packet Tracer.**

## Diseno logico

La solucion separa concursantes, jueces, entrenadores, prensa, invitados,
infraestructura y servidores. El bloque oficial es `172.23.24.0/21`; la red de
concursantes usa `/23` para soportar el maximo simultaneo de 330 participantes.

**Insertar aqui la captura final del modo Logical de Packet Tracer.**

## Anexo A: sustitucion de equipo

La propuesta economica contempla switches Cisco Catalyst 9300 de 48 puertos.
Packet Tracer no ofrece ese modelo, por lo que se utiliza Cisco Catalyst
2960-24TT para representar la funcion de acceso, VLAN y enlaces troncales.
Esta sustitucion aplica solamente al simulador y no modifica la propuesta
economica.

## Validacion antes de entrega

El archivo final fue migrado al bloque oficial `172.23.24.0/21`. Se validaron
interfaces, pools DHCP, DNS, rutas, NAT, troncales y aislamiento entre los
segmentos representativos. Falta insertar las capturas y evidencia final.

## Evidencia de trabajo colaborativo

**Insertar aqui capturas, registros de reunion o enlaces de evidencia.**
