# Conectarse a la Red de Balizas Inversas (RBN)

La Red de Balizas Inversas (Reverse Beacon Network, RBN) proporciona spots automáticos de skimmer para CW, RTTY y modos digitales. Esta página muestra cómo configurar y conectar la alimentación telnet de RBN en AetherSDR para que los spots de la RBN aparezcan en el panadapter.

## Antes de comenzar

- Conozca el nombre de host y el puerto del servidor telnet de la RBN (el servidor público es `telnet.reversebeacon.net`, puerto `7000` para skimmers de CW).
- Conozca el indicativo que utilizará para iniciar sesión en la RBN.
- Los spots solo aparecerán en el panadapter si la capa de spots principal está habilitada (`IsSpotsEnabled` está activado de forma predeterminada).

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **RBN**.
3. En el campo **Server:**, ingrese el nombre de host telnet de la RBN (p. ej., `telnet.reversebeacon.net`). Este valor se guarda como `RbnHost`.
4. En **Port:**, ingrese el puerto telnet para la alimentación del skimmer que desea usar. Rango válido: 1–65535. Este valor se guarda como `RbnPort`.
5. En el campo **Callsign:**, ingrese su indicativo. Este valor se guarda como `RbnCallsign`.
6. Si la alimentación de la RBN genera más spots de los necesarios, configure **Rate Limit:** para limitar la cantidad de spots procesados por segundo. Este valor se guarda como `RbnRateLimit`.
7. Haga clic en **Connect**. La etiqueta del botón cambia a **Disconnect** cuando se establece la sesión, y la **RBN Console** muestra el tráfico entrante.
8. Para que AetherSDR se conecte a la RBN automáticamente en cada inicio, active **Auto-connect on startup**. Este valor se guarda como `RbnAutoConnect`.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **Server:** | Nombre de host telnet de la RBN | `RbnHost` |
| **Port:** | Puerto telnet de la RBN | `RbnPort` |
| **Callsign:** | Indicativo de inicio de sesión enviado a la RBN | `RbnCallsign` |
| **Rate Limit:** | Máximo de spots de la RBN aceptados por segundo | `RbnRateLimit` |
| **Connect / Disconnect** | Activa o desactiva la sesión telnet con la RBN | — |
| **Auto-connect on startup** | Conecta a la RBN automáticamente al iniciar | `RbnAutoConnect` |
| **RBN Console** | Pantalla de solo lectura del tráfico en bruto de la RBN | — |
| **Send** | Envía un comando escrito a la sesión de la RBN | — |
| **Spot Color:** | Abre un selector de color para los spots de la RBN en el panadapter | `RbnSpotColor` |

## Reporte de estación en FreeDV Reporter

La pestaña **FreeDV** contiene una sección **Station Reporting** que permite a AetherSDR transmitir la actividad de su estación al mapa público de FreeDV Reporter en `qso.freedv.org` cuando el módem RADE está activo. Esta función está controlada por la marca de compilación `HAVE_WEBSOCKETS`; en Windows también requiere la guarda interna `HAVE_RADE`.

### Controles

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **Enable FreeDV Reporter reporting when RADE is active** | Activa el reporte de estación al mapa público de FreeDV Reporter cuando el módem RADE está activo. La casilla no se puede activar si el campo de indicativo o el de cuadrícula Maidenhead resultan estar vacíos. | `FreeDvAutoReport` |
| **Callsign:** | Indicativo reportado al mapa de FreeDV Reporter. Pasa a ser de solo lectura cuando se activa **Use radio**. | `FreeDvMyCallsign` |
| **Use radio** | Rellena automáticamente el campo de indicativo con el indicativo configurado en el radio y bloquea el campo en modo de solo lectura. Cuando el indicativo del radio cambia (por ejemplo, en Radio Setup), el campo se actualiza automáticamente. | `FreeDvUseRadioCallsign` |
| **Grid Square:** | Cuadrícula Maidenhead reportada. Pasa a ser de solo lectura cuando se activa **Use GPS**. | `FreeDvMyGrid` |
| **Use GPS** | Rellena automáticamente el campo de cuadrícula con el módulo GPS del radio y bloquea el campo en modo de solo lectura. Solo aparece en modelos de radio que tienen hardware GPS. | `FreeDvUseGpsGrid` |
| **Station Msg:** | Mensaje de texto libre opcional que se muestra junto al indicativo en el mapa público de FreeDV Reporter. | `FreeDvMyMessage` |

