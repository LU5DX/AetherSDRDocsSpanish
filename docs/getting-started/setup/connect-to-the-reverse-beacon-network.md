# Conéctese a la Reverse Beacon Network

La Reverse Beacon Network (RBN) proporciona avistamientos automatizados de CW, RTTY y skimmers digitales. Esta página muestra cómo configurar y conectar el feed telnet de RBN de AetherSDR para que los avistamientos de RBN aparezcan en su panadapter.

## Antes de comenzar

- Conozca el nombre de host y puerto del servidor telnet de RBN (el servidor público es `telnet.reversebeacon.net`, puerto `7000` para skimmers CW).
- Conozca el indicativo que usará para iniciar sesión en la RBN.
- Los avistamientos solo aparecerán en el panadapter si la superposición maestra de avistamientos está habilitada (`IsSpotsEnabled` tiene el valor predeterminado Enabled).

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **RBN**.
3. En el campo **Server:**, introduzca el nombre de host telnet de la RBN (ej., `telnet.reversebeacon.net`). Este valor persiste como `RbnHost`.
4. Establezca **Port:** en el puerto telnet para el feed del skimmer que desee. Rango válido: 1–65535. Este valor persiste como `RbnPort`.
5. En el campo **Callsign:**, introduzca su indicativo. Este valor persiste como `RbnCallsign`.
6. Si el feed de la RBN produce más avistamientos de los que necesita, ajuste **Rate Limit:** para limitar la cantidad de avistamientos procesados por segundo. Este valor persiste como `RbnRateLimit`.
7. Haga clic en **Connect**. La etiqueta del botón cambia a **Disconnect** cuando la sesión se establece, y la **RBN Console** muestra el tráfico entrante.
8. Para que AetherSDR se conecte a la RBN automáticamente en cada inicio, active **Auto-connect on startup**. Este valor persiste como `RbnAutoConnect`.

## Función de cada control

| Control                     | Comportamiento                                                                                                                                                         | Clave de configuración |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------|
| **Server:**                 | Nombre de host telnet de la RBN                                                                                                                                        | `RbnHost`              |
| **Port:**                   | Puerto telnet de la RBN                                                                                                                                                | `RbnPort`              |
| **Callsign:**               | Indicativo de inicio de sesión enviado a la RBN                                                                                                                        | `RbnCallsign`          |
| **Rate Limit:**             | Cantidad máxima de avistamientos RBN aceptados por segundo                                                                                                             | `RbnRateLimit`         |
| **Connect / Disconnect**    | Activa/desactiva la sesión telnet de la RBN                                                                                                                            | —                      |
| **Auto-connect on startup** | Se conecta a la RBN automáticamente al inicio                                                                                                                          | `RbnAutoConnect`       |
| **RBN Console**             | Visualización de solo lectura del tráfico RBN sin procesar                                                                                                             | —                      |
| **Send**                    | Envía un comando escrito a la sesión de la RBN                                                                                                                         | —                      |
| **Spot Color:**             | Abre un selector de color para los avistamientos RBN en el panadapter                                                                                                  | `RbnSpotColor`         |
| **Spot Lines:**             | Dibuja líneas verticales desde el espectro hasta cada etiqueta de avistamiento. Desactive durante concursos para reducir el desorden visual.                           | `IsSpotsLinesEnabled`  |
| Total Spots:                | Indicador en vivo de cuántos avistamientos se están rastreando actualmente en todas las fuentes. Se actualiza cuando se añaden o eliminan avistamientos. Se reinicia a 0 cuando se presiona **Clear All Spots**. | —                      |

## Al hacer doble clic en un avistamiento ahora se reenvían las sugerencias de modo

A partir de la versión v0.9.7, al hacer doble clic en una fila de la pestaña **Spot List** se sintoniza el receptor en la frecuencia del avistamiento y también se cambia el modo del receptor para que coincida con el avistamiento. Por ejemplo, hacer doble clic en un avistamiento CW cambia el receptor a CW, y hacer doble clic en un avistamiento FT8 lo cambia al modo digital apropiado, en lugar de solo cambiar la frecuencia. El modo se resuelve a partir del comentario del avistamiento mediante la lógica `SpotModeResolver` compartida entre todas las fuentes de avistamientos.

## Spot Lines

La pestaña **Display** ahora incluye una opción **Spot Lines:** (nueva en v0.9.7). Cuando está **Enabled** (valor predeterminado), AetherSDR dibuja una línea vertical corta desde la traza del espectro hasta cada etiqueta de avistamiento en el panadapter, lo que facilita ver exactamente a qué frecuencia corresponde un avistamiento. Ajústelo a **Disabled** durante concursos u otras sesiones de operación con alta densidad de avistamientos para reducir el desorden visual. Este valor persiste como `IsSpotsLinesEnabled`.

## Reporte de estación del FreeDV Reporter

La pestaña **FreeDV** contiene una sección **Station Reporting** que permite a AetherSDR transmitir la actividad de su estación al mapa público del FreeDV Reporter en `qso.freedv.org` cada vez que el módem RADE esté activo. Esta función está controlada por una compilación condicional mediante `HAVE_WEBSOCKETS`; en Windows también requiere la protección interna `HAVE_RADE`.

