# Densidad, posición, tamaño de fuente y duración de las marcas de spot

La pestaña Display en SpotHub controla cómo aparecen las etiquetas de los spots en el panadapter: cuántas se apilan verticalmente, dónde se ubican, el tamaño del texto y cuánto tiempo permanece visible cada spot antes de desvanecerse. Ajuste estas configuraciones para reducir el desorden en una banda muy concurrida o hacer que los spots sean más legibles en una pantalla pequeña.

## Antes de empezar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar estas configuraciones.
- Al menos una fuente de spots (DX cluster, RBN, WSJT-X, SpotCollector, POTA o FreeDV) debe estar activa para que pueda ver el efecto de sus cambios en tiempo real.
- La superposición maestra de spots debe estar activada. En la pestaña Display, confirme que `IsSpotsEnabled` esté activo (el conmutador "Spots:" muestra Enabled).

## Pasos
1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Confirme que **Spots:** esté configurado en Enabled. Si no lo está, haga clic en él para activar la superposición.
4. Para controlar cuántos spots se apilan verticalmente antes de que comiencen a superponerse, arrastre el control deslizante **Levels:**. Los valores más altos permiten más filas de etiquetas de spots.
5. Para mover las etiquetas de los spots hacia arriba o hacia abajo en el panadapter, arrastre el control deslizante **Position:**.
6. Para cambiar el tamaño del texto de las etiquetas de los spots, arrastre el control deslizante **Font Size:**.
7. Para establecer cuánto tiempo permanece visible un spot antes de desaparecer, arrastre el control deslizante **Spot Lifetime:**. El valor está en segundos.
8. **Auto Mode:** está habilitado por defecto. Cuando está activo, AetherSDR cambia automáticamente el modo del slice al hacer clic en un spot que contiene información de modo (por ejemplo, CW, FT8, RTTY). Haga clic en **Auto Mode:** para alternar este comportamiento.
9. Para mostrar u ocultar las líneas verticales trazadas desde el espectro hasta cada etiqueta de spot, haga clic en **Spot Lines:**. El botón alterna entre Enabled y Disabled. Desactívelo durante concursos para reducir el desorden visual.
10. Cierre el diálogo. Los cambios surten efecto de inmediato.

