# Conectarse a la Red de Balizas Inversa

La Red de Balizas Inversa (RBN, por sus siglas en inglés) proporciona avisos automáticos de CW, RTTY y skimmers digitales. Esta página muestra cómo configurar y conectar el feed telnet de RBN de AetherSDR para que los avisos de RBN aparezcan en su panadapter.

## Antes de comenzar

- Conozca el nombre de host y el puerto del servidor telnet de RBN (el servidor público es `telnet.reversebeacon.net`, puerto `7000` para skimmers de CW).
- Conozca el indicativo que utilizará para iniciar sesión en RBN.
- Los avisos solo aparecerán en el panadapter si la superposición maestra de avisos está habilitada (`IsSpotsEnabled` está en Enabled por defecto).

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **RBN**.
3. En el campo **Server:**, ingrese el nombre de host telnet de RBN (p. ej., `telnet.reversebeacon.net`). Esto se guarda como `RbnHost`.
4. Establezca **Port:** al puerto telnet del feed de skimmer que desee. Rango válido: 1–65535. Esto se guarda como `RbnPort`.
5. En el campo **Callsign:**, ingrese su indicativo. Esto se guarda como `RbnCallsign`.
6. Si el feed de RBN produce más avisos de los que necesita, establezca **Rate Limit:** para limitar la cantidad de avisos procesados por segundo. Esto se guarda como `RbnRateLimit`.
7. Haga clic en **Connect**. La etiqueta del botón cambia a **Disconnect** cuando la sesión se establece, y la **RBN Console** muestra el tráfico entrante.
8. Para que AetherSDR se conecte a RBN automáticamente en cada inicio, habilite **Auto-connect on startup**. Esto se guarda como `RbnAutoConnect`.

## Qué hace cada control

