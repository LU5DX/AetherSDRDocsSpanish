# Conectarse a la Reverse Beacon Network

La Reverse Beacon Network (RBN) proporciona avistamientos automatizados de CW, RTTY y skimmer digitales. Esta página muestra cómo configurar y conectar la fuente de datos telnet de RBN de AetherSDR para que los avistamientos de RBN aparezcan en su panadapter.

## Antes de comenzar

- Conozca el nombre de host y el puerto del servidor telnet de RBN (el servidor público es `telnet.reversebeacon.net`, puerto `7000` para skimmers de CW).
- Conozca el indicativo que usará para iniciar sesión en RBN.
- Los avistamientos solo aparecerán en el panadapter si la superposición maestra de avistamientos está habilitada (`IsSpotsEnabled` predeterminado en Enabled).

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **RBN**.
3. En el campo **Server:**, ingrese el nombre de host telnet de RBN (ej., `telnet.reversebeacon.net`). Esto se guarda como `RbnHost`.
4. Establezca **Port:** en el puerto telnet para la fuente de datos del skimmer que desee. Rango válido: 1–65535. Esto se guarda como `RbnPort`.
5. En el campo **Callsign:**, ingrese su indicativo. Esto se guarda como `RbnCallsign`.
6. Si la fuente de datos de RBN produce más avistamientos de los que necesita, establezca **Rate Limit:** para limitar la cantidad de avistamientos procesados por segundo. Esto se guarda como `RbnRateLimit`.
7. Haga clic en **Connect**. La etiqueta del botón cambia a **Disconnect** cuando la sesión se establece, y la **RBN Console** muestra el tráfico entrante.
8. Para que AetherSDR se conecte a RBN automáticamente en cada inicio, habilite **Auto-connect on startup**. Esto se guarda como `RbnAutoConnect`.
9. (Opcional) Haga clic en **Startup Commands…** para editar los comandos enviados automáticamente después de cada inicio de sesión en RBN. Un comando por línea (ej., `SET/NAME`, `SET/QTH`, `ACCEPT/SPOT`). Estos se guardan como `RbnStartupCommands`.

## Qué hace cada control

