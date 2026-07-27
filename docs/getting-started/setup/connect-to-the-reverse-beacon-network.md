# Conectarse a la Reverse Beacon Network

La Reverse Beacon Network (RBN) proporciona spots automatizados de skimmers CW, RTTY y digitales. Esta página muestra cómo configurar y conectar el feed telnet de la RBN en AetherSDR para que los spots de la RBN aparezcan en su panadapter.

## Antes de comenzar

- Conozca el nombre de host y el puerto del servidor telnet de la RBN (el servidor público es `telnet.reversebeacon.net`, puerto `7000` para skimmers CW).
- Conozca el indicativo que usará para iniciar sesión en la RBN.
- Los spots solo aparecerán en el panadapter si la superposición maestra de spots está habilitada (`IsSpotsEnabled` tiene el valor predeterminado Enabled).

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **RBN**.
3. En el campo **Server:**, ingrese el nombre de host telnet de la RBN (ej., `telnet.reversebeacon.net`). Este valor se conserva como `RbnHost`.
4. Establezca **Port:** en el puerto telnet del feed de skimmer que desee. Rango válido: 1–65535. Este valor se conserva como `RbnPort`.
5. En el campo **Callsign:**, ingrese su indicativo. Este valor se conserva como `RbnCallsign`.
6. Si el feed de la RBN produce más spots de los que necesita, ajuste **Rate Limit:** para limitar la cantidad de spots procesados por segundo. Este valor se conserva como `RbnRateLimit`.
7. Haga clic en **Connect**. La etiqueta del botón cambia a **Disconnect** cuando se establece la sesión, y la **RBN Console** muestra el tráfico entrante.
8. Para que AetherSDR se conecte a la RBN automáticamente en cada inicio, active **Auto-connect on startup**. Este valor se conserva como `RbnAutoConnect`.

## Qué hace cada control

