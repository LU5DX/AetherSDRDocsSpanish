# Conectarse a la Red de Balizas Inversa

La Red de Balizas Inversa (RBN) proporciona detecciones automatizadas de CW, RTTY y skimmers digitales. Esta página explica cómo configurar y conectar el feed telnet de RBN de AetherSDR para que las detecciones de RBN aparezcan en su panadapter.

## Antes de comenzar

- Conozca el nombre de host y el puerto del servidor telnet de RBN (el servidor público es `telnet.reversebeacon.net`, puerto `7000` para skimmers de CW).
- Conozca el indicativo que usará para iniciar sesión en RBN.
- Las detecciones solo aparecerán en el panadapter si la superposición maestra de detecciones está habilitada (`IsSpotsEnabled` tiene como valor predeterminado Enabled).

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **RBN**.
3. En el campo **Server:**, introduzca el nombre de host telnet de RBN (p. ej., `telnet.reversebeacon.net`). Este valor se guarda como `RbnHost`.
4. Defina **Port:** con el puerto telnet del feed de skimmer que desee. Rango válido: 1–65535. Este valor se guarda como `RbnPort`.
5. En el campo **Callsign:**, introduzca su indicativo. Este valor se guarda como `RbnCallsign`.
6. Si el feed de RBN produce más detecciones de las que necesita, ajuste **Rate Limit:** para limitar la cantidad de detecciones procesadas por segundo. Este valor se guarda como `RbnRateLimit`.
7. Haga clic en **Connect**. La etiqueta del botón cambia a **Disconnect** cuando la sesión se establece, y la **RBN Console** muestra el tráfico entrante.
8. Para que AetherSDR se conecte automáticamente a RBN en cada inicio, active **Auto-connect on startup**. Este valor se guarda como `RbnAutoConnect`.

## Función de cada control

| Control                                                       | Comportamiento                                                                                                                                                         | Clave de configuración                                                                                              |
|---------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| **Server:**                                                   | Nombre de host telnet de RBN                                                                                                                                           | `RbnHost`                                                                                                           |
| **Port:**                                                     | Puerto telnet de RBN                                                                                                                                                   | `RbnPort`                                                                                                           |
| **Callsign:**                                                 | Indicativo de inicio de sesión enviado a RBN                                                                                                                           | `RbnCallsign`                                                                                                       |
| **Rate Limit:**                                               | Máximo de detecciones de RBN aceptadas por segundo                                                                                                                     | `RbnRateLimit`                                                                                                      |
| **Connect / Disconnect**                                      | Activa o desactiva la sesión telnet de RBN                                                                                                                             | —                                                                                                                   |
| **Auto-connect on startup**                                   | Conecta a RBN automáticamente al inicio                                                                                                                                | `RbnAutoConnect`                                                                                                    |
| **RBN Console**                                               | Visualización de solo lectura del tráfico RBN sin procesar                                                                                                             | —                                                                                                                   |
| **Send**                                                      | Envía un comando escrito a la sesión de RBN                                                                                                                            | —                                                                                                                   |
| **Spot Color:**                                               | Abre un selector de color para las detecciones de RBN en el panadapter                                                                                                 | `RbnSpotColor`                                                                                                      |
| **Spot Lines:**                                               | Dibuja líneas verticales desde el espectro hasta cada etiqueta de detección. Desactívelo durante concursos para reducir el desorden visual.                            | `IsSpotsLinesEnabled`                                                                                               |
| Total Spots:                                                  | Indicador en vivo de cuántas detecciones se rastrean actualmente en todas las fuentes. Se actualiza cuando se añaden o eliminan detecciones. Se reinicia a 0 al pulsar **Clear All Spots**. | —                                                                                                                   |
| Auto:                                                         | Cambia automáticamente el modo del slice al hacer clic en una detección que incluya información de modo (p. ej., CW, FT8, RTTY).                                       | `SpotAutoSwitchMode`                                                                                                |
| Signals (Signal History)                                      | Marcadores dorados para señales de ancho de voz detectadas en el panadapter.                                                                                           | `SHistoryMarkersEnabled`                                                                                            |
| QRM (Signal History)                                          | Marcadores rojos para portadoras persistentes e interferencia de banda ancha.                                                                                          | `SHistoryQrmEnabled`                                                                                                |
| Clear All                                                     | Borra todas las detecciones DX, el feed de memoria, los marcadores de Signal History y los marcadores de QRM del espectro.                                             | —                                                                                                                   |
| Selector de color de texto de detección                      | Abre QColorDialog para elegir el color del texto de las detecciones.                                                                                                   | `SpotsOverrideColor`                                                                                                |
| Override Background: Enabled                                  | Activa un color de fondo personalizado para las detecciones.                                                                                                           | `IsSpotsOverrideBackgroundColorsEnabled`                                                                            |
| Override Background: Auto                                     | Selecciona automáticamente el color de fondo para lograr contraste.                                                                                                    | `IsSpotsOverrideToAutoBackgroundColorEnabled`                                                                       |
| Selector de color de fondo de detección                      | Abre QColorDialog para el color de fondo de las detecciones.                                                                                                           | `SpotsOverrideBgColor`                                                                                              |
| Background Opacity:                                           | Opacidad del color de fondo de las detecciones (0-100).                                                                                                                | `SpotsBackgroundOpacity`                                                                                            |
| DXCC Coloring (sección)                                       | Encabezado de sección para los controles de coloración DXCC en la columna izquierda debajo del divisor.                                                                | —                                                                                                                   |
| DXCC Colors:                                                  | Colorea las detecciones según el estado DXCC trabajado/confirmado/necesario.                                                                                           | `IsDxccColoringEnabled`                                                                                             |
| Log File (ADIF):                                              | Carga un archivo de registro ADIF para impulsar la coloración DXCC. Supervisa automáticamente los cambios del archivo después de seleccionarlo.                        | `DxccAdifFilePath`                                                                                                  |
| Imported: (estadísticas DXCC)                                 | Muestra el recuento de QSO y el recuento de entidades cuando se carga un registro.                                                                                     | —                                                                                                                   |
| Muestras de color DXCC (New DXCC / New Band / New Mode / Worked) | Abre un selector de color para cada categoría de estado DXCC.                                                                                                          | `DxccColorNewEntity`, `DxccColorNewBand`, `DxccColorNewMode`, `DxccColorWorked`                                     |
| Signal History (sección)                                      | Encabezado de sección para los parámetros ajustables de Signal History en la columna derecha debajo del divisor.                                                       | —                                                                                                                   |
| Marker Lifetime:                                              | Tiempo durante el que persiste un marcador de Signal History inactivo antes de eliminarse (15-300 s).                                                                  | `SHistoryLifetimeS`                                                                                                 |
| QRM Gate:                                                     | Tiempo durante el que una portadora estrecha o una señal de banda ancha debe persistir antes de clasificarse como QRM (3-30 s).                                         | `SHistoryQrmGateS`                                                                                                  |
| Edge Threshold:                                               | Umbral por encima del piso de ruido para el recorrido del borde de pendiente que refina el borde lateral de la portadora en S-History (1.0-10.0 dB).                   | `SHistorySoftEdgeDb`                                                                                                |
| Muestras de color de Signal History (Signals / QRM)           | Abre un selector de color para los marcadores de señal de voz (dorado) y los marcadores de QRM (rojo).                                                                  | `SHistoryColorSignals`, `SHistoryColorQrm`                                                                          |
| Snap to Step:                                                 | Redondea el clic para sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de la portadora.         | `SHistorySnapToStep`                                                                                                |

