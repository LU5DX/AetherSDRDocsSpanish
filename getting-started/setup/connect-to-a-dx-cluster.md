# Conectarse a un clúster DX

El diálogo SpotHub de AetherSDR se conecta a un clúster DX mediante telnet y superpone los spots entrantes sobre el panadapter. Use esta página para ingresar los datos de su servidor de clúster, iniciar sesión y comenzar a ver spots.

## Antes de comenzar

- Conozca el nombre de host y el puerto de su clúster DX preferido (por ejemplo, `dxc.nc7j.com` en el puerto `23`).
- Tenga a mano su indicativo — se envía al clúster como credencial de acceso.

## Pasos

1. Haga clic en `Settings > SpotHub...` para abrir el diálogo SpotHub.
2. Haga clic en la pestaña **Cluster**.
3. En el campo **Server:**, escriba el nombre de host de su clúster DX.
4. En el campo **Port:**, establezca el puerto telnet (rango válido: 1–65535).
5. En el campo **Callsign:**, escriba su indicativo.
6. Haga clic en **Connect**. La etiqueta del botón cambia a **Disconnect** cuando se establece la sesión. El tráfico sin procesar del clúster aparece en el área de solo lectura **Cluster Console**.
7. Opcional: para enviar un comando al clúster, escríbalo en el campo de línea de comandos junto a **Send** y haga clic en **Send**.
8. Opcional: para reconectarse automáticamente la próxima vez que AetherSDR inicie, active **Auto-connect on startup**.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración | Valor predeterminado | Rango |
|---|---|---|---|---|
| **Server:** | Nombre de host del servidor telnet del clúster DX. | `ClusterHost` | — | — |
| **Port:** | Puerto telnet en el servidor del clúster. | `ClusterPort` | — | 1–65535 |
| **Callsign:** | Indicativo de acceso enviado al clúster al conectarse. | `ClusterCallsign` | — | — |
| **Connect / Disconnect** | Alterna la conexión telnet. La etiqueta refleja el estado actual. | — | Connect | — |
| **Auto-connect on startup** | Reconecta al clúster automáticamente al iniciar. | `ClusterAutoConnect` | — | — |
| **Cluster Console** | Visualización de solo lectura del tráfico telnet sin procesar del clúster. | — | — | — |
| **Send** | Envía el comando escrito al clúster. Activo solo mientras está conectado. | — | — | — |
| **Spot Color:** | Abre un selector de color para definir el color de los spots del clúster en el panadapter. | `ClusterSpotColor` | — | — |

## Consejos

- Los spots aparecen en el panadapter solo cuando la superposición maestra de spots está activada. Si no ve spots después de conectarse, abra la pestaña **Display** y confirme que **Spots:** esté configurado en Enabled (el valor predeterminado).
- Haga doble clic en cualquier fila de la pestaña **Spot List** para sintonizar el VFO activo en la frecuencia de ese spot. Consulte [Sintonizar un spot haciendo doble clic en la lista de spots](../../features/dx-cluster/tune-to-a-spot-by-double-clicking-the-spot-list.md).

## Solución de problemas

- **El botón permanece en "Connect" y la consola muestra "Error: ..."** — El nombre de host o el puerto es incorrecto, o el servidor del clúster no es accesible. Verifique la dirección del servidor y el puerto, compruebe su conexión de red e inténtelo de nuevo.
- **No aparecen spots en el panadapter después de conectarse** — Confirme que el interruptor **Spots:** en la pestaña **Display** esté en Enabled. Compruebe también que la banda de los spots entrantes coincida con el rango de frecuencias actual del panadapter.
- **La Cluster Console está vacía después de conectarse** — Algunos clústeres requieren que envíe un comando (como su indicativo nuevamente o `SET/DX`) antes de transmitir spots. Escriba el comando en el campo de línea de comandos y haga clic en **Send**.

## Relacionados

- [Descripción general de SpotHub](../../features/dx-cluster/overview.md)
- [Conectarse a la Reverse Beacon Network](connect-to-the-reverse-beacon-network.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](../../features/dx-cluster/tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Elegir colores para cada fuente de spots](../../features/dx-cluster/pick-colors-for-each-spot-source.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md)
- [Activar el coloreado DXCC desde un registro ADIF](../../features/dx-cluster/enable-dxcc-coloring-from-an-adif-log.md)
- [Borrar todos los spots del panadapter](../../features/dx-cluster/clear-all-spots-from-the-panadapter.md)
