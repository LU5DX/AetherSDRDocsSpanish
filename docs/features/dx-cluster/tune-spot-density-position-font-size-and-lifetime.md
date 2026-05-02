# Ajustar densidad, posición, tamaño de fuente y duración de los spots

La pestaña Display en SpotHub controla cómo aparecen las etiquetas de spots en el panadapter: cuántas se apilan verticalmente, dónde se ubican, qué tan grande es el texto y cuánto tiempo permanece visible cada spot antes de desvanecerse. Ajuste estos parámetros para reducir el desorden en una banda concurrida o hacer que los spots sean más legibles en una pantalla pequeña.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar estos parámetros.
- Al menos una fuente de spots (clúster DX, RBN, WSJT-X, SpotCollector, POTA o FreeDV) debe estar activa para que pueda ver el efecto de los cambios en tiempo real.
- La superposición maestra de spots debe estar activada. En la pestaña Display, confirme que `IsSpotsEnabled` esté activo (el botón "Spots:" muestra Enabled).

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Confirme que **Spots:** esté configurado en Enabled. Si no lo está, haga clic para activar la superposición.
4. Para controlar cuántos spots se apilan verticalmente antes de que comiencen a superponerse, arrastre el control deslizante **Levels:**. Los valores más altos permiten más filas de etiquetas de spots.
5. Para mover las etiquetas de spots hacia arriba o hacia abajo en el panadapter, arrastre el control deslizante **Position:**.
6. Para cambiar el tamaño del texto de las etiquetas de spots, arrastre el control deslizante **Font Size:**.
7. Para definir cuánto tiempo permanece visible un spot antes de desaparecer, arrastre el control deslizante **Spot Lifetime:**. El valor se expresa en segundos.
8. Si desea que AetherSDR ajuste automáticamente la densidad de spots según el nivel de zoom actual del panadapter, haga clic en **Auto Mode:** para activarlo. Cuando Auto Mode está activado, el control deslizante **Levels:** no tiene efecto.
9. Cierre el cuadro de diálogo. Los cambios se aplican de inmediato.

## Qué hace cada control

| Control | Clave de parámetro | Comportamiento |
|---|---|---|
| **Spots:** | `IsSpotsEnabled` | Interruptor maestro para la superposición de spots en el panadapter. |
| **Auto Mode:** | `SpotsAutoMode` | Ajusta automáticamente la densidad de spots según el nivel de zoom. Anula Levels. De forma predeterminada está Enabled. |
| **Levels:** | `SpotsStackLevels` | Número de filas de apilamiento vertical para las etiquetas de spots. |
| **Position:** | `SpotsPosition` | Posición vertical de la banda de etiquetas de spots en el panadapter. |
| **Font Size:** | `SpotsFontSize` | Tamaño del texto en cada etiqueta de spot. |
| **Spot Lifetime:** | `SpotsLifetime` | Segundos que permanece visible una etiqueta de spot antes de desvanecerse. |
| **Enable FreeDV Reporter reporting when RADE is active** | `FreeDvAutoReport` | Activa el reporte de la estación al mapa público FreeDV Reporter (qso.freedv.org) siempre que el módem RADE esté activo. Requiere un indicativo válido y un cuadrado de cuadrícula, o la casilla de verificación se niega a activarse. Si alguno de los campos está vacío al marcarla, aparece un cuadro de diálogo de advertencia y la casilla vuelve a desmarcarse. |
| **Callsign: (FreeDV Reporter)** | `FreeDvMyCallsign` | Indicativo a reportar al mapa FreeDV Reporter. Es de solo lectura cuando **Use radio (callsign)** está marcado. Se actualiza automáticamente cuando cambia el indicativo de la radio y **Use radio** está activo. |
| **Use radio (callsign)** | `FreeDvUseRadioCallsign` | Rellena automáticamente el campo del indicativo con el indicativo configurado en la radio y bloquea el campo como solo lectura. Predeterminado: activado. |
| **Grid Square: (FreeDV Reporter)** | `FreeDvMyGrid` | Cuadrado de cuadrícula Maidenhead a reportar. Es de solo lectura cuando **Use GPS (grid)** está marcado. |
| **Use GPS (grid)** | `FreeDvUseGpsGrid` | Rellena automáticamente el campo de cuadrícula con el módulo GPS de la radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. |
| **Station Msg: (FreeDV Reporter)** | `FreeDvMyMessage` | Mensaje de texto libre opcional que se muestra junto al indicativo en el mapa público FreeDV Reporter. |