| Control                                                       | Comportamiento                                                                                                                                                         | Clave de configuración                                                                                              |
|---------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| **Server:**                                                   | Nombre de host telnet de la RBN                                                                                                                                        | `RbnHost`                                                                                                           |
| **Port:**                                                     | Puerto telnet de la RBN                                                                                                                                                | `RbnPort`                                                                                                           |
| **Callsign:**                                                 | Indicativo de inicio de sesión enviado a la RBN                                                                                                                        | `RbnCallsign`                                                                                                       |
| **Rate Limit:**                                               | Máximo de spots de la RBN aceptados por segundo                                                                                                                        | `RbnRateLimit`                                                                                                      |
| **Connect / Disconnect**                                      | Activa o desactiva la sesión telnet de la RBN                                                                                                                          | —                                                                                                                   |
| **Auto-connect on startup**                                   | Se conecta a la RBN automáticamente al iniciar                                                                                                                         | `RbnAutoConnect`                                                                                                    |
| **RBN Console**                                               | Visualización de solo lectura del tráfico sin procesar de la RBN                                                                                                       | —                                                                                                                   |
| **Send**                                                      | Envía un comando escrito a la sesión de la RBN                                                                                                                         | —                                                                                                                   |
| **Spot Color:**                                               | Abre un selector de color para los spots de la RBN en el panadapter                                                                                                    | `RbnSpotColor`                                                                                                      |
| **Spot Lines:**                                               | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Desactívelo durante concursos para reducir el desorden visual.                                 | `IsSpotsLinesEnabled`                                                                                               |
| Total Spots:                                                  | Indicador en vivo de cuántos spots se están rastreando actualmente en todas las fuentes. Se actualiza cuando se añaden o borran spots. Se reinicia a 0 al pulsar **Clear All Spots**. | —                                                                                                                   |
| Auto:                                                         | Cambia automáticamente el modo del slice al hacer clic en un spot que incluya información de modo (ej., CW, FT8, RTTY).                                                | `SpotAutoSwitchMode`                                                                                                |
| Signals (Signal History)                                      | Marcadores dorados para señales de ancho de voz detectadas en el panadapter.                                                                                           | `SHistoryMarkersEnabled`                                                                                            |
| QRM (Signal History)                                          | Marcadores rojos para portadoras persistentes e interferencia de banda ancha.                                                                                          | `SHistoryQrmEnabled`                                                                                                |
| Clear All                                                     | Borra todos los spots DX, el feed de memoria, los marcadores de Signal History y los marcadores QRM del espectro.                                                      | —                                                                                                                   |
| Override Colors:                                              | Fuerza un solo color de texto para todos los spots. El botón siempre muestra la etiqueta **Enabled** y cambia su estado visual marcado/desmarcado.                     | `IsSpotsOverrideColorsEnabled`                                                                                      |
| Spot text color picker                                        | Abre un QColorDialog para elegir el color del texto del spot.                                                                                                          | `SpotsOverrideColor`                                                                                                |
| Override Background: Enabled                                  | Activa un color de fondo personalizado para los spots.                                                                                                                 | `IsSpotsOverrideBackgroundColorsEnabled`                                                                            |
| Override Background: Auto                                     | Selecciona automáticamente el color de fondo para contraste.                                                                                                           | `IsSpotsOverrideToAutoBackgroundColorEnabled`                                                                       |
| Spot background color picker                                  | Abre un QColorDialog para el color de fondo del spot.                                                                                                                  | `SpotsOverrideBgColor`                                                                                              |
| Background Opacity:                                           | Opacidad del color de fondo del spot (0-100).                                                                                                                          | `SpotsBackgroundOpacity`                                                                                            |
| DXCC Coloring (sección)                                       | Encabezado de sección para los controles de coloración DXCC en la columna izquierda debajo del divisor.                                                               | —                                                                                                                   |
| DXCC Colors:                                                  | Colorea los spots según el estado DXCC trabajado/confirmado/necesitado. El botón siempre muestra la etiqueta **Enabled**.                                              | `IsDxccColoringEnabled`                                                                                             |
| Log File (ADIF):                                              | Carga un archivo de registro ADIF para impulsar la coloración DXCC. Vigila automáticamente los cambios del archivo tras la selección.                                 | `DxccAdifFilePath`                                                                                                  |
| Imported: (estadísticas DXCC)                                 | Muestra el recuento de QSO y el recuento de entidades cuando se carga un registro.                                                                                     | —                                                                                                                   |
| Muestras de color DXCC (New DXCC / New Band / New Mode / Worked) | Abre un selector de color para cada categoría de estado DXCC.                                                                                                        | `DxccColorNewEntity`, `DxccColorNewBand`, `DxccColorNewMode`, `DxccColorWorked`                                     |
| Signal History (sección)                                      | Encabezado de sección para los parámetros ajustables de Signal History en la columna derecha debajo del divisor.                                                       | —                                                                                                                   |
| Marker Lifetime:                                              | Tiempo que persiste un marcador de Signal History inactivo antes de eliminarse (15-300 seg).                                                                           | `SHistoryLifetimeS`                                                                                                 |
| QRM Gate:                                                     | Tiempo que debe persistir una portadora estrecha o una señal de banda ancha antes de clasificarse como QRM (3-30 seg).                                                 | `SHistoryQrmGateS`                                                                                                  |
| Edge Threshold:                                               | Umbral por encima del piso de ruido para la búsqueda del borde de pendiente que refina el borde del lado de la portadora de S-History (1.0-10.0 dB).                   | `SHistorySoftEdgeDb`                                                                                                |
| Muestras de color Signal History (Signals / QRM)             | Abre un selector de color para los marcadores de señal de voz (dorados) y los marcadores QRM (rojos).                                                                 | `SHistoryColorSignals`, `SHistoryColorQrm`                                                                          |
| Snap to Step:                                                 | Redondea el clic-sintonización de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de portadora. El botón siempre muestra la etiqueta **Enabled**. | `SHistorySnapToStep`                                                                                                |
| Bands:                                                        | Casillas de verificación por banda para alternar la visibilidad de los spots en la tabla de Spot List. Dispuestas en un diseño de flujo para mantenerse legibles cuando SpotHub es estrecho. | —                                                                                                                   |
| Clear                                                         | Vacía la lista de spots actual.                                                                                                                                        | —                                                                                                                   |
| Spot table                                                    | Tabla ordenable de spots. Haga doble clic en una fila para sintonizar. Columnas: Time, Freq, DX Call, Comment, Spotter, Band, Mode, Source.                            | —                                                                                                                   |

## Hacer doble clic en un spot ahora envía sugerencias de modo

A partir de v0.9.7, hacer doble clic en una fila de la pestaña **Spot List** sintoniza el receptor a la frecuencia del spot y también cambia el modo del receptor para que coincida con el spot. Por ejemplo, hacer doble clic en un spot CW cambia el receptor a CW, y hacer doble clic en un spot FT8 lo cambia al modo digital apropiado, en lugar de solo cambiar la frecuencia. El modo se resuelve a partir del comentario del spot mediante la lógica `SpotModeResolver` compartida en todas las fuentes de spots.

## Spot Lines

La pestaña **Display** ahora incluye una alternancia **Spot Lines:** (nueva en v0.9.7). Cuando está **Enabled** (el valor predeterminado), AetherSDR dibuja una línea vertical corta desde la traza del espectro hasta cada etiqueta de spot en el panadapter, facilitando la visualización de la frecuencia exacta a la que corresponde un spot. Ajústelo a **Disabled** durante concursos u otras sesiones de operación con alta densidad de spots para reducir el desorden visual. Este valor se conserva como `IsSpotsLinesEnabled`.

## Etiquetas de botones de alternancia simplificadas

En v26.6.3, los botones de alternancia **Override Colors:**, **DXCC Colors:**, **Spot Lines:** y **Snap to Step:** en la pestaña **Display** ya no cambian su texto entre **Enabled** y **Disabled** al hacer clic. En su lugar, el botón siempre muestra su etiqueta predeterminada (ej., **Enabled**) y utiliza su estado visual marcado/desmarcado (presionado o elevado) para indicar la configuración actual. Esto aplica a:

