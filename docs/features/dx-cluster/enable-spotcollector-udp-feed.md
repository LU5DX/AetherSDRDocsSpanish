# Habilitar la fuente UDP de SpotCollector

AetherSDR puede recibir spots de DX transmitidos por SpotCollector de Ham Radio Deluxe a través de UDP y mostrarlos en el panadapter. Esta página explica cómo iniciar el listener, configurar el puerto correcto y hacer que se inicie automáticamente.

## Antes de comenzar

- SpotCollector debe estar instalado, configurado y ejecutándose en la misma máquina o red local, y configurado para transmitir spots vía UDP.
- Anote el puerto UDP en el que SpotCollector está transmitiendo; deberá ingresarlo en AetherSDR.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **SpotCollector**.
3. Configure **UDP Port:** con el puerto en el que SpotCollector está transmitiendo. Rango válido: 1–65535. Este valor se guarda como `SpotCollectorPort`.
4. Haga clic en **Start**.
5. Confirme que el indicador de estado cambie a **Listening**. Los spots entrantes aparecerán en la consola **SpotCollector Spots** a medida que lleguen.
6. Para que el listener se inicie automáticamente cada vez que se inicie AetherSDR, active **Auto-start on startup**. Esto se guarda como `SpotCollectorAutoStart`.

## Qué hace cada control

