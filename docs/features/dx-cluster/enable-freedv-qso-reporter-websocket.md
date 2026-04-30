# Habilitar el Reportero QSO de FreeDV por WebSocket

Conecte AetherSDR al reportero QSO de FreeDV en `qso.freedv.org` para recibir actividad de FreeDV en su panadapter.

## Antes de comenzar

- La fuente WebSocket de FreeDV está disponible solo en compilaciones de AetherSDR compiladas con soporte de WebSocket (`HAVE_WEBSOCKETS`). Si la pestaña FreeDV no aparece en SpotHub, su compilación no la incluye.
- Los spots aparecen en el panadapter solo cuando la superposición de spots maestra está habilitada. Consulte [Ajustar la densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md) si los spots no son visibles después de conectarse.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **FreeDV**.
3. Confirme que el indicador **Server:** muestre `qso.freedv.org (WebSocket)`. Este punto final es fijo y no puede cambiarse.
4. Haga clic en **Start**. El indicador de estado cambia a **Connected** cuando el intercambio de WebSocket se completa correctamente.
5. Opcionalmente haga clic en **Auto-start on startup** para que la conexión se establezca automáticamente cada vez que AetherSDR se inicie.
6. Opcionalmente haga clic en **Spot Color:** para abrir el selector de color y asignar un color distinto a los spots de FreeDV en el panadapter. El color elegido se guarda en `FreeDvSpotColor`.

## Reportar su estación al mapa del Reportero de FreeDV

El grupo **Station Reporting** en la parte inferior de la pestaña **FreeDV** le permite transmitir su actividad al mapa público del Reportero de FreeDV en `qso.freedv.org` cada vez que el módem RADE está activo.

### Requisitos antes de habilitar

- Un indicativo válido debe estar presente en el campo **Callsign:** (u obtenido de la radio).
- Una cuadrícula Maidenhead válida debe estar presente en el campo **Grid Square:** (u obtenida del GPS de la radio).

Si alguno de estos valores está en blanco cuando marca **Enable FreeDV Reporter reporting when RADE is active**, AetherSDR muestra una advertencia y deja la casilla desmarcada. Esto evita que valores en blanco o de marcador de posición se transmitan al mapa público compartido.

### Pasos de configuración

1. En el grupo **Station Reporting**, revise el campo **Callsign:**.
   - Si **Use radio** está marcado (el valor predeterminado), el campo se rellena previamente con el indicativo configurado en su radio y es de solo lectura. Los cambios al indicativo de la radio en Radio Setup se reflejan automáticamente.
   - Desmarque **Use radio** para ingresar un indicativo manualmente. El valor ingresado se guarda en `FreeDvMyCallsign` y se convierte a mayúsculas al guardarlo.
2. Revise el campo **Grid Square:**.
   - Si su radio tiene hardware GPS y **Use GPS** está marcado (el valor predeterminado en modelos con GPS), el campo se rellena previamente desde la posición GPS de la radio y es de solo lectura. La casilla **Use GPS** está oculta en modelos de radio sin hardware GPS.
   - Desmarque **Use GPS** (o si la casilla no está presente) para ingresar una cuadrícula manualmente. El valor se guarda en `FreeDvMyGrid` y se convierte a mayúsculas al guardarlo.
