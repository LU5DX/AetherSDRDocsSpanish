# Conéctese a la Reverse Beacon Network

La Reverse Beacon Network (RBN) proporciona avistamientos automatizados de CW, RTTY y skimmers digitales. Esta página muestra cómo configurar y conectar la fuente telnet de la RBN de AetherSDR para que los avistamientos de la RBN aparezcan en su panadapter.

## Antes de comenzar

- Conozca el nombre de host y el puerto del servidor telnet de la RBN (el servidor público es `telnet.reversebeacon.net`, puerto `7000` para skimmers CW).
- Conozca el indicativo que usará para iniciar sesión en la RBN.
- Los avistamientos solo aparecerán en el panadapter si la superposición maestra de avistamientos está habilitada (`IsSpotsEnabled` está en Enabled de forma predeterminada).

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **RBN**.
3. En el campo **Server:**, ingrese el nombre de host telnet de la RBN (ej., `telnet.reversebeacon.net`). Esto se conserva como `RbnHost`.
4. Establezca **Port:** en el puerto telnet para la fuente del skimmer que desee. Rango válido: 1–65535. Esto se conserva como `RbnPort`.
5. En el campo **Callsign:**, ingrese su indicativo. Esto se conserva como `RbnCallsign`.
6. Si la fuente de la RBN produce más avistamientos de los que necesita, establezca **Rate Limit:** para limitar la cantidad de avistamientos procesados por segundo. Esto se conserva como `RbnRateLimit`.
7. Haga clic en **Connect**. La etiqueta del botón cambia a **Disconnect** cuando se establece la sesión, y la **RBN Console** muestra el tráfico entrante.
8. Para que AetherSDR se conecte a la RBN automáticamente en cada inicio, habilite **Auto-connect on startup**. Esto se conserva como `RbnAutoConnect`.

## Qué hace cada control

