# Usar RIT para desplazar la frecuencia de recepción para una estación a la deriva

RIT (Receive Incremental Tuning) desplaza la frecuencia de recepción en una pequeña cantidad sin mover la frecuencia de transmisión ni la lectura del VFO. Úselo cuando una estación se desvía ligeramente de su frecuencia de sintonía y desea seguirla sin reajustar toda la slice.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles de RIT están inactivos sin una conexión de radio.
- Abra el applet RX Controls. Haga clic en el botón de la bandeja RX en la barra lateral derecha si el applet no está visible.
- Seleccione la slice que desea ajustar usando las pestañas de slice (A..H) en la parte superior del applet, si hay más de una slice activa.

## Pasos

1. En el applet RX Controls, localice la fila RIT cerca de la parte inferior del applet.
2. Haga clic en RIT para habilitar Receive Incremental Tuning. El botón se ilumina cuando está activo.
3. Use los botones `<` y `>` junto al spinbox de desplazamiento RIT, o desplace la rueda del ratón sobre el spinbox, para ajustar el desplazamiento. Cada paso mueve la frecuencia de recepción en 10 Hz. El spinbox muestra el desplazamiento actual (predeterminado: `+0 Hz`).
4. Continúe ajustando hasta que la estación a la deriva esté centrada en la banda de paso.
5. Para volver al desplazamiento cero sin deshabilitar RIT, haga clic en RIT 0. El desplazamiento se restablece a `+0 Hz`.
6. Para desactivar RIT por completo, haga clic en RIT nuevamente. La frecuencia de recepción vuelve a la frecuencia del VFO.

## Qué hace cada control

| Control     | Tipo                   | Predeterminado |
|-------------|------------------------|----------------|
| RIT         | Botón de alternancia   | Off            |
| RIT offset  | Spinbox                | `+0 Hz`        |
| RIT 0       | Botón pulsador         | —              |

## Consejos

- RIT afecta solo la frecuencia de recepción. Su frecuencia de transmisión permanece en el VFO. Si también necesita desplazar su frecuencia de transmisión, use XIT en lugar de o junto con RIT.
- El paso mínimo de 10 Hz es adecuado para trabajo en SSB y CW. Para una estación que se desvía lentamente, unos pocos toques en `>` o un breve desplazamiento de la rueda del ratón suele ser suficiente.
- Hacer clic en RIT 0 antes de desactivar RIT es una buena práctica. Esto asegura que RIT ya esté en cero si lo vuelve a habilitar más tarde.

## Colores de pestañas de slice y distintivo (v0.9.3)

Desde v0.9.3, los botones de pestaña de slice (A..H) y el distintivo Slice en la esquina superior izquierda del applet toman su color del singleton SliceColorManager en lugar de una tabla de colores fija. Esto significa:

- Los colores por slice son personalizables y persisten entre sesiones.
- El mismo color se refleja en los botones de pestaña de slice, el distintivo Slice, los widgets VFO y las tiras del medidor dondequiera que se muestre la slice.
- No se requiere ninguna acción de su parte; los colores se actualizan automáticamente cuando una slice se conecta o cambia su color.

## Formato del texto del distintivo de slice (v26.5.2.1)

Desde v26.5.2.1, la etiqueta del distintivo de slice utiliza formato de texto enriquecido para que la letra de la slice pueda representarse como HTML. Esto permite caracteres especiales de color o estilo si es necesario. El distintivo aún muestra la letra de la slice vinculada actualmente (A..H).

## Comportamiento de la pestaña de slice al reconectar (v0.9.5.1)

Desde v0.9.5.1, la fila de pestañas de slice se reconstruye correctamente siempre que el número de slices disponibles cambia en un ciclo de desconexión y reconexión. Específicamente:

- Cuando el radio informa un recuento de slices diferente al reconectar, los botones de pestaña existentes se eliminan por completo antes de crear otros nuevos. El distintivo Slice estático se restaura y es visible mientras no haya pestañas presentes.
- Los manejadores de señal de clic se conectan solo una vez por vida útil del applet, independientemente de cuántas veces el radio se conecte o reconecte. Esto evita que se activen eventos duplicados cuando se hace clic en una pestaña de slice después de una reconexión.

No se requiere ninguna acción de su parte. Si se conecta a un radio con una configuración de slice diferente, la fila de pestañas se actualiza automáticamente.

## Comportamiento del modo RADE