## Al hacer doble clic en una detección ahora se envían indicaciones de modo

A partir de la versión v0.9.7, al hacer doble clic en una fila de la pestaña **Spot List** se sintoniza el receptor a la frecuencia de la detección y también se cambia el modo del receptor para que coincida con la detección. Por ejemplo, al hacer doble clic en una detección de CW, el receptor cambia a CW, y al hacer doble clic en una detección de FT8, cambia al modo digital apropiado, en lugar de solo cambiar la frecuencia. El modo se resuelve a partir del comentario de la detección mediante la lógica `SpotModeResolver` compartida entre todas las fuentes de detecciones.

## Spot Lines

La pestaña **Display** ahora incluye una opción **Spot Lines:** (nueva en v0.9.7). Cuando está **Enabled** (valor predeterminado), AetherSDR dibuja una línea vertical corta desde la traza del espectro hasta cada etiqueta de detección en el panadapter, lo que facilita ver exactamente a qué frecuencia corresponde una detección. Ajústelo a **Disabled** durante concursos u otras sesiones de operación con alta densidad de detecciones para reducir el desorden visual. Este valor se guarda como `IsSpotsLinesEnabled`.

## Informes de estación en FreeDV Reporter

La pestaña **FreeDV** contiene una sección **Station Reporting** que permite a AetherSDR transmitir la actividad de su estación al mapa público de FreeDV Reporter en `qso.freedv.org` siempre que el módem RADE esté activo. Esta función está protegida por la compilación mediante `HAVE_WEBSOCKETS`; en Windows también requiere la protección interna `HAVE_RADE`.

### Controles

| Control                             | Comportamiento                                                                                                                                                                    | Clave de configuración  |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|
| **Enable FreeDV Reporter reporting when RADE is active** | Activa los informes de estación al mapa público de FreeDV Reporter siempre que el módem RADE esté activo. La casilla no se activa si el indicativo o el campo de cuadrícula se resuelven como un valor vacío. | `FreeDvAutoReport`       |
| **Callsign:**                      | Indicativo informado al mapa de FreeDV Reporter. Se vuelve de solo lectura cuando **Use radio** está marcado.                                                                     | `FreeDvMyCallsign`        |
| **Use radio**                      | Rellena previamente el campo de indicativo desde el indicativo configurado en la radio y bloquea el campo como solo lectura. Cuando el indicativo de la radio cambia (por ejemplo, en Radio Setup), el campo se actualiza automáticamente. | `FreeDvUseRadioCallsign`  |
| **Grid Square:**                   | Cuadrícula Maidenhead informada. Se vuelve de solo lectura cuando **Use GPS** está marcado.                                                                                       | `FreeDvMyGrid`            |
| **Use GPS**                        | Rellena previamente el campo de cuadrícula desde el módulo GPS de la radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS.      | `FreeDvUseGpsGrid`        |
| **Station Msg:**                   | Mensaje de texto libre opcional que se muestra junto al indicativo en el mapa público de FreeDV Reporter.                                                                         | `FreeDvMyMessage`         |

