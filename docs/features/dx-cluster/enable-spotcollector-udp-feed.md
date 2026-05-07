# Habilitar alimentación UDP de SpotCollector

AetherSDR puede recibir spots de DX transmitidos por SpotCollector de Ham Radio Deluxe a través de UDP y mostrarlos en el panadapter. Esta página explica cómo iniciar el listener, configurar el puerto correcto y hacer que se inicie automáticamente.

## Antes de comenzar

- SpotCollector debe estar instalado, configurado y ejecutándose en el mismo equipo o red local, y configurado para transmitir spots a través de UDP.
- Anote el puerto UDP en el que SpotCollector está transmitiendo; deberá ingresarlo en AetherSDR.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **SpotCollector**.
3. Establezca **UDP Port:** en el puerto en el que SpotCollector está transmitiendo. Rango válido: 1–65535. Este valor se guarda como `SpotCollectorPort`.
4. Haga clic en **Start**.
5. Confirme que el indicador de estado cambia a **Listening**. Los spots entrantes aparecerán en la consola **SpotCollector Spots** a medida que lleguen.
6. Para que el listener se inicie automáticamente cada vez que se lance AetherSDR, habilite **Auto-start on startup**. Esto se guarda como `SpotCollectorAutoStart`.

## Qué hace cada control
| Control                                                  | Descripción                                                                                                                                                                                                                                                  | Clave de configuración                                                                        |
|----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| **UDP Port:**                                            | Puerto UDP en el que AetherSDR escucha las transmisiones de SpotCollector. Rango válido: 1–65535.                                                                                                                                                            | `SpotCollectorPort`                                                                           |
| **Start / Stop**                                         | Inicia o detiene el listener UDP.                                                                                                                                                                                                                            | —                                                                                             |
| **Auto-start on startup**                                | Inicia el listener automáticamente al inicio.                                                                                                                                                                                                                 | `SpotCollectorAutoStart`                                                                      |
| **SpotCollector Spots**                                  | Consola de solo lectura que muestra los spots recibidos de SpotCollector.                                                                                                                                                                                                 | —                                                                                             |
| **Enable FreeDV Reporter reporting when RADE is active** | Habilita el informe de estación al mapa público de FreeDV Reporter (qso.freedv.org) siempre que el módem RADE esté activo. Requiere un indicativo y un cuadrado de cuadrícula válidos; si alguno de estos campos está en blanco o no se puede resolver, la casilla se niega a habilitarse y muestra una advertencia. | `FreeDvAutoReport`                                                                            |
| **Callsign: (FreeDV Reporter)**                          | Indicativo para informar al mapa de FreeDV Reporter. De solo lectura cuando **Use radio** está marcado. Cuando **Use radio** está marcado, el campo se completa desde el indicativo configurado en la radio y se actualiza automáticamente si ese indicativo cambia.                       | `FreeDvMyCallsign`                                                                            |
| **Use radio (callsign)**                                 | Precarga el campo de indicativo desde el indicativo configurado en la radio y bloquea el campo como solo lectura.                                                                                                                                                             | `FreeDvUseRadioCallsign`                                                                      |
| **Grid Square: (FreeDV Reporter)**                       | Cuadrado de cuadrícula de Maidenhead para informar. De solo lectura cuando **Use GPS** está marcado.                                                                                                                                                                                     | `FreeDvMyGrid`                                                                                |
| **Use GPS (grid)**                                       | Precarga el campo de cuadrícula desde el módulo GPS de la radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS.                                                                                                                       | `FreeDvUseGpsGrid`                                                                            |
| **Station Msg: (FreeDV Reporter)**                       | Mensaje de texto libre opcional que se muestra junto al indicativo en el mapa público de FreeDV Reporter.                                                                                                                                                                      | `FreeDvMyMessage`                                                                             |
| **Auto Mode:**                                           | Cambia automáticamente el modo del slice al hacer clic en un spot que incluye información de modo (por ejemplo, CW, FT8, RTTY). El valor predeterminado es **Enabled**.                                                                                                                      | `SpotsAutoMode`                                                                               |
| **Spot Lines:**                                          | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. El valor predeterminado es **Enabled**. Deshabilítelo durante concursos para reducir el desorden visual.                                                                                                                      | `IsSpotsLinesEnabled`                                                                         |
| Total Spots:                                             | Lectura en vivo de cuántos spots se están rastreando actualmente en todas las fuentes.                                                                                                                                                                                     | Se actualiza cada vez que se agregan o borran spots. Se reinicia a 0 cuando se presiona **Clear All Spots**. |
## Informes de FreeDV Reporter

