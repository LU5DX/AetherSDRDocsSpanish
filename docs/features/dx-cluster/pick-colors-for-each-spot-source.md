# Asignar colores a cada fuente de spots

AetherSDR puede mostrar spots de hasta seis fuentes simultáneamente. Asignar un color distinto a cada fuente facilita distinguirlas en el panadapter de un vistazo.

## Antes de comenzar

- Abra SpotHub: `Settings > SpotHub...`
- Al menos una fuente de spots debe estar configurada para que pueda ver el efecto de su elección de color.

## Pasos

### Color de spot de DX Cluster

1. En SpotHub, haga clic en la pestaña **Cluster**.
2. Haga clic en el botón **Spot Color:**.
3. Elija un color en el selector de color que se abre y confirme su selección.
4. El nuevo color se guarda en `ClusterSpotColor` y se aplica inmediatamente a los spots de cluster en el panadapter.

### Color de spot de RBN

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

> **Nota:** La pestaña FreeDV solo está presente si AetherSDR fue compilado con soporte WebSocket.

### SpotCollector

SpotCollector no tiene un selector de color de spot dedicado en SpotHub. Consulte las opciones de la pestaña Display a continuación si necesita una anulación uniforme para todas las fuentes.

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

La versión 0.9.3 añade un grupo **Station Reporting** dentro de la pestaña **FreeDV**. Cuando está habilitado, AetherSDR transmite la actividad de su estación al mapa público de FreeDV Reporter en qso.freedv.org cada vez que el módem RADE está activo.

> **Nota:** Station Reporting solo está presente si AetherSDR fue compilado con soporte WebSocket (`HAVE_WEBSOCKETS`). En compilaciones de Windows, además requiere `HAVE_RADE`.

### Habilitar reportes

1. Haga clic en la pestaña **FreeDV** en SpotHub.
2. En el grupo **Station Reporting**, complete un indicativo válido y cuadrícula (véase a continuación) antes de habilitar la casilla de verificación.
3. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si alguno de los campos de indicativo o cuadrícula está en blanco cuando marca la casilla, aparece un diálogo de advertencia y la casilla vuelve a desmarcarse. Complete ambos campos primero e intente de nuevo.
4. La configuración se guarda en `FreeDvAutoReport`.

### Campo de indicativo

- El campo **Callsign:** (`FreeDvMyCallsign`) establece el indicativo reportado al mapa público.
- Cuando **Use radio** está marcado (valor por defecto), el campo se rellena previamente desde el indicativo configurado de la radio y se bloquea como solo lectura. El campo se actualiza automáticamente si cambia el indicativo en Radio Setup.
- Desmarque **Use radio** para escribir un indicativo manualmente. El valor se guarda en `FreeDvMyCallsign` y se convierte a mayúsculas al salir.
- **Use radio** se guarda en `FreeDvUseRadioCallsign`.

### Campo de cuadrícula

- El campo **Grid Square:** (`FreeDvMyGrid`) establece el localizador Maidenhead reportado al mapa público.
- En modelos de radio con hardware GPS, aparece una casilla de verificación **Use GPS**. Cuando está marcada (valor por defecto), el campo se rellena previamente desde el módulo GPS de la radio y se bloquea como solo lectura.
- Desmarque **Use GPS** para escribir una cuadrícula manualmente. El valor se guarda en `FreeDvMyGrid` y se convierte a mayúsculas al salir.
- **Use GPS** se guarda en `FreeDvUseGpsGrid`. La casilla se oculta en modelos de radio que no tienen hardware GPS.

### Mensaje de estación

- El campo opcional **Station Msg:** (`FreeDvMyMessage`) acepta texto libre que aparece junto a su indicativo en el mapa público de FreeDV Reporter. Déjelo en blanco si no tiene nada que añadir.

## Consejos

- Si todos los colores por fuente son demasiado sutiles para distinguir, use **Override Colors:** en la pestaña **Display** para forzar un color de texto único en todas las fuentes, guardado en `IsSpotsOverrideColorsEnabled` y `SpotsOverrideColor`.
- La coloración DXCC (habilitada con **DXCC Coloring** en la pestaña **Display**) puede anular los colores por fuente para indicar estado trabajado, confirmado o necesario. Si sus colores de spots no aparecen como se establece, compruebe si `DxccColoringEnabled` está activo.

## Relacionado

- [Descripción general de SpotHub](overview.md)
- [Iniciar escucha UDP de WSJT-X y filtrar para CQ, POTA o llamadas dirigidas a mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Sondear activaciones de POTA](poll-pota-activations.md)
- [Habilitar WebSocket del reportero de QSO de FreeDV](enable-freedv-qso-reporter-websocket.md)
- [Habilitar coloración DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md)
- [Ajustar densidad, posición, tamaño de fuente y vida útil de spots](tune-spot-density-position-font-size-and-lifetime.md)
