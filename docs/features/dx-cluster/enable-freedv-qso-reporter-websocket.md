# Habilitar el reportero WebSocket de FreeDV QSO

Conecte AetherSDR al reportero FreeDV QSO en `qso.freedv.org` para recibir spots de actividad FreeDV en su panadapter.

## Antes de comenzar

- La fuente WebSocket de FreeDV está disponible solo en compilaciones de AetherSDR compiladas con soporte WebSocket (`HAVE_WEBSOCKETS`). Si la pestaña FreeDV no aparece en SpotHub, su compilación no la incluye.
- Los spots aparecen en el panadapter solo cuando la superposición maestra de spots está habilitada. Consulte [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md) si los spots no son visibles después de conectarse.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **FreeDV**.
3. Confirme que el indicador **Server:** muestre `qso.freedv.org (WebSocket)`. Este punto final es fijo y no se puede cambiar.
4. Haga clic en **Start**. El indicador de estado cambia a **Connected** cuando el handshake WebSocket se completa correctamente.
5. Opcionalmente, haga clic en **Auto-start on startup** para que la conexión se establezca automáticamente cada vez que se inicie AetherSDR.
6. Opcionalmente, haga clic en **Spot Color:** para abrir el selector de color y asignar un color distintivo a los spots de FreeDV en el panadapter. El color elegido se guarda en `FreeDvSpotColor`.

## Reportar su estación al mapa del Reportero FreeDV

El grupo **Station Reporting** en la parte inferior de la pestaña **FreeDV** le permite transmitir su actividad al mapa público del Reportero FreeDV en `qso.freedv.org` siempre que el módem RADE esté activo.

### Requisitos antes de habilitar

- Un indicativo válido debe estar presente en el campo **Callsign:** (u obtenido de la radio).
- Un cuadrado de cuadrícula Maidenhead válido debe estar presente en el campo **Grid Square:** (u obtenido del GPS de la radio).

Si alguno de estos valores está en blanco cuando marca **Enable FreeDV Reporter reporting when RADE is active**, AetherSDR muestra una advertencia y deja la casilla sin marcar. Esto evita que se transmitan valores en blanco o de marcador de posición al mapa público compartido.

### Pasos de configuración

1. En el grupo **Station Reporting**, revise el campo **Callsign:**
   - Si **Use radio** está marcado (valor predeterminado), el campo se rellena previamente con el indicativo configurado en su radio y es de solo lectura. Los cambios al indicativo de la radio en Radio Setup se reflejan automáticamente.
   - Desmarque **Use radio** para ingresar un indicativo manualmente. El valor ingresado se guarda en `FreeDvMyCallsign` y se convierte a mayúsculas al guardar.
2. Revise el campo **Grid Square:**
   - Si su radio tiene hardware GPS y **Use GPS** está marcado (valor predeterminado en modelos con capacidad GPS), el campo se rellena previamente desde la posición fija del GPS de la radio y es de solo lectura. La casilla **Use GPS** está oculta en modelos de radio sin hardware GPS.
   - Desmarque **Use GPS** (o si la casilla no está presente) para ingresar un cuadrado de cuadrícula manualmente. El valor se guarda en `FreeDvMyGrid` y se convierte a mayúsculas al guardar.
3. Opcionalmente, complete **Station Msg:** con una breve nota de texto libre. Este mensaje aparece junto a su indicativo en el mapa público del Reportero FreeDV y se guarda en `FreeDvMyMessage`.
4. Marque **Enable FreeDV Reporter reporting when RADE is active**. AetherSDR valida el indicativo y la cuadrícula antes de aceptar el cambio, luego guarda `FreeDvAutoReport = True` y emite la señal de reporte habilitado.

## Funciones de cada control

