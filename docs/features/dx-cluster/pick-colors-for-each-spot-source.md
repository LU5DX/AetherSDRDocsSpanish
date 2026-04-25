# Seleccionar colores para cada fuente de spots

AetherSDR puede mostrar spots de hasta seis fuentes simultáneamente. Asignar un color distinto a cada fuente facilita identificarlas en el panadapter de un vistazo.

## Antes de comenzar

- Abra SpotHub: `Settings > SpotHub...`
- Al menos una fuente de spots debe estar configurada para poder ver el efecto del color elegido.

## Pasos

### Color de spots del clúster DX

1. En SpotHub, haga clic en la pestaña **Cluster**.
2. Haga clic en el botón **Spot Color:**.
3. Elija un color en el selector de color que se abre y confirme la selección.
4. El nuevo color se guarda en `ClusterSpotColor` y se aplica de inmediato a los spots del clúster en el panadapter.

### Color de spots de RBN

1. Haga clic en la pestaña **RBN**.
2. Haga clic en el botón **Spot Color:**.
3. Elija un color y confírmelo.
4. Se guarda en `RbnSpotColor`.

### Colores de spots de WSJT-X

WSJT-X admite cuatro colores independientes, uno por categoría de decodificación.

1. Haga clic en la pestaña **WSJT-X**.
2. Haga clic en el botón de color correspondiente a cada categoría que desee cambiar:
   - **CQ color** — spots decodificados como llamadas CQ. Se guarda en `WsjtxColorCQ`.
   - **POTA color** — spots decodificados como llamadas CQ POTA. Se guarda en `WsjtxColorPOTA`.
   - **Calling Me color** — decodificaciones dirigidas a su indicativo. Se guarda en `WsjtxColorCallingMe`.
   - **Default color** — todas las demás decodificaciones de WSJT-X. Se guarda en `WsjtxColorDefault`.
3. Confirme cada color en el selector de color antes de pasar al siguiente.

### Color de spots de POTA

1. Haga clic en la pestaña **POTA**.
2. Haga clic en el botón **Spot Color:**.
3. Elija un color y confírmelo.
4. Se guarda en `PotaSpotColor`.

### Color de spots de FreeDV

1. Haga clic en la pestaña **FreeDV**.
2. Haga clic en el botón **Spot Color:**.
3. Elija un color y confírmelo.
4. Se guarda en `FreeDvSpotColor`.

> **Nota:** La pestaña FreeDV solo está disponible si AetherSDR fue compilado con soporte WebSocket.

### SpotCollector

SpotCollector no dispone de un selector de color de spots dedicado en SpotHub. Consulte las opciones de la pestaña Display a continuación si necesita un color uniforme que reemplace al de todas las fuentes.

## Qué hace cada control

| Control | Pestaña | Ajuste guardado | Propósito |
|---|---|---|---|
| **Spot Color:** | Cluster | `ClusterSpotColor` | Color para todos los spots recibidos desde el feed telnet del clúster DX. |
| **Spot Color:** | RBN | `RbnSpotColor` | Color para todos los spots recibidos desde la Reverse Beacon Network. |
| **CQ color** | WSJT-X | `WsjtxColorCQ` | Color para las decodificaciones de WSJT-X que son llamadas CQ. |
| **POTA color** | WSJT-X | `WsjtxColorPOTA` | Color para las decodificaciones de WSJT-X que son llamadas CQ POTA. |
| **Calling Me color** | WSJT-X | `WsjtxColorCallingMe` | Color para las decodificaciones de WSJT-X dirigidas a su indicativo. |
| **Default color** | WSJT-X | `WsjtxColorDefault` | Color para todas las demás decodificaciones de WSJT-X. |
| **Spot Color:** | POTA | `PotaSpotColor` | Color para los spots recibidos desde el feed de activaciones de POTA. |
| **Spot Color:** | FreeDV | `FreeDvSpotColor` | Color para los spots recibidos desde el reportador de QSO de FreeDV. |

## Consejos

- Si todos los colores por fuente son demasiado similares para distinguirlos, use **Override Colors:** en la pestaña **Display** para forzar un único color de texto en todas las fuentes; se guarda en `IsSpotsOverrideColorsEnabled` y `SpotsOverrideColor`.
- El coloreado DXCC (habilitado con **DXCC Coloring** en la pestaña **Display**) puede reemplazar los colores por fuente para indicar el estado de trabajado, confirmado o necesario. Si los colores de sus spots no aparecen como los configuró, verifique si `DxccColoringEnabled` está activo.

## Relacionado

- [Descripción general de SpotHub](overview.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas a su indicativo](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Consultar activaciones de POTA](poll-pota-activations.md)
- [Habilitar el WebSocket del reportador de QSO de FreeDV](enable-freedv-qso-reporter-websocket.md)
- [Habilitar el coloreado DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