- **Override Colors:** (configuración `IsSpotsOverrideColorsEnabled`)
- **Spot Lines:** (configuración `IsSpotsLinesEnabled`)
- **DXCC Colors:** (configuración `IsDxccColoringEnabled`)
- **Snap to Step:** (configuración `SHistorySnapToStep`)

Todos los demás botones de alternancia en el diálogo SpotHub continúan mostrando texto que refleja su estado activado/desactivado.

## Estilo adaptable al tema

A partir de v26.6.1, el diálogo SpotHub utiliza estilo adaptable al tema. Las etiquetas de estado y los colores de las pestañas ahora respetan el tema seleccionado, utilizando tokens de color semánticos como `{{color.accent}}`, `{{color.text.label}}` y `{{color.accent.danger}}` en lugar de valores hexadecimales fijos. Esto significa que los indicadores de estado (Connected, Disconnected, Error) ajustan automáticamente sus colores cuando cambia de tema.

## Cambio en el valor predeterminado de Auto Mode

En v0.9.5.1, la alternancia **Auto Mode:** en la pestaña **Display** tiene el valor predeterminado **Enabled** para instalaciones nuevas. La configuración se conserva como `SpotAutoSwitchMode`. Las instalaciones existentes donde el valor se haya guardado explícitamente no se ven afectadas.

## Mejoras en la pestaña Spot List (v26.7.4)

La pestaña **Spot List** utiliza un diseño de flujo para sus casillas de verificación de filtro de banda. Esto evita que las casillas de verificación se compriman hasta volverse ilegibles cuando el diálogo SpotHub es estrecho. Las casillas de verificación pasan a una nueva fila cuando se queda sin espacio horizontal, manteniendo legible el estado marcado.

Las columnas de la **Spot table** se pueden mostrar u ocultar haciendo clic derecho en el encabezado de la tabla y marcando o desmarcando los nombres de las columnas. El menú permanece abierto mientras alterna múltiples casillas de verificación, lo que le permite ajustar varias columnas de una sola vez en lugar de tener que volver a abrir el menú por cada columna.

El ancho mínimo del diálogo SpotHub se ha reducido a 360 píxeles, lo que permite redimensionar el diálogo a un tamaño más estrecho una vez que se ocultan columnas en la tabla Spot List.

## Consejos

- La **RBN Console** es de solo lectura y muestra las líneas telnet sin procesar a medida que llegan. Use la línea de comandos **Send** debajo de ella para enviar comandos de filtro directamente al servidor RBN (ej., `set/skimmer` o comandos de filtro de banda compatibles con la RBN).
- Si el panadapter se satura durante un concurso, reduzca **Rate Limit:** para disminuir la densidad de spots sin desconectarse. También puede desactivar **Spot Lines:** en la pestaña **Display** para reducir aún más el desorden visual.
- Para cambiar el aspecto de los spots en el panadapter (tamaño, posición, duración y apilamiento), consulte [Ajustar densidad, posición, tamaño de fuente y duración de los spots](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md).
- Los spots de la RBN usan el color establecido por **Spot Color:** en la pestaña RBN. Para sobrescribir todos los colores de las fuentes de spots con un solo color, use la alternancia **Override Colors:** en la pestaña **Display**.

## Solución de problemas

- **El botón Connect vuelve inmediatamente a Connect con un error en la consola** — El nombre de host o el puerto son incorrectos, o el servidor RBN es inalcanzable. Verifique `RbnHost` y `RbnPort` y compruebe su conexión de red.
- **No aparecen spots en el panadapter después de conectar** — Confirme que **Spots:** en la pestaña **Display** esté configurado en Enabled (`IsSpotsEnabled`). También verifique que la banda que está monitoreando no esté oculta en las casillas de verificación de filtro de banda de la pestaña **Spot List**.
- **El panadapter está inundado de spots** — Reduzca **Rate Limit:** a un valor más bajo para limitar la tasa de spots entrantes. Alternativamente, desactive **Spot Lines:** (`IsSpotsLinesEnabled`) en la pestaña **Display** para que las áreas densas de spots sean más fáciles de leer sin reducir la cantidad de spots mostrados.
- **Hacer doble clic en un spot cambia la frecuencia pero no cambia el modo** — El comentario del spot puede no contener un token de modo reconocible. El cambio de modo depende de que el comentario del spot contenga una cadena de modo conocida (ej., `CW`, `FT8`, `SSB`). Si el spotter no incluyó un modo en el comentario, solo cambiará la frecuencia.
- **Los botones de alternancia no muestran el cambio de texto Enabled/Disabled** — Este comportamiento es esperado a partir de v26.6.3. Los botones **Override Colors:**, **Spot Lines:**, **DXCC Colors:** y **Snap to Step:** siempre muestran **Enabled** independientemente del estado. Su estado visual marcado/desmarcado indica si la función está activa.
