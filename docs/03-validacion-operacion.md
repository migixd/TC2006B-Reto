# Validacion y operacion

## Pruebas obligatorias

| ID | Prueba | Criterio de aceptacion |
| --- | --- | --- |
| V01 | Nombres fisicos | Edificios, closets, racks, patch panels y TO estan etiquetados. |
| V02 | Direccionamiento | No quedan direcciones `172.16.x.x` en el diseno final. |
| V03 | DHCP por VLAN | Cada cliente obtiene IP, mascara, gateway y DNS correctos. |
| V04 | DNS | Todos los segmentos autorizados consultan `172.23.28.226`. |
| V05 | Gateway | Cada cliente alcanza su gateway. |
| V06 | Internet | Los segmentos autorizados alcanzan Internet mediante NAT. |
| V07 | Aislamiento | Invitados y prensa no alcanzan concursantes. |
| V08 | Troncales | Las VLAN requeridas atraviesan los enlaces troncales. |
| V09 | Interfaces | Cada interfaz de interconexion tiene etiqueta e IP visible. |
| V10 | Capacidad | Concursantes usa `/23` y soporta 330 clientes simultaneos. |

## Lista previa a entrega

- [x] Abrir y guardar la ultima version de `ActReto03.pkt`.
- [x] Ejecutar `show ip interface brief`, `show vlan brief` y
      `show interfaces trunk` donde aplique.
- [x] Confirmar pools DHCP y exclusiones.
- [x] Probar pings permitidos y bloqueados.
- [ ] Capturar vista Physical ordenada.
- [ ] Completar la redistribucion fisica y las conexiones pendientes.
- [ ] Validar una terminal representativa por Wiring Closet.
- [ ] Capturar vista Logical con colores, etiquetas e interfaces.
- [ ] Agregar capturas y evidencia colaborativa al PDF.
- [ ] Comprimir `.pkt` y PDF como `ActReto03.zip`.

## Hallazgo actual

La migracion IP y la conectividad representativa fueron validadas. DHCP y DNS
responden desde `172.23.28.226`; EIGRP, NAT, Internet, troncales y la ACL
`BLOQUEAR-CONCURSANTES` funcionan. La construccion fisica sigue en progreso:
faltan conexiones en algunos espacios, validacion por closet, capturas y
evidencia del reporte final.