| Control                                                  | Tipo          | Comportamiento                                                                                                                                                                                                                            |
|----------------------------------------------------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Server:**                                              | Indicador     | Punto final fijo: `qso.freedv.org (WebSocket)`. Solo lectura.                                                                                                                                                                             |
| **Start / Stop**                                         | Botón pulsador| Conecta o desconecta el WebSocket FreeDV.                                                                                                                                                                                                |
| **Auto-start on startup**                                | Botón de alternancia | Inicia la conexión FreeDV automáticamente al arrancar. Guardado en `FreeDvAutoStart`.                                                                                                                                                     |
| **FreeDV Spots**                                         | Campo de texto| Consola de solo lectura que muestra la actividad FreeDV entrante.                                                                                                                                                                         |
| **Spot Color:**                                          | Botón pulsador| Abre un selector de color para los spots FreeDV en el panadapter. Guardado en `FreeDvSpotColor`.                                                                                                                                          |
| **Enable FreeDV Reporter reporting when RADE is active** | Casilla de verificación | Habilita el reporte de estación al mapa público del Reportero FreeDV cuando el módem RADE está activo. Rechazado si el indicativo o la cuadrícula están en blanco. Guardado en `FreeDvAutoReport`. Limitado por compilación a `HAVE_WEBSOCKETS`; en Windows también requiere `HAVE_RADE`. |
| **Callsign:**                                            | Campo de texto| Indicativo a reportar al mapa del Reportero FreeDV. Solo lectura cuando **Use radio** está marcado. Guardado en `FreeDvMyCallsign`.                                                                                                       |
| **Use radio**                                            | Casilla de verificación | Rellena previamente **Callsign:** con el indicativo configurado en la radio y bloquea el campo como solo lectura. Se sincroniza automáticamente cuando cambia el indicativo de la radio. Guardado en `FreeDvUseRadioCallsign`. Valor predeterminado: habilitado. |
| **Grid Square:**                                         | Campo de texto| Cuadrado de cuadrícula Maidenhead a reportar. Solo lectura cuando **Use GPS** está marcado. Guardado en `FreeDvMyGrid`.                                                                                                                  |
| **Use GPS**                                              | Casilla de verificación | Rellena previamente **Grid Square:** desde el módulo GPS de la radio y bloquea el campo como solo lectura. Se muestra solo en modelos de radio con hardware GPS. Guardado en `FreeDvUseGpsGrid`. Valor predeterminado: habilitado en modelos con GPS. |
| **Station Msg:**                                         | Campo de texto| Mensaje de texto libre opcional que se muestra junto a su indicativo en el mapa público del Reportero FreeDV. Guardado en `FreeDvMyMessage`.                                                                                              |
| **Auto Mode:**                                           | Botón de alternancia | Cambia automáticamente el modo del slice al hacer clic en un spot que incluya información de modo (por ejemplo, CW, FT8, RTTY). Valor predeterminado: **Enabled** (a partir de v0.9.5.1). Guardado en `SpotAutoSwitchMode`.               |
| **Spot Lines:**                                          | Botón de alternancia | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Deshabilite durante concursos para reducir el desorden visual. Valor predeterminado: **Enabled**. Guardado en `IsSpotsLinesEnabled`. Nuevo en v0.9.7.           |
| Total Spots:                                             | Indicador     | Lectura en vivo de cuántos spots se rastrean actualmente en todas las fuentes. Se actualiza cuando se agregan o eliminan spots. Se restablece a 0 al presionar **Clear All Spots**.                                                         |
## Sintonizar un spot haciendo doble clic en la lista de spots

Hacer doble clic en una fila de la pestaña **Spot List** sintoniza el slice activo en la frecuencia del spot. A partir de v0.9.7, AetherSDR también reenvía el modo extraído del comentario del spot, por lo que el slice cambia al modo apropiado (por ejemplo, CW o SSB) para coincidir con el spot en lugar de solo cambiar la frecuencia.

## Consejos

- La actividad entrante aparece en la consola **FreeDV Spots**, así como en la tabla unificada de spots en la pestaña **Spot List**.
- Si desea que los spots de FreeDV se destaquen de los spots del clúster DX o RBN, establezca un color único usando **Spot Color:** antes de conectarse.
- Si **Use radio** está marcado, actualizar su indicativo en Radio Setup actualiza inmediatamente el campo **Callsign:** sin necesidad de volver a abrir SpotHub.
- La transmisión del reportero solo se activa mientras el módem RADE está en funcionamiento. Puede dejar la casilla habilitada en todo momento; no se envían datos cuando RADE está inactivo.
- **Auto Mode:** en la pestaña **Display** tiene como valor predeterminado **Enabled** a partir de v0.9.5.1. La densidad de spots se ajusta automáticamente a medida que hace zoom en el panadapter sin necesidad de configuración manual. Si deshabilitó previamente **Auto Mode:** y guardó la configuración de una versión anterior, verifique si el nuevo valor predeterminado es apropiado para su flujo de trabajo. La configuración se guarda en `SpotAutoSwitchMode`.
- **Spot Lines:** está habilitado de forma predeterminada. Durante concursos, considere deshabilitarlo en la pestaña **Display** para reducir el desorden visual en el panadapter. La configuración se guarda en `IsSpotsLinesEnabled`.

## Solución de problemas

- **Falta la pestaña FreeDV** — Su compilación de AetherSDR fue compilada sin soporte WebSocket. La pestaña está oculta en el momento de la compilación y no se puede habilitar en tiempo de ejecución.
- **El estado permanece como Disconnected después de hacer clic en Start** — Verifique su conexión a internet. El punto final fijo `qso.freedv.org` debe ser accesible desde su máquina en el puerto WebSocket. Los firewalls o configuraciones de proxy pueden bloquear la conexión.
- **Los spots aparecen en la consola pero no en el panadapter** — Verifique que **Spots:** esté configurado como **Enabled** en la pestaña **Display** de SpotHub.
- **Aparece la advertencia "Please set both a callsign and a grid square"** — Complete tanto **Callsign:** como **Grid Square:** antes de marcar **Enable FreeDV Reporter reporting when RADE is active**. Si **Use radio** o **Use GPS** está marcado pero la radio aún no ha proporcionado esos valores, desmarque la opción correspondiente e ingrese los valores manualmente.
- **La casilla Use GPS no es visible** — Su modelo de radio no tiene hardware GPS. Ingrese un cuadrado de cuadrícula manualmente en el campo **Grid Square:**.
- **Hacer doble clic en un spot no cambia el modo** — La información del modo se analiza desde el comentario del spot. Si el comentario no contiene un token de modo reconocido, solo se aplica la frecuencia. Verifique la columna Comment del spot en la pestaña **Spot List** para confirmar si la información del modo está presente.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Elegir colores para cada fuente de spot](pick-colors-for-each-spot-source.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
<!-- docmesh:llm version=V0.9.7 date=2026-05-03 -->