Cuando selecciona RADE del combo de modo, la slice se coloca en modo RADE (Rapid Automatic Detection and Excitation). Tenga en cuenta que RADE es un modo solo del lado del cliente: el radio devuelve el modo real (DIGL/DIGU) inmediatamente después de la selección. Cuando cambia de RADE a otro modo, no se emite ninguna señal de desactivación de RADE porque el modo de la slice nunca es `"RADE"` en el lado del radio. Esto evita desactivaciones espurias al cambiar de modo.

## Comportamiento del modo NT

Desde v0.9.3, el modo NT se trata como un modo digital en todo el applet RX Controls:

- **Los preajustes de ancho de filtro** aplican la lista de preajustes digital (DIG) a las slices NT, igual que DIGU y DIGL.
- **La visualización del ancho de filtro** calcula el ancho de filtro NT utilizando el borde superior (hi), de forma coherente con el manejo de DIGU y FDV.
- **El squelch** está deshabilitado para slices NT. Debido a que el audio se enruta a través de DAX en modos digitales, el control de squelch no tiene sentido. El botón SQL y el control deslizante de nivel de squelch se atenúan cuando NT es el modo activo. Si el squelch estaba activo cuando cambió a NT, se desactiva automáticamente y se restaura cuando sale de NT.

## Comportamiento del squelch en modo RTTY (v26.5.1)

Desde v26.5.1, el modo RTTY se agrega a la lista de modos que deshabilitan automáticamente el squelch. Cuando cambia al modo RTTY:

- El botón **SQL** y el control deslizante de **nivel de squelch** se deshabilitan.
- Si el squelch estaba activo, se desactiva automáticamente y el estado guardado se restaura cuando sale de RTTY.

