# Iniciar el listener UDP de WSJT-X y filtrar por CQ, POTA o llamadas hacia mí

Configure AetherSDR para recibir transmisiones decodificadas de WSJT-X a través de UDP y mostrar solo las categorías de spots que le interesan — llamadas CQ, activaciones POTA o estaciones que llaman a su indicativo — como superposiciones en el panadapter.

## Antes de comenzar

- WSJT-X debe estar ejecutándose en la misma máquina o red y configurado para enviar mensajes de estado UDP a la dirección y puerto que usted establecerá aquí.
- Conozca la dirección UDP y el puerto al que WSJT-X está transmitiendo (revise WSJT-X en **File > Settings > Reporting**, sección UDP Server).
- Su indicativo debe estar configurado en WSJT-X para que el filtro "Calling Me" funcione.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **WSJT-X**.
3. En **Address:**, ingrese la dirección de enlace UDP en la que AetherSDR debe escuchar (se guarda como `WsjtxAddress`). Use `127.0.0.1` si WSJT-X se ejecuta en la misma máquina, o `0.0.0.0` para escuchar en todas las interfaces.
4. En **Port:**, ingrese el número de puerto UDP que coincida con el puerto configurado en WSJT-X (se guarda como `WsjtxPort`; rango válido 1–65535).
5. Haga clic en **Start**. El indicador de estado cambia a **Listening**.
6. Para iniciar el listener automáticamente cada vez que AetherSDR se lance, habilite **Auto-start on startup (WSJT-X)** (se guarda como `WsjtxAutoStart`).
7. En las casillas de verificación de filtros, habilite una o más de las siguientes opciones para restringir qué decodificaciones aparecen como spots en el panadapter:
   - **CQ** — muestra estaciones que envían una llamada CQ general (se guarda como `WsjtxFilterCQ`).
   - **CQ POTA** — muestra estaciones que envían CQ POTA (se guarda como `WsjtxFilterPOTA`).
   - **Calling Me** — muestra decodificaciones dirigidas a su indicativo (se guarda como `WsjtxFilterCallingMe`).
8. Opcionalmente, asigne un color distintivo a cada categoría haciendo clic en el botón de color correspondiente:
   - **CQ color** (se guarda como `WsjtxColorCQ`)
   - **POTA color** (se guarda como `WsjtxColorPOTA`)
   - **Calling Me color** (se guarda como `WsjtxColorCallingMe`)
   - **Default color** para decodificaciones que no pasan ningún filtro activo (se guarda como `WsjtxColorDefault`)
