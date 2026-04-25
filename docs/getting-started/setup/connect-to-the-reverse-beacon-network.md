# Conectarse a la Reverse Beacon Network

La Reverse Beacon Network (RBN) proporciona spots automáticos de skimmer para CW, RTTY y modos digitales. Esta página muestra cómo configurar y conectar el feed telnet de RBN en AetherSDR para que los spots aparezcan en el panadapter.

## Antes de comenzar

- Conozca el hostname y el puerto del servidor telnet de RBN (el servidor público es `telnet.reversebeacon.net`, puerto `7000` para skimmers de CW).
- Conozca el indicativo con el que iniciará sesión en RBN.
- Los spots solo aparecerán en el panadapter si la capa de spots principal está habilitada (`IsSpotsEnabled` tiene el valor predeterminado Enabled).

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **RBN**.
3. En el campo **Server:**, ingrese el hostname telnet de RBN (p. ej., `telnet.reversebeacon.net`). Se guarda como `RbnHost`.
4. Configure **Port:** con el puerto telnet del feed de skimmer que desea usar. Rango válido: 1–65535. Se guarda como `RbnPort`.
5. En el campo **Callsign:**, ingrese su indicativo. Se guarda como `RbnCallsign`.
6. Si el feed de RBN genera más spots de los necesarios, configure **Rate Limit:** para limitar la cantidad de spots procesados por segundo. Se guarda como `RbnRateLimit`.
7. Haga clic en **Connect**. La etiqueta del botón cambia a **Disconnect** cuando la sesión se establece, y la **RBN Console** muestra el tráfico entrante.
8. Para que AetherSDR se conecte a RBN automáticamente en cada inicio, habilite **Auto-connect on startup**. Se guarda como `RbnAutoConnect`.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración | Valor predeterminado / Rango |
|---|---|---|---|
| **Server:** | Hostname telnet de RBN | `RbnHost` | — |
| **Port:** | Puerto telnet de RBN | `RbnPort` | 1–65535 |
| **Callsign:** | Indicativo de inicio de sesión enviado a RBN | `RbnCallsign` | — |
| **Rate Limit:** | Máximo de spots de RBN aceptados por segundo | `RbnRateLimit` | — |
| **Connect / Disconnect** | Activa o desactiva la sesión telnet de RBN | — | Inicia como Connect |
| **Auto-connect on startup** | Conecta a RBN automáticamente al iniciar | `RbnAutoConnect` | — |
| **RBN Console** | Visualización de solo lectura del tráfico bruto de RBN | — | — |
| **Send** | Envía un comando escrito a la sesión de RBN | — | — |
| **Spot Color:** | Abre un selector de color para los spots de RBN en el panadapter | `RbnSpotColor` | — |

## Consejos

- La **RBN Console** es de solo lectura y muestra las líneas telnet en bruto a medida que llegan. Use la línea de comando **Send** ubicada debajo para enviar comandos de filtro directamente al servidor de RBN (p. ej., `set/skimmer` u otros comandos de filtro por banda compatibles con RBN).
- Si el panadapter se satura durante un concurso, reduzca **Rate Limit:** para disminuir la densidad de spots sin desconectarse.
- Para cambiar la apariencia de los spots en el panadapter —tamaño, posición, tiempo de vida y apilamiento— consulte [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los spots](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md).
- Los spots de RBN usan el color definido en **Spot Color:** de la pestaña RBN. Para aplicar un único color a todas las fuentes de spots, use el interruptor **Override Colors:** en la pestaña **Display**.

## Solución de problemas

- **El botón Connect vuelve a Connect de inmediato con un error en la consola** — El hostname o el puerto son incorrectos, o el servidor de RBN no es accesible. Verifique `RbnHost` y `RbnPort`, y compruebe su conexión de red.
- **No aparecen spots en el panadapter después de conectarse** — Confirme que **Spots:** en la pestaña **Display** esté configurado como Enabled (`IsSpotsEnabled`). Verifique también que la banda que está monitoreando no esté oculta en los casilleros de filtro de banda de la pestaña **Spot List**.
- **El panadapter se inunda de spots** — Reduzca **Rate Limit:** a un valor menor para limitar la tasa de spots entrantes.

## Temas relacionados

- [Conectarse a un clúster DX](connect-to-a-dx-cluster.md)
- [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los spots](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md)
- [Elegir colores para cada fuente de spots](../../features/dx-cluster/pick-colors-for-each-spot-source.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](../../features/dx-cluster/tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Descripción general de SpotHub](../../features/dx-cluster/overview.md)
