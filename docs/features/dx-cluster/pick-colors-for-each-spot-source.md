# Elegir colores para cada fuente de spots

AetherSDR puede mostrar spots de hasta seis fuentes simultáneamente. Asignar un color distinto a cada fuente facilita identificarlas en el panadapter de un vistazo.

## Antes de comenzar

- Abra SpotHub: `Settings > SpotHub...`
- Al menos una fuente de spots debe estar configurada para poder ver el efecto de su elección de color.

## Pasos

### Color de spots del clúster DX

1. En SpotHub, haga clic en la pestaña **Cluster**.
2. Haga clic en el botón **Spot Color:**.
3. Elija un color en el selector de color que se abre y confirme su selección.
4. El nuevo color se guarda en `ClusterSpotColor` y se aplica inmediatamente a los spots del clúster en el panadapter.

### Color de spots de RBN

1. Haga clic en la pestaña **RBN**.
2. Haga clic en el botón **Spot Color:**.
3. Elija un color y confirme.
4. Se guarda en `RbnSpotColor`.

### Colores de spots de WSJT-X

WSJT-X admite cuatro colores separados, uno por categoría de decodificación.

1. Haga clic en la pestaña **WSJT-X**.
2. Haga clic en el botón de color para cada categoría que desee cambiar:
   - **CQ color** — spots decodificados como llamadas CQ. Se guarda en `WsjtxColorCQ`.
   - **POTA color** — spots decodificados como llamadas CQ POTA. Se guarda en `WsjtxColorPOTA`.
   - **Calling Me color** — decodificaciones dirigidas a su indicativo. Se guarda en `WsjtxColorCallingMe`.
   - **Default color** — todas las demás decodificaciones de WSJT-X. Se guarda en `WsjtxColorDefault`.
3. Confirme cada color en el selector de color antes de pasar al siguiente.

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

> **Nota:** La pestaña FreeDV solo está presente si AetherSDR fue compilado con soporte para WebSocket.

### SpotCollector

SpotCollector no cuenta con un selector de color de spots dedicado en SpotHub. Consulte las opciones de la pestaña Display a continuación si necesita un color uniforme que reemplace el de todas las fuentes.

## Qué hace cada control

| Control | Pestaña | Configuración guardada |
|---|---|---|
| **Spot Color:** | Cluster | `ClusterSpotColor` |
| **Spot Color:** | RBN | `RbnSpotColor` |
| **CQ color** | WSJT-X | `WsjtxColorCQ` |
| **POTA color** | WSJT-X | `WsjtxColorPOTA` |
| **Calling Me color** | WSJT-X | `WsjtxColorCallingMe` |
| **Default color** | WSJT-X | `WsjtxColorDefault` |
| **Spot Color:** | POTA | `PotaSpotColor` |
| **Spot Color:** | FreeDV | `FreeDvSpotColor` |
| **Enable FreeDV Reporter reporting when RADE is active** | FreeDV | `FreeDvAutoReport` |
| **Callsign:** | FreeDV — Station Reporting | `FreeDvMyCallsign` |
| **Use radio (callsign)** | FreeDV — Station Reporting | `FreeDvUseRadioCallsign` |
| **Grid Square:** | FreeDV — Station Reporting | `FreeDvMyGrid` |
| **Use GPS (grid)** | FreeDV — Station Reporting | `FreeDvUseGpsGrid` |
| **Station Msg:** | FreeDV — Station Reporting | `FreeDvMyMessage` |

## FreeDV Reporter — Station Reporting

La versión v0.9.3 añade un grupo **Station Reporting** dentro de la pestaña **FreeDV**. Cuando está habilitado, AetherSDR transmite la actividad de su estación al mapa público de FreeDV Reporter en qso.freedv.org cada vez que el módem RADE está activo.

> **Nota:** Station Reporting solo está disponible si AetherSDR fue compilado con soporte para WebSocket (`HAVE_WEBSOCKETS`). En las compilaciones para Windows, además requiere `HAVE_RADE`.

### Habilitar el reporte

1. Haga clic en la pestaña **FreeDV** en SpotHub.
2. En el grupo **Station Reporting**, ingrese un indicativo válido y un localizador de cuadrícula (véase más adelante) antes de activar la casilla de verificación.
3. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si el campo del indicativo o el de la cuadrícula está vacío al marcar la casilla, aparece un diálogo de advertencia y la casilla vuelve a desmarcarse. Complete ambos campos primero y vuelva a intentarlo.
4. La configuración se guarda en `FreeDvAutoReport`.

### Campo Callsign

- El campo **Callsign:** (`FreeDvMyCallsign`) define el indicativo que se reporta al mapa público.
- Cuando **Use radio** está marcado (valor predeterminado), el campo se completa automáticamente con el indicativo configurado en el radio y queda bloqueado en modo de solo lectura. El campo se actualiza automáticamente si cambia el indicativo en Radio Setup.
- Desmarque **Use radio** para escribir un indicativo manualmente. El valor se guarda en `FreeDvMyCallsign` y se convierte a mayúsculas al salir.
- **Use radio** se guarda en `FreeDvUseRadioCallsign`.

### Campo Grid Square

- El campo **Grid Square:** (`FreeDvMyGrid`) define el localizador Maidenhead que se reporta al mapa público.
- En modelos de radio con hardware GPS, aparece una casilla **Use GPS**. Cuando está marcada (valor predeterminado), el campo se completa automáticamente con los datos del módulo GPS del radio y queda bloqueado en modo de solo lectura.
- Desmarque **Use GPS** para escribir un localizador de cuadrícula manualmente. El valor se guarda en `FreeDvMyGrid` y se convierte a mayúsculas al salir.
- **Use GPS** se guarda en `FreeDvUseGpsGrid`. La casilla está oculta en modelos de radio que no tienen hardware GPS.

### Mensaje de estación

- El campo opcional **Station Msg:** (`FreeDvMyMessage`) acepta texto libre que aparece junto a su indicativo en el mapa público de FreeDV Reporter. Déjelo en blanco si no tiene nada que agregar.

## Cambio en el valor predeterminado de Auto Mode en v0.9.5.1

El botón **Auto Mode:** en la pestaña **Display** ahora tiene como valor predeterminado **Enabled** en las instalaciones nuevas. Si está actualizando desde una versión anterior y `SpotAutoSwitchMode` no había sido configurado previamente, AetherSDR lo tratará como habilitado tras la actualización. Para desactivarlo, abra la pestaña **Display** y haga clic en **Auto Mode:** hasta que muestre **Disabled**.

## Consejos

- Si todos los colores por fuente son demasiado similares para distinguirlos, use **Override Colors:** en la pestaña **Display** para forzar un único color de texto en todas las fuentes; se guarda en `IsSpotsOverrideColorsEnabled` y `SpotsOverrideColor`.
- El coloreado por DXCC (habilitado con **DXCC Coloring** en la pestaña **Display**) puede reemplazar los colores por fuente para indicar el estado de trabajado, confirmado o pendiente. Si sus colores de spots no aparecen como los configuró, compruebe si `DxccColoringEnabled` está activo.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Consultar activaciones de POTA](poll-pota-activations.md)
- [Habilitar el WebSocket del reportador de QSO de FreeDV](enable-freedv-qso-reporter-websocket.md)
- [Habilitar el coloreado por DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md)
- [Ajustar la densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
