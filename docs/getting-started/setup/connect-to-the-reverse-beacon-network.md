# Conectar a la Red de Balizas Inversas (RBN)

Esta página explica cómo configurar AetherSDR para recibir spots de la Red de Balizas Inversas (Reverse Beacon Network, RBN) y mostrarlos en el panadapter. La RBN proporciona spots automatizados de skimmer en CW, RTTY y modos digitales, útiles para operación en concursos y DX.

## Antes de comenzar

- Tenga a mano el nombre de host y el puerto telnet de la RBN que desea usar (el servidor público es `rbn.ad3w.com`, normalmente en el puerto `7000`).
- Tenga listo su indicativo — se usa como credencial de inicio de sesión en el servidor RBN.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **RBN**.
3. En el campo **Server:**, introduzca el nombre de host telnet de la RBN (por ejemplo, `rbn.ad3w.com`). Este valor se guarda como `RbnHost`.
4. En el campo **Port:**, introduzca el puerto telnet (rango válido: 1–65535). Este valor se guarda como `RbnPort`.
5. En el campo **Callsign:**, introduzca su indicativo. Este valor se guarda como `RbnCallsign`.
6. Si la fuente RBN genera más spots de los necesarios, establezca **Rate Limit:** con el número máximo de spots por segundo que desea aceptar. Este valor se guarda como `RbnRateLimit`.
7. Haga clic en **Connect**. La etiqueta del botón cambia a **Disconnect** cuando la sesión se establece. El tráfico telnet sin procesar de la RBN aparece en el área **RBN Console**.
8. Para que AetherSDR se conecte a la RBN automáticamente cada vez que arranque, habilite **Auto-connect on startup**. Esto se guarda en `RbnAutoConnect`.
9. Para cambiar el color de los spots de la RBN en el panadapter, haga clic en **Spot Color:** y elija un color en el selector. Esto se guarda en `RbnSpotColor`.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración | Valor predeterminado | Rango válido |
|---|---|---|---|---|
| **Server:** | Nombre de host telnet de la RBN | `RbnHost` | — | Cualquier nombre de host o IP |
| **Port:** | Puerto telnet de la RBN | `RbnPort` | — | 1–65535 |
| **Callsign:** | Indicativo de inicio de sesión enviado a la RBN | `RbnCallsign` | — | — |
| **Rate Limit:** | Máximo de spots aceptados por segundo | `RbnRateLimit` | — | — |
| **Connect / Disconnect** | Activa o desactiva la conexión telnet | — | Connect | — |
| **Auto-connect on startup** | Conecta a la RBN automáticamente al iniciar | `RbnAutoConnect` | — | — |
| **RBN Console** | Visualización de solo lectura del tráfico telnet sin procesar de la RBN | — | — | — |
| **Send** | Envía un comando escrito al servidor RBN | — | — | — |
| **Spot Color:** | Abre el selector de color para los spots de la RBN en el panadapter | `RbnSpotColor` | — | — |

## Consejos

- El volumen de spots de la RBN es alto, especialmente durante los concursos. Use **Rate Limit:** para evitar que el panadapter se sature.
- La **RBN Console** muestra la salida telnet sin procesar. Si el inicio de sesión falla, el mensaje de error aparece allí.
- Los spots de todas las fuentes activas (Cluster, RBN, WSJT-X, etc.) se combinan en la pestaña **Spot List** y se pueden ordenar por banda, frecuencia, modo o fuente.
- Haga doble clic en cualquier fila de la tabla de spots para sintonizar el equipo en esa frecuencia. Consulte [Sintonizar un spot haciendo doble clic en la lista de spots](../../features/dx-cluster/tune-to-a-spot-by-double-clicking-the-spot-list.md).

## Solución de problemas

- **La RBN Console muestra "--- Disconnected ---" inmediatamente después de conectar** — Es posible que el servidor haya rechazado el inicio de sesión. Verifique que el indicativo en **Callsign:** sea correcto y que el nombre de host y el puerto sean accesibles desde su red.
- **Aparecen spots pero el panadapter no muestra nada** — Compruebe que **Spots:** esté habilitado en la pestaña **Display** (interruptor principal, guardado como `IsSpotsEnabled`). Confirme también que la banda de los spots entrantes coincida con la vista actual del panadapter.
- **Demasiados spots ralentizan la visualización** — Reduzca **Rate Limit:** para disminuir el caudal de datos, o use las casillas de banda en la pestaña **Spot List** para ocultar las bandas en las que no está operando.

## Relacionado

- [Conectar a un cluster DX](connect-to-a-dx-cluster.md)
- [Descripción general de SpotHub](../../features/dx-cluster/overview.md)
- [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los spots](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](../../features/dx-cluster/tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Elegir colores para cada fuente de spots](../../features/dx-cluster/pick-colors-for-each-spot-source.md)
- [Habilitar coloración DXCC desde un registro ADIF](../../features/dx-cluster/enable-dxcc-coloring-from-an-adif-log.md)
- [Borrar todos los spots del panadapter](../../features/dx-cluster/clear-all-spots-from-the-panadapter.md)
