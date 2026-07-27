# Elige colores para cada fuente de spots

AetherSDR puede mostrar spots de hasta seis fuentes simultáneamente. Asignar un color distintivo a cada fuente facilita distinguirlas de un vistazo en el panadapter.

## Antes de empezar

- Abra SpotHub: `Settings > SpotHub...`
- Debe tener al menos una fuente de spots configurada para poder ver el efecto de su elección de color.

## Pasos

### Color de spot de DX Cluster
1. En SpotHub, haga clic en la pestaña **Cluster**.
2. Haga clic en el botón **Spot Color:**.
3. Elija un color en el selector de color que se abre y confirme su selección.
4. El nuevo color se guarda en `ClusterSpotColor` y se aplica inmediatamente a los spots del cluster en el panadapter.

### Color de spot de RBN

1. Haga clic en la pestaña **RBN**.
2. Haga clic en el botón **Spot Color:**.
3. Elija un color y confirme.
4. Se guarda en `RbnSpotColor`.

### Colores de spot de WSJT-X

WSJT-X admite cuatro colores separados, uno por categoría de decodificación.

1. Haga clic en la pestaña **WSJT-X**.
2. Haga clic en el botón de color para cada categoría que desee cambiar:
   - **CQ color** — spots decodificados como llamadas CQ. Se guarda en `WsjtxColorCQ`.
   - **POTA color** — spots decodificados como llamadas CQ POTA. Se guarda en `WsjtxColorPOTA`.
   - **Calling Me color** — decodificaciones dirigidas a su indicativo. Se guarda en `WsjtxColorCallingMe`.
   - **Default color** — todas las demás decodificaciones de WSJT-X. Se guarda en `WsjtxColorDefault`.
3. Confirme cada color en el selector de color antes de pasar al siguiente.

### Color de spot de POTA

1. Haga clic en la pestaña **POTA**.
2. Haga clic en el botón **Spot Color:**.
3. Elija un color y confirme.
4. Se guarda en `PotaSpotColor`.

### Color de spot de FreeDV

1. Haga clic en la pestaña **FreeDV**.
2. Haga clic en el botón **Spot Color:**.
3. Elija un color y confirme.
4. Se guarda en `FreeDvSpotColor`.

> **Nota:** La pestaña FreeDV solo está presente si AetherSDR se compiló con soporte WebSocket.

### SpotCollector

SpotCollector no tiene un selector de color de spot dedicado en SpotHub. Consulte las opciones de la pestaña Display a continuación si necesita una anulación uniforme para todas las fuentes.

