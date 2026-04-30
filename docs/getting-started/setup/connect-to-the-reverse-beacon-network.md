# Conectar a la Red de Radiobalizas Inversa

La Red de Radiobalizas Inversa (RBN) proporciona spots automatizados de CW, RTTY y skimmer digital. Esta página muestra cómo configurar y conectar el feed telnet de RBN de AetherSDR para que los spots de RBN aparezcan en su panadapter.

## Antes de comenzar

- Conozca el nombre de host y puerto del servidor telnet de RBN (el servidor público es `telnet.reversebeacon.net`, puerto `7000` para skimmers de CW).
- Conozca el indicativo que usará para iniciar sesión en RBN.
- Los spots solo aparecerán en el panadapter si la superposición maestra de spots está habilitada (`IsSpotsEnabled` está habilitada de forma predeterminada).

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **RBN**.
3. En el campo **Server:**, ingrese el nombre de host telnet de RBN (por ejemplo, `telnet.reversebeacon.net`). Esto persiste como `RbnHost`.
4. Establezca **Port:** en el puerto telnet del feed del skimmer que desee. Rango válido: 1–65535. Esto persiste como `RbnPort`.
5. En el campo **Callsign:**, ingrese su indicativo. Esto persiste como `RbnCallsign`.
6. Si el feed de RBN genera más spots de los que necesita, establezca **Rate Limit:** para limitar la cantidad de spots procesados por segundo. Esto persiste como `RbnRateLimit`.
7. Haga clic en **Connect**. La etiqueta del botón cambia a **Disconnect** cuando se establece la sesión, y la **RBN Console** muestra el tráfico entrante.
8. Para que AetherSDR se conecte a RBN automáticamente en cada inicio, habilite **Auto-connect on startup**. Esto persiste como `RbnAutoConnect`.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **Server:** | Nombre de host telnet de RBN | `RbnHost` |
| **Port:** | Puerto telnet de RBN | `RbnPort` |
| **Callsign:** | Indicativo de inicio de sesión enviado a RBN | `RbnCallsign` |
| **Rate Limit:** | Número máximo de spots de RBN aceptados por segundo | `RbnRateLimit` |
| **Connect / Disconnect** | Activa/desactiva la sesión telnet de RBN | — |
| **Auto-connect on startup** | Se conecta a RBN automáticamente al inicio | `RbnAutoConnect` |
| **RBN Console** | Pantalla de solo lectura del tráfico bruto de RBN | — |
| **Send** | Envía un comando escrito a la sesión de RBN | — |
| **Spot Color:** | Abre un selector de color para spots de RBN en el panadapter | `RbnSpotColor` |

## Informes de estación FreeDV Reporter

La pestaña **FreeDV** contiene una sección **Station Reporting** que permite que AetherSDR transmita la actividad de su estación al mapa público de FreeDV Reporter en `qso.freedv.org` siempre que el módem RADE esté activo. Esta característica está controlada por `HAVE_WEBSOCKETS`; en Windows también requiere la protección interna `HAVE_RADE`.

### Controles

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **Enable FreeDV Reporter reporting when RADE is active** | Habilita informes de estación al mapa público de FreeDV Reporter siempre que el módem RADE esté activo. La casilla se niega a habilitarse si el campo de indicativo o cuadrícula se resuelve como vacío. | `FreeDvAutoReport` |
| **Callsign:** | Indicativo informado al mapa de FreeDV Reporter. Se vuelve de solo lectura cuando se marca **Use radio**. | `FreeDvMyCallsign` |
| **Use radio** | Rellena previamente el campo de indicativo desde el indicativo configurado de la radio y bloquea el campo como de solo lectura. Cuando el indicativo de la radio cambia (por ejemplo, en Radio Setup), el campo se actualiza automáticamente. | `FreeDvUseRadioCallsign` |
| **Grid Square:** | Cuadrícula de Maidenhead informada. Se vuelve de solo lectura cuando se marca **Use GPS**. | `FreeDvMyGrid` |
| **Use GPS** | Rellena previamente el campo de cuadrícula desde el módulo GPS de la radio y bloquea el campo como de solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. | `FreeDvUseGpsGrid` |
| **Station Msg:** | Mensaje de texto libre opcional mostrado junto al indicativo en el mapa público de FreeDV Reporter. | `FreeDvMyMessage` |

### Habilitación de informes de estación

1. Haga clic en la pestaña **FreeDV** dentro de `Settings > SpotHub...`.
2. En el grupo **Station Reporting**, ingrese o confirme su **Callsign:**. Marque **Use radio** para obtenerlo de la radio automáticamente.
3. Ingrese o confirme su **Grid Square:**. En radios con hardware GPS, marque **Use GPS** para rellenarlo automáticamente.
4. Opcionalmente, complete **Station Msg:** con una breve nota de texto libre.
5. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si el indicativo o la cuadrícula se resuelve como un valor vacío, aparece un diálogo de advertencia y la casilla se revierte a no marcada. Complete el campo faltante e intente nuevamente.
   - Cuando está habilitado, la configuración persiste como `FreeDvAutoReport`.

> **Nota:** El mapa de FreeDV Reporter es un recurso público compartido por la comunidad. AetherSDR bloquea la habilitación de esta característica si el indicativo o la cuadrícula están en blanco para evitar que valores de marcador de posición como `N0CALL` o `AA00` aparezcan en el mapa.

## Consejos

- La **RBN Console** es de solo lectura y muestra líneas telnet sin procesar según llegan. Use la línea de comando **Send** debajo de ella para enviar comandos de filtro directamente al servidor RBN (por ejemplo, `set/skimmer` o comandos de filtro de banda compatibles con RBN).
- Si el panadapter se abarrota durante una contienda, reduzca **Rate Limit:** para reducir la densidad de spots sin desconectar.
- Para cambiar cómo se ven los spots en el panadapter —tamaño, posición, duración y apilamiento— consulte [Tune spot density, position, font size and lifetime](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md).
- Los spots de RBN utilizan el color establecido por **Spot Color:** en la pestaña RBN. Para anular todos los colores de fuente de spots con un solo color, use el botón **Override Colors:** en la pestaña **Display**.

## Solución de problemas

- **El botón Connect vuelve a Connect inmediatamente con un error en la consola** — El nombre de host o puerto es incorrecto, o el servidor RBN es inaccesible. Verifique `RbnHost` y `RbnPort` y compruebe su conexión de red.
- **No aparecen spots en el panadapter después de conectar** — Confirme que **Spots:** en la pestaña **Display** está establecido en Enabled (`IsSpotsEnabled`). También verifique que la banda que está monitoreando no esté oculta en las casillas de filtro de banda de la pestaña **Spot List**.
- **El panadapter se inunda de spots** — Reduzca **Rate Limit:** a un valor más bajo para limitar la tasa de spots entrantes.
- **La casilla de FreeDV Reporter se revierte inmediatamente a no marcada** — Un valor de indicativo o cuadrícula no se pudo resolver. Ingrese valores en los campos **Callsign:** y **Grid Square:**, o habilite **Use radio** y **Use GPS** para que AetherSDR pueda leerlos de la radio.

## Relacionado

- [Connect to a DX cluster](connect-to-a-dx-cluster.md)
- [Tune spot density, position, font size and lifetime](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md)
- [Pick colors for each spot source](../../features/dx-cluster/pick-colors-for-each-spot-source.md)
- [Tune to a spot by double-clicking the spot list](../../features/dx-cluster/tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [SpotHub overview](../../features/dx-cluster/overview.md)