### Activar los informes de estación

1. Haga clic en la pestaña **FreeDV** dentro de `Settings > SpotHub...`.
2. En el grupo **Station Reporting**, introduzca o confirme su **Callsign:**. Marque **Use radio** para obtenerlo automáticamente de la radio.
3. Introduzca o confirme su **Grid Square:**. En radios con hardware GPS, marque **Use GPS** para que se complete automáticamente.
4. Opcionalmente, rellene **Station Msg:** con una nota breve de texto libre.
5. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si el indicativo o la cuadrícula se resuelven como un valor vacío, aparece un cuadro de diálogo de advertencia y la casilla se desmarca. Rellene el campo faltante e intente de nuevo.
   - Cuando está activada, la configuración se guarda como `FreeDvAutoReport`.

> **Nota:** El mapa de FreeDV Reporter es un recurso público compartido por la comunidad. AetherSDR bloquea la activación de esta función si el indicativo o la cuadrícula están en blanco para evitar que aparezcan valores provisionales como `N0CALL` o `AA00` en el mapa.

## Cambio en el valor predeterminado de Auto Mode

En la versión v0.9.5.1, la opción **Auto Mode:** de la pestaña **Display** tiene como valor predeterminado **Enabled** para instalaciones nuevas. La configuración se guarda como `SpotAutoSwitchMode`. Las instalaciones existentes donde el valor se haya guardado explícitamente no se ven afectadas.

## Consejos

- La **RBN Console** es de solo lectura y muestra las líneas telnet sin procesar a medida que llegan. Use la línea de comandos **Send** debajo de ella para enviar comandos de filtro directamente al servidor RBN (p. ej., `set/skimmer` o comandos de filtro de banda compatibles con RBN).
- Si el panadapter se satura durante un concurso, reduzca **Rate Limit:** para disminuir la densidad de detecciones sin desconectarse. También puede desactivar **Spot Lines:** en la pestaña **Display** para reducir aún más el desorden visual.
- Para cambiar el aspecto de las detecciones en el panadapter (tamaño, posición, duración y apilamiento), consulte [Ajustar densidad, posición, tamaño de fuente y duración de las detecciones](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md).
- Las detecciones de RBN usan el color definido por **Spot Color:** en la pestaña RBN. Para sobrescribir los colores de todas las fuentes de detecciones con un solo color, use la opción **Override Colors:** en la pestaña **Display**.

## Solución de problemas

- **El botón Connect vuelve inmediatamente a Connect con un error en la consola** — El nombre de host o el puerto son incorrectos, o el servidor RBN no está accesible. Verifique `RbnHost` y `RbnPort` y compruebe su conexión de red.
- **No aparecen detecciones en el panadapter después de conectar** — Confirme que **Spots:** en la pestaña **Display** está en Enabled (`IsSpotsEnabled`). También verifique que la banda que está monitoreando no esté oculta en las casillas de verificación del filtro de bandas de la pestaña **Spot List**.
- **El panadapter está inundado de detecciones** — Reduzca **Rate Limit:** a un valor más bajo para limitar la tasa de detecciones entrantes. Alternativamente, desactive **Spot Lines:** (`IsSpotsLinesEnabled`) en la pestaña **Display** para que las áreas densas en detecciones sean más fáciles de leer sin reducir la cantidad de detecciones mostradas.
- **Al hacer doble clic en una detección cambia la frecuencia pero no cambia el modo** — El comentario de la detección puede no contener un token de modo reconocible. El cambio de modo depende de que el comentario de la detección contenga una cadena de modo conocida (p. ej., `CW`, `FT8`, `SSB`). Si el remitente no incluyó un modo en el comentario, solo cambia la frecuencia.
- **La casilla de FreeDV Reporter se desmarca inmediatamente** — No se pudo resolver un valor de indicativo o cuadrícula. Introduzca valores en los campos **Callsign:** y **Grid Square:**, o active **Use radio** y **Use GPS** para que AetherSDR pueda leerlos de la radio.
- **Auto Mode: ahora está en Enabled después de actualizar** — La versión v0.9.5.1 cambió el valor predeterminado de `SpotAutoSwitchMode` de `False` a `True`. Si prefiere el comportamiento anterior, abra `Settings > SpotHub...`, haga clic en la pestaña **Display** y haga clic en **Auto Mode:** para establecerlo en **Disabled**.

## Relacionado

- [Conectarse a un clúster DX](connect-to-a-dx-cluster.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de las detecciones
