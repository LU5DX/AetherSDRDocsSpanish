# Usar RIT para compensar la frecuencia de recepción de una estación que se desvía

RIT (Receive Incremental Tuning) desplaza la frecuencia de recepción en una pequeña cantidad sin mover la frecuencia de transmisión ni la lectura del VFO. Úselo cuando una estación se desvíe ligeramente de su frecuencia de marcación y desee seguirla sin reajustar toda la slice.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Los controles RIT están inactivos sin una conexión de radio.
- Abra el applet RX Controls. Haga clic en el botón de la bandeja RX en la barra lateral derecha si el applet no está visible.
- Seleccione la slice que desea ajustar usando las pestañas de slice (A..H) en la parte superior del applet, si hay más de una slice activa.

## Pasos

1. En el applet RX Controls, localice la fila RIT cerca de la parte inferior del applet.
2. Haga clic en RIT para habilitar Receive Incremental Tuning. El botón se ilumina cuando está activo.
3. Use los botones `<` y `>` junto al cuadro de ajuste de compensación RIT, o desplace la rueda del ratón sobre el cuadro de ajuste, para ajustar la compensación. Cada paso mueve la frecuencia de recepción en 10 Hz. El cuadro de ajuste muestra la compensación actual (predeterminado: `+0 Hz`).
4. Continúe ajustando hasta que la estación que se desvía esté centrada en la banda pasante.
5. Para volver a la compensación cero sin deshabilitar RIT, haga clic en RIT 0. La compensación se restablece a `+0 Hz`.
6. Para desactivar RIT por completo, haga clic en RIT nuevamente. La frecuencia de recepción vuelve a la frecuencia del VFO.

## Qué hace cada control

| Control      | Tipo            | Predeterminado |
|--------------|-----------------|----------------|
| RIT          | Botón de alternancia | Desactivado    |
| RIT offset   | Cuadro de ajuste | `+0 Hz`        |
| RIT 0        | Botón pulsador   | —              |

## Consejos

- RIT afecta solo a la frecuencia de recepción. Su frecuencia de transmisión permanece en el VFO. Si también necesita compensar su frecuencia de transmisión, use XIT en lugar de o junto con RIT.
- El paso mínimo de 10 Hz es adecuado para trabajo en SSB y CW. Para una estación que se desvía lentamente, suelen bastar unas pocas pulsaciones de `>` o un breve desplazamiento de la rueda del ratón.
- Hacer clic en RIT 0 antes de desactivar RIT es una buena práctica. Significa que RIT ya está en cero si lo vuelve a habilitar más tarde.

## Colores de pestañas y distintivos de slice (v0.9.3)

Desde v0.9.3, los botones de las pestañas de slice (A..H) y el distintivo Slice en la esquina superior izquierda del applet toman su color del singleton SliceColorManager en lugar de una tabla de colores fija. Esto significa que:

- Los colores por slice son personalizables y persisten entre sesiones.
- El mismo color se refleja en los botones de las pestañas de slice, el distintivo Slice, los widgets VFO y las barras de medidor dondequiera que se muestre la slice.
- No se requiere ninguna acción de su parte; los colores se actualizan automáticamente cuando una slice se conecta o se cambia su color.

## Formato de texto del distintivo de slice (v26.5.2.1)

Desde v26.5.2.1, la etiqueta del distintivo de slice utiliza formato de texto enriquecido para que la letra de la slice pueda representarse como HTML. Esto permite caracteres especiales de color o estilo si es necesario. El distintivo sigue mostrando la letra de la slice actualmente vinculada (A..H).

## Comportamiento de las pestañas de slice al reconectar (v0.9.5.1)

Desde v0.9.5.1, la fila de pestañas de slice se reconstruye correctamente cada vez que el número de slices disponibles cambia durante un ciclo de desconexión y reconexión. Específicamente:

- Cuando la radio informa un recuento de slices diferente al reconectar, los botones de pestaña existentes se eliminan por completo antes de crear otros nuevos. El distintivo Slice estático se restaura y es visible mientras no haya pestañas presentes.
- Los manejadores de señal de clic se conectan solo una vez por vida útil del applet, independientemente de cuántas veces la radio se conecte o reconecte. Esto evita que se disparen eventos duplicados cuando se hace clic en una pestaña de slice después de una reconexión.

No se requiere ninguna acción de su parte. Si se reconecta a una radio con una configuración de slice diferente, la fila de pestañas se actualiza automáticamente.

## Comportamiento del modo RADE

Cuando selecciona RADE del combo de modos, la slice se coloca en modo RADE (Rapid Automatic Detection and Excitation). Tenga en cuenta que RADE es un modo solo del lado del cliente: la radio envía de vuelta el modo real (DIGL/DIGU) inmediatamente después de la selección. Cuando cambia de RADE a otro modo, no se emite ninguna señal de desactivación de RADE porque el modo de la slice nunca es `"RADE"` en el lado de la radio. Esto evita desactivaciones espurias al cambiar de modo.

## Comportamiento del modo NT

Desde v0.9.3, el modo NT se trata como un modo digital en todo el applet RX Controls:

