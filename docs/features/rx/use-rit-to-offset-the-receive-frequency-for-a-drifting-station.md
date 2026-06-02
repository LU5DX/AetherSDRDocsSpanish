# Usar RIT para compensar la frecuencia de recepción de una estación a la deriva

RIT (Receive Incremental Tuning) desplaza la frecuencia de recepción en una cantidad pequeña sin mover la frecuencia de transmisión ni la lectura del VFO. Úselo cuando una estación se desvía ligeramente de su frecuencia de marcación y desea seguirla sin reajustar toda la franja.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Los controles RIT están inactivos sin conexión de radio.
- Abra el applet RX Controls. Haga clic en el botón de la bandeja RX en la barra lateral derecha si el applet no está visible.
- Seleccione la franja que desea ajustar usando las pestañas de franja (A..H) en la parte superior del applet, si hay más de una franja activa.

## Pasos

1. En el applet RX Controls, localice la fila RIT cerca de la parte inferior del applet.
2. Haga clic en RIT para habilitar Receive Incremental Tuning. El botón se ilumina cuando está activo.
3. Use los botones `<` y `>` al lado del cuadro de ajuste de compensación RIT, o desplace la rueda del ratón sobre el cuadro de ajuste, para ajustar la compensación. Cada paso mueve la frecuencia de recepción en 10 Hz. El cuadro de ajuste muestra la compensación actual (predeterminada: `+0 Hz`).
4. Continúe ajustando hasta que la estación a la deriva esté centrada en la banda pasante.
5. Para volver a la compensación cero sin deshabilitar RIT, haga clic en RIT 0. La compensación se restablece a `+0 Hz`.
6. Para desactivar RIT por completo, haga clic en RIT nuevamente. La frecuencia de recepción vuelve a la frecuencia del VFO.

## Qué hace cada control

| Control      | Tipo             | Predeterminado |
|--------------|------------------|----------------|
| RIT          | Botón de alternancia | Desactivado    |
| RIT offset   | Cuadro de ajuste | `+0 Hz`        |
| RIT 0        | Botón pulsador   | —              |

## Consejos

- RIT afecta solo la frecuencia de recepción. Su frecuencia de transmisión permanece en el VFO. Si también necesita compensar su frecuencia de transmisión, use XIT en lugar de RIT o junto con él.
- El paso mínimo de 10 Hz es adecuado para trabajo en SSB y CW. Para una estación que se desvía lentamente, generalmente bastan unas pocas pulsaciones de `>` o un breve desplazamiento de la rueda del ratón.
- Haga clic en RIT 0 antes de desactivar RIT, es una buena práctica. Significa que RIT ya está en cero si lo reactiva más tarde.

## Pestañas de franja y colores de la insignia (v0.9.3)

A partir de v0.9.3, los botones de pestaña de franja (A..H) y la insignia de franja en la esquina superior izquierda del applet toman su color del singleton SliceColorManager en lugar de una tabla de colores fija. Esto significa:

- Los colores por franja son personalizables y persisten entre sesiones.
- El mismo color se refleja en los botones de pestaña de franja, la insignia de franja, los widgets VFO y las barras de medidor dondequiera que se muestre la franja.
- No se requiere ninguna acción de su parte; los colores se actualizan automáticamente cuando una franja se conecta o se cambia su color.

## Formato de texto de la insignia de franja (v26.5.2.1)

A partir de v26.5.2.1, la etiqueta de la insignia de franja utiliza formato de texto enriquecido para que la letra de la franja pueda representarse como HTML. Esto permite caracteres de color o estilo especiales si es necesario. La insignia aún muestra la letra de la franja actualmente vinculada (A..H).

## Comportamiento de las pestañas de franja al reconectar (v0.9.5.1)

A partir de v0.9.5.1, la fila de pestañas de franja se reconstruye correctamente siempre que el número de franjas disponibles cambia en un ciclo de desconexión y reconexión. Específicamente:

- Cuando la radio informa un recuento de franjas diferente al reconectar, los botones de pestaña existentes se eliminan por completo antes de crear otros nuevos. La insignia de franja estática se restaura y es visible mientras no hay pestañas presentes.
- Los controladores de señal de clic se conectan solo una vez por vida útil del applet, independientemente de cuántas veces la radio se conecte o reconecte. Esto evita que se disparen eventos duplicados cuando se hace clic en una pestaña de franja después de una reconexión.

No se requiere ninguna acción de su parte. Si se reconecta a una radio con una configuración de franja diferente, la fila de pestañas se actualiza automáticamente.

## Comportamiento del modo RADE

Cuando selecciona RADE en el combo de modos, la franja se coloca en modo RADE (Rapid Automatic Detection and Excitation). Tenga en cuenta que RADE es un modo solo del lado del cliente: la radio devuelve el modo real (DIGL/DIGU) inmediatamente después de la selección. Cuando cambia de RADE a otro modo, no se emite ninguna señal de desactivación de RADE porque el modo de la franja nunca es `"RADE"` en el lado de la radio. Esto evita desactivaciones espurias al cambiar de modos.