9. Establezca **Spot Life:** al número de segundos que un spot de WSJT-X debe permanecer visible en el panadapter (se guarda como `WsjtxSpotLife`).
10. Confirme que las transmisiones decodificadas están llegando a la consola **WSJT-X Decodes** en la parte inferior de la pestaña.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **Address:** | Dirección de enlace UDP para mensajes WSJT-X entrantes. | `WsjtxAddress` |
| **Port:** | Número de puerto UDP. Debe coincidir con el puerto de reporte de WSJT-X. | `WsjtxPort` |
| **Start / Stop** | Inicia o detiene el listener UDP. | — |
| **Auto-start on startup (WSJT-X)** | Inicia el listener automáticamente al abrir la aplicación. | `WsjtxAutoStart` |
| **CQ** | Pasa solo transmisiones CQ al panadapter. | `WsjtxFilterCQ` |
| **CQ POTA** | Pasa solo transmisiones CQ POTA. | `WsjtxFilterPOTA` |
| **Calling Me** | Pasa solo decodificaciones dirigidas a su indicativo. | `WsjtxFilterCallingMe` |
| **CQ color** | Color para spots CQ en el panadapter. | `WsjtxColorCQ` |
| **POTA color** | Color para spots CQ POTA. | `WsjtxColorPOTA` |
| **Calling Me color** | Color para spots que llaman a su indicativo. | `WsjtxColorCallingMe` |
| **Default color** | Color para spots que no coinciden con ningún filtro activo. | `WsjtxColorDefault` |
| **Spot Life:** | Segundos que un spot de WSJT-X permanece en el panadapter antes de desvanecerse. | `WsjtxSpotLife` |
| **WSJT-X Decodes** | Consola de solo lectura que muestra las transmisiones decodificadas a medida que llegan. | — |
| **Spots:** | Interruptor maestro para la superposición de spots DX en el panadapter. Predeterminado: habilitado. | `IsSpotsEnabled` |
| **Spot Lines:** | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Deshabilítelo durante concursos para reducir el desorden visual. Predeterminado: habilitado. | `IsSpotsLinesEnabled` |
| Total Spots: | Lectura en vivo de cuántos spots se están rastreando actualmente en todas las fuentes. Se restablece a 0 cuando se presiona **Clear All Spots**. | — |
| **Auto:** | Cambia automáticamente el modo del slice al hacer clic en un spot que incluya información de modo (p. ej., CW, FT8, RTTY). Predeterminado: habilitado. | `SpotAutoSwitchMode` (cambiado de `SpotsAutoMode` en v26.5.1) |
| **Signals (Signal History)** | Marcadores dorados para señales de ancho de voz detectadas en el panadapter. Predeterminado: deshabilitado. | `SHistoryMarkersEnabled` (nuevo en v26.5.1, mismo interruptor que View > Signal History Markers) |
| **QRM (Signal History)** | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Predeterminado: deshabilitado. | `SHistoryQrmEnabled` (nuevo en v26.5.1, mismo interruptor que View > QRM History Markers) |
| **Clear All** | Borra todos los spots DX, la alimentación de memoria y los marcadores de Signal History y QRM del espectro. | — |
| **Levels:** | Número de filas de apilamiento vertical para spots. Predeterminado: 3. Rango válido: 1–10. | `SpotsMaxLevel` (migrado de `SpotsStackLevels` en v0.9.7) |
| **Position:** | Posición vertical en el panadapter. Predeterminado: 50. Rango válido: 0–100. | `SpotsStartingHeightPercentage` (migrado de `SpotsPosition` en v0.9.7) |
| **Font Size:** | Tamaño del texto de los spots. Predeterminado: 16. Rango válido: 8–32. | `SpotFontSize` (migrado de `SpotsFontSize` en v0.9.7) |
| **Spot Lifetime:** | Segundos antes de que un spot se desvanezca. Rango válido: 10 seg – 24 h (pasos no lineales). | `DxClusterSpotLifetimeSec` (migrado de `SpotsLifetime` en v0.9.7, migra la clave antigua basada en minutos) |
| **Override Colors:** | Fuerza un color de texto único para todos los spots. El botón siempre muestra "Enabled". | `IsSpotsOverrideColorsEnabled` |
| **Spot text color picker** | Abre QColorDialog para elegir el color del texto de los spots. Predeterminado: `#FFFF00`. | `SpotsOverrideColor` |
| **Override Background: Enabled** | Habilita un color de fondo personalizado para los spots. Predeterminado: habilitado. | `IsSpotsOverrideBackgroundColorsEnabled` |
| **Override Background: Auto** | Selecciona automáticamente el color de fondo para contraste. Predeterminado: habilitado. | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| **Spot background color picker** | Abre QColorDialog para el color de fondo de los spots. Predeterminado: `#000000`. | `SpotsOverrideBgColor` |
| **Background Opacity:** | Opacidad del color de fondo de los spots. Predeterminado: 48. Rango válido: 0–100. | `SpotsBackgroundOpacity` (migrado de `SpotsOverrideBgOpacity` en v0.9.7) |
| **DXCC Colors:** | Colorea los spots según el estado DXCC trabajado/confirmado/necesario. El botón siempre muestra "Enabled". | `IsDxccColoringEnabled` (cambiado de `DxccColoringEnabled` en v26.5.1) |
| **Log File (ADIF):** | Carga un archivo de registro ADIF para impulsar el coloreado DXCC. Supervisa automáticamente el archivo para detectar cambios después de la selección. | `DxccAdifFilePath` (cambiado de `DxccAdifPath` en v26.5.1) |
| **Imported: (DXCC stats)** | Muestra el recuento de QSO y el número de entidades cuando se carga un registro. Formato: `<N> QSOs / <M> entities`. | — |
| **DXCC Color swatches (New DXCC / New Band / New Mode / Worked)** | Abre un selector de color para cada categoría de estado DXCC. | `DxccColorNewEntity`, `DxccColorNewBand`, `DxccColorNewMode`, `DxccColorWorked` (nuevo en v26.5.1) |
| **Marker Lifetime:** | Cuánto tiempo persiste un marcador inactivo de Signal History antes de eliminarse. Predeterminado: 60 s. Rango válido: 15–300 seg. | `SHistoryLifetimeS` (nuevo en v26.5.1) |
| **QRM Gate:** | Cuánto tiempo debe persistir una portadora estrecha o señal de banda ancha antes de clasificarse como QRM. Predeterminado: 6 s. Rango válido: 3–30 seg. | `SHistoryQrmGateS` (nuevo en v26.5.1) |
| **Edge Threshold:** | Umbral por encima del piso de ruido para la caminata de borde de pendiente que refina el borde lateral de la portadora de S-History. Predeterminado: 3.0 dB. Rango válido: 1.0–10.0 dB. | `SHistorySoftEdgeDb` (nuevo en v26.5.1) |
| **Signal History color swatches (Signals / QRM)** | Abre un selector de color para los marcadores de señal de voz (dorado) y los marcadores QRM (rojo). Predeterminado: `#FFC800` / `#FF0000`. | `SHistoryColorSignals`, `SHistoryColorQrm` (nuevo en v26.5.1) |
| **Snap to Step:** | Redondea el clic-para-sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo. El botón siempre muestra "Enabled". Predeterminado: deshabilitado. | `SHistorySnapToStep` (nuevo en v26.5.1) |

