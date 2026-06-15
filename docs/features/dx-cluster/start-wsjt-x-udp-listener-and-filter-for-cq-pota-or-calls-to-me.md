# Iniciar el Oyente UDP de WSJT-X y Filtro para CQ, POTA o Llamadas a Mí

Configure AetherSDR para recibir transmisiones decodificadas desde WSJT-X a través de UDP y mostrar solo las categorías de spots que le interesen — llamadas CQ, activaciones POTA o estaciones llamando a su señal distintiva — como superposiciones en el panadapter.

## Antes de empezar

- WSJT-X debe estar ejecutándose en el mismo equipo o en la red y configurado para enviar mensajes de estado UDP a la dirección y puerto que configurará aquí.
- Conozca la dirección UDP y el puerto al que WSJT-X está transmitiendo (verifique en WSJT-X en **File > Settings > Reporting**, sección UDP Server).
- Su señal distintiva debe estar configurada en WSJT-X para que el filtro "Calling Me" funcione.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **WSJT-X**.
3. En **Address:**, introduzca la dirección de enlace UDP en la que AetherSDR debe escuchar (almacenada como `WsjtxAddress`). Use `127.0.0.1` si WSJT-X se ejecuta en el mismo equipo, o `0.0.0.0` para escuchar en todas las interfaces.
4. En **Port:**, introduzca el número de puerto UDP que coincida con el puerto configurado en WSJT-X (almacenado como `WsjtxPort`; rango válido 1–65535).
5. Haga clic en **Start**. El indicador de estado cambia a **Listening**.
6. Para iniciar el oyente automáticamente cada vez que se lance AetherSDR, active **Auto-start on startup (WSJT-X)** (almacenado como `WsjtxAutoStart`).
7. Debajo de las casillas de verificación del filtro, active una o más de las siguientes opciones para restringir qué decodificaciones aparecen como spots en el panadapter:
   - **CQ** — muestra estaciones que envían una llamada CQ general (almacenado como `WsjtxFilterCQ`).
   - **CQ POTA** — muestra estaciones que envían CQ POTA (almacenado como `WsjtxFilterPOTA`).
   - **Calling Me** — muestra decodificaciones dirigidas a su señal distintiva (almacenado como `WsjtxFilterCallingMe`).
8. Opcionalmente, asigne un color distinto a cada categoría haciendo clic en el botón de color correspondiente:
   - **CQ color** (almacenado como `WsjtxColorCQ`)
   - **POTA color** (almacenado como `WsjtxColorPOTA`)
   - **Calling Me color** (almacenado como `WsjtxColorCallingMe`)
   - **Default color** para decodificaciones que no pasan ningún filtro activo (almacenado como `WsjtxColorDefault`)
9. Establezca **Spot Life:** en el número de segundos que un spot de WSJT-X debe permanecer visible en el panadapter (almacenado como `WsjtxSpotLife`).
10. Confirme que las transmisiones decodificadas están llegando en la consola **WSJT-X Decodes** en la parte inferior de la pestaña.

## Qué hace cada control

