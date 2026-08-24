# Elija colores para cada fuente de spots

AetherSDR puede mostrar spots de hasta seis fuentes simultáneamente. Asignar un color distintivo a cada fuente facilita distinguirlas de un vistazo en el panadapter.

## Antes de comenzar

- Abra SpotHub: `Settings > SpotHub...`
- Debe tener al menos una fuente de spots configurada para poder ver el efecto de su elección de color.

## Pasos

### Color de spots del DX Cluster
1. En SpotHub, haga clic en la pestaña **Cluster**.
2. Haga clic en el botón **Spot Color:**.
3. Elija un color en el selector que se abre y confirme su selección.
4. El nuevo color se guarda en `ClusterSpotColor` y se aplica inmediatamente a los spots del cluster en el panadapter.

### Color de spots de RBN

1. Haga clic en la pestaña **RBN**.
2. Haga clic en el botón **Spot Color:**.
3. Elija un color y confirme.
4. Se guarda en `RbnSpotColor`.

### Colores de spots de WSJT-X

WSJT-X admite cuatro colores separados, uno por categoría de decodificación.

1. Haga clic en la pestaña **WSJT-X**.
2. Haga clic en el botón de color de cada categoría que desee cambiar:
   - **CQ color** — spots decodificados como llamadas CQ. Se guarda en `WsjtxColorCQ`.
   - **POTA color** — spots decodificados como llamadas CQ POTA. Se guarda en `WsjtxColorPOTA`.
   - **Calling Me color** — decodificaciones dirigidas a su indicativo. Se guarda en `WsjtxColorCallingMe`.
   - **Default color** — todas las demás decodificaciones de WSJT-X. Se guarda en `WsjtxColorDefault`.
3. Confirme cada color en el selector antes de pasar al siguiente.

### Color de spots de POTA

1. Haga clic en la pestaña **POTA**.
2. Haga clic en el botón **Spot Color:**.
3. Elija un color y confirme.
4. Se guarda en `PotaSpotColor`.

### Color de spots de FreeDV

1. Haga clic en la pestaña **FreeDV**.
2. Haga clic en el botón **Spot Color:**.
3. Elija un color y confirme.
4. Se guarda en `FreeDvSpotColor`.

> **Nota:** La pestaña FreeDV solo está presente si AetherSDR se compiló con soporte WebSocket.

### SpotCollector

SpotCollector no tiene un selector de color de spots dedicado en SpotHub. Consulte las opciones de la pestaña Display a continuación si necesita una anulación uniforme para todas las fuentes.

