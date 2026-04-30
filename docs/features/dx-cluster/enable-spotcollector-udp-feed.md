# Habilitar alimentación de UDP de SpotCollector

AetherSDR puede recibir manchas (spots) de DX transmitidas por SpotCollector de Ham Radio Deluxe por UDP y mostrarlas en el panadapter. Esta página explica cómo iniciar el receptor (listener), establecer el puerto correcto y configurarlo para iniciarse automáticamente.

## Antes de comenzar

- SpotCollector debe estar instalado, configurado y ejecutándose en la misma máquina o red local, y configurado para transmitir manchas por UDP.
- Anote el puerto UDP en el que SpotCollector está transmitiendo; deberá ingresarlo en AetherSDR.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **SpotCollector**.
3. Establezca **UDP Port:** al puerto en el que SpotCollector está transmitiendo. Rango válido: 1–65535. Este valor se guarda como `SpotCollectorPort`.
4. Haga clic en **Start**.
5. Confirme que el indicador de estado cambia a **Listening**. Los spots entrantes aparecerán en la consola **SpotCollector Spots** a medida que lleguen.
6. Para que el receptor se inicie automáticamente cada vez que se inicia AetherSDR, habilite **Auto-start on startup**. Se guarda como `SpotCollectorAutoStart`.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| **UDP Port:** | Puerto UDP en el que AetherSDR escucha las transmisiones de SpotCollector. Rango válido: 1–65535. | `SpotCollectorPort` |
| **Start / Stop** | Inicia o detiene el receptor UDP. | — |
| **Auto-start on startup** | Inicia el receptor automáticamente al iniciar. | `SpotCollectorAutoStart` |
| **SpotCollector Spots** | Consola de solo lectura que muestra los spots recibidos de SpotCollector. | — |
| **Enable FreeDV Reporter reporting when RADE is active** | Habilita el reporte de estación al mapa público de FreeDV Reporter (qso.freedv.org) siempre que el módem RADE esté activo. Requiere un indicativo válido y un localizador (grid square) — si alguno de los campos está vacío o no se puede resolver, la casilla se niega a habilitarse y muestra una advertencia. | `FreeDvAutoReport` |
| **Callsign: (FreeDV Reporter)** | Indicativo a reportar al mapa de FreeDV Reporter. De solo lectura cuando **Use radio** está marcado. Cuando **Use radio** está marcado, el campo se rellena del indicativo configurado de la radio y se actualiza automáticamente si ese indicativo cambia. | `FreeDvMyCallsign` |
| **Use radio (callsign)** | Rellena el campo de indicativo del indicativo configurado de la radio y bloquea el campo como de solo lectura. | `FreeDvUseRadioCallsign` |
| **Grid Square: (FreeDV Reporter)** | Localizador Maidenhead a reportar. De solo lectura cuando **Use GPS** está marcado. | `FreeDvMyGrid` |
| **Use GPS (grid)** | Rellena el campo de localizador desde el módulo GPS de la radio y bloquea el campo como de solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. | `FreeDvUseGpsGrid` |
| **Station Msg: (FreeDV Reporter)** | Mensaje de texto libre opcional que se muestra junto al indicativo en el mapa público de FreeDV Reporter. | `FreeDvMyMessage` |

## Reporte a FreeDV Reporter

La pestaña **FreeDV** contiene un grupo **Station Reporting** que controla si AetherSDR transmite la actividad de su estación al mapa público de FreeDV Reporter en qso.freedv.org.

### Requisitos antes de habilitar

- Un indicativo válido debe estar disponible — ya sea de la radio (cuando **Use radio** está marcado) o escrito en el campo **Callsign:**.
- Un localizador Maidenhead válido debe estar disponible — ya sea del módulo GPS de la radio (cuando **Use GPS** está marcado, en hardware compatible) o escrito en el campo **Grid Square:**.

Si alguno de estos valores falta cuando intenta habilitar **Enable FreeDV Reporter reporting when RADE is active**, AetherSDR muestra una advertencia y deja la casilla desmarcada. Esto evita que valores en blanco o de marcador de posición aparezcan en el mapa público compartido.

### Pasos para habilitar el reporte

1. Abra `Settings > SpotHub...` y haga clic en la pestaña **FreeDV**.
2. En el grupo **Station Reporting**, confirme que el campo **Callsign:** muestra su indicativo.
   - Si **Use radio** está marcado, el campo se rellena automáticamente del indicativo configurado de la radio y es de solo lectura. Desmarque **Use radio** para ingresar un indicativo manualmente.
3. Confirme que el campo **Grid Square:** muestra su localizador Maidenhead.
   - En radios con hardware GPS, marque **Use GPS** para rellenarlo automáticamente. Desmarque **Use GPS** para escribir un localizador manualmente.
4. Opcionalmente ingrese un mensaje corto en **Station Msg:** — aparecerá junto a su indicativo en el mapa.
5. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si alguno de los campos de indicativo o localizador está vacío, aparecerá un diálogo de advertencia. Rellene el valor faltante e intente de nuevo.
6. El reporte ahora está activo siempre que el módem RADE esté ejecutándose.

## Consejos

- Los spots recibidos de SpotCollector aparecen junto a spots de otras fuentes en la pestaña **Spot List**. La columna **Source** los identifica.
- Si la superposición de spots en el panadapter no es visible, verifique que **Spots:** esté configurado en **Enabled** en la pestaña **Display**.

## Solución de problemas

- **El estado permanece Stopped / no aparecen spots** — Verifique que SpotCollector esté transmitiendo activamente y que el puerto UDP en AetherSDR coincida con el puerto configurado en SpotCollector. Compruebe que ningún cortafuegos bloquee el tráfico UDP en ese puerto.
- **El receptor se inicia pero el panadapter no muestra spots** — Confirme que la superposición de spots maestro esté activada: abra la pestaña **Display** y verifique que **Spots:** esté **Enabled**.
- **La casilla de FreeDV Reporter se desmarca a sí misma con una advertencia** — El campo de indicativo o localizador está vacío o no se pudo resolver. Rellene ambos campos (o habilite **Use radio** / **Use GPS** si la radio puede proporcionar los valores) antes de habilitar el reporte.

## Relacionado

- [Descripción general de SpotHub](overview.md)
- [Ajustar densidad de spots, posición, tamaño de fuente y duración](tune-spot-density-position-font-size-and-lifetime.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Borrar todos los spots del panadapter](clear-all-spots-from-the-panadapter.md)