| Control                                                       | Comportamiento                                                                                                                                                         | Clave de ajuste                                                                                                      |
|---------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| **Server:**                                                   | Nombre de host telnet de RBN                                                                                                                                           | `RbnHost`                                                                                                          |
| **Port:**                                                     | Puerto telnet de RBN                                                                                                                                                   | `RbnPort`                                                                                                          |
| **Callsign:**                                                 | Indicativo de inicio de sesión enviado a RBN                                                                                                                            | `RbnCallsign`                                                                                                      |
| **Rate Limit:**                                               | Máximo de avisos de RBN aceptados por segundo                                                                                                                          | `RbnRateLimit`                                                                                                     |
| **Connect / Disconnect**                                      | Alterna la sesión telnet de RBN                                                                                                                                        | —                                                                                                                  |
| **Auto-connect on startup**                                   | Se conecta a RBN automáticamente al iniciar                                                                                                                            | `RbnAutoConnect`                                                                                                   |
| **RBN Console**                                               | Pantalla de solo lectura del tráfico RBN bruto                                                                                                                         | —                                                                                                                  |
| **Send**                                                      | Envía un comando escrito a la sesión de RBN                                                                                                                            | —                                                                                                                  |
| **Spot Color:**                                               | Abre un selector de color para los avisos de RBN en el panadapter                                                                                                      | `RbnSpotColor`                                                                                                     |
| **Spot Lines:**                                               | Dibuja líneas verticales desde el espectro hasta cada etiqueta de aviso. Desactívelas durante concursos para reducir el desorden visual.                               | `IsSpotsLinesEnabled`                                                                                              |
| Total Spots:                                                  | Lectura en vivo de cuántos avisos se están rastreando actualmente en todas las fuentes. Se actualiza cuando se agregan o eliminan avisos. Se restablece a 0 al presionar **Clear All Spots**. | —                                                                                                                  |
| Auto:                                                         | Cambia automáticamente el modo del slice al hacer clic en un aviso que incluya información de modo (p. ej., CW, FT8, RTTY).                                            | `SpotAutoSwitchMode`                                                                                               |
| Signals (Signal History)                                      | Marcadores dorados para señales detectadas de ancho de voz en el panadapter.                                                                                           | `SHistoryMarkersEnabled`                                                                                           |
| QRM (Signal History)                                          | Marcadores rojos para portadoras persistentes e interferencia de banda ancha.                                                                                          | `SHistoryQrmEnabled`                                                                                               |
| Clear All                                                     | Borra todos los avisos de DX, el feed de memoria, los marcadores de Signal History y los marcadores de QRM del espectro.                                               | —                                                                                                                  |
| Override Colors:                                              | Fuerza un único color de texto para todos los avisos. El botón siempre muestra la etiqueta **Enabled** y cambia su estado marcado/no marcado.                           | `IsSpotsOverrideColorsEnabled`                                                                                     |
| Selector de color de texto de avisos                          | Abre QColorDialog para elegir el color del texto de los avisos.                                                                                                        | `SpotsOverrideColor`                                                                                               |
| Override Background: Enabled                                  | Habilita un color de fondo personalizado para los avisos.                                                                                                              | `IsSpotsOverrideBackgroundColorsEnabled`                                                                           |
| Override Background: Auto                                     | Selecciona automáticamente el color de fondo para contraste.                                                                                                           | `IsSpotsOverrideToAutoBackgroundColorEnabled`                                                                      |
| Selector de color de fondo de avisos                          | Abre QColorDialog para el color de fondo de los avisos.                                                                                                                | `SpotsOverrideBgColor`                                                                                             |
| Background Opacity:                                           | Opacidad del color de fondo de los avisos (0-100).                                                                                                                     | `SpotsBackgroundOpacity`                                                                                           |
| DXCC Coloring (sección)                                       | Encabezado de sección para los controles de coloración DXCC en la columna izquierda debajo del divisor.                                                               | —                                                                                                                  |
| DXCC Colors:                                                  | Colorea los avisos según el estado DXCC trabajado/confirmado/necesario. El botón siempre muestra la etiqueta **Enabled**.                                              | `IsDxccColoringEnabled`                                                                                            |
| Log File (ADIF):                                              | Carga un archivo de registro ADIF para impulsar la coloración DXCC. Supervisa automáticamente el archivo para detectar cambios después de la selección.                | `DxccAdifFilePath`                                                                                                 |
| Imported: (estadísticas DXCC)                                 | Muestra el conteo de QSO y el conteo de entidades cuando se carga un registro.                                                                                         | —                                                                                                                  |
| Muestras de color DXCC (New DXCC / New Band / New Mode / Worked) | Abre un selector de color para cada categoría de estado DXCC.                                                                                                          | `DxccColorNewEntity`, `DxccColorNewBand`, `DxccColorNewMode`, `DxccColorWorked`                                    |
| Signal History (sección)                                      | Encabezado de sección para los parámetros ajustables de Signal History en la columna derecha debajo del divisor.                                                      | —                                                                                                                  |
| Marker Lifetime:                                              | Cuánto tiempo persiste un marcador de Signal History inactivo antes de eliminarse (15-300 seg).                                                                        | `SHistoryLifetimeS`                                                                                                |
| QRM Gate:                                                     | Cuánto tiempo debe persistir una portadora estrecha o señal de banda ancha antes de clasificarse como QRM (3-30 seg).                                                  | `SHistoryQrmGateS`                                                                                                 |
| Edge Threshold:                                               | Umbral sobre el piso de ruido para el recorrido de borde de pendiente que refina el borde del lado de la portadora de S-History (1.0-10.0 dB).                          | `SHistorySoftEdgeDb`                                                                                               |
| Muestras de color de Signal History (Signals / QRM)           | Abre un selector de color para los marcadores de señal de voz (dorados) y los marcadores de QRM (rojos).                                                               | `SHistoryColorSignals`, `SHistoryColorQrm`                                                                         |
| Snap to Step:                                                 | Redondea el clic-para-sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de portadora. El botón siempre muestra la etiqueta **Enabled**. | `SHistorySnapToStep`                                                                                               |
| Bands:                                                        | Casillas de verificación por banda para alternar la visibilidad de avisos en la tabla de la lista de avisos. Se envuelven en un diseño de flujo para seguir siendo legibles cuando SpotHub es estrecho. | —                                                                                                                  |
| Clear                                                         | Vacía la lista de avisos actual.                                                                                                                                       | —                                                                                                                  |
| Tabla de avisos                                               | Tabla de avisos ordenable. Haga doble clic en una fila para sintonizar. Columnas: Time, Freq, DX Call, Comment, Spotter, Band, Mode, Source.                            | —                                                                                                                  |

