# Conectarse a la Red de Balizas Inversas (RBN)

La Red de Balizas Inversas (Reverse Beacon Network, RBN) detecta automáticamente señales CW, RTTY y digitales escuchadas por una red mundial de estaciones skimmer. Esta página explica cómo conectar AetherSDR al flujo telnet de la RBN para que los avisos de la RBN aparezcan en su panadapter.

## Antes de comenzar

- Conozca su indicativo de llamada — se utiliza como credencial de acceso al servidor telnet de la RBN.
- Conozca el nombre de host y el puerto del servidor telnet de la RBN. El servidor público estándar es `rbn.telegraphy.de` en el puerto `7000`, pero verifique en [reversebeacon.net](https://www.reversebeacon.net) si la dirección ha cambiado.
- Para que los avisos se muestren en el panadapter, es necesario que la capa de avisos principal esté habilitada (consulte la pestaña Display, `IsSpotsEnabled`).

## Pasos

1. Haga clic en `Settings > SpotHub...` para abrir el cuadro de diálogo SpotHub.
2. Haga clic en la pestaña **RBN**.
3. En el campo **Server:**, ingrese el nombre de host telnet de la RBN (guardado como `RbnHost`).
4. En el cuadro numérico **Port:**, ingrese el puerto telnet en el rango 1–65535 (guardado como `RbnPort`).
5. En el campo **Callsign:**, ingrese su indicativo (guardado como `RbnCallsign`).
6. Si desea limitar la cantidad de avisos por segundo que se procesan, establezca el valor preferido en **Rate Limit:** (guardado como `RbnRateLimit`).
7. Haga clic en **Connect**. La etiqueta del botón cambia a **Disconnect** y el área de consola inferior muestra `--- Connected ---` seguido del tráfico entrante de la RBN en la **RBN Console**.
8. Para conectarse automáticamente cada vez que AetherSDR se inicia, haga clic en **Auto-connect on startup** para activarlo (guardado como `RbnAutoConnect`).
9. Para elegir un color de visualización para los avisos de la RBN en el panadapter, haga clic en **Spot Color:** y seleccione un color en el selector (guardado como `RbnSpotColor`).

## Qué hace cada control

| Control | Comportamiento | Clave de configuración | Rango / valor predeterminado |
|---|---|---|---|
| **Server:** | Nombre de host del servidor telnet de la RBN. | `RbnHost` | Cualquier nombre de host |
| **Port:** | Puerto telnet en el servidor de la RBN. | `RbnPort` | 1–65535 |
| **Callsign:** | Indicativo de acceso enviado a la RBN al conectar. | `RbnCallsign` | Su indicativo |
| **Rate Limit:** | Máximo de avisos de la RBN procesados por segundo. | `RbnRateLimit` | Consulte el rango del cuadro numérico |
| **Connect / Disconnect** | Activa o desactiva la conexión telnet a la RBN. | — | Etiqueta predeterminada: Connect |
| **Auto-connect on startup** | Conecta a la RBN automáticamente al iniciar AetherSDR. | `RbnAutoConnect` | — |
| **RBN Console** | Visualización de solo lectura del tráfico telnet entrante de la RBN. | — | — |
| **Send** | Envía un comando escrito a la sesión de la RBN. | — | — |
| **Spot Color:** | Abre un selector de color para los avisos de la RBN en el panadapter. | `RbnSpotColor` | — |

## Consejos

- El control **Rate Limit:** es útil durante un fin de semana de concurso activo, cuando la RBN puede generar cientos de avisos por segundo. Reducirlo evita que la lista de avisos y el panadapter se saturen.
- Puede escribir comandos telnet de la RBN (por ejemplo, `set/skimmer` o `set/dx`) en la línea de comandos situada debajo de la consola y hacer clic en **Send** para enviarlos al servidor.
- Los avisos de la RBN aparecen junto a los avisos del cluster DX en la pestaña **Spot List**. Use las casillas de verificación de banda para filtrar por banda. Haga doble clic en cualquier fila para sintonizar directamente esa frecuencia.

## Solución de problemas

- **El botón permanece en "Connect" y la consola muestra un error** — El nombre de host o el puerto es incorrecto, o un cortafuegos está bloqueando el tráfico telnet saliente. Verifique la dirección y el puerto del servidor, y compruebe que su red permita conexiones TCP salientes en el puerto configurado.
- **Los avisos aparecen en la consola pero no en el panadapter** — Es posible que la capa de avisos principal esté deshabilitada. Abra la pestaña **Display** en SpotHub y confirme que **Spots:** esté habilitado (`IsSpotsEnabled`). Confirme también que haya una slice de radio abierta y visible.
- **"Auto-connect on startup" no se reconecta tras una interrupción de red** — La conexión automática solo se activa al iniciar la aplicación. Si la sesión se interrumpe durante el uso, haga clic en **Connect** manualmente para reconectarse.

## Temas relacionados

- [Descripción general de SpotHub](../../features/dx-cluster/overview.md)
- [Conectarse a un cluster DX](connect-to-a-dx-cluster.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los avisos](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md)
- [Elegir colores para cada fuente de avisos](../../features/dx-cluster/pick-colors-for-each-spot-source.md)
- [Sintonizar un aviso haciendo doble clic en la lista de avisos](../../features/dx-cluster/tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Habilitar coloreado DXCC desde un registro ADIF](../../features/dx-cluster/enable-dxcc-coloring-from-an-adif-log.md)
