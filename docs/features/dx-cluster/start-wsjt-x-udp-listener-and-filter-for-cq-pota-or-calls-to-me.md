# Iniciar el escucha UDP de WSJT-X y filtrar por CQ, POTA o llamadas a mí

Configure AetherSDR para recibir transmisiones decodificadas de WSJT-X a través de UDP y mostrar solo las categorías de spots que le interesan — llamadas CQ, activaciones POTA o estaciones llamando su indicativo — como superposiciones en el panadapter.

## Antes de comenzar

- WSJT-X debe estar en ejecución en la misma máquina o red y configurado para enviar mensajes de estado UDP a la dirección y puerto que establecerá aquí.
- Debe conocer la dirección y puerto UDP a los que WSJT-X está transmitiendo (consulte WSJT-X en **File > Settings > Reporting**, sección UDP Server).
- Su indicativo debe estar configurado en WSJT-X para que el filtro "Calling Me" funcione.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **WSJT-X**.
3. En **Address:**, ingrese la dirección UDP en la que AetherSDR debe escuchar (almacenada como `WsjtxAddress`). Use `127.0.0.1` si WSJT-X se ejecuta en la misma máquina, o `0.0.0.0` para escuchar en todas las interfaces.
4. En **Port:**, ingrese el número de puerto UDP que coincida con el puerto configurado en WSJT-X (almacenado como `WsjtxPort`; rango válido 1–65535).
5. Haga clic en **Start**. El indicador de estado cambia a **Listening**.
6. Para iniciar el escucha automáticamente cada vez que AetherSDR se inicia, active **Auto-start on startup (WSJT-X)** (almacenado como `WsjtxAutoStart`).
7. Bajo las casillas de filtro, active una o más de las siguientes opciones para restringir qué decodificaciones aparecen como spots en el panadapter:
   - **CQ** — muestra estaciones enviando una llamada CQ general (almacenado como `WsjtxFilterCQ`).
   - **CQ POTA** — muestra estaciones enviando CQ POTA (almacenado como `WsjtxFilterPOTA`).
   - **Calling Me** — muestra decodificaciones dirigidas a su indicativo (almacenado como `WsjtxFilterCallingMe`).
8. Opcionalmente asigne un color distinto a cada categoría haciendo clic en el botón de color correspondiente:
   - **CQ color** (almacenado como `WsjtxColorCQ`)
   - **POTA color** (almacenado como `WsjtxColorPOTA`)
   - **Calling Me color** (almacenado como `WsjtxColorCallingMe`)
   - **Default color** para decodificaciones que no cumplen ningún filtro activo (almacenado como `WsjtxColorDefault`)
9. Establezca **Spot Life:** al número de segundos que un spot de WSJT-X debe permanecer visible en el panadapter (almacenado como `WsjtxSpotLife`).
10. Confirme que las transmisiones decodificadas están llegando en la consola **WSJT-X Decodes** en la parte inferior de la pestaña.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **Address:** | Dirección UDP en la que escuchar mensajes de WSJT-X entrantes. | `WsjtxAddress` |
| **Port:** | Número de puerto UDP. Debe coincidir con el puerto de informes de WSJT-X. | `WsjtxPort` |
| **Start / Stop** | Inicia o detiene el escucha UDP. | — |
| **Auto-start on startup (WSJT-X)** | Inicia el escucha automáticamente al lanzar la aplicación. | `WsjtxAutoStart` |
| **CQ** | Pasa solo transmisiones CQ al panadapter. | `WsjtxFilterCQ` |
| **CQ POTA** | Pasa solo transmisiones CQ POTA. | `WsjtxFilterPOTA` |
| **Calling Me** | Pasa solo decodificaciones dirigidas a su indicativo. | `WsjtxFilterCallingMe` |
| **CQ color** | Color para spots CQ en el panadapter. | `WsjtxColorCQ` |
| **POTA color** | Color para spots CQ POTA. | `WsjtxColorPOTA` |
| **Calling Me color** | Color para spots que llaman su indicativo. | `WsjtxColorCallingMe` |
| **Default color** | Color para spots que no coinciden con ningún filtro activo. | `WsjtxColorDefault` |
| **Spot Life:** | Segundos que un spot de WSJT-X permanece en el panadapter antes de desaparecer. | `WsjtxSpotLife` |
| **WSJT-X Decodes** | Consola de solo lectura que muestra transmisiones decodificadas a medida que llegan. | — |

## Informes de estación FreeDV Reporter

La pestaña **FreeDV** contiene un grupo **Station Reporting** que permite a AetherSDR transmitir la actividad de su estación al mapa público de FreeDV Reporter en `qso.freedv.org`. Esta sección solo está presente en compilaciones compiladas con `HAVE_WEBSOCKETS`; en Windows además requiere `HAVE_RADE`.