## Qué hace cada control
| Control                                                  | Clave de configuración                                                                   | Comportamiento                                                                                                                                                                                                                                                                                           |
|----------------------------------------------------------|------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Spots:**                                               | `IsSpotsEnabled`                                                                         | Conmutador maestro de la superposición de spots en el panadapter.                                                                                                                                                                                                                                        |
| **Auto Mode:**                                           | `SpotsAutoMode`                                                                          | Selecciona automáticamente la densidad de spots según el nivel de zoom. Predeterminado: Enabled.                                                                                                                                                                                                         |
| **Levels:**                                              | `SpotsStackLevels`                                                                       | Número de filas de apilamiento vertical para las etiquetas de spots.                                                                                                                                                                                                                                     |
| **Position:**                                            | `SpotsPosition`                                                                          | Posición vertical de la banda de etiquetas de spots en el panadapter.                                                                                                                                                                                                                                    |
| **Font Size:**                                           | `SpotsFontSize`                                                                          | Tamaño del texto en cada etiqueta de spot.                                                                                                                                                                                                                                                               |
| **Spot Lifetime:**                                       | `SpotsLifetime`                                                                          | Segundos que una etiqueta de spot permanece visible antes de desvanecerse.                                                                                                                                                                                                                               |
| **Spot Lines:**                                          | `IsSpotsLinesEnabled`                                                                    | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Predeterminado: Enabled. Desactívelo durante concursos para reducir el desorden visual. Nuevo en v0.9.7.                                                                                                                          |
| **Override Colors:**                                     | `IsSpotsOverrideColorsEnabled`                                                           | Fuerza un solo color de texto para todos los spots.                                                                                                                                                                                                                                                      |
| **Override Background: Enabled / Auto**                  | `IsSpotsOverrideBackgroundColorsEnabled` / `IsSpotsOverrideToAutoBackgroundColorEnabled` | Habilita un color de fondo personalizado para los spots y el modo de contraste automático.                                                                                                                                                                                                               |
| **Background Opacity:**                                  | `SpotsOverrideBgOpacity`                                                                 | Opacidad del color de fondo de los spots. Predeterminado: 48.                                                                                                                                                                                                                                            |
| **DXCC Coloring**                                        | `DxccColoringEnabled`                                                                    | Colorea los spots según el estado de trabajado/confirmado/necesitado.                                                                                                                                                                                                                                    |
| **Log File (ADIF):**                                     | `DxccAdifPath`                                                                           | Carga un archivo de registro ADIF para impulsar la coloración DXCC.                                                                                                                                                                                                                                      |
| **Auto-Reload Log:**                                     | `DxccAutoReload`                                                                         | Vuelve a leer el archivo ADIF automáticamente cuando cambia en el disco.                                                                                                                                                                                                                                 |
| **Enable FreeDV Reporter reporting when RADE is active** | `FreeDvAutoReport`                                                                       | Habilita la notificación de la estación al mapa público de FreeDV Reporter (qso.freedv.org) siempre que el módem RADE esté activo. Requiere un indicativo y un cuadrado de cuadrícula válidos; de lo contrario, la casilla de verificación se niega a activarse. Si alguno de los campos está vacío al marcarla, aparece un diálogo de advertencia y la casilla vuelve a estar desmarcada. |
| **Callsign: (FreeDV Reporter)**                          | `FreeDvMyCallsign`                                                                       | Indicativo para notificar al mapa de FreeDV Reporter. De solo lectura cuando **Use radio (callsign)** está marcado. Se actualiza automáticamente cuando el indicativo de la radio cambia y **Use radio** está activo.                                                                                     |
| **Use radio (callsign)**                                 | `FreeDvUseRadioCallsign`                                                                 | Rellena previamente el campo del indicativo desde el indicativo configurado de la radio y bloquea el campo como solo lectura. Predeterminado: enabled.                                                                                                                                                   |
| **Grid Square: (FreeDV Reporter)**                       | `FreeDvMyGrid`                                                                           | Cuadrado de cuadrícula Maidenhead para notificar. De solo lectura cuando **Use GPS (grid)** está marcado.                                                                                                                                                                                                |
| **Use GPS (grid)**                                       | `FreeDvUseGpsGrid`                                                                       | Rellena previamente el campo de la cuadrícula desde el módulo GPS de la radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS.                                                                                                                         |
| **Station Msg: (FreeDV Reporter)**                       | `FreeDvMyMessage`                                                                        | Mensaje de texto libre opcional que se muestra junto al indicativo en el mapa público de FreeDV Reporter.                                                                                                                                                                                                |
| **Total Spots:**                                         | —                                                                                        | Lectura en vivo de cuántos spots se están rastreando actualmente en todas las fuentes. Se actualiza cuando se agregan o eliminan spots. Se restablece a 0 cuando se presiona **Clear All Spots**.                                                                                                         |
## Hacer doble clic en un spot para sintonizar

Hacer doble clic en una fila de la Spot List sintoniza el slice activo a la frecuencia del spot. A partir de v0.9.7, AetherSDR también reenvía el modo extraído del comentario del spot (por ejemplo, CW, FT8 o SSB) para que el modo del slice cambie automáticamente para coincidir con el spot, no solo con la frecuencia.

## Notificación de FreeDV Reporter

La pestaña **FreeDV** en SpotHub contiene un grupo **Station Reporting**. Cuando **Enable FreeDV Reporter reporting when RADE is active** está marcado, AetherSDR notifica su estación al mapa público de FreeDV Reporter en qso.freedv.org siempre que el módem RADE esté en funcionamiento.

