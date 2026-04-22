# Elegir colores para cada fuente de spots

AetherSDR puede mostrar spots de múltiples fuentes simultáneamente. Asignar un color distinto a cada fuente le permite distinguirlas de un vistazo en el panadapter.

## Antes de comenzar

- Abra `Settings > SpotHub...` para acceder al diálogo de SpotHub.
- Al menos una fuente de spots debe estar configurada para poder ver el resultado. Los colores surten efecto de inmediato; no se requiere conexión con la radio.

## Pasos

### Spots del DX Cluster

1. Haga clic en `Settings > SpotHub...`.
2. Haga clic en la pestaña **Cluster**.
3. Haga clic en **Spot Color:**.
4. Elija un color en el selector de color que se abre y confírmelo.

El color elegido se guarda en `ClusterSpotColor`.

### Spots de Reverse Beacon Network

1. Haga clic en `Settings > SpotHub...`.
2. Haga clic en la pestaña **RBN**.
3. Haga clic en **Spot Color:** (RBN).
4. Elija un color y confírmelo.

El color elegido se guarda en `RbnSpotColor`.

### Spots de WSJT-X

Los spots de WSJT-X admiten cuatro colores independientes, uno por cada categoría de decodificación.

1. Haga clic en `Settings > SpotHub...`.
2. Haga clic en la pestaña **WSJT-X**.
3. Haga clic en el botón de color de cada categoría que desee cambiar:

   | Botón | Se aplica a | Clave de configuración |
   |---|---|---|
   | CQ color | Llamadas CQ | `WsjtxColorCQ` |
   | POTA color | Llamadas CQ POTA | `WsjtxColorPOTA` |
   | Calling Me color | Decodificaciones dirigidas a su indicativo | `WsjtxColorCallingMe` |
   | Default color | Todas las demás decodificaciones de WSJT-X | `WsjtxColorDefault` |

4. Elija un color y confírmelo para cada botón que haya hecho clic.

### Spots de POTA

1. Haga clic en `Settings > SpotHub...`.
2. Haga clic en la pestaña **POTA**.
3. Haga clic en **Spot Color:** (POTA).
4. Elija un color y confírmelo.

El color elegido se guarda en `PotaSpotColor`.

### Spots de FreeDV

1. Haga clic en `Settings > SpotHub...`.
2. Haga clic en la pestaña **FreeDV**.
3. Haga clic en **Spot Color:** (FreeDV).
4. Elija un color y confírmelo.

El color elegido se guarda en `FreeDvSpotColor`.

## Qué hace cada control

| Control | Pestaña | Qué configura | Clave de configuración |
|---|---|---|---|
| Spot Color: | Cluster | Color para los spots del DX cluster en el panadapter | `ClusterSpotColor` |
| Spot Color: (RBN) | RBN | Color para los spots de RBN en el panadapter | `RbnSpotColor` |
| CQ color | WSJT-X | Color para los spots de decodificaciones CQ | `WsjtxColorCQ` |
| POTA color | WSJT-X | Color para los spots de decodificaciones CQ POTA | `WsjtxColorPOTA` |
| Calling Me color | WSJT-X | Color para las decodificaciones dirigidas a su indicativo | `WsjtxColorCallingMe` |
| Default color | WSJT-X | Color para todas las demás decodificaciones de WSJT-X | `WsjtxColorDefault` |
| Spot Color: (POTA) | POTA | Color para los spots de activaciones POTA | `PotaSpotColor` |
| Spot Color: (FreeDV) | FreeDV | Color para los spots del reportero de QSO de FreeDV | `FreeDvSpotColor` |

## Consejos

- La pestaña **Display** tiene un interruptor **Override Colors:** (`IsSpotsOverrideColorsEnabled`) que fuerza un único color de texto para todos los spots independientemente de la fuente. Si los colores por fuente no parecen tener efecto, verifique que esta anulación no esté activa.
- Si también desea que el fondo del panadapter detrás de las etiquetas de spots sea uniforme, consulte los controles **Override Background** en la pestaña **Display**.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Consultar activaciones POTA](poll-pota-activations.md)
- [Habilitar el WebSocket del reportero de QSO de FreeDV](enable-freedv-qso-reporter-websocket.md)
- [Habilitar coloración DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md)