## Reporte a FreeDV Reporter

La pestaña **FreeDV** en SpotHub contiene un grupo **Station Reporting**. Cuando **Enable FreeDV Reporter reporting when RADE is active** está marcado, AetherSDR reporta su estación al mapa público FreeDV Reporter en qso.freedv.org siempre que el módem RADE esté en ejecución.

Antes de activar el reporte, proporcione un indicativo y un cuadrado de cuadrícula. AetherSDR resuelve estos valores en el siguiente orden de prioridad:

1. **Indicativo** — si **Use radio (callsign)** está marcado y la radio tiene un indicativo configurado, ese valor se utiliza y el campo queda bloqueado. De lo contrario, escriba un indicativo directamente en el campo **Callsign:**.
2. **Cuadrado de cuadrícula** — si **Use GPS (grid)** está marcado y la radio tiene hardware GPS con una posición válida, la cuadrícula se rellena automáticamente y queda bloqueada. Esta casilla solo aparece en modelos de radio con hardware GPS. De lo contrario, escriba un cuadrado de cuadrícula Maidenhead (hasta seis caracteres) en el campo **Grid Square:**.

Si el indicativo o la cuadrícula están vacíos cuando marca **Enable FreeDV Reporter reporting when RADE is active**, aparece un cuadro de diálogo de advertencia y la casilla vuelve a desmarcarse. Esto evita que valores en blanco o de marcador de posición aparezcan en el mapa público compartido por la comunidad.

Opcionalmente, escriba un mensaje breve en **Station Msg:** para que se muestre junto a su indicativo en el mapa.

La pestaña FreeDV solo está presente en compilaciones generadas con `HAVE_WEBSOCKETS`. En Windows, la casilla de reporte además requiere que `HAVE_RADE` esté definido.

## Consejos

- Si las etiquetas de spots se superponen de forma excesiva en una banda concurrida, aumente **Levels:** para agregar más filas de apilamiento, o disminuya **Spot Lifetime:** para que los spots antiguos desaparezcan más rápido.
- **Auto Mode:** está activado de forma predeterminada a partir de la versión v0.9.5.1. Desactívelo si desea controlar manualmente la densidad mediante el control deslizante **Levels:**.
- Los spots de WSJT-X tienen su propio parámetro de duración por fuente (**Spot Life:** en la pestaña WSJT-X, almacenado como `WsjtxSpotLife`). El control deslizante **Spot Lifetime:** en la pestaña Display se aplica a todas las demás fuentes.
- Cuando **Use radio (callsign)** está activo, el campo del indicativo se actualiza automáticamente si cambia el indicativo en Radio Setup sin necesidad de volver a abrir SpotHub.

## Solución de problemas

- **Las etiquetas de spots no son visibles en absoluto** — Verifique que **Spots:** en la pestaña Display esté configurado en Enabled (`IsSpotsEnabled`). Confirme también que al menos una fuente de spots esté conectada y recibiendo spots.
- **Cambiar Levels: no tiene efecto** — Es probable que **Auto Mode:** esté activado. Haga clic en **Auto Mode:** para desactivarlo y luego ajuste **Levels:** manualmente.
- **La casilla "Enable FreeDV Reporter" sigue volviendo a desmarcarse** — Deben estar configurados tanto un indicativo como un cuadrado de cuadrícula antes de activar el reporte. Rellene los campos **Callsign:** y **Grid Square:** (o active **Use radio** y **Use GPS** si la radio proporciona esos valores) y luego marque la casilla nuevamente.
- **La pestaña FreeDV o la casilla de reporte no son visibles** — Su compilación de AetherSDR fue generada sin `HAVE_WEBSOCKETS` (pestaña no presente) o sin `HAVE_RADE` en Windows (casilla no presente).

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Borrar todos los spots del panadapter](clear-all-spots-from-the-panadapter.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
