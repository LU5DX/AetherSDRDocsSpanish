# Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a usted

Configure AetherSDR para recibir transmisiones decodificadas de WSJT-X por UDP y mostrar solo las categorías de spots que le interesan — llamadas CQ, activaciones POTA o estaciones que lo llaman a usted — como superposiciones en el panadapter.

## Antes de comenzar

- WSJT-X debe estar en ejecución en la misma máquina o red, y configurado para enviar mensajes de estado UDP a la dirección y puerto que establecerá aquí.
- Conozca la dirección UDP y el puerto al que WSJT-X está transmitiendo (verifíquelo en WSJT-X en **File > Settings > Reporting**, sección UDP Server).
- Su indicativo debe estar configurado en WSJT-X para que funcione el filtro "Calling Me".

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **WSJT-X**.
3. En **Address:**, ingrese la dirección de enlace UDP en la que AetherSDR debe escuchar (almacenada como `WsjtxAddress`). Use `127.0.0.1` si WSJT-X se ejecuta en la misma máquina, o `0.0.0.0` para escuchar en todas las interfaces.
4. En **Port:**, ingrese el número de puerto UDP que coincida con el puerto configurado en WSJT-X (almacenado como `WsjtxPort`; rango válido 1–65535).
5. Haga clic en **Start**. El indicador de estado cambia a **Listening**.
6. Para iniciar el receptor automáticamente cada vez que AetherSDR se inicie, habilite **Auto-start on startup (WSJT-X)** (almacenado como `WsjtxAutoStart`).
7. Bajo las casillas de verificación de filtro, habilite una o más de las siguientes opciones para restringir qué decodificaciones aparecen como spots en el panadapter:
   - **CQ** — muestra estaciones que envían una llamada CQ general (almacenado como `WsjtxFilterCQ`).
   - **CQ POTA** — muestra estaciones que envían CQ POTA (almacenado como `WsjtxFilterPOTA`).
   - **Calling Me** — muestra decodificaciones dirigidas a su indicativo (almacenado como `WsjtxFilterCallingMe`).
8. Opcionalmente, asigne un color distintivo a cada categoría haciendo clic en el botón de color correspondiente:
   - **CQ color** (almacenado como `WsjtxColorCQ`)
   - **POTA color** (almacenado como `WsjtxColorPOTA`)
   - **Calling Me color** (almacenado como `WsjtxColorCallingMe`)
   - **Default color** para decodificaciones que no pasan ningún filtro activo (almacenado como `WsjtxColorDefault`)
9. Establezca **Spot Life:** con el número de segundos que un spot de WSJT-X debe permanecer visible en el panadapter (almacenado como `WsjtxSpotLife`).
10. Confirme que las transmisiones decodificadas estén llegando en la consola **WSJT-X Decodes** en la parte inferior de la pestaña.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **Address:** | Dirección de enlace UDP para mensajes entrantes de WSJT-X. | `WsjtxAddress` |
| **Port:** | Número de puerto UDP. Debe coincidir con el puerto de reporte de WSJT-X. | `WsjtxPort` |
| **Start / Stop** | Inicia o detiene el receptor UDP. | — |
| **Auto-start on startup (WSJT-X)** | Inicia el receptor automáticamente al lanzar la aplicación. | `WsjtxAutoStart` |
| **CQ** | Pasa al panadapter solo las transmisiones CQ. | `WsjtxFilterCQ` |
| **CQ POTA** | Pasa solo las transmisiones CQ POTA. | `WsjtxFilterPOTA` |
| **Calling Me** | Pasa solo las decodificaciones dirigidas a su indicativo. | `WsjtxFilterCallingMe` |
| **CQ color** | Color para los spots CQ en el panadapter. | `WsjtxColorCQ` |
| **POTA color** | Color para los spots CQ POTA. | `WsjtxColorPOTA` |
| **Calling Me color** | Color para los spots que lo llaman a usted. | `WsjtxColorCallingMe` |
| **Default color** | Color para los spots que no coinciden con ningún filtro activo. | `WsjtxColorDefault` |
| **Spot Life:** | Segundos que un spot de WSJT-X permanece en el panadapter antes de desvanecerse. | `WsjtxSpotLife` |
| **WSJT-X Decodes** | Consola de solo lectura que muestra las transmisiones decodificadas a medida que llegan. | — |

## Reporte de estación en FreeDV Reporter

La pestaña **FreeDV** contiene un grupo **Station Reporting** que permite a AetherSDR transmitir la actividad de su estación al mapa público de FreeDV Reporter en `qso.freedv.org`. Esta sección solo está presente en compilaciones realizadas con `HAVE_WEBSOCKETS`; en Windows además requiere `HAVE_RADE`.

### Controles

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **Enable FreeDV Reporter reporting when RADE is active** | Habilita el reporte de estación al mapa público de FreeDV Reporter siempre que el módem RADE esté activo. La casilla rechaza habilitarse si el campo de indicativo o de localizador de cuadrícula se resuelve como un valor vacío; un diálogo de advertencia explica qué falta. Valor predeterminado: deshabilitado. | `FreeDvAutoReport` |
| **Callsign:** | Indicativo enviado al mapa de FreeDV Reporter. El campo es de solo lectura mientras **Use radio** esté marcado. El indicativo se actualiza automáticamente si lo cambia en Radio Setup mientras **Use radio** está activo. | `FreeDvMyCallsign` |
| **Use radio (callsign)** | Rellena automáticamente el campo de indicativo con el indicativo configurado en el radio y bloquea el campo como solo lectura. Valor predeterminado: habilitado. | `FreeDvUseRadioCallsign` |
| **Grid Square:** | Localizador de cuadrícula Maidenhead enviado al mapa de FreeDV Reporter. El campo es de solo lectura mientras **Use GPS** esté marcado. | `FreeDvMyGrid` |
| **Use GPS (grid)** | Rellena automáticamente el campo de cuadrícula con datos del módulo GPS del radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. | `FreeDvUseGpsGrid` |
| **Station Msg:** | Mensaje de texto libre opcional que se muestra junto a su indicativo en el mapa público de FreeDV Reporter. | `FreeDvMyMessage` |