| Control                                                       | Comportamiento                                                                                                                                                               | Clave de configuración                                                                                             |
|---------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| **Server:**                                                   | Nombre de host telnet de la RBN                                                                                                                                              | `RbnHost`                                                                                                          |
| **Port:**                                                     | Puerto telnet de la RBN                                                                                                                                                      | `RbnPort`                                                                                                          |
| **Callsign:**                                                 | Indicativo de inicio de sesión enviado a la RBN                                                                                                                              | `RbnCallsign`                                                                                                      |
| **Rate Limit:**                                               | Máximo de avistamientos RBN aceptados por segundo                                                                                                                            | `RbnRateLimit`                                                                                                     |
| **Connect / Disconnect**                                      | Activa/desactiva la sesión telnet de la RBN                                                                                                                                  | —                                                                                                                  |
| **Auto-connect on startup**                                   | Se conecta a la RBN automáticamente al inicio                                                                                                                                | `RbnAutoConnect`                                                                                                   |
| **RBN Console**                                               | Visualización de solo lectura del tráfico RBN en bruto                                                                                                                       | —                                                                                                                  |
| **Send**                                                      | Envía un comando escrito a la sesión de la RBN                                                                                                                               | —                                                                                                                  |
| **Spot Color:**                                               | Abre un selector de color para los avistamientos RBN en el panadapter                                                                                                        | `RbnSpotColor`                                                                                                     |
| **Spot Lines:**                                               | Dibuja líneas verticales desde el espectro hasta cada etiqueta de avistamiento. Deshabilitar durante concursos para reducir el desorden visual.                              | `IsSpotsLinesEnabled`                                                                                              |
| Total Spots:                                                  | Indicador en vivo de cuántos avistamientos se están rastreando actualmente en todas las fuentes. Se actualiza cuando se añaden o eliminan avistamientos. Se reinicia a 0 al presionar **Clear All Spots**. | —                                                                                                                  |
| Auto:                                                         | Cambia automáticamente el modo del slice al hacer clic en un avistamiento que incluya información de modo (ej., CW, FT8, RTTY).                                                | `SpotAutoSwitchMode`                                                                                               |
| Signals (Signal History)                                      | Marcadores dorados para señales de ancho de voz detectadas en el panadapter.                                                                                                 | `SHistoryMarkersEnabled`                                                                                           |
| QRM (Signal History)                                          | Marcadores rojos para portadoras persistentes e interferencias de banda ancha.                                                                                               | `SHistoryQrmEnabled`                                                                                               |
| Clear All                                                     | Limpia todos los avistamientos DX, la fuente de memoria, los marcadores de Signal History y los marcadores QRM del espectro.                                                   | —                                                                                                                  |
| Override Colors:                                              | Fuerza un solo color de texto para todos los avistamientos. El botón siempre está etiquetado como **Enabled** y cambia al estado marcado/desmarcado.                           | `IsSpotsOverrideColorsEnabled`                                                                                     |
| Spot text color picker                                        | Abre QColorDialog para seleccionar el color del texto de los avistamientos.                                                                                                   | `SpotsOverrideColor`                                                                                               |
| Override Background: Enabled                                  | Habilita un color de fondo personalizado para los avistamientos.                                                                                                             | `IsSpotsOverrideBackgroundColorsEnabled`                                                                           |
| Override Background: Auto                                     | Selecciona automáticamente el color de fondo para contraste.                                                                                                                 | `IsSpotsOverrideToAutoBackgroundColorEnabled`                                                                      |
| Spot background color picker                                  | Abre QColorDialog para el color de fondo de los avistamientos.                                                                                                               | `SpotsOverrideBgColor`                                                                                             |
| Background Opacity:                                           | Opacidad del color de fondo de los avistamientos (0-100).                                                                                                                    | `SpotsBackgroundOpacity`                                                                                           |
| DXCC Coloring (sección)                                       | Encabezado de sección para los controles de coloración DXCC en la columna izquierda debajo del divisor.                                                                      | —                                                                                                                  |
| DXCC Colors:                                                  | Colorea los avistamientos según el estado DXCC trabajado/confirmado/necesario. El botón siempre está etiquetado como **Enabled**.                                              | `IsDxccColoringEnabled`                                                                                            |
| Log File (ADIF):                                              | Carga un archivo de registro ADIF para impulsar la coloración DXCC. Supervisa automáticamente los cambios del archivo después de la selección.                                | `DxccAdifFilePath`                                                                                                 |
| Imported: (estadísticas DXCC)                                 | Muestra el conteo de QSO y el conteo de entidades cuando se carga un registro.                                                                                               | —                                                                                                                  |
| Muestras de color DXCC (New DXCC / New Band / New Mode / Worked) | Abre un selector de color para cada categoría de estado DXCC.                                                                                                               | `DxccColorNewEntity`, `DxccColorNewBand`, `DxccColorNewMode`, `DxccColorWorked`                                    |
| Signal History (sección)                                      | Encabezado de sección para los parámetros ajustables de Signal History en la columna derecha debajo del divisor.                                                             | —                                                                                                                  |
| Marker Lifetime:                                              | Cuánto tiempo persiste un marcador de Signal History inactivo antes de ser eliminado (15-300 seg).                                                                            | `SHistoryLifetimeS`                                                                                                |
| QRM Gate:                                                     | Cuánto tiempo debe persistir una portadora estrecha o una señal de banda ancha antes de clasificarse como QRM (3-30 seg).                                                   | `SHistoryQrmGateS`                                                                                                 |
| Edge Threshold:                                               | Umbral por encima del piso de ruido para el recorrido del borde de pendiente que refina el borde lateral de la portadora de S-History (1.0-10.0 dB).                          | `SHistorySoftEdgeDb`                                                                                               |
| Muestras de color de Signal History (Signals / QRM)           | Abre un selector de color para los marcadores de señales de voz (dorados) y los marcadores QRM (rojos).                                                                       | `SHistoryColorSignals`, `SHistoryColorQrm`                                                                         |
| Snap to Step:                                                 | Redondea el clic para sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de portadora. El botón siempre está etiquetado como **Enabled**. | `SHistorySnapToStep`                                                                                               |

## Hacer doble clic en un avistamiento ahora envía sugerencias de modo

A partir de v0.9.7, hacer doble clic en una fila de la pestaña **Spot List** sintoniza el receptor a la frecuencia del avistamiento y también cambia el modo del receptor para que coincida con el avistamiento. Por ejemplo, hacer doble clic en un avistamiento CW cambia el receptor a CW, y hacer doble clic en un avistamiento FT8 lo cambia al modo digital apropiado, en lugar de solo cambiar la frecuencia. El modo se resuelve a partir del comentario del avistamiento mediante la lógica `SpotModeResolver` compartida entre todas las fuentes de avistamientos.

## Spot Lines

La pestaña **Display** ahora incluye una alternancia **Spot Lines:** (nuevo en v0.9.7). Cuando está **Enabled** (predeterminado), AetherSDR dibuja una línea vertical corta desde la traza del espectro hasta cada etiqueta de avistamiento en el panadapter, lo que facilita ver exactamente a qué frecuencia corresponde un avistamiento. Ajústelo a **Disabled** durante concursos u otras sesiones de operación con alta densidad de avistamientos para reducir el desorden visual. Esto se conserva como `IsSpotsLinesEnabled`.

