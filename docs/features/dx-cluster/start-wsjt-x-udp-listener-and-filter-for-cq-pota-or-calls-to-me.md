# Iniciar el receptor UDP de WSJT-X y el filtro para CQ, POTA o llamadas dirigidas a mí

Configure AetherSDR para recibir transmisiones decodificadas de WSJT-X a través de UDP y muestre únicamente las categorías de spots que le interesen — llamadas CQ, activaciones POTA o estaciones que llaman a su indicativo — como superposiciones en el panadapter.

## Antes de comenzar

- WSJT-X debe estar ejecutándose en el mismo equipo o en la misma red y configurado para enviar mensajes de estado UDP a la dirección y puerto que establecerá aquí.
- Conozca la dirección y el puerto UDP a los que WSJT-X está transmitiendo (verifique en WSJT-X en **File > Settings > Reporting**, sección UDP Server).
- Su indicativo debe estar configurado en WSJT-X para que el filtro "Calling Me" funcione.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **WSJT-X**.
3. En **Address:**, introduzca la dirección de enlace UDP en la que AetherSDR debe escuchar (almacenada como `WsjtxAddress`). Use `127.0.0.1` si WSJT-X se ejecuta en el mismo equipo, o `0.0.0.0` para escuchar en todas las interfaces.
4. En **Port:**, introduzca el número de puerto UDP que coincida con el puerto configurado en WSJT-X (almacenado como `WsjtxPort`; rango válido 1–65535).
5. Haga clic en **Start**. El indicador de estado cambia a **Listening**.
6. Para iniciar el receptor automáticamente cada vez que se lance AetherSDR, habilite **Auto-start on startup (WSJT-X)** (almacenado como `WsjtxAutoStart`).
7. Debajo de las casillas de verificación del filtro, habilite una o más de las siguientes opciones para restringir qué decodificaciones aparecen como spots en el panadapter:
   - **CQ** — muestra estaciones que envían una llamada CQ general (almacenado como `WsjtxFilterCQ`).
   - **CQ POTA** — muestra estaciones que envían CQ POTA (almacenado como `WsjtxFilterPOTA`).
   - **Calling Me** — muestra decodificaciones dirigidas a su indicativo (almacenado como `WsjtxFilterCallingMe`).
8. Opcionalmente, asigne un color distinto a cada categoría haciendo clic en el botón de color correspondiente:
   - **CQ color** (almacenado como `WsjtxColorCQ`)
   - **POTA color** (almacenado como `WsjtxColorPOTA`)
   - **Calling Me color** (almacenado como `WsjtxColorCallingMe`)
   - **Default color** para decodificaciones que no pasan ningún filtro activo (almacenado como `WsjtxColorDefault`)
9. Establezca **Spot Life:** en el número de segundos que un spot de WSJT-X debe permanecer visible en el panadapter (almacenado como `WsjtxSpotLife`).
10. Confirme que las transmisiones decodificadas están llegando a la consola **WSJT-X Decodes** en la parte inferior de la pestaña.

## Qué hace cada control

| Control                            | Comportamiento                                                                                                                                                         | Clave de configuración |
|------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------|
| **Address:**                       | Dirección de enlace UDP para mensajes WSJT-X entrantes.                                                                                                                | `WsjtxAddress`         |
| **Port:**                          | Número de puerto UDP. Debe coincidir con el puerto de reporte de WSJT-X.                                                                                               | `WsjtxPort`            |
| **Start / Stop**                   | Inicia o detiene el receptor UDP.                                                                                                                                      | —                      |
| **Auto-start on startup (WSJT-X)** | Inicia el receptor automáticamente al iniciar.                                                                                                                          | `WsjtxAutoStart`       |
| **CQ**                             | Solo pasa transmisiones CQ al panadapter.                                                                                                                              | `WsjtxFilterCQ`        |
| **CQ POTA**                        | Solo pasa transmisiones CQ POTA.                                                                                                                                       | `WsjtxFilterPOTA`      |
| **Calling Me**                     | Solo pasa decodificaciones dirigidas a su indicativo.                                                                                                                  | `WsjtxFilterCallingMe` |
| **CQ color**                       | Color para spots CQ en el panadapter.                                                                                                                                  | `WsjtxColorCQ`         |
| **POTA color**                     | Color para spots CQ POTA.                                                                                                                                              | `WsjtxColorPOTA`       |
| **Calling Me color**               | Color para spots que llaman a su indicativo.                                                                                                                           | `WsjtxColorCallingMe`  |
| **Default color**                  | Color para spots que no coinciden con ningún filtro activo.                                                                                                            | `WsjtxColorDefault`    |
| **Spot Life:**                     | Segundos que un spot de WSJT-X permanece en el panadapter antes de desvanecerse.                                                                                       | `WsjtxSpotLife`        |
| **WSJT-X Decodes**                 | Consola de solo lectura que muestra las transmisiones decodificadas a medida que llegan.                                                                                | —                      |
| **Spot Lines:**                    | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Desactive durante concursos para reducir el desorden visual. Valor predeterminado: Activado.    | `IsSpotsLinesEnabled`  |
| Total Spots:                       | Lectura en vivo de cuántos spots se están rastreando actualmente en todas las fuentes. Se actualiza cuando se añaden o borran spots. Se restablece a 0 al presionar **Clear All Spots**. | —                      |
## Sintonizar desde la lista de spots