### Controles

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **Enable FreeDV Reporter reporting when RADE is active** | Habilita el reporte de estación al mapa público del FreeDV Reporter cada vez que el módem RADE esté activo. La casilla de verificación se niega a habilitarse si el campo de indicativo o de cuadrícula se resuelve en un valor vacío. | `FreeDvAutoReport` |
| **Callsign:** | Indicativo reportado al mapa del FreeDV Reporter. Se vuelve de solo lectura cuando **Use radio** está marcado. | `FreeDvMyCallsign` |
| **Use radio** | Rellena previamente el campo de indicativo desde el indicativo configurado en la radio y bloquea el campo como solo lectura. Cuando el indicativo de la radio cambia (por ejemplo, en Radio Setup), el campo se actualiza automáticamente. | `FreeDvUseRadioCallsign` |
| **Grid Square:** | Cuadrícula Maidenhead reportada. Se vuelve de solo lectura cuando **Use GPS** está marcado. | `FreeDvMyGrid` |
| **Use GPS** | Rellena previamente el campo de cuadrícula desde el módulo GPS de la radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. | `FreeDvUseGpsGrid` |
| **Station Msg:** | Mensaje de texto libre opcional que se muestra junto al indicativo en el mapa público del FreeDV Reporter. | `FreeDvMyMessage` |

### Habilitación del reporte de estación

1. Haga clic en la pestaña **FreeDV** dentro de `Settings > SpotHub...`.
2. En el grupo **Station Reporting**, introduzca o confirme su **Callsign:**. Marque **Use radio** para obtenerlo automáticamente de la radio.
3. Introduzca o confirme su **Grid Square:**. En radios con hardware GPS, marque **Use GPS** para completarlo automáticamente.
4. Opcionalmente, rellene **Station Msg:** con una nota de texto libre breve.
5. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si el indicativo o la cuadrícula se resuelven en un valor vacío, aparece un cuadro de diálogo de advertencia y la casilla de verificación se desmarca. Rellene el campo faltante e intente de nuevo.
   - Cuando está habilitado, la configuración persiste como `FreeDvAutoReport`.

> **Nota:** El mapa del FreeDV Reporter es un recurso público compartido por la comunidad. AetherSDR bloquea la habilitación de esta función si el indicativo o la cuadrícula están en blanco para evitar que valores provisionales como `N0CALL` o `AA00` aparezcan en el mapa.

## Cambio en el valor predeterminado de Auto Mode

En la versión v0.9.5.1, la opción **Auto Mode:** en la pestaña **Display** tiene el valor predeterminado **Enabled** para instalaciones nuevas. La configuración persiste como `SpotAutoSwitchMode`. Las instalaciones existentes donde el valor se haya guardado explícitamente no se ven afectadas.

## Consejos

- La **RBN Console** es de solo lectura y muestra las líneas telnet sin procesar a medida que llegan. Use la línea de comando **Send** debajo de ella para emitir comandos de filtro directamente al servidor RBN (ej., `set/skimmer` o comandos de filtro de banda compatibles con la RBN).
- Si el panadapter se satura durante un concurso, reduzca **Rate Limit:** para disminuir la densidad de avistamientos sin desconectarse. También puede desactivar **Spot Lines:** en la pestaña **Display** para reducir aún más el desorden visual.
- Para cambiar el aspecto de los avistamientos en el panadapter (tamaño, posición, tiempo de vida y apilamiento), consulte [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los avistamientos](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md).
- Los avistamientos RBN usan el color establecido por **Spot Color:** en la pestaña RBN. Para anular los colores de todas las fuentes de avistamientos con un solo color, use la opción **Override Colors:** en la pestaña **Display**.

## Solución de problemas

- **El botón Connect vuelve a Connect inmediatamente con un error en la consola** — El nombre de host o el puerto son incorrectos, o el servidor RBN no es accesible. Verifique `RbnHost` y `RbnPort` y compruebe su conexión de red.
- **No aparecen avistamientos en el panadapter después de conectarse** — Confirme que **Spots:** en la pestaña **Display** esté en Enabled (`IsSpotsEnabled`). También verifique que la banda que está monitoreando no esté oculta en las casillas de verificación del filtro de bandas en la pestaña **Spot List**.
- **El panadapter está inundado de avistamientos** — Reduzca **Rate Limit:** a un valor más bajo para limitar la tasa de avistamientos entrantes. Alternativamente, desactive **Spot Lines:** (`IsSpotsLinesEnabled`) en la pestaña **Display** para que las áreas densas de avistamientos sean más legibles sin reducir la cantidad de avistamientos mostrados.
- **Al hacer doble clic en un avistamiento cambia la frecuencia pero no cambia el modo** — El comentario del avistamiento puede no contener una etiqueta de modo reconocible. El cambio de modo depende de que el comentario del avistamiento contenga una cadena de modo conocida (ej., `CW`, `FT8`, `SSB`). Si el avistador no incluyó un modo en el comentario, solo cambia la frecuencia.
- **La casilla de verificación del FreeDV Reporter se desmarca inmediatamente** — No se pudo resolver un valor de indicativo o cuadrícula. Introduzca valores en los campos **Callsign:** y **Grid Square:**, o active **Use radio** y **Use GPS** para que AetherSDR pueda leerlos de la radio.
- **Auto Mode ahora está en Enabled después de actualizar** — La versión v0.9.5.1 cambió el valor predeterminado de `SpotAutoSwitchMode` de `False` a `True`. Si prefiere el comportamiento anterior, abra `Settings > SpotHub...`, haga clic en la pestaña **Display** y haga clic en **Auto Mode:** para establecerlo en **Disabled**.

## Relacionados

- [Conectarse a un clúster DX](connect-to-a-dx-cluster.md)
- [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los avistamientos](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md)
- [Elegir colores para cada fuente de avistamientos](../../features/dx-cluster/pick-colors-for-each-spot-source.md)
- [Sintonizar un avistamiento haciendo doble clic en la lista de avistamientos](../../features/dx-cluster/tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Descripción general de SpotHub](../../features/dx-cluster/overview.md)
