# Habilitar la fuente UDP de SpotCollector

AetherSDR puede recibir avisos de DX (spots) transmitidos por SpotCollector de Ham Radio Deluxe a través de UDP y mostrarlos en el panadapter. Esta página explica cómo iniciar el receptor, configurar el puerto correcto y habilitarlo para que arranque automáticamente.

## Antes de comenzar

- SpotCollector debe estar instalado, configurado y en ejecución en la misma máquina o red local, y configurado para transmitir spots por UDP.
- Anote el puerto UDP en el que SpotCollector está transmitiendo — deberá ingresarlo en AetherSDR.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **SpotCollector**.
3. Establezca **UDP Port:** en el puerto en el que SpotCollector está transmitiendo. Rango válido: 1–65535. Este valor se guarda como `SpotCollectorPort`.
4. Haga clic en **Start**.
5. Confirme que el indicador de estado cambia a **Listening**. Los spots entrantes aparecerán en la consola **SpotCollector Spots** a medida que lleguen.
6. Para que el receptor se inicie automáticamente cada vez que AetherSDR arranque, habilite **Auto-start on startup**. Esto se guarda como `SpotCollectorAutoStart`.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| **UDP Port:** | Puerto UDP en el que AetherSDR escucha las transmisiones de SpotCollector. Rango válido: 1–65535. | `SpotCollectorPort` |
| **Start / Stop** | Inicia o detiene el receptor UDP. | — |
| **Auto-start on startup** | Inicia el receptor automáticamente al arrancar. | `SpotCollectorAutoStart` |
| **SpotCollector Spots** | Consola de solo lectura que muestra los spots recibidos de SpotCollector. | — |
| **Enable FreeDV Reporter reporting when RADE is active** | Habilita el reporte de la estación al mapa público FreeDV Reporter (qso.freedv.org) cuando el módem RADE está activo. Requiere un indicativo y un localizador de cuadrícula válidos — si alguno de los dos campos está vacío o no puede resolverse, la casilla se niega a habilitarse y muestra una advertencia. | `FreeDvAutoReport` |
| **Callsign: (FreeDV Reporter)** | Indicativo que se reporta al mapa de FreeDV Reporter. Es de solo lectura cuando **Use radio** está marcado. Con **Use radio** marcado, el campo se completa con el indicativo configurado en la radio y se actualiza automáticamente si dicho indicativo cambia. | `FreeDvMyCallsign` |
| **Use radio (callsign)** | Completa el campo de indicativo con el indicativo configurado en la radio y bloquea el campo como solo lectura. | `FreeDvUseRadioCallsign` |
| **Grid Square: (FreeDV Reporter)** | Cuadrícula Maidenhead que se reporta. Es de solo lectura cuando **Use GPS** está marcado. | `FreeDvMyGrid` |
| **Use GPS (grid)** | Completa el campo de cuadrícula con el módulo GPS de la radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. | `FreeDvUseGpsGrid` |
| **Station Msg: (FreeDV Reporter)** | Mensaje de texto libre opcional que aparece junto al indicativo en el mapa público de FreeDV Reporter. | `FreeDvMyMessage` |

## Reporte a FreeDV Reporter

La pestaña **FreeDV** contiene un grupo **Station Reporting** que controla si AetherSDR transmite la actividad de su estación al mapa público de FreeDV Reporter en qso.freedv.org.

### Requisitos antes de habilitar

- Debe haber un indicativo válido disponible — ya sea proveniente de la radio (cuando **Use radio** está marcado) o escrito manualmente en el campo **Callsign:**.
- Debe haber una cuadrícula Maidenhead válida disponible — ya sea del módulo GPS de la radio (cuando **Use GPS** está marcado, en hardware compatible) o escrita manualmente en el campo **Grid Square:**.

Si alguno de los valores falta al intentar habilitar **Enable FreeDV Reporter reporting when RADE is active**, AetherSDR muestra una advertencia y deja la casilla sin marcar. Esto evita que valores vacíos o de marcador de posición aparezcan en el mapa público compartido.

### Pasos para habilitar el reporte

1. Abra `Settings > SpotHub...` y haga clic en la pestaña **FreeDV**.
2. En el grupo **Station Reporting**, confirme que el campo **Callsign:** muestra su indicativo.
   - Si **Use radio** está marcado, el campo se completa automáticamente con el indicativo configurado en la radio y es de solo lectura. Desmarque **Use radio** para ingresar un indicativo manualmente.
3. Confirme que el campo **Grid Square:** muestra su localizador Maidenhead.
   - En radios con hardware GPS, marque **Use GPS** para completarlo automáticamente. Desmarque **Use GPS** para escribir una cuadrícula manualmente.
4. Opcionalmente, ingrese un mensaje breve en **Station Msg:** — aparecerá junto a su indicativo en el mapa.
5. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si el indicativo o la cuadrícula están vacíos, aparece un cuadro de diálogo de advertencia. Complete el valor faltante y vuelva a intentarlo.
6. El reporte estará activo siempre que el módem RADE esté en funcionamiento.

## Cambio en el valor predeterminado de Auto Mode

A partir de la versión v0.9.5.1, **Auto Mode:** (`SpotAutoSwitchMode`) tiene como valor predeterminado **Enabled** en nuevas instalaciones. Si está actualizando y desea conservar el comportamiento anterior, abra la pestaña **Display** y establezca **Auto Mode:** en **Disabled**.

## Consejos

- Los spots recibidos de SpotCollector aparecen junto a los spots de otras fuentes en la pestaña **Spot List**. La columna **Source** los identifica.
- Si la superposición de spots en el panadapter no es visible, verifique que **Spots:** esté configurado en **Enabled** en la pestaña **Display**.

## Solución de problemas

- **El estado permanece en Stopped / no aparecen spots** — Verifique que SpotCollector esté transmitiendo activamente y que el puerto UDP en AetherSDR coincida con el puerto configurado en SpotCollector. Compruebe que ningún firewall esté bloqueando el tráfico UDP en ese puerto.
- **El receptor inicia pero el panadapter no muestra spots** — Confirme que la superposición principal de spots esté activa: abra la pestaña **Display** y verifique que **Spots:** esté en **Enabled**.
- **La casilla de FreeDV Reporter se desmarca sola con una advertencia** — El campo de indicativo o de cuadrícula está vacío o no pudo resolverse. Complete ambos campos (o habilite **Use radio** / **Use GPS** si la radio puede proveer los valores) antes de habilitar el reporte.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Ajustar la densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Borrar todos los spots del panadapter](clear-all-spots-from-the-panadapter.md)