Esto evita que el squelch elimine los caracteres FSK y rompa la decodificación (#2504).

## Persistencia del nivel de squelch manual (v26.5.2.1)

Desde v26.5.2.1, el umbral de squelch manual que establece con el control deslizante de nivel de squelch se guarda y restaura entre sesiones. Cuando el modo de squelch automático está activo, el radio puede cambiar el nivel de squelch internamente; el cliente ahora recuerda su última preferencia manual para que se conserve cuando regrese al control de squelch manual. La configuración se almacena en `LastManualSquelchLevel` con un valor predeterminado de 20.

## Menú de antena RX (v26.5.2.1)

Desde v26.5.2.1, el menú de antena RX se completa desde el `rxAntennaList()` dedicado de la slice cuando está disponible, recurriendo a la `ant_list` general del estado del panadapter. Esto garantiza que solo vea antenas válidas para la slice actual. Los elementos del menú muestran el nombre de la antena con información sobre herramientas y sugerencia de estado que muestra el identificador de antena sin procesar. Seleccionar un elemento llama a `setRxAntenna()` con la cadena de datos de la antena en lugar del texto de la etiqueta del menú.

## Menú de antena TX (v26.5.2.1)

Desde v26.5.2.1, el menú de antena TX utiliza un algoritmo de filtrado refinado. Una función de respaldo `likelyTxAntennaFallbackToken()` acepta tokens de antena que comienzan con `ANT`, `TX`, o son exactamente `XVTR`. Los puertos que comienzan con `RX` se excluyen. Los elementos del menú muestran el nombre de la antena con información sobre herramientas y sugerencia de estado. Seleccionar un elemento llama a `setTxAntenna()` con la cadena de datos de la antena.

## Preajustes de ancho de filtro (v0.9.5.1)

Desde v0.9.5.1, las entradas de preajuste de filtro pueden almacenar un valor de ancho simple o un par explícito de banda de paso lo:hi. Esto coincide con el formato de almacenamiento utilizado por VfoWidget (#2259). El comportamiento desde su perspectiva es:

- Los preajustes que guardó en versiones anteriores (valores de ancho simples) continúan cargándose y funcionando sin ningún cambio.
- Cuando se guarda un preajuste desde una posición de banda de paso personalizada, se almacenan los bordes de filtro bajo y alto. Cuando se recupera ese preajuste, la banda de paso se restaura exactamente a la misma posición, no solo al mismo ancho.
- La configuración `FilterPresets` en AppSettings utiliza el formato `lo:hi` para entradas que reconocen la banda de paso y un entero simple para entradas de solo ancho. Las múltiples entradas están separadas por comas, por ejemplo: `300:3000,100:2900,2700`.
- Se muestran como máximo seis preajustes en el applet RX Controls, independientemente de cuántos estén almacenados.

Haga clic derecho en un botón de preajuste de filtro para guardar el ancho de filtro actual (y la posición de la banda de paso, si corresponde) como ese preajuste. Haga clic en un botón de preajuste para aplicarlo.

## Escalonamiento del ancho de filtro (v0.9.8)

Desde v0.9.8, el método `stepFilterWidth()` recorre la lista de preajustes por modo para encontrar el preajuste de filtro siguiente más estrecho o más ancho. Esto significa que los atajos de ampliar/estrechar (si están disponibles) producen una geometría de borde correcta para el modo para todos los modos (LSB, CWL, DIGL, RTTY, AM, CW, USB) en lugar de aplicar un desplazamiento fijo simple. La lectura del ancho de filtro, compartida con el panel VFO a través de `RxApplet::formatFilterWidth()`, utiliza lógica consciente del modo, por lo que los modos SSB y digitales muestran el ancho etiquetado correcto.

Si tiene atajos de teclado de ampliar o estrechar vinculados a `stepFilterWidth()`:

- Presionar el atajo de ampliar selecciona el siguiente preajuste más ancho en la lista de preajustes de filtro del modo actual que sea más ancho que el ancho actual.
- Presionar el atajo de estrechar selecciona el siguiente preajuste más estrecho.
- Si no existe un preajuste más ancho/estrecho, la pulsación de tecla se ignora.

No se requiere ninguna acción de su parte; el comportamiento de escalonamiento se actualiza automáticamente en v0.9.8.

## Comportamiento del botón de silencio (v26.5.3)

Desde v26.5.3, el botón de silencio utiliza un sistema de discriminación de clics:

- **Un clic** silencia o reactiva el sonido solo de la slice actual. La acción se aplaza por el intervalo de doble clic de la plataforma (aproximadamente 400 ms) para que un doble clic pueda anularla.
- **Doble clic** silencia o reactiva el sonido de todas las slices propiedad de este cliente, emitido a través de la señal `muteAllToggled`.
- El icono visual (🔊/🔇) se actualiza solo cuando el radio reconoce el cambio de estado de silencio a través de `SliceModel::audioMuteChanged`. Esto sigue la Política de Configuración de Autoridad del Radio (#2489): el radio es la fuente de verdad para el silencio de audio.
- El estado de silencio NO se guarda ni restaura al reconectar.

## Analizador de entrada de frecuencia (v26.5.3)

Desde v26.5.3, la entrada de frecuencia utiliza un `FrequencyEntryParser` dedicado para la normalización y validación de texto:

- Cuando escribe una frecuencia en MHz y presiona Enter, el analizador normaliza el texto eliminando cualquier punto después del primer punto decimal. Por ejemplo, `14.200.000` se convierte en `14.200000`.
- El analizador detecta si ingresó un valor explícito en MHz (contiene un punto decimal) o un número sin procesar. Si ingresa un valor superior a 54.0 MHz como una entrada explícita en MHz (por ejemplo, `144.0`), se aplica el límite de frecuencia XVTR de 50000.0 MHz, lo que permite la operación en VHF/UHF sin requerir una antena XVTR.
- Si ingresa un valor superior a 54.0 MHz sin un punto decimal, el sistema divide el valor por 1000 (tratando kHz como Hz) o por 1e6 (tratando Hz como MHz) según corresponda.
- En cualquier entrada válida (0.001 a maxMhz), se emite la señal `directEntryCommitted(freqMhz, QStringLiteral("rx-direct-entry"))` para volver a centrar el panadapter.

## Etiquetas del control deslizante de ganancia AF y pan (v26.5.3)

Desde v26.5.3, los controles deslizantes de ganancia AF y pan muestran etiquetas de porcentaje y posición:

- **Control deslizante de ganancia AF**: Muestra el valor actual como un porcentaje (por ejemplo, `70%`) usando `percentText()`.
- **Control deslizante Pan**: Muestra `C` en el centro (50), `Lx` para el desplazamiento izquierdo (por ejemplo, `L20` para 30% desde el centro) y `Rx` para el desplazamiento derecho (por ejemplo, `R30` para 80% desde el centro) usando `panText()`. La etiqueta se actualiza mientras arrastra el control deslizante.

## Corrección del cambio de modo RADE (v26.5.3)

Desde v26.5.3, al cambiar del modo RADE a través del combo de modo, el applet emite `radeActivated(false)` solo si la slice estaba realmente en modo RADE. Esto evita señales de desactivación obsoletas al cambiar de modo en una slice que no es RADE (#2376).

## Relacionado

- [Use XIT para desplazar la frecuencia de transmisión sin cambiar RX](use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Sintonice el radio a una frecuencia (escriba MHz en la lectura)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Elija un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