### Activar el reporte de estación

1. Haga clic en la pestaña **FreeDV** dentro de `Settings > SpotHub...`.
2. En el grupo **Station Reporting**, ingrese o confirme su **Callsign:**. Active **Use radio** para obtenerlo del radio automáticamente.
3. Ingrese o confirme su **Grid Square:**. En radios con hardware GPS, active **Use GPS** para rellenarlo automáticamente.
4. Opcionalmente, rellene **Station Msg:** con una nota breve de texto libre.
5. Active **Enable FreeDV Reporter reporting when RADE is active**.
   - Si el indicativo o la cuadrícula resultan estar vacíos, aparece un cuadro de diálogo de advertencia y la casilla vuelve a estar sin marcar. Complete el campo que falta e inténtelo de nuevo.
   - Cuando se activa, la configuración se guarda como `FreeDvAutoReport`.

> **Nota:** El mapa de FreeDV Reporter es un recurso público compartido por la comunidad. AetherSDR impide activar esta función si el indicativo o la cuadrícula están en blanco, para evitar que aparezcan en el mapa valores de marcador de posición como `N0CALL` o `AA00`.

## Cambio en el valor predeterminado de Auto Mode

En la versión v0.9.5.1, el botón **Auto Mode:** de la pestaña **Display** cambia su valor predeterminado a **Enabled** para nuevas instalaciones. La configuración se guarda como `SpotAutoSwitchMode`. Las instalaciones existentes en las que el valor se haya guardado explícitamente no se ven afectadas.

## Consejos

- La **RBN Console** es de solo lectura y muestra las líneas telnet en bruto a medida que llegan. Use la línea de comando **Send** que aparece debajo para enviar comandos de filtro directamente al servidor de la RBN (p. ej., `set/skimmer` o comandos de filtro de banda compatibles con la RBN).
- Si el panadapter se satura durante un concurso, reduzca **Rate Limit:** para disminuir la densidad de spots sin desconectarse.
- Para cambiar la apariencia de los spots en el panadapter — tamaño, posición, duración y apilamiento — consulte [Ajustar la densidad, posición, tamaño de fuente y duración de los spots](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md).
- Los spots de la RBN utilizan el color definido en **Spot Color:** de la pestaña RBN. Para reemplazar los colores de todas las fuentes de spots con un único color, use el botón **Override Colors:** de la pestaña **Display**.

## Solución de problemas

- **El botón Connect vuelve a Connect inmediatamente con un error en la consola** — El nombre de host o el puerto es incorrecto, o el servidor de la RBN no es accesible. Verifique `RbnHost` y `RbnPort` y compruebe su conexión de red.
- **No aparecen spots en el panadapter después de conectarse** — Confirme que **Spots:** en la pestaña **Display** está configurado como Enabled (`IsSpotsEnabled`). Compruebe también que la banda que está monitoreando no esté oculta en las casillas de filtro de banda de la pestaña **Spot List**.
- **El panadapter está inundado de spots** — Reduzca **Rate Limit:** a un valor menor para limitar la tasa de spots entrantes.
- **La casilla de FreeDV Reporter vuelve a estar sin marcar inmediatamente** — No se pudo resolver el indicativo o la cuadrícula. Ingrese valores en los campos **Callsign:** y **Grid Square:**, o active **Use radio** y **Use GPS** para que AetherSDR los lea desde el radio.
- **Auto Mode: aparece como Enabled después de actualizar** — La versión v0.9.5.1 cambió el valor predeterminado de `SpotAutoSwitchMode` de `False` a `True`. Si prefiere el comportamiento anterior, abra `Settings > SpotHub...`, haga clic en la pestaña **Display** y haga clic en **Auto Mode:** para configurarlo como **Disabled**.

## Relacionados

- [Conectarse a un clúster DX](connect-to-a-dx-cluster.md)
- [Ajustar la densidad, posición, tamaño de fuente y duración de los spots](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md)
- [Elegir colores para cada fuente de spots](../../features/dx-cluster/pick-colors-for-each-spot-source.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](../../features/dx-cluster/tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Descripción general de SpotHub](../../features/dx-cluster/overview.md)