Al hacer doble clic en una fila de la pestaña **Spot List**, se sintoniza el slice activo en la frecuencia de ese spot. A partir de la versión v0.9.7, AetherSDR también reenvía cualquier información de modo extraída del comentario del spot, por lo que el slice cambia automáticamente al modo correcto (por ejemplo, CW o SSB) para coincidir con el spot, en lugar de solo cambiar la frecuencia.

## Reporte de estación FreeDV Reporter

La pestaña **FreeDV** contiene un grupo **Station Reporting** que permite a AetherSDR transmitir la actividad de su estación al mapa público de FreeDV Reporter en `qso.freedv.org`. Esta sección solo está presente en compilaciones realizadas con `HAVE_WEBSOCKETS`; en Windows, además requiere `HAVE_RADE`.

### Controles

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **Enable FreeDV Reporter reporting when RADE is active** | Habilita el reporte de estación al mapa público de FreeDV Reporter cuando el módem RADE está activo. La casilla de verificación se negará a activarse si el indicativo o el campo de cuadrícula se resuelven como un valor vacío; un cuadro de diálogo de advertencia explica qué falta. Valor predeterminado: deshabilitado. | `FreeDvAutoReport` |
| **Callsign:** | Indicativo enviado al mapa de FreeDV Reporter. El campo es de solo lectura mientras **Use radio** está marcado. El indicativo se actualiza automáticamente si lo cambia en Radio Setup mientras **Use radio** está activo. | `FreeDvMyCallsign` |
| **Use radio (callsign)** | Rellena previamente el campo de indicativo desde el indicativo configurado en la radio y bloquea el campo como solo lectura. Valor predeterminado: habilitado. | `FreeDvUseRadioCallsign` |
| **Grid Square:** | Cuadrícula Maidenhead enviada al mapa de FreeDV Reporter. El campo es de solo lectura mientras **Use GPS** está marcado. | `FreeDvMyGrid` |
| **Use GPS (grid)** | Rellena previamente el campo de cuadrícula desde el módulo GPS de la radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. | `FreeDvUseGpsGrid` |
| **Station Msg:** | Mensaje de texto libre opcional que se muestra junto a su indicativo en el mapa público de FreeDV Reporter. | `FreeDvMyMessage` |

### Habilitar el reporte de FreeDV Reporter

1. Abra `Settings > SpotHub...` y haga clic en la pestaña **FreeDV**.
2. En el grupo **Station Reporting**, verifique que el campo **Callsign:** muestre su indicativo.
   - Si **Use radio** está marcado, el indicativo se toma automáticamente de la radio. Desmárquelo para introducir un indicativo manualmente.
3. Verifique que el campo **Grid Square:** muestre su localizador Maidenhead (por ejemplo, `FN20`).
   - En radios con hardware GPS, marque **Use GPS (grid)** para completar el campo automáticamente. De lo contrario, introduzca la cuadrícula manualmente.
4. Opcionalmente, introduzca un mensaje breve en **Station Msg:** para que aparezca junto a su indicativo en el mapa.
5. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si el indicativo o la cuadrícula están vacíos, aparece un cuadro de diálogo de advertencia y la casilla de verificación se deja sin marcar. Complete el campo faltante e intente nuevamente.
   - Cuando la casilla de verificación se active correctamente, AetherSDR comenzará a reportar a `qso.freedv.org` siempre que el módem RADE esté activo.
6. Para reportar automáticamente en cada inicio, active también **Auto-start on startup (FreeDV)** (almacenado como `FreeDvAutoStart`) para que el WebSocket de FreeDV se conecte sin intervención manual.

