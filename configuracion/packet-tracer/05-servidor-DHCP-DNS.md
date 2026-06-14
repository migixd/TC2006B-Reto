# Servidor DHCP-DNS-OMI

## Interfaz

En **Desktop > IP Configuration**:

- IP: `172.23.28.226`
- Mascara: `255.255.255.248`
- Gateway: `172.23.28.225`
- DNS: `172.23.28.226`

## Pools DHCP

En **Services > DHCP**, activar el servicio y crear:

| Pool | Gateway | DNS | Inicio | Mascara | Maximo |
| --- | --- | --- | --- | --- | ---: |
| CONCURSANTES | `172.23.24.1` | `172.23.28.226` | `172.23.24.10` | `255.255.254.0` | 330 |
| INVITADOS | `172.23.26.1` | `172.23.28.226` | `172.23.26.10` | `255.255.254.0` | 300 |
| JUECES | `172.23.28.1` | `172.23.28.226` | `172.23.28.10` | `255.255.255.224` | 20 |
| ENTRENADORES | `172.23.28.65` | `172.23.28.226` | `172.23.28.70` | `255.255.255.192` | 40 |
| PRENSA | `172.23.28.129` | `172.23.28.226` | `172.23.28.135` | `255.255.255.192` | 32 |
| INFRAESTRUCTURA | `172.23.28.193` | `172.23.28.226` | `172.23.28.200` | `255.255.255.224` | 20 |

No crear pool para Servidores; sus direcciones deben ser estaticas.

## DNS

En **Services > DNS**, activar el servicio y agregar:

| Nombre | Direccion |
| --- | --- |
| `servicios.omi.local` | `172.23.28.226` |
| `concurso.omi.local` | `200.1.1.50` |

## Servicio web interno

En `DHCP-DNS-OMI`, entrar a **Services > HTTP**:

1. Activar `HTTP: On`.
2. Editar `index.html` con la pagina de servicios internos de la OMI.
3. Guardar los cambios.

La pagina debe abrir desde los clientes mediante:

```text
http://servicios.omi.local
```

## Servidor web Concurso

El servidor externo `Concurso` utiliza:

- IP: `200.1.1.50`
- Servicio: HTTP
- Nombre DNS: `concurso.omi.local`

En el Server-PT `Concurso`, entrar a **Services > HTTP**:

1. Activar `HTTP: On`.
2. Editar y guardar `index.html` con la pagina oficial del concurso.

La pagina debe abrir mediante:

```text
http://200.1.1.50
http://concurso.omi.local
```

No se modificaron los pools DHCP al agregar estos servicios.