## Qué hace cada control
| Control                                                       | Pestaña                                                                                                                  | Configuración guardada                                                                                                                                                 |
|---------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Spot Color:**                                               | Cluster                                                                                                                  | `ClusterSpotColor`                                                                                                                                                     |
| **Startup Commands…**                                         | Cluster                                                                                                                  | `DxClusterStartupCommands` — comandos enviados automáticamente tras cada inicio de sesión (#2683). Un comando por línea.                                               |
| **Spot Color:**                                               | RBN                                                                                                                      | `RbnSpotColor`                                                                                                                                                         |
| **Startup Commands…**                                         | RBN                                                                                                                      | `RbnStartupCommands` — configuración independiente de los comandos de inicio del DX cluster. Un comando por línea.                                                    |
| **CQ color**                                                  | WSJT-X                                                                                                                   | `WsjtxColorCQ`                                                                                                                                                         |
| **POTA color**                                                | WSJT-X                                                                                                                   | `WsjtxColorPOTA`                                                                                                                                                       |
| **Calling Me color**                                          | WSJT-X                                                                                                                   | `WsjtxColorCallingMe`                                                                                                                                                  |
| **Default color**                                             | WSJT-X                                                                                                                   | `WsjtxColorDefault`                                                                                                                                                    |
| **Spot Color:**                                               | POTA                                                                                                                     | `PotaSpotColor`                                                                                                                                                        |
| **Spot Color:**                                               | FreeDV                                                                                                                   | `FreeDvSpotColor`                                                                                                                                                      |
| **Enable FreeDV Reporter reporting when RADE is active**      | FreeDV                                                                                                                   | `FreeDvAutoReport`                                                                                                                                                     |
| **Callsign:**                                                 | FreeDV — Station Reporting                                                                                               | `FreeDvMyCallsign`                                                                                                                                                     |
| **Use radio (callsign)**                                      | FreeDV — Station Reporting                                                                                               | `FreeDvUseRadioCallsign`                                                                                                                                               |
| **Grid Square:**                                              | FreeDV — Station Reporting                                                                                               | `FreeDvMyGrid`                                                                                                                                                         |
| **Use GPS (grid)**                                            | FreeDV — Station Reporting                                                                                               | `FreeDvUseGpsGrid`                                                                                                                                                     |
| **Station Msg:**                                              | FreeDV — Station Reporting                                                                                               | `FreeDvMyMessage`                                                                                                                                                      |
| **Auto:**                                                     | Display                                                                                                                  | `SpotAutoSwitchMode` — clave de configuración cambiada desde `SpotsAutoMode` en v26.5.1. Valor predeterminado cambiado a **Enabled** en v0.9.5.1.                      |
| **Signals (Signal History)**                                  | Display                                                                                                                  | `SHistoryMarkersEnabled` — nuevo en v26.5.1 (#2426). Misma opción que View > Signal History Markers.                                                                   |
| **QRM (Signal History)**                                      | Display                                                                                                                  | `SHistoryQrmEnabled` — nuevo en v26.5.1 (#2426). Misma opción que View > QRM History Markers.                                                                         |
| **Clear All**                                                 | Display                                                                                                                  | Limpia todos los spots DX, la fuente de memoria, los marcadores de Signal History y los marcadores QRM del espectro.                                                  |
| **Spot Lines:**                                               | Display                                                                                                                  | `IsSpotsLinesEnabled` — nuevo en v0.9.7                                                                                                                                 |
| Recuento total de spots                                       | Barra de estado                                                                                                          | Lectura en vivo de cuántos spots se están rastreando actualmente en todas las fuentes. Se actualiza cuando se añaden o eliminan spots. Se reinicia a 0 al pulsar **Clear All Spots**. |
| **Selector de color de texto de spot**                        | Display                                                                                                                  | `SpotsOverrideColor` — predeterminado `#FFFF00`                                                                                                                         |
| **Override Background: Enabled**                              | Display                                                                                                                  | `IsSpotsOverrideBackgroundColorsEnabled`                                                                                                                               |
| **Override Background: Auto**                                 | Display                                                                                                                  | `IsSpotsOverrideToAutoBackgroundColorEnabled`                                                                                                                          |
| **Selector de color de fondo de spot**                        | Display                                                                                                                  | `SpotsOverrideBgColor` — predeterminado `#000000`                                                                                                                      |
| **Background Opacity:**                                       | Display                                                                                                                  | `SpotsBackgroundOpacity` — clave de configuración migrada desde `SpotsOverrideBgOpacity` en v0.9.7                                                                      |
| **Total Spots:**                                              | Display                                                                                                                  | Recuento en vivo de spots rastreados actualmente en todas las fuentes.                                                                                                 |
| **DXCC Colors:**                                              | Display — Sección DXCC Coloring                                                                                          | `IsDxccColoringEnabled` — clave de configuración cambiada desde `DxccColoringEnabled` en v26.5.1.                                                                      |
| **Log File (ADIF):**                                          | Display — Sección DXCC Coloring                                                                                          | `DxccAdifFilePath` — clave de configuración cambiada desde `DxccAdifPath` en v26.5.1. La recarga automática está siempre activada cuando se selecciona un archivo.     |
| **Imported: (estadísticas DXCC)**                             | Display — Sección DXCC Coloring                                                                                          | Muestra el recuento de QSO y el número de entidades cuando se carga un registro. Formato: '<N> QSOs / <M> entities'.                                                  |
| **Muestras de color DXCC** (New DXCC / New Band / New Mode / Worked) | Display — Sección DXCC Coloring                                                                                    | `DxccColorNewEntity` / `DxccColorNewBand` / `DxccColorNewMode` / `DxccColorWorked` — nuevo en v26.5.1                                                                 |
| **Marker Lifetime:**                                          | Display — Sección Signal History                                                                                         | `SHistoryLifetimeS` — nuevo en v26.5.1. Predeterminado 60 s.                                                                                                           |
| **QRM Gate:**                                                 | Display — Sección Signal History                                                                                         | `SHistoryQrmGateS` — nuevo en v26.5.1. Predeterminado 6 s.                                                                                                             |
| **Edge Threshold:**                                           | Display — Sección Signal History                                                                                         | `SHistorySoftEdgeDb` — nuevo en v26.5.1. Predeterminado 3.0 dB.                                                                                                        |
| **Muestras de color de Signal History** (Signals / QRM)       | Display — Sección Signal History                                                                                         | `SHistoryColorSignals` (dorado) / `SHistoryColorQrm` (rojo) — nuevo en v26.5.1.                                                                                        |
| **Snap to Step:**                                             | Display — Sección Signal History                                                                                         | `SHistorySnapToStep` — nuevo en v26.5.1. Predeterminado Disabled.                                                                                                      |

## FreeDV Reporter — Station Reporting

v0.9.3 añade un grupo **Station Reporting** dentro de la pestaña **FreeDV**. Cuando está activado, AetherSDR transmite la actividad de su estación al mapa público de FreeDV Reporter en qso.freedv.org siempre que el módem RADE esté activo.

> **Nota:** Station Reporting solo está presente si AetherSDR se compiló con soporte WebSocket (`HAVE_WEBSOCKETS`). En las compilaciones para Windows, adicionalmente requiere `HAVE_RADE`.

### Habilitar el reporte

1. Haga clic en la pestaña **FreeDV** en SpotHub.
2. En el grupo **Station Reporting**, rellene un indicativo y un cuadrado de cuadrícula válidos (ver más abajo) antes de activar la casilla de verificación.
3. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si el campo de indicativo o de cuadrado de cuadrícula está vacío cuando marca la casilla, aparece un diálogo de advertencia y la casilla se desmarca. Rellene ambos campos primero y luego intente de nuevo.
4. La configuración se guarda en `FreeDvAutoReport`.

### Campo de indicativo

- El campo **Callsign:** (`FreeDvMyCallsign`) establece el indicativo reportado al mapa público.
- Cuando **Use radio** está marcado (predeterminado), el campo se rellena automáticamente desde el indicativo configurado en la radio y se bloquea como solo lectura. El campo se actualiza automáticamente si cambia el indicativo en Radio Setup.
- Desmarque **Use radio** para escribir un indicativo manualmente. El valor se guarda en `FreeDvMyCallsign` y se convierte a mayúsculas al salir.
- **Use radio** se guarda en `FreeDvUseRadioCallsign`.

### Campo de cuadrado de cuadrícula

- El campo **Grid Square:** (`FreeDvMyGrid`) establece el localizador Maidenhead reportado al mapa público.
- En modelos de radio con hardware GPS, aparece una casilla **Use GPS**. Cuando está marcada (predeterminado), el campo se rellena automáticamente desde el módulo GPS de la radio y se bloquea como solo lectura.
- Desmarque **Use GPS** para escribir un cuadrado de cuadrícula manualmente. El valor se guarda en `FreeDvMyGrid` y se convierte a mayúsculas al salir.
- **Use GPS** se guarda en `FreeDvUseGpsGrid`. La casilla está oculta en modelos de radio que no tienen hardware GPS.

### Mensaje de estación

- El campo opcional **Station Msg:** (`FreeDvMyMessage`) acepta texto libre que aparece junto a su indicativo en el mapa público de FreeDV Reporter. Déjelo en blanco si no tiene nada que añadir.

## Modo automático predeterminado cambiado en v0.9.5.1

La opción **Auto:** en la pestaña **Display** ahora tiene como predeterminado **Enabled** para nuevas instalaciones. Si está actualizando desde una versión anterior y `SpotAutoSwitchMode` no se había configurado previamente, AetherSDR lo tratará como activado después de la actualización. Para desactivarlo, abra la pestaña **Display** y haga clic en **Auto:** hasta que muestre **Disabled**.

> **Nota:** La clave de configuración cambió de `SpotsAutoMode` a `SpotAutoSwitchMode` en v26.5.1.

## Líneas de spot (nuevo en v0.9.7)

La opción **Spot Lines:** en la pestaña **Display** controla si se dibujan líneas verticales desde la línea base del espectro hasta cada etiqueta de spot en el panadapter. La configuración se guarda en `IsSpotsLinesEnabled` y tiene como predeterminado **Enabled**.

Para desactivar las líneas de spot:

1. Abra SpotHub: `Settings > SpotHub...`
2. Haga clic en la pestaña **Display**.
3. Haga clic en **Spot Lines:** hasta que muestre **Disabled**.

Desactivar las líneas de spot reduce el desorden visual durante concursos o cuando la densidad de spots es alta.

## Marcadores de Signal History y QRM (nuevo en v26.5.1)

La pestaña **Display** incluye controles de Signal History para detectar y marcar señales en el panadapter:

- **Signals (Signal History):** Marcadores dorados para señales de ancho de voz detectadas en el panadapter. Guardado en `SHistoryMarkersEnabled`.
- **QRM (Signal History):** Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Guardado en `SHistoryQrmEnabled`.

Ambas opciones reflejan los mismos controles que se encuentran en `View > Signal History Markers` y `View > QRM History Markers`.

### Ajustes de Signal History

La sección **Signal History** debajo del divisor en la pestaña Display proporciona ajustes finos:

- **Marker Lifetime:** Control deslizante (15–300 segundos, predeterminado 60 s) que controla cuánto tiempo persiste un marcador de Signal History inactivo. Guardado en `SHistoryLifetimeS`.
- **QRM Gate:** Control deslizante (3–30 segundos, predeterminado 6 s) que controla cuánto tiempo debe persistir una portadora estrecha o una señal de banda ancha antes de clasificarse como QRM. Guardado en `SHistoryQrmGateS`.
- **Edge Threshold:** Control deslizante (1.0–10.0 dB, predeterminado 3.0 dB) para el recorrido del borde de pendiente que refina el borde lateral de la portadora en S-History. Los valores más bajos están más cerca de la portadora pero son más sensibles al ruido. Guardado en `SHistorySoftEdgeDb`.
- **Muestras de color de Signal History:** Haga clic para abrir un selector de color para los marcadores de señal de voz (dorado predeterminado `#FFC800`) y los marcadores QRM (rojo predeterminado `#FF0000`). Guardado en `SHistoryColorSignals` y `SHistoryColorQrm`.
- **Snap to Step:** Activar fuerza los marcadores de Signal History a alinearse con los límites de paso del panadapter (por ejemplo, 100 Hz, 1 kHz). Guardado en `SHistorySnapToStep`.
