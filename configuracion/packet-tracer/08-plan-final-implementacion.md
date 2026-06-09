# Plan final de implementacion

## Estado y objetivo

La topologia redistribuida funciona con direcciones heredadas `172.16.x.x`.
El objetivo pendiente es migrarla al bloque oficial `172.23.24.0/21` sin
alterar la distribucion fisica validada.

## Antes de migrar

1. Guardar `ActReto03-antes-migracion-IP.pkt`.
2. Confirmar que funcionan PC concursante, laptop invitada y salida a Internet.
3. No guardar sobre el respaldo.

## Orden obligatorio de migracion

### Fase 1: capa 2

1. Aplicar `01-SWDistribucionExternos.txt`.
2. Aplicar `02-switches-acceso.txt` en Jueces, Entrenadores y Prensa.
3. Conservar `DIST-ALUMNOS` y sus switches de examen en VLAN 1.
4. Confirmar troncal VLAN `10,20,30,40,60,70`.

### Fase 2: servidor unificado

1. Conectar `DHCP-DNS-OMI FastEthernet0` a
   `SWDistribucionExternos FastEthernet0/24` con Copper Straight-Through.
2. Configurar interfaz y pools siguiendo `05-servidor-DHCP-DNS.md`.
3. Activar servicios DHCP y DNS.

### Fase 3: routers

1. Aplicar `04-router-Frontera.txt`.
2. Aplicar `03-router-Alumnos.txt`.
3. Esperar a que EIGRP forme vecindad nuevamente.
4. Confirmar rutas y gateways con `show ip route`.

### Fase 4: clientes

1. En cada terminal representativa seleccionar DHCP nuevamente.
2. Confirmar que ya no recibe direcciones `172.16.x.x`.
3. Ejecutar las pruebas de `06-validacion.txt`.

## Criterios de terminacion

- No quedan direcciones internas `172.16.x.x`.
- Concursantes recibe `172.23.24.x/23`.
- Jueces recibe `172.23.26.0/27`.
- Entrenadores recibe `172.23.26.32/27`.
- Prensa recibe `172.23.26.64/27`.
- Invitados recibe `172.23.26.96/27`.
- DHCP y DNS responden en `172.23.26.162`.
- EIGRP, NAT, Internet y aislamiento funcionan.