### Notas sobre la validación del indicativo y la cuadrícula

Cuando marca **Enable FreeDV Reporter reporting when RADE is active**, AetherSDR resuelve el indicativo y la cuadrícula efectivos utilizando el mismo orden de prioridad que el motor de reporte principal:

- **Indicativo**: indicativo de la radio (si **Use radio** está marcado y la radio tiene uno configurado); de lo contrario, el valor en el campo **Callsign:**.
- **Cuadrícula**: cuadrícula GPS (si **Use GPS** está marcado y la radio tiene hardware GPS con una posición fija); de lo contrario, el valor en el campo **Grid Square:**.

Si alguno de los valores resueltos está vacío, la casilla de verificación se desmarca automáticamente y un cuadro de diálogo le solicita que proporcione la información faltante. Esto evita que se transmitan valores en blanco o provisionales al mapa comunitario compartido.

## Cambio en el valor predeterminado de Auto Mode

A partir de la versión v0.9.5.1, la opción **Auto Mode:** en la pestaña **Display** tiene como valor predeterminado **Enabled** (almacenado como `SpotAutoSwitchMode`). En versiones anteriores, el valor predeterminado era Disabled. Si no ha cambiado esta configuración, AetherSDR ahora cambiará automáticamente el modo del slice cuando haga clic en un spot que incluya información de modo (por ejemplo, CW, FT8, RTTY) inmediatamente después de una instalación nueva o un restablecimiento de la configuración.

## Control Spot Lines añadido (v0.9.7)

La pestaña **Display** ahora incluye una opción **Spot Lines:** (almacenado como `IsSpotsLinesEnabled`; valor predeterminado Enabled). Cuando está habilitada, AetherSDR dibuja una línea vertical desde la línea base del espectro hasta cada etiqueta de spot, lo que facilita localizar la frecuencia exacta de un spot. Desactive esta opción durante concursos o cuando el panadapter esté abarrotado para reducir el desorden visual.

## Consejos

- Si ninguna de las tres casillas de verificación de filtro (**CQ**, **CQ POTA**, **Calling Me**) está marcada, todas las transmisiones decodificadas se muestran en el panadapter independientemente de su contenido.
- Los spots de WSJT-X aparecen en la pestaña unificada **Spot List** junto con spots de otras fuentes. Haga doble clic en cualquier fila para sintonizar directamente esa frecuencia. AetherSDR también cambiará el modo del slice para que coincida con el modo del spot si está presente en el comentario.
- Los spots de WSJT-X solo aparecerán en el panadapter si la opción maestra **Spots:** en la pestaña **Display** está habilitada (almacenado como `IsSpotsEnabled`; valor predeterminado Enabled).
- FT8 opera en un ciclo de 15 segundos. Mantenga **Spot Life:** en 15 segundos o un múltiplo de ello para que los spots caduquen limpiamente entre ciclos.
- El reporte de FreeDV Reporter es un recurso comunitario. No lo active con un indicativo de prueba o una cuadrícula provisional.

## Solución de problemas

- **El estado permanece en Stopped / no aparecen decodificaciones en la consola** — Verifique que la dirección y el puerto en AetherSDR coincidan exactamente con lo configurado en WSJT-X en **File > Settings > Reporting**. Confirme que ningún cortafuegos esté bloqueando el puerto UDP. Haga clic en **Stop** y luego en **Start** después de corregir los valores.
- **Los spots aparecen en la pestaña Spot List pero no en el panadapter** — Abra `Settings > SpotHub...`, vaya a la pestaña **Display** y confirme que **Spots:** esté configurado en Enabled.
- **El filtro "Calling Me" no muestra spots** — WSJT-X debe tener su indicativo introducido en su configuración y debe estar decodificando activamente transmisiones dirigidas a ese indicativo. Verifique su indicativo en WSJT-X en **File > Settings > General**.
- **Al hacer doble clic en un spot no cambia el modo del slice** — La información del modo se lee del comentario del spot. Si el comentario no contiene una cadena de modo reconocible, solo cambia la frecuencia. Verifique que la fuente del spot esté incluyendo datos de modo en sus comentarios.
- **La casilla de verificación de FreeDV Reporter se desmarca inmediatamente** — El campo de indicativo o de cuadrícula está vacío o no se pudo resolver. Complete ambos campos (o active **Use radio** / **Use GPS** para que se completen desde la radio) e intente nuevamente.
- **La sección FreeDV Reporter no es visible**