## Etiquetas de botones de alternancia simplificadas

En v26.6.3, los botones de alternancia **Override Colors:**, **DXCC Colors:**, **Spot Lines:** y **Snap to Step:** en la pestaña **Display** ya no cambian su texto entre **Enabled** y **Disabled** al hacer clic. En su lugar, el botón siempre muestra su etiqueta predeterminada (ej., **Enabled**) y usa su estado visual marcado/desmarcado (presionado o elevado) para indicar la configuración actual. Esto se aplica a:

- **Override Colors:** (configuración `IsSpotsOverrideColorsEnabled`)
- **Spot Lines:** (configuración `IsSpotsLinesEnabled`)
- **DXCC Colors:** (configuración `IsDxccColoringEnabled`)
- **Snap to Step:** (configuración `SHistorySnapToStep`)

Todos los demás botones de alternancia en el diálogo de SpotHub continúan mostrando texto que refleja su estado de activado/desactivado.

## Estilo con reconocimiento de tema

A partir de v26.6.1, el diálogo de SpotHub utiliza estilo con reconocimiento de tema. Las etiquetas de estado y los colores de las pestañas ahora respetan el tema seleccionado, usando tokens de color semánticos como `{{color.accent}}`, `{{color.text.label}}` y `{{color.accent.danger}}` en lugar de valores hexadecimales codificados. Esto significa que los indicadores de estado (Connected, Disconnected, Error) ajustan automáticamente sus colores cuando cambia de tema.

## Cambio del valor predeterminado de Auto Mode

En v0.9.5.1, la alternancia **Auto Mode:** en la pestaña **Display** tiene como valor predeterminado **Enabled** para instalaciones nuevas. La configuración se conserva como `SpotAutoSwitchMode`. Las instalaciones existentes donde el valor se haya guardado explícitamente no se ven afectadas.

## Consejos

- La **RBN Console** es de solo lectura y muestra líneas telnet en bruto a medida que llegan. Use la línea de comandos **Send** debajo de ella para enviar comandos de filtro directamente al servidor RBN (ej., `set/skimmer` o comandos de filtro de banda compatibles con la RBN).
- Si el panadapter se satura durante un concurso, reduzca **Rate Limit:** para disminuir la densidad de avistamientos sin desconectarse. También puede deshabilitar **Spot Lines:** en la pestaña **Display** para reducir aún más el desorden visual.
- Para cambiar el aspecto de los avistamientos en el panadapter (tamaño, posición, duración y apilamiento), consulte [Tune spot density, position, font size and lifetime](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md).
- Los avistamientos RBN usan el color establecido por **Spot Color:** en la pestaña RBN. Para sobrescribir todos los colores de las fuentes de avistamientos con un solo color, use la alternancia **Override Colors:** en la pestaña **Display**.

## Solución de problemas

- **El botón Connect vuelve a Connect inmediatamente con un error en la consola** — El nombre de host o el puerto son incorrectos, o el servidor RBN es inalcanzable. Verifique `RbnHost` y `RbnPort` y compruebe su conexión de red.
- **No aparecen avistamientos en el panadapter después de conectarse** — Confirme que **Spots:** en la pestaña **Display** esté en Enabled (`IsSpotsEnabled`). También verifique que la banda que está monitoreando no esté oculta en las casillas de verificación del filtro de banda de la pestaña **Spot List**.
- **El panadapter está inundado de avistamientos** — Reduzca **Rate Limit:** a un valor más bajo para limitar la tasa de avistamientos entrantes. Alternativamente, deshabilite **Spot Lines:** (`IsSpotsLinesEnabled`) en la pestaña **Display** para que las áreas densas de avistamientos sean más fáciles de leer sin reducir la cantidad de avistamientos mostrados.
- **Hacer doble clic en un avistamiento cambia la frecuencia pero no el modo** — El comentario del avistamiento puede no contener un token de modo reconocible. El cambio de modo depende de que el comentario del avistamiento contenga una cadena de modo conocida (ej., `CW`, `FT8`, `SSB`). Si el informante no incluyó un modo en el comentario, solo cambia la frecuencia.
- **Los botones de alternancia no muestran el cambio de texto Enabled/Disabled** — Este es un comportamiento esperado a partir de v26.6.3. Los botones **Override Colors:**, **Spot Lines:**, **DXCC Colors:** y **Snap to Step:** siempre muestran **Enabled** independientemente del estado. Su estado visual marcado/desmarcado indica si la función está activa.