### Controles

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **Enable FreeDV Reporter reporting when RADE is active** | Habilita los informes de estación al mapa público de FreeDV Reporter siempre que el módem RADE esté activo. La casilla se niega a activarse si el campo de indicativo o de cuadrícula se resuelve a un valor vacío; un diálogo de advertencia explica qué falta. Predeterminado: desactivado. | `FreeDvAutoReport` |
| **Callsign:** | Indicativo enviado al mapa de FreeDV Reporter. El campo es de solo lectura mientras **Use radio** está marcado. El indicativo se actualiza automáticamente si lo cambia en Radio Setup mientras **Use radio** está activo. | `FreeDvMyCallsign` |
| **Use radio (callsign)** | Rellena previamente el campo de indicativo desde el indicativo configurado en la radio y bloquea el campo como de solo lectura. Predeterminado: activado. | `FreeDvUseRadioCallsign` |
| **Grid Square:** | Cuadrícula Maidenhead enviada al mapa de FreeDV Reporter. El campo es de solo lectura mientras **Use GPS** está marcado. | `FreeDvMyGrid` |
| **Use GPS (grid)** | Rellena previamente el campo de cuadrícula desde el módulo GPS de la radio y bloquea el campo como de solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. | `FreeDvUseGpsGrid` |
| **Station Msg:** | Mensaje de texto libre opcional que se muestra junto a su indicativo en el mapa público de FreeDV Reporter. | `FreeDvMyMessage` |

### Habilitar los informes de FreeDV Reporter

1. Abra `Settings > SpotHub...` y haga clic en la pestaña **FreeDV**.
2. En el grupo **Station Reporting**, verifique que el campo **Callsign:** muestre su indicativo.
   - Si **Use radio** está marcado, el indicativo se toma automáticamente de la radio. Desmarquélo para ingresar un indicativo manualmente.
3. Verifique que el campo **Grid Square:** muestre su localizador Maidenhead (p. ej. `FN20`).
   - En radios con hardware GPS, marque **Use GPS (grid)** para rellenar el campo automáticamente. De lo contrario, ingrese la cuadrícula manualmente.
4. Opcionalmente ingrese un mensaje corto en **Station Msg:** para que aparezca junto a su indicativo en el mapa.
5. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si el indicativo o la cuadrícula están vacíos, aparece un diálogo de advertencia y la casilla se deja sin marcar. Rellene el campo faltante e intente nuevamente.
   - Cuando la casilla se activa correctamente, AetherSDR comienza a informar a `qso.freedv.org` siempre que el módem RADE esté activo.
6. Para informar automáticamente en cada inicio, active también **Auto-start on startup (FreeDV)** (almacenado como `FreeDvAutoStart`) para que el WebSocket de FreeDV se conecte sin intervención manual.

### Notas sobre la validación de indicativo y cuadrícula

Cuando marca **Enable FreeDV Reporter reporting when RADE is active**, AetherSDR resuelve el indicativo y la cuadrícula efectivos utilizando el mismo orden de prioridad que utiliza el motor de informes principal:

- **Indicativo**: indicativo de la radio (si **Use radio** está marcado y la radio tiene uno configurado), de lo contrario el valor en el campo **Callsign:**.
- **Cuadrícula**: cuadrícula GPS (si **Use GPS** está marcado y la radio tiene hardware GPS con una solución), de lo contrario el valor en el campo **Grid Square:**.

Si alguno de los valores resueltos está vacío, la casilla se desmarca automáticamente y un diálogo le pide que proporcione la información faltante. Esto evita que valores en blanco o de marcador de posición se transmitan al mapa compartido de la comunidad.

## Consejos

- Si ninguna de las tres casillas de filtro (**CQ**, **CQ POTA**, **Calling Me**) está marcada, todas las transmisiones decodificadas se muestran en el panadapter independientemente de su contenido.
- Los spots de WSJT-X aparecen en la pestaña unificada **Spot List** junto con spots de otras fuentes. Haga doble clic en cualquier fila para sintonizar directamente esa frecuencia.
- Los spots de WSJT-X solo aparecerán en el panadapter si el control **Spots:** maestro en la pestaña **Display** está habilitado (almacenado como `IsSpotsEnabled`; predeterminado Habilitado).
- FT8 funciona en un ciclo de 15 segundos. Mantenga **Spot Life:** en 15 segundos o un múltiplo del mismo para que los spots se desvanezcan limpiamente entre ciclos.
- FreeDV Reporter es un recurso comunitario. No lo habilite con un indicativo de prueba o una cuadrícula de marcador de posición.

## Solución de problemas

- **El estado permanece en Stopped / no aparecen decodificaciones en la consola** — Verifique que la dirección y el puerto en AetherSDR coincidan exactamente con lo configurado en WSJT-X en **File > Settings > Reporting**. Confirme que ningún firewall está bloqueando el puerto UDP. Haga clic en **Stop** luego en **Start** después de corregir los valores.
- **Los spots aparecen en la pestaña Spot List pero no en el panadapter** — Abra `Settings > SpotHub...`, vaya a la pestaña **Display**, y confirme que **Spots:** está configurado en Enabled.
- **El filtro "Calling Me" no muestra spots** — WSJT-X debe tener su indicativo ingresado en su configuración y debe estar decodificando activamente transmisiones dirigidas a ese indicativo. Verifique su indicativo en WSJT-X en **File > Settings > General**.
- **La casilla de FreeDV Reporter se desmarca inmediatamente** — El campo de indicativo o cuadrícula está vacío o no se resolvió. Rellene ambos campos (o active **Use radio** / **Use GPS** para que se rellenen desde la radio) e intente nuevamente.
- **La sección de FreeDV Reporter no es visible** — La compilación no incluye soporte WebSocket (`HAVE_WEBSOCKETS`). Comuníquese con su proveedor de paquetes o compile AetherSDR desde la fuente con soporte WebSocket habilitado.

## Relacionado

- [Descripción general de SpotHub](overview.md)
- [Ajustar densidad, posición, tamaño de fuente y duración del spot](tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Elegir colores para cada fuente de spot](pick-colors-for-each-spot-source.md)
- [Consultar activaciones POTA](poll-pota-activations.md)
- [Configurar modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