| Control                                                       | Comportamiento                                                                                                                                                               | Clave de configuración                                                                                            |
|---------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| **Server:**                                                   | Nombre de host telnet de RBN                                                                                                                                                 | `RbnHost`                                                                                                         |
| **Port:**                                                     | Puerto telnet de RBN                                                                                                                                                         | `RbnPort`                                                                                                         |
| **Callsign:**                                                 | Indicativo de inicio de sesión enviado a RBN                                                                                                                                 | `RbnCallsign`                                                                                                     |
| **Rate Limit:**                                               | Máximo de avistamientos de RBN aceptados por segundo                                                                                                                         | `RbnRateLimit`                                                                                                    |
| **Connect / Disconnect**                                      | Alterna la sesión telnet de RBN                                                                                                                                              | —                                                                                                                 |
| **Auto-connect on startup**                                   | Se conecta a RBN automáticamente al iniciar                                                                                                                                  | `RbnAutoConnect`                                                                                                  |
| **Startup Commands…**                                         | Abre un diálogo para editar comandos enviados automáticamente después de cada inicio de sesión en RBN. Un comando por línea.                                                  | `RbnStartupCommands`                                                                                              |
| **RBN Console**                                               | Visualización de solo lectura del tráfico bruto de RBN                                                                                                                        | —                                                                                                                 |
| **Send**                                                      | Envía un comando escrito a la sesión de RBN                                                                                                                                  | —                                                                                                                 |
| **Spot Color:**                                               | Abre un selector de color para los avistamientos de RBN en el panadapter                                                                                                     | `RbnSpotColor`                                                                                                    |
| **Spot Lines:**                                               | Dibuja líneas verticales desde el espectro hasta cada etiqueta de avistamiento. Desactívelo durante concursos para reducir el desorden visual.                               | `IsSpotsLinesEnabled`                                                                                             |
| Total Spots:                                                  | Lectura en vivo de cuántos avistamientos se rastrean actualmente en todas las fuentes. Se actualiza cuando se agregan o eliminan avistamientos. Se reinicia a 0 al presionar **Clear All Spots**. | —                                                                                                                 |
| Auto:                                                         | Cambia automáticamente el modo de la slice al hacer clic en un avistamiento que incluya información de modo (ej., CW, FT8, RTTY).                                              | `SpotAutoSwitchMode`                                                                                              |
| Signals (Signal History)                                      | Marcadores dorados para señales detectadas de ancho de voz en el panadapter.                                                                                                 | `SHistoryMarkersEnabled`                                                                                          |
| QRM (Signal History)                                          | Marcadores rojos para portadoras persistentes e interferencia de banda ancha.                                                                                                | `SHistoryQrmEnabled`                                                                                              |
| Clear All                                                     | Elimina todos los avistamientos DX, fuente de datos de memoria, marcadores de Signal History y marcadores QRM del espectro.                                                   | —                                                                                                                 |
| Selector de color de texto de avistamiento                    | Abre QColorDialog para seleccionar el color del texto del avistamiento.                                                                                                      | `SpotsOverrideColor`                                                                                              |
| Override Background: Enabled                                  | Habilita un color de fondo personalizado para los avistamientos.                                                                                                             | `IsSpotsOverrideBackgroundColorsEnabled`                                                                          |
| Override Background: Auto                                     | Selecciona automáticamente el color de fondo para contraste.                                                                                                                 | `IsSpotsOverrideToAutoBackgroundColorEnabled`                                                                     |
| Selector de color de fondo de avistamiento                    | Abre QColorDialog para el color de fondo del avistamiento.                                                                                                                   | `SpotsOverrideBgColor`                                                                                            |
| Background Opacity:                                           | Opacidad del color de fondo del avistamiento (0-100).                                                                                                                        | `SpotsBackgroundOpacity`                                                                                          |
| DXCC Coloring (sección)                                       | Encabezado de sección para los controles de coloración DXCC en la columna izquierda debajo del divisor.                                                                      | —                                                                                                                 |
| DXCC Colors:                                                  | Colorea los avistamientos según el estado DXCC trabajado/confirmado/necesario.                                                                                               | `IsDxccColoringEnabled`                                                                                           |
| Log File (ADIF):                                              | Carga un archivo de registro ADIF para impulsar la coloración DXCC. Vigila automáticamente el archivo en busca de cambios después de la selección.                           | `DxccAdifFilePath`                                                                                                |
| Imported: (estadísticas DXCC)                                 | Muestra el recuento de QSO y el recuento de entidades cuando se carga un registro.                                                                                           | —                                                                                                                 |
| Muestras de color DXCC (New DXCC / New Band / New Mode / Worked) | Abre un selector de color para cada categoría de estado DXCC.                                                                                                                 | `DxccColorNewEntity`, `DxccColorNewBand`, `DxccColorNewMode`, `DxccColorWorked`                                   |
| Signal History (sección)                                      | Encabezado de sección para los parámetros ajustables de Signal History en la columna derecha debajo del divisor.                                                             | —                                                                                                                 |
| Marker Lifetime:                                              | Cuánto tiempo persiste un marcador de Signal History inactivo antes de ser eliminado (15-300 seg).                                                                           | `SHistoryLifetimeS`                                                                                               |
| QRM Gate:                                                     | Cuánto tiempo debe persistir una portadora estrecha o una señal de banda ancha antes de clasificarse como QRM (3-30 seg).                                                    | `SHistoryQrmGateS`                                                                                                |
| Edge Threshold:                                               | Umbral por encima del piso de ruido para la caminata por el borde de pendiente que refina el borde lateral de la portadora de S-History (1.0-10.0 dB).                       | `SHistorySoftEdgeDb`                                                                                              |
| Muestras de color de Signal History (Signals / QRM)           | Abre un selector de color para los marcadores de señales de voz (dorados) y los marcadores QRM (rojos).                                                                      | `SHistoryColorSignals`, `SHistoryColorQrm`                                                                        |
| Snap to Step:                                                 | Redondea el clic para sintonizar de S-History al múltiplo más cercano del tamaño de paso de la slice activa, ocultando el pequeño desplazamiento de la portadora.            | `SHistorySnapToStep`                                                                                              |

## Hacer doble clic en un avistamiento ahora reenvía sugerencias de modo

A partir de la v0.9.7, hacer doble clic en una fila de la pestaña **Spot List** sintoniza el receptor a la frecuencia del avistamiento y también cambia el modo del receptor para que coincida con el avistamiento. Por ejemplo, hacer doble clic en un avistamiento CW cambia el receptor a CW, y hacer doble clic en un avistamiento FT8 lo cambia al modo digital apropiado, en lugar de solo cambiar la frecuencia. El modo se resuelve a partir del comentario del avistamiento mediante la lógica `SpotModeResolver` compartida en todas las fuentes de avistamientos.

## Spot Lines

La pestaña **Display** ahora incluye una alternancia **Spot Lines:** (nueva en v0.9.7). Cuando está **Enabled** (el valor predeterminado), AetherSDR dibuja una línea vertical corta desde el trazo del espectro hasta cada etiqueta de avistamiento en el panadapter, lo que facilita ver exactamente a qué frecuencia corresponde un avistamiento. Ajústelo a **Disabled** durante concursos u otras sesiones de operación con alta densidad de avistamientos para reducir el desorden visual. Esto se guarda como `IsSpotsLinesEnabled`.

## Reporte de estación FreeDV Reporter

La pestaña **FreeDV** contiene una sección **Station Reporting** que permite a AetherSDR difundir la actividad de su estación al mapa público FreeDV Reporter en `qso.freedv.org` cuando el módem RADE está activo. Esta característica está protegida por compilación con `HAVE_WEBSOCKETS`; en Windows también requiere la protección interna `HAVE_RADE`.

