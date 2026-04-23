# Conectarse a un clúster DX

Abra el diálogo SpotHub e introduzca el nombre de host, el puerto y el indicativo de su clúster para que los spots DX aparezcan como superposiciones en el panadapter.

## Antes de comenzar

- Conozca el nombre de host (o dirección IP) y el puerto telnet del clúster DX que desea utilizar (por ejemplo, `dxc.k0xm.net`, puerto `23`).
- Tenga a mano su indicativo — el clúster lo utiliza para el inicio de sesión.

## Pasos

1. Haga clic en `Settings > SpotHub...` para abrir el diálogo SpotHub.
2. Haga clic en la pestaña **Cluster**.
3. En el campo **Server:**, escriba el nombre de host o la dirección IP del clúster. Este valor se guarda como `ClusterHost`.
4. En el campo **Port:**, establezca el puerto telnet (rango válido: 1–65535). Este valor se guarda como `ClusterPort`.
5. En el campo **Callsign:**, escriba su indicativo. Este valor se guarda como `ClusterCallsign`.
6. Haga clic en **Connect**. La etiqueta del botón cambia a **Disconnect** cuando la sesión se establece, y la **Cluster Console** muestra `--- Connected ---`.
7. Para conectarse automáticamente cada vez que AetherSDR se inicia, haga clic en **Auto-connect on startup** para habilitarlo. Este valor se guarda como `ClusterAutoConnect`.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración | Valor predeterminado | Rango válido |
|---|---|---|---|---|
| **Server:** | Nombre de host del clúster DX. | `ClusterHost` | — | Cualquier nombre de host o IP |
| **Port:** | Puerto telnet del clúster. | `ClusterPort` | — | 1–65535 |
| **Callsign:** | Indicativo de inicio de sesión enviado al clúster al conectarse. | `ClusterCallsign` | — | — |
| **Connect / Disconnect** | Activa o desactiva la conexión telnet. | — | Connect | — |
| **Auto-connect on startup** | Reconecta a este clúster cada vez que AetherSDR se inicia. | `ClusterAutoConnect` | — | — |
| **Cluster Console** | Visualización de solo lectura del tráfico sin procesar del clúster. | — | — | — |
| **Send** (línea de comandos) | Envía un comando escrito al clúster conectado. | — | — | — |
| **Spot Color:** | Abre un selector de color para los spots provenientes del clúster en el panadapter. | `ClusterSpotColor` | — | — |

## Consejos

- La **Cluster Console** muestra la salida telnet sin procesar, incluidos los mensajes de inicio de sesión. Si el clúster requiere una contraseña, escríbala en el campo de comandos y haga clic en **Send**.
- Para sintonizar directamente una frecuencia detectada en un spot, cambie a la pestaña **Spot List** y haga doble clic en la fila correspondiente.
- Las superposiciones de spots en el panadapter se controlan globalmente mediante el selector **Spots:** en la pestaña **Display** (`IsSpotsEnabled`, valor predeterminado: habilitado). Si los spots no son visibles después de conectarse, verifique ese selector.

## Solución de problemas

- **El botón permanece como "Connect" después de hacer clic** — El nombre de host o el puerto del clúster es incorrecto, o el servidor no es accesible desde su red. Revise la **Cluster Console** en busca de una línea de error y verifique el nombre de host y el puerto.
- **No aparecen spots en el panadapter a pesar de estar conectado** — Confirme que **Spots:** en la pestaña **Display** esté habilitado. Verifique también que la banda de los spots entrantes no esté oculta mediante las casillas **Bands:** en la pestaña **Spot List**.
- **"Error: …" mostrado en la consola** — El clúster rechazó la conexión o la interrumpió. Esto suele ser un problema de inicio de sesión; observe la **Cluster Console** para ver el mensaje de inicio de sesión del clúster y envíe su indicativo manualmente con **Send** para confirmar las credenciales.

## Relacionado

- [Descripción general de SpotHub](../../features/dx-cluster/overview.md)
- [Conectarse a la Reverse Beacon Network](connect-to-the-reverse-beacon-network.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](../../features/dx-cluster/tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md)
- [Habilitar el coloreado DXCC desde un registro ADIF](../../features/dx-cluster/enable-dxcc-coloring-from-an-adif-log.md)
- [Elegir colores para cada fuente de spots](../../features/dx-cluster/pick-colors-for-each-spot-source.md)
- [Borrar todos los spots del panadapter](../../features/dx-cluster/clear-all-spots-from-the-panadapter.md)
