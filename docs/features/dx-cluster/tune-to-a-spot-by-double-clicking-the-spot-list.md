# Sintonizar una Etiqueta Haciendo Doble Clic en la Lista de Etiquetas

La pestaña Spot List en SpotHub muestra todas las etiquetas en vivo de todas las fuentes activas en una única tabla ordenable. Al hacer doble clic en una fila, se sintoniza el VFO activo a la frecuencia de esa etiqueta.

## Antes de comenzar

- Al menos una fuente de etiquetas (DX Cluster, RBN, WSJT-X, SpotCollector, POTA o FreeDV) debe estar conectada y recibiendo etiquetas.
- La radio debe estar conectada a AetherSDR.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña "Spot List".
3. Opcionalmente, use las casillas de verificación "Bands:" para filtrar la tabla por banda. Desmarque cualquier banda que no desee ver.
4. Haga clic en el encabezado de una columna para ordenar la tabla por esa columna. Las columnas son: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band, Source.
5. Haga doble clic en cualquier fila de la tabla de etiquetas. AetherSDR sintoniza el VFO activo a la frecuencia que se muestra en esa fila.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Bands: | Casillas de verificación por banda. Desmarque una banda para ocultar sus etiquetas de la tabla. | — |
| Clear | Elimina todas las etiquetas actualmente mostradas en la tabla. | — |
| Spot table | Tabla ordenable de todas las etiquetas en vivo. Haga doble clic en una fila para sintonizar. Columnas: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band, Source. | — |
| Enable FreeDV Reporter reporting when RADE is active | Habilita el informe de estación al mapa público de FreeDV Reporter (qso.freedv.org) siempre que el módem RADE esté activo. Requiere un indicativo válido y un cuadro de red; si alguno de los campos está en blanco o no se puede resolver, la casilla se niega a habilitarse y muestra una advertencia. | `FreeDvAutoReport` |
| Callsign: (FreeDV Reporter) | Indicativo para informar al mapa de FreeDV Reporter. Solo lectura cuando "Use radio" está marcado. Cuando "Use radio" está marcado, el campo se actualiza automáticamente si el indicativo cambia en Radio Setup. | `FreeDvMyCallsign` |
| Use radio (callsign) | Rellena previamente el campo de indicativo desde el indicativo configurado de la radio y bloquea el campo como solo lectura. | `FreeDvUseRadioCallsign` |
| Grid Square: (FreeDV Reporter) | Cuadro de red Maidenhead para informar. Solo lectura cuando "Use GPS" está marcado. | `FreeDvMyGrid` |
| Use GPS (grid) | Rellena previamente el campo de red desde el módulo GPS de la radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. | `FreeDvUseGpsGrid` |
| Station Msg: (FreeDV Reporter) | Mensaje de texto libre opcional que se muestra junto al indicativo en el mapa público de FreeDV Reporter. | `FreeDvMyMessage` |

## Habilitar la transmisión de FreeDV Reporter

La casilla de verificación "Enable FreeDV Reporter reporting when RADE is active" transmite la actividad de su estación al mapa comunitario público en qso.freedv.org. Debido a que el mapa se comparte, AetherSDR valida su configuración antes de habilitarlo:

1. Abra `Settings > SpotHub...` y haga clic en la pestaña "FreeDV".
2. En el grupo "Station Reporting", establezca su indicativo y cuadro de red:
   - Si "Use radio" está marcado, el indicativo se lee desde la radio. Si la radio no tiene un indicativo configurado, ingrese uno manualmente después de desmarcar "Use radio".
   - Si "Use GPS" se muestra y está marcado, el cuadro se lee desde el módulo GPS de la radio. De lo contrario, escriba un cuadro de red Maidenhead válido (por ejemplo, `EM72`) en el campo "Grid Square:".
3. Opcionalmente, ingrese un mensaje corto en "Station Msg:" para mostrar junto a su indicativo en el mapa.
4. Marque "Enable FreeDV Reporter reporting when RADE is active".
   - Si no se puede resolver el indicativo o el cuadro de red a un valor no en blanco, AetherSDR muestra un diálogo de advertencia y deja la casilla desmarcada. Corrija el campo faltante e intente nuevamente.
5. AetherSDR comienza a informar automáticamente siempre que el módem RADE esté activo.

> **Nota:** Esta función requiere una compilación con `HAVE_WEBSOCKETS` habilitado. En Windows, `HAVE_RADE` también debe estar presente en la compilación para evitar errores de compilación.

## Consejos

- Ordene por "Freq (kHz)" para encontrar etiquetas cerca de su frecuencia actual.
- Ordene por "Band" para agrupar todas las etiquetas en una banda determinada antes de hacer doble clic.
- Las etiquetas se agregan primero las más nuevas; la tabla contiene un máximo de las etiquetas más recientes en todas las fuentes.
- Ocultar bandas con las casillas de verificación "Bands:" afecta solo la vista de Spot List, no la superposición del panadapter.

## Relacionado

- [Descripción general de SpotHub](overview.md)
- [Conectar a un cluster DX](../../getting-started/setup/connect-to-a-dx-cluster.md)
- [Conectar a la Red de Faros Inversos](../../getting-started/setup/connect-to-the-reverse-beacon-network.md)
- [Iniciar el escucha UDP de WSJT-X y filtrar por CQ, POTA o llamadas hacia mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Sondear activaciones de POTA](poll-pota-activations.md)
- [Ajustar la densidad de etiquetas, posición, tamaño de fuente y duración](tune-spot-density-position-font-size-and-lifetime.md)