| Control                                                       | Descripción                                                                                                                                                                                                                                                  | Clave de configuración                            |
|---------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------|
| **UDP Port:**                                                 | Puerto UDP en el que AetherSDR escucha las transmisiones de SpotCollector. Rango válido: 1–65535.                                                                                                                                                            | `SpotCollectorPort`                               |
| **Start / Stop**                                              | Inicia o detiene el listener UDP.                                                                                                                                                                                                                            | —                                                 |
| **Auto-start on startup**                                     | Inicia el listener automáticamente al iniciar.                                                                                                                                                                                                               | `SpotCollectorAutoStart`                          |
| **SpotCollector Spots**                                       | Consola de solo lectura que muestra los spots recibidos de SpotCollector.                                                                                                                                                                                    | —                                                 |
| **Enable FreeDV Reporter reporting when RADE is active**      | Habilita la notificación de su estación al mapa público de FreeDV Reporter (qso.freedv.org) cuando el módem RADE esté activo. Requiere un indicativo y un cuadrado de cuadrícula válidos; si alguno de estos campos está en blanco o no se puede resolver, la casilla se niega a activarse y muestra una advertencia. | `FreeDvAutoReport`                                |
| **Callsign: (FreeDV Reporter)**                               | Indicativo para notificar al mapa de FreeDV Reporter. De solo lectura cuando **Use radio** está marcado. Cuando **Use radio** está marcado, el campo se completa con el indicativo configurado en la radio y se actualiza automáticamente si ese indicativo cambia. | `FreeDvMyCallsign`                                |
| **Use radio (callsign)**                                      | Rellena previamente el campo de indicativo desde el indicativo configurado en la radio y bloquea el campo como solo lectura.                                                                                                                                | `FreeDvUseRadioCallsign`                          |
| **Grid Square: (FreeDV Reporter)**                            | Cuadrado de cuadrícula Maidenhead para notificar. De solo lectura cuando **Use GPS** está marcado.                                                                                                                                                           | `FreeDvMyGrid`                                    |
| **Use GPS (grid)**                                            | Rellena previamente el campo de cuadrícula desde el módulo GPS de la radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS.                                                                                | `FreeDvUseGpsGrid`                                |
| **Station Msg: (FreeDV Reporter)**                            | Mensaje de texto libre opcional que se muestra junto al indicativo en el mapa público de FreeDV Reporter.                                                                                                                                                   | `FreeDvMyMessage`                                 |
| **Auto (Display tab)**                                        | Cambia automáticamente el modo del slice al hacer clic en un spot que incluya información de modo (p. ej., CW, FT8, RTTY). La clave de configuración cambió de `SpotsAutoMode` a `SpotAutoSwitchMode` en v26.5.1. El valor predeterminado es **Enabled**. | `SpotAutoSwitchMode`                              |
| **Spot Lines:**                                               | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. El valor predeterminado es **Enabled**. Desactívelo durante concursos para reducir el desorden visual.                                                                                | `IsSpotsLinesEnabled`                             |
| Total Spots:                                                  | Lectura en vivo de cuántos spots se están rastreando actualmente en todas las fuentes.                                                                                                                                                                      | Se actualiza cada vez que se añaden o borran spots. Se reinicia a 0 cuando se presiona **Clear All**. |
| **Signals (Display tab)**                                     | Marcadores dorados para señales de ancho de voz detectadas en el panadapter. Nuevo en v26.5.1 (#2426). El mismo conmutador que View > Signal History Markers.                                                                                                | `SHistoryMarkersEnabled`                          |
| **QRM (Display tab)**                                         | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Nuevo en v26.5.1 (#2426). El mismo conmutador que View > QRM History Markers.                                                                                                  | `SHistoryQrmEnabled`                              |
| **Clear All (Display tab)**                                   | Borra todos los spots de DX, la fuente de memoria, los marcadores de Signal History y los marcadores QRM del espectro.                                                                                                                                       | —                                                 |
| **Spot text color picker**                                    | Abre QColorDialog para elegir el color del texto del spot.                                                                                                                                                                                                   | `SpotsOverrideColor`                              |
| **Override Background: Enabled**                              | Habilita un color de fondo personalizado para los spots.                                                                                                                                                                                                     | `IsSpotsOverrideBackgroundColorsEnabled`          |
| **Override Background: Auto**                                 | Selecciona automáticamente el color de fondo para lograr contraste.                                                                                                                                                                                          | `IsSpotsOverrideToAutoBackgroundColorEnabled`     |
| **Spot background color picker**                              | Abre QColorDialog para el color de fondo del spot.                                                                                                                                                                                                           | `SpotsOverrideBgColor`                            |
| **DXCC Coloring (section)**                                   | Encabezado de sección para los controles de coloración DXCC en la columna izquierda debajo del divisor en la pestaña Display.                                                                                                                                | —                                                 |
| **DXCC Colors:**                                              | Colorea los spots según el estado de DXCC trabajado/confirmado/necesario. La clave de configuración cambió de `DxccColoringEnabled` a `IsDxccColoringEnabled` en v26.5.1.                                                                                    | `IsDxccColoringEnabled`                           |
| **Log File (ADIF):**                                          | Carga un archivo de registro ADIF para impulsar la coloración DXCC. Vigila automáticamente el archivo en busca de cambios después de la selección. La clave de configuración cambió de `DxccAdifPath` a `DxccAdifFilePath` en v26.5.1. La recarga automática está siempre activada cuando se selecciona un archivo (sin conmutador separado). | `DxccAdifFilePath`                                |
| **Imported: (DXCC stats)**                                    | Muestra el recuento de QSO y el recuento de entidades cuando se carga un registro. Formato: '<N> QSOs / <M> entities'.                                                                                                                                      | —                                                 |
| **DXCC Color swatches (New DXCC / New Band / New Mode / Worked)** | Abre un selector de color para cada categoría de estado DXCC. Nuevo en v26.5.1 — reemplaza el esquema de color DXCC fijo anterior.                                                                                                                           | `DxccColorNewEntity` / `DxccColorNewBand` / `DxccColorNewMode` / `DxccColorWorked` |
| **Signal History (section)**                                  | Encabezado de sección para los parámetros ajustables de Signal History en la columna derecha debajo del divisor en la pestaña Display. Nuevo en v26.5.1 (#2506).                                                                                             | —                                                 |
| **Marker Lifetime:**                                          | Cuánto tiempo persiste un marcador de Signal History inactivo antes de ser eliminado. Control deslizante. Valor predeterminado 60 s, rango 15–300 s. Nuevo en v26.5.1.                                                                                       | `SHistoryLifetimeS`                               |
| **QRM Gate:**                                                 | Cuánto tiempo debe persistir una portadora estrecha o una señal de banda ancha antes de clasificarse como QRM. Control deslizante. Valor predeterminado 6 s, rango 3–30 s. Nuevo en v26.5.1.                                                                | `SHistoryQrmGateS`                                |
| **Edge Threshold:**                                           | Umbral por encima del piso de ruido para la caminata de borde de pendiente que refina el borde del lado de la portadora de S-History. Control deslizante. Valor predeterminado 3.0 dB, rango 1.0–10.0 dB. Nuevo en v26.5.1.                                 | `SHistorySoftEdgeDb`                              |
| **Signal History color swatches (Signals / QRM)**             | Abre un selector de color para los marcadores de señal de voz (dorados) y los marcadores QRM (rojos). Nuevo en v26.5.1.                                                                                                                                      | `SHistoryColorSignals` / `SHistoryColorQrm`       |
| **Snap to Step:**                                             | Redondea el clic para sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de la portadora. Nuevo en v26.5.1. Valor predeterminado Disabled.                                              | `SHistorySnapToStep`                              |

## Notificación FreeDV Reporter

La pestaña **FreeDV** contiene un grupo **Station Reporting** que controla si AetherSDR transmite la actividad de su estación al mapa público de FreeDV Reporter en qso.freedv.org.

### Requisitos antes de habilitar

- Debe estar disponible un indicativo válido, ya sea desde la radio (cuando **Use radio** está marcado) o escrito en el campo **Callsign:**.
- Debe estar disponible un cuadrado de cuadrícula Maidenhead válido, ya sea desde el módulo GPS de la radio (cuando **Use GPS** está marcado, en hardware compatible) o escrito en el campo **Grid Square:**.

Si falta alguno de los valores cuando intente activar **Enable FreeDV Reporter reporting when RADE is active**, AetherSDR muestra una advertencia y deja la casilla sin marcar. Esto evita que aparezcan valores en blanco o de marcador de posición en el mapa público compartido.

### Pasos para habilitar la notificación

1. Abra `Settings > SpotHub...` y haga clic en la pestaña **FreeDV**.
2. En el grupo **Station Reporting**, confirme que el campo **Callsign:** muestra su indicativo.
   - Si **Use radio** está marcado, el campo se completa automáticamente desde el indicativo configurado en la radio y es de solo lectura. Desmarque **Use radio** para ingresar un indicativo manualmente.
3. Confirme que el campo **Grid Square:** muestra su localizador Maidenhead.
   - En radios con hardware GPS, marque **Use GPS** para completarlo automáticamente. Desmarque **Use GPS** para escribir un cuadrado de cuadrícula manualmente.
4. Opcionalmente, ingrese un mensaje breve en **Station Msg:** — aparece junto a su indicativo en el mapa.
5. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si el indicativo o el cuadrado de cuadrícula están en blanco, aparece un cuadro de diálogo de advertencia. Complete el valor faltante e intente de nuevo.
6. La notificación ahora está activa siempre que el módem RADE esté funcionando.

## Cambio del valor predeterminado de Auto Mode

A partir de v0.9.5.1, **Auto** (`SpotAutoSwitchMode`) tiene el valor predeterminado **Enabled** para instalaciones nuevas. Si está actualizando y desea conservar el comportamiento anterior, abra la pestaña **Display** y configure **Auto** en **Disabled**.

## Sintonizar un spot haciendo doble clic

Al hacer doble clic en una fila en la pestaña **Spot List**, se sintoniza el slice activo en la frecuencia de ese spot. A partir de v0.9.7, AetherSDR también lee la sugerencia de modo del comentario del spot y la reenvía al receptor, por lo que el slice cambia al modo correcto (por ejemplo, CW o SSB) al mismo tiempo que cambia la frecuencia. No se requiere configuración adicional.

## Modo de ventana sin marco

En v26.5.1, el cuadro de diálogo SpotHub se actualizó para admitir el modo de ventana sin marco. Cuando el modo sin marco está habilitado (predeterminado), el diálogo presenta una barra de título personalizada y un redimensionamiento de borde en 8 ejes. La barra de título muestra "SpotHub" y se puede usar para arrastrar la ventana. Esto proporciona una apariencia consistente con otros diálogos de AetherSDR.

## Consejos
- Los spots recibidos de SpotCollector aparecen junto con los spots de otras fuentes en la pestaña **Spot List**. La columna **Source** los identifica.
- Si la superposición de spots en el panadapter no es visible, verifique que **Spots:** esté configurado en **Enabled** en la pestaña **Display**.
- **Auto** tiene el valor predeterminado **Enabled**. Cuando hace doble clic en un spot que incluye información de modo (p. ej., CW, FT8, RTTY), el modo del slice cambia automáticamente. Desactívelo en la pestaña **Display** si prefiere cambiar de modo manualmente.
- Use **Spot Lines:** en la pestaña **Display** para controlar si se dibujan líneas verticales desde el espectro hasta cada etiqueta de spot. Desactívelo durante concursos para reducir el desorden visual.
- La pestaña **Display** se reorganizó en v26.5.1 (#2506). Los controles de Signal History ahora aparecen en una sección dedicada en lugar de subpestañas separadas. La pestaña tiene una fila de alternancia superior, controles deslizantes comunes, luego un diseño de dos columnas con DXCC Coloring a la izquierda y Signal History a la derecha.

## Solución de problemas

- **El estado permanece en Stopped / no aparecen spots** — Verifique que SpotCollector esté transmitiendo activamente y que el puerto UDP en AetherSDR coincida con el puerto configurado en SpotCollector. Compruebe que ningún firewall esté bloqueando el tráfico UDP en ese puerto.
- **El listener se inicia pero el panadapter no muestra spots** — Confirme que la superposición maestra de spots esté activada: abra la pestaña **Display** y verifique que **Spots:** esté **Enabled**.
- **La casilla FreeDV Reporter se desmarca con una advertencia** — El campo de indicativo o cuadrado de cuadrícula está vacío o no se pudo resolver. Complete ambos campos (o active **Use radio** / **Use GPS** si la radio puede proporcionar los valores) antes de habilitar la notificación.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Ajustar la densidad, posición, tamaño de fuente y tiempo de vida de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Elegir colores para cada fuente de spot](pick-colors-for-each-spot-source.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Borrar todos los spots del panadapter](clear-all-spots-from-the-panadapter.md)
