# Conectarse a la Red de Balizas Inversas (RBN)

La Red de Balizas Inversas (Reverse Beacon Network, RBN) proporciona spots automáticos de skimmer para CW, RTTY y modos digitales. Esta página explica cómo configurar y conectar la fuente telnet de RBN en AetherSDR para que los spots aparezcan en el panadapter.

## Antes de comenzar

- Tenga a mano el nombre de host y el puerto del servidor telnet de RBN (el servidor público es `telnet.reversebeacon.net`, puerto `7000` para skimmers de CW).
- Tenga listo el indicativo con el que iniciará sesión en la RBN.
- Los spots solo aparecerán en el panadapter si la superposición maestra de spots está habilitada (`IsSpotsEnabled` tiene el valor predeterminado Enabled).

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **RBN**.
3. En el campo **Server:**, ingrese el nombre de host telnet de la RBN (p. ej., `telnet.reversebeacon.net`). Este valor se guarda como `RbnHost`.
4. En **Port:**, introduzca el puerto telnet del feed de skimmer que desea usar. Rango válido: 1–65535. Este valor se guarda como `RbnPort`.
5. En el campo **Callsign:**, ingrese su indicativo. Este valor se guarda como `RbnCallsign`.
6. Si el feed de RBN genera más spots de los necesarios, configure **Rate Limit:** para limitar la cantidad de spots procesados por segundo. Este valor se guarda como `RbnRateLimit`.
7. Haga clic en **Connect**. La etiqueta del botón cambia a **Disconnect** cuando la sesión se establece correctamente, y la **RBN Console** muestra el tráfico entrante.
8. Para que AetherSDR se conecte a la RBN automáticamente en cada inicio, habilite **Auto-connect on startup**. Este valor se guarda como `RbnAutoConnect`.

## Función de cada control

| Control | Comportamiento | Clave de configuración | Valor predeterminado / Rango |
|---|---|---|---|
| **Server:** | Nombre de host telnet de la RBN | `RbnHost` | — |
| **Port:** | Puerto telnet de la RBN | `RbnPort` | 1–65535 |
| **Callsign:** | Indicativo de inicio de sesión enviado a la RBN | `RbnCallsign` | — |
| **Rate Limit:** | Máximo de spots de RBN aceptados por segundo | `RbnRateLimit` | — |
| **Connect / Disconnect** | Activa o desactiva la sesión telnet de RBN | — | Inicia como Connect |
| **Auto-connect on startup** | Conecta a la RBN automáticamente al iniciar | `RbnAutoConnect` | — |
| **RBN Console** | Visualización de solo lectura del tráfico bruto de RBN | — | — |
| **Send** | Envía un comando escrito a la sesión de RBN | — | — |
| **Spot Color:** | Abre un selector de color para los spots de RBN en el panadapter | `RbnSpotColor` | — |

## Consejos

- La **RBN Console** es de solo lectura y muestra las líneas telnet en bruto a medida que llegan. Use la línea de comando **Send** que aparece debajo para enviar comandos de filtro directamente al servidor RBN (p. ej., `set/skimmer` u otros comandos de filtro por banda compatibles con la RBN).
- Si el panadapter se satura durante un concurso, reduzca **Rate Limit:** para disminuir la densidad de spots sin desconectarse.
- Para cambiar el aspecto de los spots en el panadapter (tamaño, posición, duración y apilamiento), consulte [Ajustar la densidad, posición, tamaño de fuente y duración de los spots](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md).
- Los spots de RBN utilizan el color definido en **Spot Color:** en la pestaña RBN. Para reemplazar el color de todas las fuentes de spots con un único color, use el interruptor **Override Colors:** en la pestaña **Display**.

## Solución de problemas

- **El botón Connect vuelve a Connect inmediatamente con un error en la consola** — El nombre de host o el puerto es incorrecto, o el servidor RBN no es accesible. Verifique `RbnHost` y `RbnPort` y compruebe su conexión de red.
- **No aparecen spots en el panadapter tras conectarse** — Confirme que **Spots:** en la pestaña **Display** esté configurado como Enabled (`IsSpotsEnabled`). También verifique que la banda que está monitoreando no esté oculta en las casillas de filtro por banda de la pestaña **Spot List**.
- **El panadapter se inunda de spots** — Reduzca **Rate Limit:** a un valor menor para limitar la tasa de spots entrantes.

## Temas relacionados

- [Conectarse a un clúster DX](connect-to-a-dx-cluster.md)
- [Ajustar la densidad, posición, tamaño de fuente y duración de los spots](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md)
- [Elegir colores para cada fuente de spots](../../features/dx-cluster/pick-colors-for-each-spot-source.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](../../features/dx-cluster/tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Descripción general de SpotHub](../../features/dx-cluster/overview.md)
