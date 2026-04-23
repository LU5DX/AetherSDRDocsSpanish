# Elegir colores para cada fuente de spots

Cada fuente de spots en SpotHub tiene su propio ajuste de color para que pueda identificar de un vistazo el origen de un spot en el panadapter. Esta página explica cómo configurar el color de spot para cada fuente.

## Antes de comenzar

- Abra AetherSDR con al menos una fuente de spots configurada. Los colores se aplican de inmediato a cualquier spot ya visible.
- La superposición de spots en el panadapter debe estar activa (`IsSpotsEnabled` establecido en Enabled) para que los colores sean visibles. Consulte [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los spots](tune-spot-density-position-font-size-and-lifetime.md) si necesita activarla primero.

## Pasos

1. Vaya a `Settings > SpotHub...` para abrir el diálogo SpotHub.
2. Para establecer el color de los spots del **clúster DX**, haga clic en la pestaña **Cluster** y luego en **Spot Color:**. Elija un color en el selector de color y confirme. La selección se guarda en `ClusterSpotColor`.
3. Para establecer el color de los spots de **RBN**, haga clic en la pestaña **RBN** y luego en **Spot Color:**. Elija un color y confirme. Se guarda en `RbnSpotColor`.
4. Para establecer los colores de spots de **WSJT-X**, haga clic en la pestaña **WSJT-X**. Hay cuatro selectores de color independientes, uno por cada categoría:
   - Haga clic en el botón de color junto a **CQ** para establecer el color de las llamadas CQ. Se guarda en `WsjtxColorCQ`.
   - Haga clic en el botón de color junto a **CQ POTA** para establecer el color de las llamadas POTA. Se guarda en `WsjtxColorPOTA`.
   - Haga clic en el botón de color junto a **Calling Me** para establecer el color de los decodificados dirigidos a su indicativo. Se guarda en `WsjtxColorCallingMe`.
   - Haga clic en el botón de color junto a **Default** para establecer el color de reserva para todos los demás spots de WSJT-X. Se guarda en `WsjtxColorDefault`.
5. Para establecer el color de los spots de **POTA**, haga clic en la pestaña **POTA** y luego en **Spot Color:**. Elija un color y confirme. Se guarda en `PotaSpotColor`.
6. Para establecer el color de los spots de **FreeDV**, haga clic en la pestaña **FreeDV** y luego en **Spot Color:**. Elija un color y confirme. Se guarda en `FreeDvSpotColor`.

## Qué hace cada control

| Control | Pestaña | Ajuste guardado | Descripción |
|---|---|---|---|
| **Spot Color:** | Cluster | `ClusterSpotColor` | Color aplicado a todos los spots recibidos desde la fuente telnet del clúster DX. |
| **Spot Color:** | RBN | `RbnSpotColor` | Color aplicado a todos los spots recibidos desde la Red de Balizas Inversas (Reverse Beacon Network). |
| Botón de color CQ | WSJT-X | `WsjtxColorCQ` | Color para los decodificados de WSJT-X que son llamadas CQ. |
| Botón de color POTA | WSJT-X | `WsjtxColorPOTA` | Color para los decodificados de WSJT-X que son llamadas CQ POTA. |
| Botón de color Calling Me | WSJT-X | `WsjtxColorCallingMe` | Color para los decodificados de WSJT-X dirigidos a su indicativo. |
| Botón de color Default | WSJT-X | `WsjtxColorDefault` | Color de reserva para los decodificados de WSJT-X que no coinciden con ningún filtro activo. |
| **Spot Color:** | POTA | `PotaSpotColor` | Color aplicado a todos los spots provenientes del sondeo de activaciones POTA. |
| **Spot Color:** | FreeDV | `FreeDvSpotColor` | Color aplicado a todos los spots provenientes del WebSocket del reportador de QSO FreeDV. |

## Consejos

- La pestaña **FreeDV** solo está presente en versiones que incluyen soporte WebSocket. Si la pestaña no aparece, su versión no lo incluye.
- Si desea que todos los spots compartan un único color sin importar la fuente, active **Override Colors:** en la pestaña **Display**. Ese ajuste (`IsSpotsOverrideColorsEnabled`) reemplaza todos los colores individuales por fuente.
- El color Default de WSJT-X se aplica únicamente a los spots que no coinciden con ningún filtro habilitado (CQ, CQ POTA o Calling Me). Si no hay filtros marcados, el color Default se usa para todos los spots de WSJT-X.

## Temas relacionados

- [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Iniciar el listener UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Habilitar el coloreado DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md)
- [Sondear activaciones POTA](poll-pota-activations.md)
- [Habilitar el WebSocket del reportador de QSO FreeDV](enable-freedv-qso-reporter-websocket.md)
- [Conectarse a un clúster DX](../../getting-started/setup/connect-to-a-dx-cluster.md)
- [Conectarse a la Red de Balizas Inversas](../../getting-started/setup/connect-to-the-reverse-beacon-network.md)