## Doble clic en un aviso ahora reenvía indicaciones de modo

A partir de v0.9.7, hacer doble clic en una fila de la pestaña **Spot List** sintoniza el receptor a la frecuencia del aviso y también cambia el modo del receptor para que coincida con el aviso. Por ejemplo, hacer doble clic en un aviso de CW cambia el receptor a CW, y hacer doble clic en un aviso de FT8 lo cambia al modo digital apropiado, en lugar de solo cambiar la frecuencia. El modo se resuelve a partir del comentario del aviso mediante la lógica `SpotModeResolver` compartida en todas las fuentes de avisos.

## Spot Lines

La pestaña **Display** ahora incluye un conmutador **Spot Lines:** (nuevo en v0.9.7). Cuando está **Enabled** (el valor predeterminado), AetherSDR dibuja una línea vertical corta desde la traza del espectro hasta cada etiqueta de aviso en el panadapter, lo que facilita ver exactamente a qué frecuencia corresponde un aviso. Configúrelo en **Disabled** durante concursos u otras sesiones de operación con alta densidad de avisos para reducir el desorden visual. Esto se guarda como `IsSpotsLinesEnabled`.

## Etiquetas de botones de alternancia simplificadas

En v26.6.3, los botones de alternancia **Override Colors:**, **DXCC Colors:**, **Spot Lines:** y **Snap to Step:** en la pestaña **Display** ya no cambian su texto entre **Enabled** y **Disabled** al hacer clic. En su lugar, el botón siempre muestra su etiqueta predeterminada (p. ej., **Enabled**) y usa su estado visual marcado/no marcado (presionado o elevado) para indicar el ajuste actual. Esto se aplica a:

- **Override Colors:** (ajuste `IsSpotsOverrideColorsEnabled`)
- **Spot Lines:** (ajuste `IsSpotsLinesEnabled`)
- **DXCC Colors:** (ajuste `IsDxccColoringEnabled`)
- **Snap to Step:** (ajuste `SHistorySnapToStep`)

Todos los demás botones de alternancia en el diálogo SpotHub continúan mostrando texto que refleja su estado de activado/desactivado.

## Estilo consciente del tema

A partir de v26.6.1, el diálogo SpotHub utiliza un estilo consciente del tema. Las etiquetas de estado y los colores de la pestaña ahora respetan el tema seleccionado, utilizando tokens de color semánticos como `{{color.accent}}`, `{{color.text.label}}` y `{{color.accent.danger}}` en lugar de valores hexadecimales codificados. Esto significa que los indicadores de estado (Connected, Disconnected, Error) ajustan automáticamente sus colores cuando cambia de tema.

## Cambio predeterminado de Auto Mode

En v0.9.5.1, el conmutador **Auto Mode:** en la pestaña **Display** está en **Enabled** por defecto para instalaciones nuevas. El ajuste se guarda como `SpotAutoSwitchMode`. Las instalaciones existentes donde el valor se haya guardado explícitamente no se ven afectadas.

## Mejoras en la pestaña Spot List (v26.7.4)