Antes de habilitar la notificación, proporcione tanto un indicativo como un cuadrado de cuadrícula. AetherSDR resuelve estos valores en el siguiente orden de prioridad:

1. **Callsign** — si **Use radio (callsign)** está marcado y la radio tiene un indicativo configurado, se usa ese valor y el campo se bloquea. De lo contrario, escriba un indicativo directamente en el campo **Callsign:**.
2. **Grid Square** — si **Use GPS (grid)** está marcado y la radio tiene hardware GPS con una fijación válida, la cuadrícula se completa automáticamente y se bloquea. Esta casilla de verificación solo aparece en modelos de radio con hardware GPS. De lo contrario, escriba un cuadrado de cuadrícula Maidenhead (hasta seis caracteres) en el campo **Grid Square:**.

Si el indicativo o la cuadrícula están vacíos cuando marca **Enable FreeDV Reporter reporting when RADE is active**, aparece un diálogo de advertencia y la casilla de verificación vuelve a estar desmarcada. Esto evita que aparezcan valores en blanco o de marcador de posición en el mapa público compartido por la comunidad.

Opcionalmente, escriba un mensaje corto en **Station Msg:** para que se muestre junto a su indicativo en el mapa.

La pestaña FreeDV solo está presente en compilaciones compiladas con `HAVE_WEBSOCKETS`. En Windows, la casilla de verificación de notificación requiere adicionalmente que se defina `HAVE_RADE`.

## Consejos
- Si las etiquetas de los spots se superponen mucho en una banda concurrida, aumente **Levels:** para agregar más filas de apilamiento, o disminuya **Spot Lifetime:** para que los spots antiguos se borren antes.
- Desactive **Spot Lines:** durante concursos o en bandas muy concurridas para reducir el desorden visual sin ocultar las etiquetas de los spots.
- Los spots de WSJT-X tienen su propia configuración de duración por fuente (**Spot Life:** en la pestaña WSJT-X, almacenado como `WsjtxSpotLife`). El control deslizante **Spot Lifetime:** en la pestaña Display se aplica a todas las demás fuentes.
- Cuando **Use radio (callsign)** está activo, el campo del indicativo se actualiza automáticamente si cambia el indicativo en Radio Setup sin volver a abrir SpotHub.

## Solución de problemas

- **Las etiquetas de los spots no son visibles en absoluto** — Verifique que **Spots:** en la pestaña Display esté configurado en Enabled (`IsSpotsEnabled`). También confirme que al menos una fuente de spots esté conectada y recibiendo spots.
- **Cambiar Levels: no tiene efecto** — **Auto Mode:** probablemente esté habilitado. Haga clic en **Auto Mode:** para deshabilitarlo y luego ajuste **Levels:** manualmente.
- **La casilla "Enable FreeDV Reporter" sigue volviendo a estar desmarcada** — Tanto un indicativo como un cuadrado de cuadrícula deben estar configurados antes de habilitar. Complete los campos **Callsign:** y **Grid Square:** (o habilite **Use radio** y **Use GPS** si la radio proporciona esos valores) y luego marque la casilla nuevamente.
- **La pestaña FreeDV o la casilla de verificación de notificación no son visibles** — Su compilación de AetherSDR se compiló sin `HAVE_WEBSOCKETS` (pestaña no presente) o sin `HAVE_RADE` en Windows (casilla no presente).
- **Hacer doble clic en un spot no cambia el modo del slice** — Confirme que el comentario del spot contenga una cadena de modo reconocible. La extracción del modo depende del texto del comentario proporcionado por la fuente del spot; los spots sin información de modo en el comentario seguirán sintonizando la frecuencia pero no cambiarán el modo.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Elegir colores para cada fuente de spot](pick-colors-for-each-spot-source.md)
- [Borrar todos los spots del panadapter](clear-all-spots-from-the-panadapter.md)
- [Iniciar el listener UDP de WSJT-X y filtrar por CQ, POTA o llamadas a mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
<!-- docmesh:llm version=V0.9.7 date=2026-05-03 -->