La pestaña **FreeDV** contiene un grupo **Station Reporting** que controla si AetherSDR transmite la actividad de su estación al mapa público de FreeDV Reporter en qso.freedv.org.

### Requisitos antes de habilitar

- Debe estar disponible un indicativo válido, ya sea desde la radio (cuando **Use radio** está marcado) o escrito en el campo **Callsign:**.
- Debe estar disponible un cuadrado de cuadrícula de Maidenhead válido, ya sea desde el módulo GPS de la radio (cuando **Use GPS** está marcado, en hardware compatible) o escrito en el campo **Grid Square:**.

Si falta alguno de los valores al intentar habilitar **Enable FreeDV Reporter reporting when RADE is active**, AetherSDR muestra una advertencia y deja la casilla sin marcar. Esto evita que aparezcan valores en blanco o de marcador de posición en el mapa público compartido.

### Pasos para habilitar los informes

1. Abra `Settings > SpotHub...` y haga clic en la pestaña **FreeDV**.
2. En el grupo **Station Reporting**, confirme que el campo **Callsign:** muestra su indicativo.
   - Si **Use radio** está marcado, el campo se completa automáticamente desde el indicativo configurado en la radio y es de solo lectura. Desmarque **Use radio** para ingresar un indicativo manualmente.
3. Confirme que el campo **Grid Square:** muestra su localizador de Maidenhead.
   - En radios con hardware GPS, marque **Use GPS** para completarlo automáticamente. Desmarque **Use GPS** para escribir un cuadrado de cuadrícula manualmente.
4. Opcionalmente, ingrese un mensaje corto en **Station Msg:** — aparece junto a su indicativo en el mapa.
5. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si el indicativo o el cuadrado de cuadrícula están en blanco, aparece un cuadro de diálogo de advertencia. Complete el valor faltante e intente nuevamente.
6. Los informes ahora están activos siempre que el módem RADE esté en ejecución.

## Cambio predeterminado de Auto Mode

A partir de la v0.9.5.1, **Auto Mode:** (`SpotsAutoMode`) está predeterminado en **Enabled** para instalaciones nuevas. Si está actualizando y desea conservar el comportamiento anterior, abra la pestaña **Display** y establezca **Auto Mode:** en **Disabled**.

## Sintonizar un spot haciendo doble clic

Al hacer doble clic en una fila de la pestaña **Spot List**, el slice activo se sintoniza en la frecuencia de ese spot. A partir de la v0.9.7, AetherSDR también lee la sugerencia de modo del comentario del spot y la reenvía al receptor, por lo que el slice cambia al modo correcto (por ejemplo, CW o SSB) al mismo tiempo que cambia la frecuencia. No se requiere configuración adicional.

## Consejos
- Los spots recibidos de SpotCollector aparecen junto a los spots de otras fuentes en la pestaña **Spot List**. La columna **Source** los identifica.
- Si la superposición de spots del panadapter no es visible, verifique que **Spots:** esté configurado en **Enabled** en la pestaña **Display**.
- **Auto Mode** está predeterminado en **Enabled**. Cuando hace doble clic en un spot que incluye información de modo (por ejemplo, CW, FT8, RTTY), el modo del slice cambia automáticamente. Deshabilítelo en la pestaña **Display** si prefiere cambiar los modos manualmente.
- Use **Spot Lines:** en la pestaña **Display** para controlar si se dibujan líneas verticales desde el espectro hasta cada etiqueta de spot. Deshabilítelo durante concursos para reducir el desorden visual.

## Solución de problemas

- **El estado permanece Stopped / no aparecen spots** — Verifique que SpotCollector esté transmitiendo activamente y que el puerto UDP en AetherSDR coincida con el puerto configurado en SpotCollector. Compruebe que ningún firewall esté bloqueando el tráfico UDP en ese puerto.
- **El listener se inicia pero el panadapter no muestra spots** — Confirme que la superposición maestra de spots esté activada: abra la pestaña **Display** y verifique que **Spots:** esté en **Enabled**.
- **La casilla FreeDV Reporter se desmarca sola con una advertencia** — El campo de indicativo o de cuadrado de cuadrícula está vacío o no se pudo resolver. Complete ambos campos (o habilite **Use radio** / **Use GPS** si la radio puede proporcionar los valores) antes de habilitar los informes.

## Relacionado

- [Visión general de SpotHub](overview.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Elegir colores para cada fuente de spot](pick-colors-for-each-spot-source.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Borrar todos los spots del panadapter](clear-all-spots-from-the-panadapter.md)
<!-- docmesh:llm version=V0.9.7 date=2026-05-03 -->