### Controles

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **Enable FreeDV Reporter reporting when RADE is active** | Habilita el reporte de estación al mapa público FreeDV Reporter cuando el módem RADE está activo. La casilla de verificación se niega a habilitarse si el campo de indicativo o de cuadrícula se resuelve como vacío. | `FreeDvAutoReport` |
| **Callsign:** | Indicativo reportado al mapa FreeDV Reporter. Se vuelve de solo lectura cuando **Use radio** está marcado. | `FreeDvMyCallsign` |
| **Use radio** | Pre-rellena el campo de indicativo desde el indicativo configurado de la radio y bloquea el campo como solo lectura. Cuando el indicativo de la radio cambia (por ejemplo, en Radio Setup), el campo se actualiza automáticamente. | `FreeDvUseRadioCallsign` |
| **Grid Square:** | Cuadrícula Maidenhead reportada. Se vuelve de solo lectura cuando **Use GPS** está marcado. | `FreeDvMyGrid` |
| **Use GPS** | Pre-rellena el campo de cuadrícula desde el módulo GPS de la radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. | `FreeDvUseGpsGrid` |
| **Station Msg:** | Texto libre opcional que se muestra junto al indicativo en el mapa público FreeDV Reporter. | `FreeDvMyMessage` |

### Habilitar el reporte de estación

1. Haga clic en la pestaña **FreeDV** dentro de `Settings > SpotHub...`.
2. En el grupo **Station Reporting**, ingrese o confirme su **Callsign:**. Marque **Use radio** para obtenerlo automáticamente de la radio.
3. Ingrese o confirme su **Grid Square:**. En radios con hardware GPS, marque **Use GPS** para completarlo automáticamente.
4. Opcionalmente, complete **Station Msg:** con una nota de texto libre breve.
5. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si el indicativo o la cuadrícula se resuelven como un valor vacío, aparece un diálogo de advertencia y la casilla de verificación vuelve a desmarcarse. Complete el campo faltante e intente nuevamente.
   - Cuando se habilita, la configuración se guarda como `FreeDvAutoReport`.

> **Nota:** El mapa FreeDV Reporter es un recurso público compartido por la comunidad. AetherSDR bloquea la habilitación de esta característica si el indicativo o la cuadrícula están en blanco para evitar que valores provisionales como `N0CALL` o `AA00` aparezcan en el mapa.

## Cambio del modo predeterminado Auto

En la v0.9.5.1, la alternancia **Auto Mode:** en la pestaña **Display** predetermina a **Enabled** para instalaciones nuevas. La configuración se guarda como `SpotAutoSwitchMode`. Las instalaciones existentes donde el valor se haya guardado explícitamente no se ven afectadas.

## Consejos

- La **RBN Console** es de solo lectura y muestra las líneas telnet brutas a medida que llegan. Use la línea de comando **Send** debajo de ella para emitir comandos de filtro directamente al servidor RBN (ej., `set/skimmer` o comandos de filtro de banda compatibles con RBN).
- Use el botón **Startup Commands…** para automatizar la configuración al iniciar sesión. Por ejemplo, para establecer su nombre y ubicación en cada conexión, agregue `SET/NAME <su nombre>` y `SET/QTH <su ciudad>`.
- Si el panadapter se satura durante un concurso, reduzca **Rate Limit:** para disminuir la densidad de avistamientos sin desconectarse. También puede deshabilitar **Spot Lines:** en la pestaña **Display** para reducir aún más el desorden visual.
- Para cambiar cómo se ven los avistamientos en el panadapter (tamaño, posición, duración y apilamiento), consulte [Ajustar densidad, posición, tamaño de fuente y duración de los avistamientos](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md).
- Los avistamientos de RBN usan el color establecido por **Spot Color:** en la pestaña RBN. Para anular todos los colores de las fuentes de avistamientos con un solo color, use la alternancia **Override Colors:** en la pestaña **Display**.

## Solución de problemas

- **El botón Connect vuelve inmediatamente a Connect con un error en la consola** — El nombre de host o el puerto son incorrectos, o el servidor RBN es inalcanzable. Verifique `RbnHost` y `RbnPort` y compruebe su conexión de red.
- **No aparecen avistamientos en el panadapter después de conectarse** — Confirme que **Spots:** en la pestaña **Display** esté configurado en Enabled (`IsSpotsEnabled`). También verifique que la banda que está monitoreando no esté oculta en las casillas de verificación del filtro de banda de la pestaña **Spot List**.
- **El panadapter está inundado de avistamientos** — Reduzca **Rate Limit:** a un valor más bajo para limitar la tasa de avistamientos entrantes. Alternativamente, deshabilite **Spot Lines:** (`IsSpotsLinesEnabled`) en la pestaña **Display** para que las áreas densas de avistamientos sean más fáciles de leer sin reducir la cantidad de avistamientos mostrados.
- **Hacer doble clic en un avistamiento cambia la frecuencia pero no cambia el modo** — El comentario del avistamiento puede no contener un token de modo reconocible. El cambio de modo depende de que el comentario del avistamiento contenga una cadena de modo conocida (ej., `CW`, `FT8`, `SSB`). Si el avistador no incluyó un modo en el comentario, solo cambia la frecuencia.
- **La casilla de verificación FreeDV Reporter se desmarca inmediatamente** — Un indicativo o una cuadrícula