La pestaña **Spot List** utiliza un diseño de flujo para sus casillas de verificación de filtro de banda. Esto evita que las casillas se compriman hasta quedar ilegibles cuando el diálogo SpotHub es estrecho. Las casillas se envuelven a una nueva fila cuando se agota el espacio horizontal, manteniendo legible el estado marcado.

Las columnas de la **Spot table** se pueden mostrar u ocultar haciendo clic derecho en el encabezado de la tabla y marcando o desmarcando los nombres de las columnas. El menú permanece abierto mientras alterna varias casillas, para que pueda ajustar varias columnas de una sola vez en lugar de reabrir el menú por cada columna.

El ancho mínimo del diálogo SpotHub se ha reducido a 360 píxeles, lo que permite reducir el tamaño del diálogo una vez que se ocultan columnas en la tabla de la lista de avisos.

## Ordenamiento de la lista de avisos por Time (v26.8.4)

A partir de v26.8.4, hacer clic en el encabezado de la columna **Time** en la **Spot table** ordena los avisos por su marca de tiempo UTC. Anteriormente, la columna Time no tenía un valor ordenable, por lo que hacer clic en ella no hacía nada — y una vez que ordenaba por **Freq**, no había forma de volver al orden predeterminado de más reciente primero. Ahora siempre puede restaurar la vista de más reciente primero haciendo clic en **Time**. Los avisos se ordenan por su tiempo UTC real, no por el texto mostrado, por lo que las entradas de diferentes fuentes permanecen correctamente ordenadas incluso cuando usan formatos de hora ligeramente diferentes.

## Consejos

- La **RBN Console** es de solo lectura y muestra las líneas telnet brutas a medida que llegan. Use la línea de comando **Send** debajo de ella para emitir comandos de filtro directamente al servidor RBN (p. ej., `set/skimmer` o comandos de filtro de banda compatibles con RBN).
- Si el panadapter se satura durante un concurso, reduzca **Rate Limit:** para disminuir la densidad de avisos sin desconectarse. También puede deshabilitar **Spot Lines:** en la pestaña **Display** para reducir aún más el desorden visual.
- Para cambiar cómo se ven los avisos en el panadapter — tamaño, posición, duración y apilamiento — consulte [Ajustar densidad, posición, tamaño de fuente y duración de los avisos](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md).
- Los avisos de RBN usan el color establecido por **Spot Color:** en la pestaña RBN. Para sobrescribir todos los colores de las fuentes de avisos con un solo color, use el conmutador **Override Colors:** en la pestaña **Display**.

## Solución de problemas

- **El botón Connect vuelve a Connect inmediatamente con un error en la consola** — El nombre de host o el puerto son incorrectos, o el servidor RBN es inalcanzable. Verifique `RbnHost` y `RbnPort` y revise su conexión de red.
- **No aparecen avisos en el panadapter después de conectarse** — Confirme que **Spots:** en la pestaña **Display** esté en Enabled (`IsSpotsEnabled`). También verifique que la banda que está monitoreando no esté oculta en las casillas de filtro de banda de la pestaña **Spot List**.
- **El panadapter está inundado de avisos** — Reduzca **Rate Limit:** a un valor más bajo para limitar la tasa de avisos entrantes. Alternativamente, deshabilite **Spot Lines:** (`IsSpotsLinesEnabled`) en la pestaña **Display** para que las áreas con avisos densos sean más fáciles de leer sin reducir el número de avisos mostrados.
- **Hacer doble clic en un aviso cambia la frecuencia pero no cambia el modo** — El comentario del aviso puede no contener un token de modo reconocible. El cambio de modo depende de que el comentario del aviso contenga una cadena de modo conocida (p. ej., `CW`, `FT8`, `SSB`). Si el spotter no incluyó un modo en el comentario, solo cambiará la frecuencia.
- **Los botones de alternancia no muestran el cambio de texto Enabled/Disabled** — Este es el comportamiento esperado a partir de v26.6.3. Los botones **Override Colors:**, **Spot Lines:**, **DXCC Colors:**