3. Opcionalmente complete **Station Msg:** con una nota breve de texto libre. Este mensaje aparece junto a su indicativo en el mapa público del Reportero de FreeDV y se guarda en `FreeDvMyMessage`.
4. Marque **Enable FreeDV Reporter reporting when RADE is active**. AetherSDR valida el indicativo y la cuadrícula antes de aceptar el cambio, luego guarda `FreeDvAutoReport` = `True` y emite la señal de reporte habilitado.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Server:** | Indicador | Punto final fijo: `qso.freedv.org (WebSocket)`. Solo lectura. |
| **Start / Stop** | Botón de presión | Conecta o desconecta el WebSocket de FreeDV. |
| **Auto-start on startup** | Botón de alternancia | Inicia la conexión de FreeDV automáticamente al lanzamiento. Se guarda en `FreeDvAutoStart`. |
| **FreeDV Spots** | Campo de texto | Consola de solo lectura que muestra la actividad entrante de FreeDV. |
| **Spot Color:** | Botón de presión | Abre un selector de color para spots de FreeDV en el panadapter. Se guarda en `FreeDvSpotColor`. |
| **Enable FreeDV Reporter reporting when RADE is active** | Casilla | Habilita el reporte de estación al mapa público del Reportero de FreeDV cada vez que el módem RADE está activo. Se rechaza si el indicativo o la cuadrícula están en blanco. Se guarda en `FreeDvAutoReport`. Controlado por compilación mediante `HAVE_WEBSOCKETS`; en Windows también requiere `HAVE_RADE`. |
| **Callsign:** | Campo de texto | Indicativo a reportar al mapa del Reportero de FreeDV. Solo lectura cuando **Use radio** está marcado. Se guarda en `FreeDvMyCallsign`. |
| **Use radio** | Casilla | Rellena previamente **Callsign:** con el indicativo configurado en la radio y bloquea el campo como solo lectura. Se sincroniza automáticamente cuando cambia el indicativo de la radio. Se guarda en `FreeDvUseRadioCallsign`. Predeterminado: habilitado. |
| **Grid Square:** | Campo de texto | Cuadrícula Maidenhead a reportar. Solo lectura cuando **Use GPS** está marcado. Se guarda en `FreeDvMyGrid`. |
| **Use GPS** | Casilla | Rellena previamente **Grid Square:** desde el módulo GPS de la radio y bloquea el campo como solo lectura. Se muestra solo en modelos de radio con hardware GPS. Se guarda en `FreeDvUseGpsGrid`. Predeterminado: habilitado en modelos con GPS. |
| **Station Msg:** | Campo de texto | Mensaje opcional de texto libre que aparece junto a su indicativo en el mapa público del Reportero de FreeDV. Se guarda en `FreeDvMyMessage`. |

## Consejos

- La actividad entrante aparece en la consola **FreeDV Spots** así como en la tabla de spots unificada en la pestaña **Spot List**.
- Si desea que los spots de FreeDV se destaquen de los spots de clúster DX o RBN, establezca un color único usando **Spot Color:** antes de conectarse.
- Si **Use radio** está marcado, actualizar su indicativo en Radio Setup refresca inmediatamente el campo **Callsign:** sin reabrirSpotHub.
- La transmisión del reportero solo se activa mientras el módem RADE está en ejecución. Puede dejar la casilla habilitada en todo momento; no se envían datos cuando RADE está inactivo.

## Solución de problemas

- **La pestaña FreeDV está ausente** — Su compilación de AetherSDR se compiló sin soporte de WebSocket. La pestaña está oculta en el momento de la compilación y no puede habilitarse en tiempo de ejecución.
- **El estado permanece Disconnected después de hacer clic en Start** — Verifique su conexión a Internet. El punto final fijo `qso.freedv.org` debe ser alcanzable desde su máquina en el puerto WebSocket. Los cortafuegos o configuraciones de proxy pueden bloquear la conexión.
- **Los spots aparecen en la consola pero no en el panadapter** — Verifique que **Spots:** esté establecido en **Enabled** en la pestaña **Display** de SpotHub.
- **Aparece la advertencia "Please set both a callsign and a grid square"** — Complete tanto **Callsign:** como **Grid Square:** antes de marcar **Enable FreeDV Reporter reporting when RADE is active**. Si **Use radio** o **Use GPS** está marcado pero la radio aún no ha proporcionado esos valores, desmarque la opción correspondiente e ingrese los valores manualmente.
- **La casilla Use GPS no es visible** — Su modelo de radio no tiene hardware GPS. Ingrese una cuadrícula manualmente en el campo **Grid Square:**.

## Relacionado

- [Descripción general de SpotHub](overview.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Ajustar la densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