| Control                       | Comportamiento                                                                                                                                                               | Clave de configuración                                                                                                   |
|-------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **Address:**                  | Dirección de enlace UDP para mensajes entrantes de WSJT-X.                                                                                                                  | `WsjtxAddress`                                                                                                           |
| **Port:**                     | Número de puerto UDP. Debe coincidir con el puerto de reporte de WSJT-X.                                                                                                    | `WsjtxPort`                                                                                                              |
| **Start / Stop**              | Inicia o detiene el oyente UDP.                                                                                                                                             | —                                                                                                                        |
| **Auto-start on startup (WSJT-X)** | Inicia el oyente automáticamente al lanzarse.                                                                                                                               | `WsjtxAutoStart`                                                                                                         |
| **CQ**                        | Solo pasa transmisiones CQ al panadapter.                                                                                                                                    | `WsjtxFilterCQ`                                                                                                          |
| **CQ POTA**                   | Solo pasa transmisiones CQ POTA.                                                                                                                                            | `WsjtxFilterPOTA`                                                                                                        |
| **Calling Me**                | Solo pasa decodificaciones dirigidas a su señal distintiva.                                                                                                                 | `WsjtxFilterCallingMe`                                                                                                   |
| **CQ color**                  | Color para spots CQ en el panadapter.                                                                                                                                       | `WsjtxColorCQ`                                                                                                           |
| **POTA color**                | Color para spots CQ POTA.                                                                                                                                                   | `WsjtxColorPOTA`                                                                                                         |
| **Calling Me color**          | Color para spots que llaman a su señal distintiva.                                                                                                                          | `WsjtxColorCallingMe`                                                                                                    |
| **Default color**             | Color para spots que no coinciden con ningún filtro activo.                                                                                                                 | `WsjtxColorDefault`                                                                                                      |
| **Spot Life:**                | Segundos que un spot de WSJT-X permanece en el panadapter antes de desvanecerse.                                                                                            | `WsjtxSpotLife`                                                                                                          |
| **WSJT-X Decodes**            | Consola de solo lectura que muestra las transmisiones decodificadas a medida que llegan.                                                                                    | —                                                                                                                        |
| **Spots:**                    | Activación general de la superposición de spots DX en el panadapter. Predeterminado: Habilitado.                                                                            | `IsSpotsEnabled`                                                                                                         |
| **Spot Lines:**               | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Deshabilite durante concursos para reducir el desorden visual. Predeterminado: Habilitado.          | `IsSpotsLinesEnabled`                                                                                                    |
| Total Spots:                  | Lectura en vivo de cuántos spots se están rastreando actualmente en todas las fuentes. Se reinicia a 0 al presionar **Clear All Spots**.                                     | —                                                                                                                        |
| **Auto:**                     | Cambia automáticamente el modo del slice al hacer clic en un spot que incluya información de modo (p. ej., CW, FT8, RTTY). Predeterminado: Habilitado.                       | `SpotAutoSwitchMode` (cambiado desde `SpotsAutoMode` en v26.5.1)                                                         |
| **Signals (Signal History)**  | Marcadores dorados para señales de ancho de voz detectadas en el panadapter. Predeterminado: Deshabilitado.                                                                 | `SHistoryMarkersEnabled` (nuevo en v26.5.1, misma activación que View > Signal History Markers)                          |
| **QRM (Signal History)**      | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Predeterminado: Deshabilitado.                                                                | `SHistoryQrmEnabled` (nuevo en v26.5.1, misma activación que View > QRM History Markers)                                |
| **Clear All**                 | Limpia todos los spots DX, la alimentación de memoria, los marcadores de Signal History y los marcadores QRM del espectro.                                                  | —                                                                                                                        |
| **Levels:**                   | Número de filas de apilamiento vertical para spots. Predeterminado: 3. Rango válido: 1–10.                                                                                  | `SpotsMaxLevel` (migrado desde `SpotsStackLevels` en v0.9.7)                                                            |
| **Position:**                 | Posición vertical en el panadapter. Predeterminado: 50. Rango válido: 0–100.                                                                                                | `SpotsStartingHeightPercentage` (migrado desde `SpotsPosition` en v0.9.7)                                                |
| **Font Size:**                | Tamaño del texto del spot. Predeterminado: 16. Rango válido: 8–32.                                                                                                          | `SpotFontSize` (migrado desde `SpotsFontSize` en v0.9.7)                                                                |
| **Spot Lifetime:**            | Segundos antes de que un spot se desvanezca. Rango válido: 10 s – 24 h (pasos no lineales).                                                                                 | `DxClusterSpotLifetimeSec` (migrado desde `SpotsLifetime` en v0.9.7, migra la clave antigua basada en minutos)           |
| **Override Colors:**          | Fuerza un solo color de texto para todos los spots. El botón siempre muestra "Enabled".                                                                                     | `IsSpotsOverrideColorsEnabled`                                                                                           |
| **Spot text color picker**    | Abre QColorDialog para elegir el color del texto del spot. Predeterminado: `#FFFF00`.                                                                                       | `SpotsOverrideColor`                                                                                                     |
| **Override Background: Enabled** | Habilita un color de fondo personalizado para el spot. Predeterminado: Habilitado.                                                                                          | `IsSpotsOverrideBackgroundColorsEnabled`                                                                                 |
| **Override Background: Auto** | Selecciona automáticamente el color de fondo para contraste. Predeterminado: Habilitado.                                                                                    | `IsSpotsOverrideToAutoBackgroundColorEnabled`                                                                            |
| **Spot background color picker** | Abre QColorDialog para el color de fondo del spot. Predeterminado: `#000000`.                                                                                               | `SpotsOverrideBgColor`                                                                                                   |
| **Background Opacity:**       | Opacidad del color de fondo del spot. Predeterminado: 48. Rango válido: 0–100.                                                                                              | `SpotsBackgroundOpacity` (migrado desde `SpotsOverrideBgOpacity` en v0.9.7)                                              |
| **DXCC Colors:**              | Colorea los spots según el estado de DXCC trabajado/confirmado/necesario. El botón siempre muestra "Enabled".                                                                | `IsDxccColoringEnabled` (cambiado desde `DxccColoringEnabled` en v26.5.1)                                                |
| **Log File (ADIF):**          | Carga un archivo de registro ADIF para impulsar el coloreado DXCC. Vigila automáticamente el archivo para detectar cambios después de la selección.                         | `DxccAdifFilePath` (cambiado desde `DxccAdifPath` en v26.5.1)                                                           |
| **Imported: (DXCC stats)**    | Muestra el recuento de QSO y el recuento de entidades cuando se carga un registro. Formato: `<N> QSOs / <M> entities`.                                                      | —                                                                                                                        |
| **DXCC Color swatches (New DXCC / New Band / New Mode / Worked)** | Abre un selector de color para cada categoría de estado DXCC.                                                                                                           | `DxccColorNewEntity`, `DxccColorNewBand`, `DxccColorNewMode`, `DxccColorWorked` (nuevo en v26.5.1)                      |
| **Marker Lifetime:**          | Cuánto tiempo persiste un marcador inactivo de Signal History antes de ser eliminado. Predeterminado: 60 s. Rango válido: 15–300 s.                                         | `SHistoryLifetimeS` (nuevo en v26.5.1)                                                                                  |
| **QRM Gate:**                 | Cuánto tiempo debe persistir una portadora estrecha o señal de banda ancha antes de clasificarse como QRM. Predeterminado: 6 s. Rango válido: 3–30 s.                       | `SHistoryQrmGateS` (nuevo en v26.5.1)                                                                                   |
| **Edge Threshold:**           | Umbral por encima del piso de ruido para la caminata por el borde de pendiente que refina el borde lateral de la portadora de S-History. Predeterminado: 3.0 dB. Rango válido: 1.0–10.0 dB. | `SHistorySoftEdgeDb` (nuevo en v26.5.1)                                                                                 |
| **Signal History color swatches (Signals / QRM)** | Abre un selector de color para los marcadores de señal de voz (dorado) y marcadores QRM (rojo). Predeterminado: `#FFC800` / `#FF0000`.                                      | `SHistoryColorSignals`, `SHistoryColorQrm` (nuevo en v26.5.1)                                                           |
| **Snap to Step:**             | Redondea el clic para sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo. El botón siempre muestra "Enabled". Predeterminado: Deshabilitado. | `SHistorySnapToStep` (nuevo en v26.5.1)                                                                                 |

