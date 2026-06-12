# Estado de construccion fisica

Fecha de corte: 12 de junio de 2026.

## Completado

- Topologia logica migrada al direccionamiento oficial.
- DHCP, DNS, EIGRP, NAT, Internet, troncales y aislamiento validados.
- Jerarquia fisica creada para CIT, ENH y EIC.
- Wiring Closets MDF/IDF y racks creados.
- Hostnames de switches de acceso definidos.
- Inventario de enlaces de `DIST-ALUMNOS` documentado.
- Matriz completa de conexiones, puertos y cables documentada en
  `12-matriz-cableado-fisico-completo.md`.

## En progreso

- Redistribucion de switches a closets y racks.
- Conexion de equipos terminales representativos.
- Acomodo visual y etiquetado dentro de racks.

## Pendiente

- Completar todas las conexiones fisicas requeridas.
- Agregar patch panels y TO donde aplique.
- Validar al menos una terminal por Wiring Closet.
- Confirmar CDP y estado de puertos despues de la redistribucion.
- Capturar vistas Physical y Logical finales.
- Integrar evidencias y generar el PDF/ZIP de entrega.

## Regla de seguridad

La copia actual de `entregables/ActReto03.pkt` es un avance de trabajo. No debe
marcarse como diseno fisico terminado hasta completar y validar los puntos
pendientes.