### Habilitación del reporte en FreeDV Reporter

1. Abra `Settings > SpotHub...` y haga clic en la pestaña **FreeDV**.
2. En el grupo **Station Reporting**, verifique que el campo **Callsign:** muestre su indicativo.
   - Si **Use radio** está marcado, el indicativo se toma automáticamente del radio. Desmarque esta opción para ingresar un indicativo manualmente.
3. Verifique que el campo **Grid Square:** muestre su localizador Maidenhead (p. ej., `FN20`).
   - En radios con hardware GPS, marque **Use GPS (grid)** para rellenar el campo automáticamente. De lo contrario, ingrese el localizador de cuadrícula manualmente.
4. Opcionalmente ingrese un mensaje corto en **Station Msg:** para que aparezca junto a su indicativo en el mapa.
5. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si el indicativo o el localizador de cuadrícula están vacíos, aparece un diálogo de advertencia y la casilla queda sin marcar. Complete el campo faltante e inténtelo de nuevo.
   - Cuando la casilla se habilita correctamente, AetherSDR comienza a reportar a `qso.freedv.org` siempre que el módem RADE esté activo.
6. Para reportar automáticamente en cada inicio, habilite también **Auto-start on startup (FreeDV)** (almacenado como `FreeDvAutoStart`) para que el WebSocket de FreeDV se conecte sin intervención manual.

### Notas sobre la validación del indicativo y el localizador

Al marcar **Enable FreeDV Reporter reporting when RADE is active**, AetherSDR resuelve el indicativo y el localizador de cuadrícula efectivos usando el mismo orden de prioridad que utiliza el motor de reporte principal:

- **Indicativo**: indicativo del radio (si **Use radio** está marcado y el radio tiene uno configurado); de lo contrario, el valor del campo **Callsign:**.
- **Localizador de cuadrícula**: cuadrícula por GPS (si **Use GPS** está marcado y el radio tiene hardware GPS con señal de posición); de lo contrario, el valor del campo **Grid Square:**.

Si cualquiera de los valores resueltos está vacío, la casilla se desmarca automáticamente y un diálogo le solicita que proporcione la información faltante. Esto evita que valores en blanco o de marcador de posición se transmitan al mapa comunitario compartido.

## Cambio en el valor predeterminado del modo automático

A partir de la versión v0.9.5.1, el botón **Auto Mode:** en la pestaña **Display** tiene como valor predeterminado **Enabled** (almacenado como `SpotAutoSwitchMode`). En versiones anteriores, el valor predeterminado era Disabled. Si no ha cambiado esta configuración, AetherSDR seleccionará automáticamente la densidad de spots según el nivel de zoom actual del panadapter inmediatamente después de una instalación nueva o un restablecimiento de configuración.

## Consejos

- Si ninguna de las tres casillas de filtro (**CQ**, **CQ POTA**, **Calling Me**) está marcada, todas las transmisiones decodificadas se muestran en el panadapter independientemente de su contenido.
- Los spots de WSJT-X aparecen en la pestaña unificada **Spot List** junto con spots de otras fuentes. Haga doble clic en cualquier fila para sintonizarse directamente a esa frecuencia.
- Los spots de WSJT-X solo aparecerán en el panadapter si el selector principal **Spots:** en la pestaña **Display** está habilitado (almacenado como `IsSpotsEnabled`; valor predeterminado: Enabled).
- FT8 opera en ciclos de 15 segundos. Mantenga **Spot Life:** en 15 segundos o un múltiplo de ese valor para que los spots expiren de forma limpia entre ciclos.
- El reporte en FreeDV Reporter es un recurso comunitario. No lo habilite con un indicativo de prueba ni un localizador de cuadrícula de marcador de posición.

## Solución de problemas

- **El estado permanece en Stopped / no aparecen decodificaciones en la consola** — Verifique que la dirección y el puerto en AetherSDR coincidan exactamente con los configurados en WSJT-X en **File > Settings > Reporting**. Confirme que ningún firewall esté bloqueando el puerto UDP. Haga clic en **Stop** y luego en **Start** después de corregir los valores.
- **Los spots aparecen en la pestaña Spot List pero no en el panadapter** — Abra `Settings > SpotHub...`, vaya a la pestaña **Display** y confirme que **Spots:** esté configurado como Enabled.
- **El filtro "Calling Me" no muestra spots** — WSJT-X debe tener su indicativo ingresado en su configuración y debe estar decodificando activamente transmisiones dirigidas a ese indicativo. Verifique su indicativo en WSJT-X en **File > Settings > General**.
- **La casilla de FreeDV Reporter se desmarca inmediatamente** — El campo de indicativo o de localizador de cuadrícula está vacío o no pudo resolverse. Complete ambos campos (o habilite **Use radio** / **Use GPS** para que se rellenen desde el radio) e inténtelo de nuevo.
- **La sección de FreeDV Reporter no está visible** — La compilación no incluye soporte para WebSocket (`HAVE_WEBSOCKETS`). Contacte a su proveedor del paquete o compile AetherSDR desde el código fuente con soporte para WebSocket habilitado.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Consultar activaciones POTA](poll-pota-activations.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
