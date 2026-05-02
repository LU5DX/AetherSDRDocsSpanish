# Habilitar el WebSocket del reportador de QSO FreeDV

Conecte AetherSDR al reportador de QSO FreeDV en `qso.freedv.org` para recibir manchas (spots) de actividad FreeDV en su panadapter.

## Antes de comenzar

- La fuente WebSocket de FreeDV está disponible únicamente en versiones de AetherSDR compiladas con soporte WebSocket (`HAVE_WEBSOCKETS`). Si la pestaña FreeDV no aparece en SpotHub, su versión no lo incluye.
- Los spots aparecen en el panadapter solo cuando la superposición maestra de spots está habilitada. Consulte [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los spots](tune-spot-density-position-font-size-and-lifetime.md) si los spots no son visibles tras conectarse.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **FreeDV**.
3. Confirme que el indicador **Server:** muestra `qso.freedv.org (WebSocket)`. Este punto de conexión es fijo y no puede modificarse.
4. Haga clic en **Start**. El indicador de estado cambia a **Connected** cuando el protocolo de enlace WebSocket se completa con éxito.
5. Opcionalmente, haga clic en **Auto-start on startup** para que la conexión se establezca automáticamente cada vez que AetherSDR se inicie.
6. Opcionalmente, haga clic en **Spot Color:** para abrir el selector de color y asignar un color distintivo a los spots FreeDV en el panadapter. El color elegido se guarda en `FreeDvSpotColor`.

## Reportar su estación al mapa FreeDV Reporter

El grupo **Station Reporting** en la parte inferior de la pestaña **FreeDV** le permite transmitir su actividad al mapa público FreeDV Reporter en `qso.freedv.org` cuando el módem RADE está activo.

### Requisitos previos para habilitarlo

- Debe haber un indicativo válido en el campo **Callsign:** (o proporcionado por el radio).
- Debe haber un localizador Maidenhead válido en el campo **Grid Square:** (o proporcionado por el GPS del radio).

Si alguno de estos valores está en blanco al marcar **Enable FreeDV Reporter reporting when RADE is active**, AetherSDR muestra una advertencia y deja la casilla sin marcar. Esto evita que valores en blanco o de marcador de posición se transmitan al mapa público compartido.

### Pasos de configuración

1. En el grupo **Station Reporting**, revise el campo **Callsign:**.
   - Si **Use radio** está marcado (opción predeterminada), el campo se rellena previamente con el indicativo configurado en su radio y es de solo lectura. Los cambios al indicativo del radio en Radio Setup se reflejan automáticamente.
   - Desmarque **Use radio** para introducir un indicativo manualmente. El valor introducido se guarda en `FreeDvMyCallsign` y se convierte a mayúsculas al guardar.
2. Revise el campo **Grid Square:**.
   - Si su radio dispone de hardware GPS y **Use GPS** está marcado (opción predeterminada en modelos con GPS), el campo se rellena previamente con la posición del GPS del radio y es de solo lectura. La casilla **Use GPS** no aparece en modelos de radio sin hardware GPS.
   - Desmarque **Use GPS** (o si la casilla no está presente) para introducir un localizador manualmente. El valor se guarda en `FreeDvMyGrid` y se convierte a mayúsculas al guardar.
3. Opcionalmente, rellene **Station Msg:** con una nota breve en texto libre. Este mensaje aparece junto a su indicativo en el mapa público FreeDV Reporter y se guarda en `FreeDvMyMessage`.
4. Marque **Enable FreeDV Reporter reporting when RADE is active**. AetherSDR valida el indicativo y el localizador antes de aceptar el cambio, luego guarda `FreeDvAutoReport` = `True` y emite la señal de reporte habilitado.