## Qué hace cada control
| Control                                                       | Pestaña                                                                                                                    | Configuración guardada                                                                                                                                                  |
|---------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Spot Color:**                                               | Cluster                                                                                                                    | `ClusterSpotColor`                                                                                                                                                     |
| **Startup Commands…**                                         | Cluster                                                                                                                    | `DxClusterStartupCommands` — comandos enviados automáticamente después de cada inicio de sesión (#2683). Un comando por línea.                                        |
| **Spot Color:**                                               | RBN                                                                                                                        | `RbnSpotColor`                                                                                                                                                         |
| **Startup Commands…**                                         | RBN                                                                                                                        | `RbnStartupCommands` — configuración independiente de los comandos de inicio del DX cluster. Un comando por línea.                                                  |
| **CQ color**                                                  | WSJT-X                                                                                                                     | `WsjtxColorCQ`                                                                                                                                                         |
| **POTA color**                                                | WSJT-X                                                                                                                     | `WsjtxColorPOTA`                                                                                                                                                       |
| **Calling Me color**                                          | WSJT-X                                                                                                                     | `WsjtxColorCallingMe`                                                                                                                                                  |
| **Default color**                                             | WSJT-X                                                                                                                     | `WsjtxColorDefault`                                                                                                                                                    |
| **Spot Color:**                                               | POTA                                                                                                                       | `PotaSpotColor`                                                                                                                                                        |
| **Spot Color:**                                               | FreeDV                                                                                                                     | `FreeDvSpotColor`                                                                                                                                                      |
| **Enable FreeDV Reporter reporting when RADE is active**      | FreeDV                                                                                                                     | `FreeDvAutoReport`                                                                                                                                                     |
| **Callsign:**                                                 | FreeDV — Station Reporting                                                                                                 | `FreeDvMyCallsign`                                                                                                                                                     |
| **Use radio (callsign)**                                      | FreeDV — Station Reporting                                                                                                 | `FreeDvUseRadioCallsign`                                                                                                                                               |
| **Grid Square:**                                              | FreeDV — Station Reporting                                                                                                 | `FreeDvMyGrid`                                                                                                                                                         |
| **Use GPS (grid)**                                            | FreeDV — Station Reporting                                                                                                 | `FreeDvUseGpsGrid`                                                                                                                                                     |
| **Station Msg:**                                              | FreeDV — Station Reporting                                                                                                 | `FreeDvMyMessage`                                                                                                                                                      |
| **Auto:**                                                     | Display                                                                                                                    | `SpotAutoSwitchMode` — clave de configuración cambiada desde `SpotsAutoMode` en v26.5.1. El valor predeterminado cambió a **Enabled** en v0.9.5.1.                   |
| **Signals (Signal History)**                                  | Display                                                                                                                    | `SHistoryMarkersEnabled` — nuevo en v26.5.1 (#2426). Mismo interruptor que View > Signal History Markers.                                                           |
| **QRM (Signal History)**                                      | Display                                                                                                                    | `SHistoryQrmEnabled` — nuevo en v26.5.1 (#2426). Mismo interruptor que View > QRM History Markers.                                                                  |
| **Clear All**                                                 | Display                                                                                                                    | Borra todos los spots de DX, la alimentación de memoria, los marcadores de Signal History y los marcadores QRM del espectro.                                          |
| **Spot Lines:**                                               | Display                                                                                                                    | `IsSpotsLinesEnabled` — nuevo en v0.9.7                                                                                                                                 |
| Total spots count                                             | Barra de estado                                                                                                            | Lectura en vivo de cuántos spots se rastrean actualmente en todas las fuentes. Se actualiza cuando se agregan o borran spots. Se restablece a 0 al presionar **Clear All Spots**. |
| **Spot text color picker**                                    | Display                                                                                                                    | `SpotsOverrideColor` — valor predeterminado `#FFFF00`                                                                                                                                           |
| **Override Background: Enabled**                              | Display                                                                                                                    | `IsSpotsOverrideBackgroundColorsEnabled`                                                                                                                                          |
| **Override Background: Auto**                                 | Display                                                                                                                    | `IsSpotsOverrideToAutoBackgroundColorEnabled`                                                                                                                                         |
| **Spot background color picker**                              | Display                                                                                                                    | `SpotsOverrideBgColor` — valor predeterminado `#000000`                                                                                                                                         |
| **Background Opacity:**                                       | Display                                                                                                                    | `SpotsBackgroundOpacity` — clave de configuración migrada desde `SpotsOverrideBgOpacity` en v0.9.7                                                                      |
| **Total Spots:**                                              | Display                                                                                                                    | Conteo en vivo de spots rastreados actualmente en todas las fuentes.                                                                                                    |
| **DXCC Colors:**                                              | Display — sección DXCC Coloring                                                                                            | `IsDxccColoringEnabled` — clave de configuración cambiada desde `DxccColoringEnabled` en v26.5.1.                                                                       |
| **Log File (ADIF):**                                          | Display — sección DXCC Coloring                                                                                            | `DxccAdifFilePath` — clave de configuración cambiada desde `DxccAdifPath` en v26.5.1. La recarga automática está siempre habilitada cuando se selecciona un archivo.  |
| **Imported: (DXCC stats)**                                    | Display — sección DXCC Coloring                                                                                            | Muestra el conteo de QSO y el número de entidades cuando se carga un registro. Formato: '<N> QSOs / <M> entities'.                                                 |
| **DXCC Color swatches** (New DXCC / New Band / New Mode / Worked) | Display — sección DXCC Coloring                                                                                          | `DxccColorNewEntity` / `DxccColorNewBand` / `DxccColorNewMode` / `DxccColorWorked` — nuevos en v26.5.1                                                                 |
| **Marker Lifetime:**                                          | Display — sección Signal History                                                                                           | `SHistoryLifetimeS` — nuevo en v26.5.1. Valor predeterminado 60 s.                                                                                                    |
| **QRM Gate:**                                                 | Display — sección Signal History                                                                                           | `SHistoryQrmGateS` — nuevo en v26.5.1. Valor predeterminado 6 s.                                                                                                      |
| **Edge Threshold:**                                           | Display — sección Signal History                                                                                           | `SHistorySoftEdgeDb` — nuevo en v26.5.1. Valor predeterminado 3.0 dB.                                                                                                  |
| **Signal History color swatches** (Signals / QRM)             | Display — sección Signal History                                                                                           | `SHistoryColorSignals` (dorado) / `SHistoryColorQrm` (rojo) — nuevos en v26.5.1.                                                                                       |
| **Snap to Step:**                                             | Display — sección Signal History                                                                                           | `SHistorySnapToStep` — nuevo en v26.5.1. Valor predeterminado Disabled.                                                                                                |

## FreeDV Reporter — Station Reporting

v0.9.3 agrega un grupo **Station Reporting** dentro de la pestaña **FreeDV**. Cuando está habilitado, AetherSDR transmite la actividad de su estación al mapa público FreeDV Reporter en qso.freedv.org siempre que el módem RADE esté activo.

> **Nota:** Station Reporting solo está presente si AetherSDR se compiló con soporte WebSocket (`HAVE_WEBSOCKETS`). En compilaciones para Windows, además requiere `HAVE_RADE`.

### Habilitar el informe

1. Haga clic en la pestaña **FreeDV** en SpotHub.
2. En el grupo **Station Reporting**, complete un indicativo y un cuadrado de rejilla válidos (ver más abajo) antes de habilitar la casilla de verificación.
3. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si el campo de indicativo o el de cuadrado de rejilla está vacío al marcar la casilla, aparece un diálogo de advertencia y la casilla vuelve a quedar sin marcar. Complete ambos campos primero y luego intente de nuevo.
4. La configuración se guarda en `FreeDvAutoReport`.

### Campo de indicativo

- El campo **Callsign:** (`FreeDvMyCallsign`) establece el indicativo que se informa al mapa público.
- Cuando **Use radio** está marcado (valor predeterminado), el campo se rellena previamente con el indicativo configurado en la radio y queda bloqueado como solo lectura. El campo se actualiza automáticamente si cambia el indicativo en Radio Setup.
- Desmarque **Use radio** para escribir un indicativo manualmente. El valor se guarda en `FreeDvMyCallsign` y se convierte a mayúsculas al salir.
- **Use radio** se guarda en `FreeDvUseRadioCallsign`.

### Campo de cuadrado de rejilla

- El campo **Grid Square:** (`FreeDvMyGrid`) establece el localizador Maidenhead que se informa al mapa público.
- En modelos de radio con hardware GPS, aparece una casilla **Use GPS**. Cuando está marcada (valor predeterminado), el campo se rellena previamente con el módulo GPS de la radio y queda bloqueado como solo lectura.
- Desmarque **Use GPS** para escribir un cuadrado de rejilla manualmente. El valor se guarda en `FreeDvMyGrid` y se convierte a mayúsculas al salir.
- **Use GPS** se guarda en `FreeDvUseGpsGrid`. La casilla está oculta en modelos de radio sin hardware GPS.

### Mensaje de estación

- El campo opcional **Station Msg:** (`FreeDvMyMessage`) acepta texto libre que aparece junto a su indicativo en el mapa público de FreeDV Reporter. Déjelo en blanco si no tiene nada que agregar.

## El modo Auto cambió su valor predeterminado en v0.9.5.1

El interruptor **Auto:** en la pestaña **Display** ahora tiene como valor predeterminado **Enabled** para instalaciones nuevas. Si está actualizando desde una versión anterior y `SpotAutoSwitchMode` no estaba configurado previamente, AetherSDR lo tratará como habilitado después de la actualización. Para deshabilitarlo, abra la pestaña **Display** y haga clic en **Auto:** hasta que muestre **Disabled**.

> **Nota:** La clave de configuración cambió de `SpotsAutoMode` a `SpotAutoSwitchMode` en v26.5.1.

## Spot Lines (nuevo en v0.9.7)

El interruptor **Spot Lines:** en la pestaña **Display** controla si se dibujan líneas verticales desde la línea base del espectro hasta cada etiqueta de spot en el panadapter. La configuración se guarda en `IsSpotsLinesEnabled` y tiene como valor predeterminado **Enabled**.

Para desactivar las líneas de spots:

1. Abra SpotHub: `Settings > SpotHub...`
2. Haga clic en la pestaña **Display**.
3. Haga clic en **Spot Lines:** hasta que muestre **Disabled**.

Desactivar las líneas de spots reduce el desorden visual durante concursos o cuando la densidad de spots es alta.

## Marcadores de Signal History y QRM (nuevos en v26.5.1)

La pestaña **Display** incluye controles de Signal History para detectar y marcar señales en el panadapter:

- **Signals (Signal History):** Marcadores dorados para señales detectadas con ancho de voz en el panadapter. Se guarda en `SHistoryMarkersEnabled`.
- **QRM (Signal History):** Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Se guarda en `SHistoryQrmEnabled`.

Ambos interruptores reflejan los mismos controles que se encuentran en `View > Signal History Markers` y `View > QRM History Markers`.

### Ajustes de Signal History

La sección **Signal History** debajo del divisor en la pestaña Display permite un ajuste fino:

- **Marker Lifetime:** Control deslizante (15–300 segundos, valor predeterminado 60 s) que controla cuánto tiempo persiste un marcador de Signal History inactivo. Se guarda en `SHistoryLifetimeS`.
- **QRM Gate:** Control deslizante (3–30 segundos, valor predeterminado 6 s) que controla cuánto tiempo debe persistir una portadora estrecha o una señal de banda ancha antes de clasificarse como QRM. Se guarda en `SHistoryQrmGateS`.
- **Edge Threshold:** Control deslizante (1.0–10.0 dB, valor predeterminado 3.0 dB) para el recorrido de borde de pendiente que refina el borde del lado de la portadora de S-History. Los valores más bajos están más cerca de la portadora pero son más sensibles al ruido. Se guarda en `SHistorySoftEdgeDb`.
- **Signal History color swatches:** Haga clic para abrir un selector de color para los marcadores de señales de voz (dorado predeterminado `#FFC800`) y los marcadores QRM (rojo predeterminado `#FF0000`). Se guarda en
