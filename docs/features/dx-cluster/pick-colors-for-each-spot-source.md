# Elija colores para cada fuente de spots

AetherSDR puede mostrar spots de hasta seis fuentes simultáneamente. Asignar un color distintivo a cada fuente facilita distinguirlas de un vistazo en el panadapter.

## Antes de comenzar

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

SpotCollector no tiene un selector de color de spot dedicado en SpotHub. Vea las opciones de la pestaña Display a continuación si necesita una anulación uniforme para todas las fuentes.

## Qué controla cada control
| Control                                                  | Pestaña                    | Configuración guardada                                                                                                                                                     |
|----------------------------------------------------------|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Spot Color:**                                          | Cluster                    | `ClusterSpotColor`                                                                                                                                                         |
| **Spot Color:**                                          | RBN                        | `RbnSpotColor`                                                                                                                                                             |
| **CQ color**                                             | WSJT-X                     | `WsjtxColorCQ`                                                                                                                                                             |
| **POTA color**                                           | WSJT-X                     | `WsjtxColorPOTA`                                                                                                                                                           |
| **Calling Me color**                                     | WSJT-X                     | `WsjtxColorCallingMe`                                                                                                                                                      |
| **Default color**                                        | WSJT-X                     | `WsjtxColorDefault`                                                                                                                                                        |
| **Spot Color:**                                          | POTA                       | `PotaSpotColor`                                                                                                                                                            |
| **Spot Color:**                                          | FreeDV                     | `FreeDvSpotColor`                                                                                                                                                          |
| **Enable FreeDV Reporter reporting when RADE is active** | FreeDV                     | `FreeDvAutoReport`                                                                                                                                                         |
| **Callsign:**                                            | FreeDV — Station Reporting | `FreeDvMyCallsign`                                                                                                                                                         |
| **Use radio (callsign)**                                 | FreeDV — Station Reporting | `FreeDvUseRadioCallsign`                                                                                                                                                   |
| **Grid Square:**                                         | FreeDV — Station Reporting | `FreeDvMyGrid`                                                                                                                                                             |
| **Use GPS (grid)**                                       | FreeDV — Station Reporting | `FreeDvUseGpsGrid`                                                                                                                                                         |
| **Station Msg:**                                         | FreeDV — Station Reporting | `FreeDvMyMessage`                                                                                                                                                          |
| **Auto Mode:**                                           | Display                    | `SpotsAutoMode` — valor predeterminado cambiado a **Enabled** en v0.9.5.1                                                                                                  |
| **Spot Lines:**                                          | Display                    | `IsSpotsLinesEnabled` — nuevo en v0.9.7                                                                                                                                    |
| Total spots count                                        | Barra de estado            | Lectura en vivo de cuántos spots se están rastreando actualmente en todas las fuentes. Se actualiza cuando se añaden o eliminan spots. Se reinicia a 0 al presionar **Clear All Spots**. |
## FreeDV Reporter — Station Reporting

v0.9.3 añade un grupo **Station Reporting** dentro de la pestaña **FreeDV**. Cuando está habilitado, AetherSDR transmite la actividad de su estación al mapa público de FreeDV Reporter en qso.freedv.org siempre que el módem RADE esté activo.

> **Nota:** Station Reporting solo está presente si AetherSDR se compiló con soporte WebSocket (`HAVE_WEBSOCKETS`). En compilaciones de Windows, adicionalmente requiere `HAVE_RADE`.

### Habilitar la notificación

1. Haga clic en la pestaña **FreeDV** en SpotHub.
2. En el grupo **Station Reporting**, complete un indicativo y un cuadrado de cuadrícula válidos (ver más abajo) antes de habilitar la casilla de verificación.
3. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si el campo de indicativo o de cuadrado de cuadrícula está vacío cuando marca la casilla, aparecerá un diálogo de advertencia y la casilla se desmarcará. Complete ambos campos primero y luego vuelva a intentarlo.
4. La configuración se guarda en `FreeDvAutoReport`.

### Campo de indicativo