## Sintonización desde la lista de spots

Al hacer doble clic en una fila de la pestaña **Spot List**, el slice activo se sintoniza a la frecuencia de ese spot. A partir de v0.9.7, AetherSDR también reenvía cualquier información de modo extraída del comentario del spot, por lo que el slice cambia automáticamente al modo correcto (por ejemplo, CW o SSB) para coincidir con el spot, en lugar de solo cambiar la frecuencia.

La pestaña **Spot List** muestra una tabla ordenable de todos los spots en vivo de cada fuente conectada. Use las casillas de verificación por banda sobre la tabla para filtrar qué bandas aparecen. Las casillas usan un diseño de flujo que se envuelve en filas adicionales cuando el diálogo es estrecho, de modo que cada etiqueta de casilla permanezca legible.

La tabla se puede ordenar haciendo clic en cualquier encabezado de columna. Tanto las columnas **Time** como **Freq** se ordenan numéricamente usando los datos subyacentes del spot, por lo que hacer clic en **Time** devuelve la lista al orden más reciente primero, incluso después de ordenar por frecuencia.

Para ocultar o mostrar columnas individuales en la tabla de spots, haga clic derecho en el encabezado de la tabla y marque o desmarque los nombres de las columnas en el menú contextual. El menú permanece abierto mientras alterna varias columnas, de modo que pueda configurar la visibilidad en una sola pasada sin que el menú se cierre después de cada cambio.

## Reporte de estación FreeDV Reporter

La pestaña **FreeDV** contiene un grupo **Station Reporting** que permite a AetherSDR transmitir la actividad de su estación al mapa público FreeDV Reporter en `qso.freedv.org`. Esta sección solo está presente en compilaciones con `HAVE_WEBSOCKETS`; en Windows requiere adicionalmente `HAVE_RADE`.

### Controles

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **Enable FreeDV Reporter reporting when RADE is active** | Habilita el reporte de estación al mapa público FreeDV Reporter siempre que el módem RADE esté activo. La casilla se niega a habilitarse si el indicativo o el campo de cuadrícula se resuelven como vacíos; un diálogo de advertencia explica qué falta. Predeterminado: deshabilitado. | `FreeDvAutoReport` |
| **Callsign:** | Indicativo enviado al mapa FreeDV Reporter. El campo es de solo lectura mientras **Use radio** esté marcado. El indicativo se actualiza automáticamente si lo cambia en Radio Setup mientras **Use radio** está activo. | `FreeDvMyCallsign` |
| **Use radio (callsign)** | Rellena previamente el campo de indicativo desde el indicativo configurado en la radio y bloquea el campo como solo lectura. Predeterminado: habilitado. | `FreeDvUseRadioCallsign` |
| **Grid Square:** | Cuadrícula Maidenhead enviada al mapa FreeDV Reporter. El campo es de solo lectura mientras |
