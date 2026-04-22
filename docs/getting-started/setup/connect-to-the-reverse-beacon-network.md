# Conectarse a la Reverse Beacon Network

La Reverse Beacon Network (RBN) proporciona informes de spots automatizados de CW, RTTY y modos digitales desde estaciones skimmer de todo el mundo. Esta página explica cómo configurar la conexión RBN de AetherSDR para que esos spots aparezcan en su panadapter.

## Antes de comenzar

- AetherSDR está instalado y en ejecución.
- Conoce el nombre de host telnet y el puerto de la RBN que desea usar (el servidor público de la RBN es `telnet.reversebeacon.net`).
- Dispone de un indicativo para usar como inicio de sesión.

## Pasos

1. Haga clic en `Settings > SpotHub...` para abrir el diálogo SpotHub.
2. Haga clic en la pestaña **RBN**.
3. En el campo **Server:**, introduzca el nombre de host telnet de la RBN.
4. En el cuadro giratorio **Port:**, introduzca el puerto telnet. Rango válido: 1–65535.
5. En el campo **Callsign:**, introduzca el indicativo con el que desea iniciar sesión.
6. En el cuadro giratorio **Rate Limit:**, establezca el número máximo de spots por segundo que desea recibir.
7. Haga clic en **Connect**. El área **RBN Console** mostrará el tráfico telnet entrante sin procesar cuando se establezca la conexión.
8. Para que AetherSDR se conecte a la RBN automáticamente cada vez que se inicie, haga clic en **Auto-connect on startup** para activar esta opción.

## Función de cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Nombre de host telnet de la RBN | `RbnHost` |
| **Port:** | Puerto telnet de la RBN (1–65535) | `RbnPort` |
| **Callsign:** | Indicativo de inicio de sesión enviado a la RBN | `RbnCallsign` |
| **Rate Limit:** | Número máximo de spots RBN por segundo entregados al panadapter | `RbnRateLimit` |
| **Connect / Disconnect** | Activa o desactiva la conexión telnet a la RBN | — |
| **Auto-connect on startup** | Conecta a la RBN automáticamente al iniciar AetherSDR | `RbnAutoConnect` |
| **RBN Console** | Visualización de solo lectura del tráfico telnet RBN sin procesar | — |
| **Send** | Envía un comando escrito al servidor RBN | — |
| **Spot Color:** | Abre un selector de color para establecer el color de los spots RBN en el panadapter | `RbnSpotColor` |

## Consejos

- La RBN puede generar una tasa de spots muy elevada durante los concursos. Establezca un valor más bajo en **Rate Limit:** si el panadapter se sobrecarga o se vuelve lento.
- La visualización de spots en el panadapter requiere que la superposición principal de spots esté activa. En la pestaña **Display**, verifique que **Spots:** esté configurado en Enabled (valor predeterminado).
- Haga doble clic en cualquier fila de spot RBN en la pestaña **Spot List** para sintonizar la radio directamente a esa frecuencia.

## Solución de problemas

- **La RBN Console no muestra tráfico tras hacer clic en Connect** — Verifique el nombre de host y el puerto. La **RBN Console** mostrará un mensaje de error de conexión si el servidor no es accesible. Compruebe que su cortafuegos permita tráfico TCP saliente en el puerto configurado.
- **Los spots aparecen en la pestaña Spot List pero no en el panadapter** — Abra `Settings > SpotHub...`, haga clic en la pestaña **Display** y confirme que **Spots:** está en Enabled.
- **Demasiados spots saturan la pantalla** — Reduzca el valor de **Rate Limit:**, o ajuste **Spot Lifetime:** y **Levels:** en la pestaña **Display** para disminuir la saturación.

## Relacionados

- [Descripción general de SpotHub](../../features/dx-cluster/overview.md)
- [Conectarse a un clúster DX](connect-to-a-dx-cluster.md)
- [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los spots](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](../../features/dx-cluster/tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Elegir colores para cada fuente de spots](../../features/dx-cluster/pick-colors-for-each-spot-source.md)
- [Borrar todos los spots del panadapter](../../features/dx-cluster/clear-all-spots-from-the-panadapter.md)
