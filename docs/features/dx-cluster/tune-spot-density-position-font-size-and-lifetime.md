# Ajustar densidad de spots, posición, tamaño de fuente y duración

La pestaña Display en SpotHub controla cómo aparecen las etiquetas de spots en el panadapter: cuántos se apilan verticalmente, dónde se sitúan, qué tan grande es el texto y cuánto tiempo vive cada spot antes de desaparecer. Ajuste estas opciones para reducir el desorden en una banda ocupada o hacer los spots más legibles en una pantalla pequeña.

## Antes de comenzar

- AetherSDR debe estar ejecutándose. No se requiere una conexión de radio para cambiar estas opciones.
- Al menos una fuente de spots (DX cluster, RBN, WSJT-X, SpotCollector, POTA o FreeDV) debe estar activa para que pueda ver el efecto de sus cambios en tiempo real.
- La superposición maestra de spots debe estar activada. En la pestaña Display, confirme que `IsSpotsEnabled` está activo (el toggle "Spots:" muestra Enabled).

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Confirme que **Spots:** está configurado como Enabled. Si no es así, haga clic para habilitar la superposición.
4. Para controlar cuántos spots se apilan verticalmente antes de que comiencen a superponerse, arrastre el control deslizante **Levels:**. Valores más altos permiten más filas de etiquetas de spots.
5. Para mover las etiquetas de spots hacia arriba o hacia abajo en el panadapter, arrastre el control deslizante **Position:**.
6. Para cambiar el tamaño del texto de las etiquetas de spots, arrastre el control deslizante **Font Size:**.
7. Para establecer cuánto tiempo permanece visible un spot antes de desaparecer, arrastre el control deslizante **Spot Lifetime:**. El valor está en segundos.
8. Si desea que AetherSDR ajuste automáticamente la densidad de spots según el nivel de zoom actual del panadapter, haga clic en **Auto Mode:** para habilitarlo. Cuando Auto Mode está activado, el control deslizante **Levels:** no tiene efecto.
9. Cierre el diálogo. Los cambios surten efecto inmediatamente.

## Qué hace cada control

| Control | Clave de configuración | Comportamiento |
|---|---|---|
| **Spots:** | `IsSpotsEnabled` | Control maestro para la superposición de spots en el panadapter. |
| **Auto Mode:** | `SpotsAutoMode` | Ajusta automáticamente la densidad de spots según el nivel de zoom. Anula Levels. |
| **Levels:** | `SpotsStackLevels` | Número de filas de apilamiento vertical para etiquetas de spots. |
| **Position:** | `SpotsPosition` | Posición vertical de la banda de etiquetas de spots en el panadapter. |
| **Font Size:** | `SpotsFontSize` | Tamaño del texto en cada etiqueta de spot. |
| **Spot Lifetime:** | `SpotsLifetime` | Segundos que permanece visible una etiqueta de spot antes de desaparecer. |
| **Enable FreeDV Reporter reporting when RADE is active** | `FreeDvAutoReport` | Habilita la notificación de estación al mapa público de FreeDV Reporter (qso.freedv.org) siempre que el módem RADE esté activo. Requiere un indicativo válido y un localizador Maidenhead o la casilla se rehúsa a habilitarse. Si alguno de estos campos está en blanco cuando marca la casilla, aparece un diálogo de advertencia y la casilla vuelve a su estado desmarcado. |
| **Callsign: (FreeDV Reporter)** | `FreeDvMyCallsign` | Indicativo a notificar al mapa de FreeDV Reporter. Solo lectura cuando **Use radio (callsign)** está marcado. Se actualiza automáticamente cuando cambia el indicativo de la radio y **Use radio** está activo. |
| **Use radio (callsign)** | `FreeDvUseRadioCallsign` | Rellena previamente el campo de indicativo desde el indicativo configurado en la radio y bloquea el campo en modo solo lectura. Predeterminado: habilitado. |
| **Grid Square: (FreeDV Reporter)** | `FreeDvMyGrid` | Localizador Maidenhead a notificar. Solo lectura cuando **Use GPS (grid)** está marcado. |
| **Use GPS (grid)** | `FreeDvUseGpsGrid` | Rellena previamente el campo de localizador desde el módulo GPS de la radio y bloquea el campo en modo solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. |
| **Station Msg: (FreeDV Reporter)** | `FreeDvMyMessage` | Mensaje de texto libre opcional que aparece junto al indicativo en el mapa público de FreeDV Reporter. |