## Corrección del cambio de modo RADE (v26.5.3)

A partir de v26.5.3, al salir del modo RADE a través del combo de modos, el applet emite `radeActivated(false)` solo si la franja estaba realmente en modo RADE. Esto evita señales de desactivación obsoletas al cambiar de modos en una franja que no es RADE (#2376).

## Comportamiento del modo NT

A partir de v0.9.3, el modo NT se trata como un modo digital en todo el applet RX Controls:

- **Los ajustes predefinidos de ancho de filtro** aplican la lista de ajustes predefinidos digitales (DIG) a las franjas NT, igual que DIGU y DIGL.
- **La visualización del ancho de filtro** calcula el ancho de filtro NT utilizando el borde superior (hi), de forma coherente con el manejo de DIGU y FDV.
- **El squelch** está deshabilitado para franjas NT. Debido a que el audio se enruta a través de DAX en modos digitales, el control de squelch no tiene sentido. El botón SQL y el control deslizante de nivel de squelch se atenúan cuando NT es el modo activo. Si el squelch estaba activado cuando cambió a NT, se desactiva automáticamente y se restaura cuando sale de NT.

## Comportamiento del squelch en modo RTTY (v26.5.1)

A partir de v26.5.1, el modo RTTY se agrega a la lista de modos que deshabilitan automáticamente el squelch. Cuando cambia al modo RTTY:

- El botón **SQL** y el control deslizante **Squelch level** están deshabilitados.
- Si el squelch estaba activado, se desactiva automáticamente y el estado guardado se restaura cuando sale de RTTY.

Esto evita que el squelch elimine los caracteres FSK y rompa la decodificación (#2504).

## Persistencia del nivel de squelch manual (v26.5.2.1)

A partir de v26.5.2.1, el umbral de squelch manual que establece con el control deslizante de nivel de squelch se guarda y restaura entre sesiones. Cuando el modo de squelch automático está activo, la radio puede cambiar el nivel de squelch internamente; el cliente ahora recuerda su última preferencia manual para que se conserve cuando regrese al control de squelch manual. El ajuste se almacena en `LastManualSquelchLevel` con un valor predeterminado de 20.

## Menú de antena RX (v26.5.2.1)

A partir de v26.5.2.1, el menú de antena RX se completa desde la lista dedicada de antenas de recepción de la franja, `rxAntennaList()`, cuando está disponible, recurriendo a la `ant_list` general del estado del panadapter. Esto garantiza que solo vea antenas válidas para la franja actual. Los elementos del menú muestran el nombre de la antena con información sobre herramientas y sugerencia de estado que muestra el identificador de antena sin procesar. Seleccionar un elemento llama a `setRxAntenna()` con la cadena de datos de la antena en lugar del texto de la etiqueta del menú.

## Menú de antena TX (v26.5.2.1)

A partir de v26.5.2.1, el menú de antena TX utiliza un algoritmo de filtrado refinado. Una función de respaldo, `likelyTxAntennaFallbackToken()`, acepta tokens de antena que comienzan con `ANT`, `TX` o son exactamente `XVTR`. Los puertos que comienzan con `RX` se excluyen. Los elementos del menú muestran el nombre de la antena con información sobre herramientas y sugerencia de estado. Seleccionar un elemento llama a `setTxAntenna()` con la cadena de datos de la antena.

## Ajustes predefinidos de ancho de filtro (v0.9.5.1)

A partir de v0.9.5.1, las entradas de ajustes predefinidos de filtro pueden almacenar un valor de ancho simple o un par de banda pasante lo:hi explícito. Esto coincide con el formato de almacenamiento utilizado por VfoWidget (#2259). El comportamiento desde su perspectiva es:

- Los ajustes predefinidos que guardó en versiones anteriores (valores de ancho simple) continúan cargándose y funcionando sin ningún cambio.
- Cuando se guarda un ajuste predefinido desde una posición de banda pasante personalizada, se almacenan tanto el borde inferior como el superior del filtro. Cuando se recupera ese ajuste predefinido, la banda pasante se restaura exactamente a la misma posición, no solo al mismo ancho.
- El ajuste `FilterPresets` en AppSettings utiliza el formato `lo:hi` para entradas que reconocen la banda pasante y un número entero simple para entradas de solo ancho. Las entradas múltiples están separadas por comas, por ejemplo: `300:3000,100:2900,2700`.
- Se muestran como máximo seis ajustes predefinidos en el applet RX Controls, independientemente de cuántos estén almacenados.

Haga clic derecho en un botón de ajuste predefinido de filtro para guardar el ancho de filtro actual (y la posición de la banda pasante, si corresponde) como ese ajuste predefinido. Haga clic en un botón de ajuste predefinido para aplicarlo.

## Escalonamiento del ancho de filtro (v0.9.8)

A partir de v0.9.8, el método `stepFilterWidth()` recorre la lista de ajustes predefinidos por modo para encontrar el siguiente ajuste predefinido de filtro más estrecho o más ancho. Esto significa que los atajos de ampliar/estrechar (si están disponibles) producen una geometría de borde correcta para el modo en todos los modos (LSB, CWL, DIGL, RTTY, AM, CW, USB) en lugar de aplicar un desplazamiento fijo simple. La lectura del ancho de filtro, compartida con el panel VFO a través de `RxApplet::formatFilterWidth()`, utiliza lógica que reconoce el modo para que los modos SSB y digitales muestren el ancho etiquetado correcto.

Si tiene atajos de teclado de ampliar o estrechar vinculados a `stepFilterWidth()`:

- Pulsar el atajo de ampliar selecciona el siguiente ajuste predefinido más ancho en la lista de ajustes predefinidos de filtro del modo actual que sea más ancho que el ancho actual.
- Pulsar el atajo de estrechar selecciona el siguiente ajuste predefinido más estrecho.
- Si no existe un ajuste predefinido más ancho/estrecho, se ignora la pulsación de tecla.

No se requiere ninguna acción de su parte; el comportamiento de escalonamiento se actualiza automáticamente en v0.9.8.

## Comportamiento del botón de silencio (v26.5.3)

A partir de v26.5.3, el botón de silencio utiliza un sistema de discriminación de clics:

- **Un solo clic** silencia o reactiva el sonido solo de la franja actual. La acción se difiere por el intervalo de doble clic de la plataforma (aproximadamente 400 ms) para que un doble clic pueda anularla.
- **Doble clic** silencia o reactiva el sonido de todas las franjas propiedad de este cliente, emitido a través de la señal `muteAllToggled`.
- El icono visual (🔊/🔇) se actualiza solo cuando la radio confirma el cambio de estado de silencio a través de `SliceModel::audioMuteChanged`. Esto sigue la política de autoridad de la radio para los ajustes (Radio-Authoritative Settings Policy) (#2489): la radio es la fuente de verdad para el silencio de audio.
- El estado de silencio NO se guarda ni se restaura al reconectar.

## Analizador de entrada de frecuencia (v26.5.3)

A partir de v26.5.3, la entrada de frecuencia utiliza un analizador de entrada de frecuencia dedicado, `FrequencyEntryParser`, para la normalización y validación de texto:

- Cuando escribe una frecuencia en MHz y presiona Enter, el analizador normaliza el texto eliminando cualquier punto después del primer punto decimal. Por ejemplo, `14.200.000` se convierte en `14.200000`.
- El analizador detecta si ingresó un valor de MHz explícito (contiene un punto decimal) o un número sin formato. Si ingresa un valor superior a 54.0 MHz como una entrada de MHz explícita (por ejemplo, `144.0`), se aplica el límite de frecuencia XVTR de 50000.0 MHz, lo que permite la operación en VHF/UHF sin requerir una antena XVTR.
- Si ingresa un valor superior a 54.0 MHz sin un punto decimal, el sistema divide el valor por 1000 (tratando kHz como Hz) o por 1e6 (tratando Hz como MHz) según corresponda.
- En cualquier entrada válida (0.001 a maxMhz), se emite la señal `directEntryCommitted(freqMhz, QStringLiteral("rx-direct-entry"))` para recentrar el panadapter.

## Etiquetas del control deslizante de ganancia AF y panorámico (v26.5.3)

A partir de v26.5.3, los controles deslizantes de ganancia AF y panorámico muestran etiquetas de porcentaje y posición:

- **Control deslizante de ganancia AF**: Muestra el valor actual como un porcentaje (por ejemplo, `70%`) usando `percentText()`.
- **Control deslizante panorámico**: Muestra `C` en el centro (50), `Lx` para el desplazamiento a la izquierda (por ejemplo, `L20` para 30 % desde el centro) y `Rx` para el desplazamiento a la derecha (por ejemplo, `R30` para 80 % desde el centro) usando `panText()`. La etiqueta se actualiza mientras arrastra el control deslizante.

## Relleno de la marca central del control deslizante panorámico (v26.6.1)

A partir de v26.6.1, el control deslizante panorámico L/R utiliza un relleno anclado al centro que se pinta desde el centro hacia afuera. Esto hace que la posición neutra sea clara de un vistazo:

- Cuando el mango está a la izquierda del centro, el pintado de la ranura borra el relleno predeterminado (0 → mango) y pinta el relleno de color de acento desde el mango hasta el centro.
- Cuando el mango está a la derecha del centro, el pintado de la ranura borra la porción (0 → centro) para que solo el segmento (centro → mango) se rellene con color de acento.
- Un pequeño punto de marca
