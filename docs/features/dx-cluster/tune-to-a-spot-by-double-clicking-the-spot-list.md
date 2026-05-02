# Sintonizar una señal haciendo doble clic en la lista de spots

La pestaña "Spot List" en SpotHub muestra todos los spots activos de todas las fuentes conectadas en una tabla ordenable. Al hacer doble clic en una fila, se sintoniza el VFO activo a la frecuencia de ese spot.

## Antes de comenzar

- Al menos una fuente de spots (DX Cluster, RBN, WSJT-X, SpotCollector, POTA o FreeDV) debe estar conectada y recibiendo spots.
- El radio debe estar conectado a AetherSDR.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña "Spot List".
3. Opcionalmente, use las casillas "Bands:" para filtrar la tabla por banda. Desmarque las bandas que no desee ver.
4. Haga clic en el encabezado de una columna para ordenar la tabla por esa columna. Las columnas son: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band, Source.
5. Haga doble clic en cualquier fila de la tabla de spots. AetherSDR sintoniza el VFO activo a la frecuencia mostrada en esa fila.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Bands: | Casillas por banda. Desmarque una banda para ocultar sus spots de la tabla. | — |
| Clear | Elimina todos los spots que se muestran actualmente en la tabla. | — |
| Spot table | Tabla ordenable de todos los spots activos. Haga doble clic en una fila para sintonizar. Columnas: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band, Source. | — |
| Auto Mode: | Selecciona automáticamente la densidad de spots según el nivel de zoom. Habilitado por defecto. | `SpotAutoSwitchMode` |
| Enable FreeDV Reporter reporting when RADE is active | Habilita el reporte de la estación al mapa público de FreeDV Reporter (qso.freedv.org) siempre que el módem RADE esté activo. Requiere un indicativo y un cuadrado de localizador válidos; si alguno de los campos está en blanco o no se puede resolver, la casilla no se activa y muestra una advertencia. | `FreeDvAutoReport` |
| Callsign: (FreeDV Reporter) | Indicativo que se reporta al mapa de FreeDV Reporter. Solo lectura cuando "Use radio" está marcado. Si "Use radio" está marcado, el campo se actualiza automáticamente si el indicativo cambia en Radio Setup. | `FreeDvMyCallsign` |
| Use radio (callsign) | Completa automáticamente el campo de indicativo con el indicativo configurado en el radio y bloquea el campo en solo lectura. | `FreeDvUseRadioCallsign` |
| Grid Square: (FreeDV Reporter) | Cuadrado Maidenhead que se reporta. Solo lectura cuando "Use GPS" está marcado. | `FreeDvMyGrid` |
| Use GPS (grid) | Completa automáticamente el campo de localizador con el módulo GPS del radio y bloquea el campo en solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. | `FreeDvUseGpsGrid` |
| Station Msg: (FreeDV Reporter) | Mensaje de texto libre opcional que se muestra junto al indicativo en el mapa público de FreeDV Reporter. | `FreeDvMyMessage` |

## Habilitar la transmisión a FreeDV Reporter

La casilla "Enable FreeDV Reporter reporting when RADE is active" transmite la actividad de su estación al mapa público de la comunidad en qso.freedv.org. Debido a que el mapa es compartido, AetherSDR valida su configuración antes de habilitarla:

1. Abra `Settings > SpotHub...` y haga clic en la pestaña "FreeDV".
2. En el grupo "Station Reporting", configure su indicativo y cuadrado de localizador:
   - Si "Use radio" está marcado, el indicativo se lee del radio. Si el radio no tiene ningún indicativo configurado, ingréselo manualmente después de desmarcar "Use radio".
   - Si "Use GPS" se muestra y está marcado, el localizador se lee del módulo GPS del radio. De lo contrario, escriba un cuadrado Maidenhead válido (por ejemplo, `EM72`) en el campo "Grid Square:".
3. Opcionalmente, ingrese un mensaje breve en "Station Msg:" para mostrarlo junto a su indicativo en el mapa.
4. Marque "Enable FreeDV Reporter reporting when RADE is active".
   - Si el indicativo o el cuadrado de localizador no pueden resolverse a un valor no vacío, AetherSDR muestra un cuadro de diálogo de advertencia y deja la casilla desmarcada. Corrija el campo faltante e inténtelo de nuevo.
5. AetherSDR comienza a reportar automáticamente siempre que el módem RADE esté activo.

> **Nota:** Esta función requiere una compilación con `HAVE_WEBSOCKETS` habilitado. En Windows, `HAVE_RADE` también debe estar presente en la compilación para evitar errores de compilación.

## Consejos

- Ordene por "Freq (kHz)" para encontrar spots cercanos a su frecuencia actual.
- Ordene por "Band" para agrupar todos los spots de una banda determinada antes de hacer doble clic.
- Los spots se agregan del más reciente al más antiguo; la tabla conserva un máximo de los spots más recientes de todas las fuentes.
- Ocultar bandas con las casillas "Bands:" afecta solo la vista de la lista de spots, no la superposición del panadapter.
- "Auto Mode:" está habilitado por defecto. Si la densidad de spots en el panadapter se ve saturada con un nivel de zoom amplio, intente deshabilitarlo y ajuste el control deslizante "Levels:" manualmente.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Conectarse a un DX cluster](../../getting-started/setup/connect-to-a-dx-cluster.md)
- [Conectarse a la Reverse Beacon Network](../../getting-started/setup/connect-to-the-reverse-beacon-network.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Consultar activaciones de POTA](poll-pota-activations.md)
- [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los spots](tune-spot-density-position-font-size-and-lifetime.md)