- El campo **Callsign:** (`FreeDvMyCallsign`) establece el indicativo que se notifica al mapa público.
- Cuando **Use radio** está marcado (predeterminado), el campo se rellena automáticamente desde el indicativo configurado en la radio y se bloquea como solo lectura. El campo se actualiza automáticamente si cambia el indicativo en Radio Setup.
- Desmarque **Use radio** para escribir un indicativo manualmente. El valor se guarda en `FreeDvMyCallsign` y se convierte a mayúsculas al salir.
- **Use radio** se guarda en `FreeDvUseRadioCallsign`.

### Campo de cuadrado de cuadrícula

- El campo **Grid Square:** (`FreeDvMyGrid`) establece el localizador Maidenhead que se notifica al mapa público.
- En modelos de radio con hardware GPS, aparece una casilla **Use GPS**. Cuando está marcada (predeterminado), el campo se rellena automáticamente desde el módulo GPS de la radio y se bloquea como solo lectura.
- Desmarque **Use GPS** para escribir un cuadrado de cuadrícula manualmente. El valor se guarda en `FreeDvMyGrid` y se convierte a mayúsculas al salir.
- **Use GPS** se guarda en `FreeDvUseGpsGrid`. La casilla está oculta en modelos de radio que no tienen hardware GPS.

### Mensaje de estación

- El campo opcional **Station Msg:** (`FreeDvMyMessage`) acepta texto libre que aparece junto a su indicativo en el mapa público de FreeDV Reporter. Déjelo en blanco si no tiene nada que añadir.

## Cambio del valor predeterminado de Auto Mode en v0.9.5.1

El interruptor **Auto Mode:** en la pestaña **Display** ahora tiene como valor predeterminado **Enabled** para instalaciones nuevas. Si está actualizando desde una versión anterior y `SpotsAutoMode` no se había establecido previamente, AetherSDR lo tratará como habilitado después de la actualización. Para deshabilitarlo, abra la pestaña **Display** y haga clic en **Auto Mode:** hasta que muestre **Disabled**.

## Spot Lines (nuevo en v0.9.7)

El interruptor **Spot Lines:** en la pestaña **Display** controla si se dibujan líneas verticales desde la línea base del espectro hasta cada etiqueta de spot en el panadapter. La configuración se guarda en `IsSpotsLinesEnabled` y tiene el valor predeterminado **Enabled**.

Para desactivar las líneas de spot:

1. Abra SpotHub: `Settings > SpotHub...`
2. Haga clic en la pestaña **Display**.
3. Haga clic en **Spot Lines:** hasta que muestre **Disabled**.

Desactivar las líneas de spot reduce el desorden visual durante concursos o cuando la densidad de spots es alta.

## Sintonización desde la lista de spots (actualizado en v0.9.7)

Hacer doble clic en una fila de la pestaña **Spot List** sintoniza el receptor activo a la frecuencia de ese spot. A partir de v0.9.7, AetherSDR también pasa la sugerencia de modo del spot al receptor, por lo que el modo (por ejemplo, CW o SSB) cambia automáticamente para coincidir con el spot en lugar de solo cambiar la frecuencia.

## Consejos

- Si todos los colores por fuente son demasiado sutiles para distinguirlos, use **Override Colors:** en la pestaña **Display** para forzar un solo color de texto en todas las fuentes, guardado en `IsSpotsOverrideColorsEnabled`.
- La coloración por DXCC (habilitada con **DXCC Coloring** en la pestaña **Display**) puede anular los colores por fuente para indicar el estado trabajado, confirmado o necesario. Si los colores de sus spots no aparecen como se configuraron, verifique si `DxccColoringEnabled` está activo.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Iniciar el listener UDP de WSJT-X y filtrar por CQ, POTA o llamadas a mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Consultar activaciones POTA](poll-pota-activations.md)
- [Habilitar el WebSocket del reportero de QSO FreeDV](enable-freedv-qso-reporter-websocket.md)
- [Habilitar la coloración DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md)
- [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los spots](tune-spot-density-position-font-size-and-lifetime.md)
<!-- docmesh:llm version=v0.9.7 date=2026-05-03 -->