## Notificación de FreeDV Reporter

La pestaña **FreeDV (tab)** en SpotHub contiene un grupo **Station Reporting**. Cuando **Enable FreeDV Reporter reporting when RADE is active** está marcada, AetherSDR notifica su estación al mapa público de FreeDV Reporter en qso.freedv.org siempre que el módem RADE esté ejecutándose.

Antes de habilitar la notificación, proporcione tanto un indicativo como un localizador Maidenhead. AetherSDR resuelve estos valores en el siguiente orden de prioridad:

1. **Callsign** — si **Use radio (callsign)** está marcado y la radio tiene un indicativo configurado, se usa ese valor y el campo queda bloqueado. De lo contrario, escriba un indicativo directamente en el campo **Callsign:**.
2. **Grid Square** — si **Use GPS (grid)** está marcado y la radio tiene hardware GPS con una posición válida, el localizador se rellena automáticamente y queda bloqueado. Esta casilla solo aparece en modelos de radio con hardware GPS. De lo contrario, escriba un localizador Maidenhead (hasta seis caracteres) en el campo **Grid Square:**.

Si el indicativo o el localizador están vacíos cuando marca **Enable FreeDV Reporter reporting when RADE is active**, aparece un diálogo de advertencia y la casilla vuelve a su estado desmarcado. Esto evita que valores en blanco o valores de marcador de posición aparezcan en el mapa público compartido por la comunidad.

Opcionalmente, escriba un mensaje breve en **Station Msg:** para mostrarlo junto a su indicativo en el mapa.

La pestaña FreeDV solo está presente en compilaciones compiladas con `HAVE_WEBSOCKETS`. En Windows, la casilla de notificación además requiere que `HAVE_RADE` esté definido.

## Consejos

- Si las etiquetas de spots se superponen mucho en una banda concurrida, aumente **Levels:** para agregar más filas de apilamiento, o disminuya **Spot Lifetime:** para que los spots antiguos desaparezcan más rápido.
- **Auto Mode:** es útil cuando cambia frecuentemente entre vistas ampliadas y reducidas. Desactívelo si desea control manual sobre la densidad.
- Los spots de WSJT-X tienen su propia configuración de duración por fuente (**Spot Life:** en la pestaña WSJT-X, almacenado como `WsjtxSpotLife`). El control deslizante **Spot Lifetime:** en la pestaña Display se aplica a todas las otras fuentes.
- Cuando **Use radio (callsign)** está activo, el campo de indicativo se actualiza automáticamente si cambia el indicativo en Radio Setup sin rearir SpotHub.

## Solución de problemas

- **Las etiquetas de spots no son visibles en absoluto** — Verifique que **Spots:** en la pestaña Display esté configurado como Enabled (`IsSpotsEnabled`). También confirme que al menos una fuente de spots esté conectada y recibiendo spots.
- **Cambiar Levels: no tiene efecto** — Es probable que **Auto Mode:** esté habilitado. Haga clic en **Auto Mode:** para deshabilitarlo, luego ajuste **Levels:** manualmente.
- **La casilla "Enable FreeDV Reporter" sigue revirtiéndose a desmarcada** — Tanto un indicativo como un localizador Maidenhead deben estar configurados antes de habilitar. Rellene los campos **Callsign:** y **Grid Square:** (o habilite **Use radio** y **Use GPS** si la radio proporciona esos valores), luego marque la casilla nuevamente.
- **La pestaña FreeDV o la casilla de notificación no es visible** — Su compilación de AetherSDR fue compilada sin `HAVE_WEBSOCKETS` (pestaña no presente) o sin `HAVE_RADE` en Windows (casilla no presente).

## Relacionado

- [Descripción general de SpotHub](overview.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Borrar todos los spots del panadapter](clear-all-spots-from-the-panadapter.md)
- [Iniciar escucha UDP de WSJT-X y filtrar para CQ, POTA o llamadas para mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