## Descripción de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Server:** | Indicador | Punto de conexión fijo: `qso.freedv.org (WebSocket)`. Solo lectura. |
| **Start / Stop** | Botón | Conecta o desconecta el WebSocket FreeDV. |
| **Auto-start on startup** | Botón de alternancia | Inicia la conexión FreeDV automáticamente al arrancar. Se guarda en `FreeDvAutoStart`. |
| **FreeDV Spots** | Campo de texto | Consola de solo lectura que muestra la actividad FreeDV entrante. |
| **Spot Color:** | Botón | Abre un selector de color para los spots FreeDV en el panadapter. Se guarda en `FreeDvSpotColor`. |
| **Enable FreeDV Reporter reporting when RADE is active** | Casilla de verificación | Habilita el reporte de estación al mapa público FreeDV Reporter cuando el módem RADE está activo. Se rechaza si el indicativo o el localizador están en blanco. Se guarda en `FreeDvAutoReport`. Condicionado en compilación por `HAVE_WEBSOCKETS`; en Windows también requiere `HAVE_RADE`. |
| **Callsign:** | Campo de texto | Indicativo a reportar al mapa FreeDV Reporter. Solo lectura cuando **Use radio** está marcado. Se guarda en `FreeDvMyCallsign`. |
| **Use radio** | Casilla de verificación | Rellena **Callsign:** con el indicativo configurado en el radio y bloquea el campo como solo lectura. Se sincroniza automáticamente cuando cambia el indicativo del radio. Se guarda en `FreeDvUseRadioCallsign`. Predeterminado: habilitado. |
| **Grid Square:** | Campo de texto | Localizador Maidenhead a reportar. Solo lectura cuando **Use GPS** está marcado. Se guarda en `FreeDvMyGrid`. |
| **Use GPS** | Casilla de verificación | Rellena **Grid Square:** con los datos del módulo GPS del radio y bloquea el campo como solo lectura. Solo visible en modelos de radio con hardware GPS. Se guarda en `FreeDvUseGpsGrid`. Predeterminado: habilitado en modelos con GPS. |
| **Station Msg:** | Campo de texto | Mensaje opcional en texto libre que aparece junto a su indicativo en el mapa público FreeDV Reporter. Se guarda en `FreeDvMyMessage`. |

## Consejos

- La actividad entrante aparece en la consola **FreeDV Spots** y también en la tabla unificada de spots de la pestaña **Spot List**.
- Si desea que los spots FreeDV se distingan de los spots de clúster DX o RBN, asigne un color único mediante **Spot Color:** antes de conectarse.
- Si **Use radio** está marcado, actualizar su indicativo en Radio Setup refresca inmediatamente el campo **Callsign:** sin necesidad de reabrir SpotHub.
- La transmisión al reportador solo se activa mientras el módem RADE está en ejecución. Puede dejar la casilla habilitada en todo momento; no se envían datos cuando RADE está inactivo.
- **Auto Mode:** en la pestaña **Display** está configurado como **Enabled** de forma predeterminada a partir de la v0.9.5.1. La densidad de spots se ajusta automáticamente al hacer zoom en el panadapter sin ninguna configuración manual. Si anteriormente deshabilitó **Auto Mode:** y guardó la configuración desde una versión anterior, verifique si el nuevo valor predeterminado es adecuado para su flujo de trabajo. La configuración se guarda en `SpotAutoSwitchMode`.

## Solución de problemas

- **La pestaña FreeDV no aparece** — Su versión de AetherSDR fue compilada sin soporte WebSocket. La pestaña queda oculta en tiempo de compilación y no puede habilitarse en tiempo de ejecución.
- **El estado permanece Disconnected tras hacer clic en Start** — Verifique su conexión a Internet. El punto de conexión fijo `qso.freedv.org` debe ser accesible desde su equipo en el puerto WebSocket. Los cortafuegos o configuraciones de proxy pueden bloquear la conexión.
- **Los spots aparecen en la consola pero no en el panadapter** — Verifique que **Spots:** esté configurado como **Enabled** en la pestaña **Display** de SpotHub.
- **Aparece la advertencia "Please set both a callsign and a grid square"** — Rellene tanto **Callsign:** como **Grid Square:** antes de marcar **Enable FreeDV Reporter reporting when RADE is active**. Si **Use radio** o **Use GPS** está marcado pero el radio aún no ha proporcionado esos valores, desmarque la opción correspondiente e introduzca los valores manualmente.
- **La casilla Use GPS no es visible** — Su modelo de radio no dispone de hardware GPS. Introduzca un localizador manualmente en el campo **Grid Square:**.

## Relacionado

- [Descripción general de SpotHub](overview.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