- **Los preajustes de ancho de filtro** aplican la lista de preajustes digital (DIG) a las slices NT, igual que DIGU y DIGL.
- **La visualización del ancho de filtro** calcula el ancho de filtro NT utilizando el borde superior (hi), de manera consistente con el manejo de DIGU y FDV.
- **El squelch** está deshabilitado para las slices NT. Debido a que el audio se enruta a través de DAX en modos digitales, el control de squelch no tiene sentido. El botón SQL y el control deslizante de nivel de squelch se atenúan cuando NT es el modo activo. Si el squelch estaba activado cuando cambió a NT, se desactiva automáticamente y se restaura cuando sale de NT.

## Comportamiento del squelch en modo RTTY (v26.5.1)

Desde v26.5.1, el modo RTTY se añade a la lista de modos que deshabilitan automáticamente el squelch. Cuando cambia al modo RTTY:

- El botón **SQL** y el control deslizante de **Nivel de squelch** se deshabilitan.
- Si el squelch estaba activado, se desactiva automáticamente y el estado guardado se restaura cuando sale de RTTY.

Esto evita que el squelch elimine los caracteres FSK y rompa la decodificación (#2504).

## Persistencia del nivel de squelch manual (v26.5.2.1)

Desde v26.5.2.1, el umbral de squelch manual que establece con el control deslizante de nivel de squelch se guarda y restaura entre sesiones. Cuando el modo de squelch automático está activo, la radio puede cambiar el nivel de squelch internamente: el cliente ahora recuerda su última preferencia manual para que se conserve cuando vuelva al control de squelch manual. La configuración se almacena en `LastManualSquelchLevel` con un valor predeterminado de 20.

## Menú de antena RX (v26.5.2.1)

Desde v26.5.2.1, el menú de antena RX se completa desde `rxAntennaList()` dedicado de la slice cuando está disponible, recurriendo a la `ant_list` general del estado del panadapter. Esto garantiza que solo vea antenas válidas para la slice actual. Los elementos del menú muestran el nombre de la antena con información sobre herramientas y sugerencia de estado que muestra el identificador de antena sin procesar. Seleccionar un elemento llama a `setRxAntenna()` con la cadena de datos de la antena en lugar del texto de la etiqueta del menú.

## Menú de antena TX (v26.5.2.1)

Desde v26.5.2.1, el menú de antena TX utiliza un algoritmo de filtrado refinado. Una función de respaldo `likelyTxAntennaFallbackToken()` acepta tokens de antena que comienzan con `ANT`, `TX`, o son exactamente `XVTR`. Los puertos que comienzan con `RX` se excluyen. Los elementos del menú muestran el nombre de la antena con información sobre herramientas y sugerencia de estado. Seleccionar un elemento llama a `setTxAntenna()` con la cadena de datos de la antena.

## Preajustes de ancho de filtro (v0.9.5.1)

Desde v0.9.5.1, las entradas de preajuste de filtro pueden almacenar un valor de ancho simple o un par de banda pasante lo:hi explícito. Esto coincide con el formato de almacenamiento utilizado por VfoWidget (#2259). El comportamiento desde su perspectiva es:

- Los preajustes que guardó en versiones anteriores (valores de ancho simple) continúan cargándose y funcionando sin ningún cambio.
- Cuando se guarda un preajuste desde una posición de banda pasante personalizada, se almacenan tanto el borde de filtro bajo como el alto. Cuando se recupera ese preajuste, la banda pasante se restaura exactamente en la misma posición, no solo con el mismo ancho.
- La configuración `FilterPresets` en AppSettings utiliza el formato `lo:hi` para entradas que reconocen la banda pasante y un entero simple para entradas de solo ancho. Varias entradas están separadas por comas, por ejemplo: `300:3000,100:2900,2700`.
- Se muestran como máximo seis preajustes en el applet RX Controls, independientemente de cuántos estén almacenados.

Haga clic derecho en un botón de preajuste de filtro para guardar el ancho de filtro actual (y la posición de la banda pasante, si corresponde) como ese preajuste. Haga clic en un botón de preajuste para aplicarlo.

## Escalonamiento del ancho de filtro (v0.9.8)

Desde v0.9.8, el método `stepFilterWidth()` recorre la lista de preajustes por modo para encontrar el siguiente preajuste de filtro más estrecho o más ancho. Esto significa que los atajos de ensanchar/estrechar (si están disponibles) producen una geometría de borde correcta para el modo para todos los modos (LSB, CWL, DIGL, RTTY, AM, CW, USB) en lugar de aplicar un desplazamiento fijo simple. La lectura del ancho de filtro, compartida con el panel VFO a través de `RxApplet::formatFilterWidth()`, utiliza lógica que reconoce el modo para que los modos SSB y digitales muestren el ancho etiquetado correcto.

Si tiene atajos de teclado de ensanchar o estrechar vinculados a `stepFilterWidth()`:

- Al presionar el atajo de ensanchar se selecciona el siguiente preajuste más ancho en la lista de preajustes de filtro del modo actual que sea más ancho que el ancho actual.
- Al presionar el atajo de estrechar se selecciona el siguiente preajuste más estrecho.
- Si no existe ningún preajuste más ancho/estrecho, se ignora la pulsación de tecla.

No se requiere ninguna acción de su parte; el comportamiento de escalonamiento se actualiza automáticamente en v0.9.8.

## Relacionados

- [Use XIT to offset the transmit frequency without changing RX](use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Tune the radio to a frequency (type MHz in the readout)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Pick a filter width preset for the current mode](pick-a-filter-width-preset-for-the-current-mode.md)
