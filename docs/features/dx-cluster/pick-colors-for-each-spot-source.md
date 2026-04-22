# Elegir colores para cada fuente de spots

AetherSDR puede mostrar spots de varias fuentes independientes en el panadapter. Esta página explica cómo asignar un color distinto a cada fuente para distinguirlas de un vistazo.

## Antes de comenzar

- Abra AetherSDR.
- Al menos una fuente de spots (clúster DX, RBN, WSJT-X, POTA, FreeDV) debe estar ya configurada. Los colores pueden establecerse antes o después de que una fuente esté conectada.

## Pasos

1. Haga clic en `Settings > SpotHub...` para abrir el diálogo SpotHub.
2. Para establecer el color de los **spots del clúster DX**, haga clic en la pestaña **Cluster** y luego en **Spot Color:**. Elija un color en el selector de colores y confirme.
3. Para establecer el color de los **spots de RBN**, haga clic en la pestaña **RBN** y luego en **Spot Color:**. Elija un color y confirme.
4. Para establecer los colores de los **spots de WSJT-X**, haga clic en la pestaña **WSJT-X**. Hay cuatro selectores de color disponibles:
   - Haga clic en **CQ color** para establecer el color de los spots CQ. Se guarda como `WsjtxColorCQ`.
   - Haga clic en **POTA color** para establecer el color de los spots CQ POTA. Se guarda como `WsjtxColorPOTA`.
   - Haga clic en **Calling Me color** para establecer el color de los decodificados dirigidos a su indicativo. Se guarda como `WsjtxColorCallingMe`.
   - Haga clic en **Default color** para establecer el color de todos los demás spots de WSJT-X. Se guarda como `WsjtxColorDefault`.
5. Para establecer el color de los **spots de POTA**, haga clic en la pestaña **POTA** y luego en **Spot Color:**. Elija un color y confirme.
6. Para establecer el color de los **spots de FreeDV**, haga clic en la pestaña **FreeDV** y luego en **Spot Color:**. Elija un color y confirme.

## Qué hace cada control

| Control | Pestaña | Descripción | Clave de configuración |
|---|---|---|---|
| Spot Color: | Cluster | Color aplicado a todos los spots de la fuente telnet del clúster DX. | `ClusterSpotColor` |
| Spot Color: | RBN | Color aplicado a todos los spots de la Red de Balizas Inversas (Reverse Beacon Network). | `RbnSpotColor` |
| CQ color | WSJT-X | Color para los spots de WSJT-X que coinciden con el filtro CQ. | `WsjtxColorCQ` |
| POTA color | WSJT-X | Color para los spots de WSJT-X que coinciden con el filtro CQ POTA. | `WsjtxColorPOTA` |
| Calling Me color | WSJT-X | Color para los decodificados de WSJT-X dirigidos a su indicativo. | `WsjtxColorCallingMe` |
| Default color | WSJT-X | Color para todos los demás spots de WSJT-X que no coinciden con ningún filtro. | `WsjtxColorDefault` |
| Spot Color: | POTA | Color aplicado a todos los spots del feed de activaciones POTA. | `PotaSpotColor` |
| Spot Color: | FreeDV | Color aplicado a todos los spots del reportador de QSO de FreeDV. | `FreeDvSpotColor` |

## Consejos

- La pestaña **Display** ofrece anulaciones globales. Si **Override Colors:** está activado, el color de anulación único reemplaza todos los colores por fuente en el panadapter. Desactívelo para restaurar los colores por fuente.
- La pestaña FreeDV solo está presente en versiones compiladas con soporte WebSocket.
- WSJT-X ofrece cuatro colores distintos porque el mismo flujo UDP puede transportar llamadas CQ, activaciones POTA y contactos dirigidos a su indicativo de forma simultánea. Asignar colores diferentes permite priorizar de un vistazo.

## Relacionado

- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Activar coloración DXCC a partir de un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md)
- [Descripción general de SpotHub](overview.md)