## Sintonización desde la Lista de Spots

Al hacer doble clic en una fila de la pestaña **Spot List** se sintoniza el slice activo a la frecuencia de ese spot. A partir de v0.9.7, AetherSDR también reenvía cualquier información de modo extraída del comentario del spot, por lo que el slice cambia automáticamente al modo correcto (por ejemplo, CW o SSB) para coincidir con el spot en lugar de solo cambiar la frecuencia.

## Informe de estación FreeDV Reporter

La pestaña **FreeDV** contiene un grupo **Station Reporting** que permite a AetherSDR transmitir la actividad de su estación al mapa público de FreeDV Reporter en `qso.freedv.org`. Esta sección solo está presente en compilaciones compiladas con `HAVE_WEBSOCKETS`; en Windows, además requiere `HAVE_RADE`.

### Controles

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **Enable FreeDV Reporter reporting when RADE is active** | Habilita el informe de estación al mapa público de FreeDV Reporter siempre que el módem RADE esté activo. La casilla de verificación se niega a habilitarse si el campo de señal distintiva o el de cuadrícula se resuelven en un valor vacío; un cuadro de diálogo de advertencia explica qué falta. Predeterminado: deshabilitado. | `FreeDvAutoReport` |
| **Callsign:** | Señal distintiva enviada al mapa de FreeDV Reporter. El campo es de solo lectura mientras **Use radio** esté marcado. La señal distintiva se actualiza automáticamente si la cambia en Radio Setup mientras **Use radio** está activo. | `FreeDvMyCallsign` |
| **Use radio (callsign)** | Rellena previamente el campo de señal distintiva desde la señal distintiva configurada en la radio y bloquea el campo como solo lectura. Predeterminado: habilitado. | `FreeDvUseRadioCallsign` |
| **Grid Square:** | Cuadrícula Maidenhead enviada al mapa de FreeDV Reporter. El campo es de solo lectura mientras **Use GPS** esté marcado. | `FreeDvMyGrid` |
| **Use GPS (grid)** | Rellena previamente el campo de cuadrícula desde el módulo GPS de la radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. | `FreeDvUseGpsGrid` |
| **Station Msg:** | Mensaje de texto libre opcional que se muestra junto a su señal distintiva en el mapa público de FreeDV Reporter. | `FreeDvMyMessage` |

### Habilitación del informe de FreeDV Reporter

1. Abra `Settings > SpotHub...` y haga clic en la pestaña **FreeDV**.
2. En el grupo **Station Reporting**, verifique que el campo **Callsign:** muestre su señal distintiva.
   - Si **Use radio** está marcado, la señal distintiva se
