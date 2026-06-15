# Use RIT para desplazar la frecuencia de recepción de una estación que se desvía

RIT (Receive Incremental Tuning) desplaza la frecuencia de recepción en una pequeña cantidad sin mover la frecuencia de transmisión ni la lectura del VFO. Úselo cuando una estación se desvía ligeramente de su frecuencia de marcación y desea seguirla sin reajustar toda la franja (slice).

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles RIT están inactivos sin una conexión al radio.
- Abra el applet RX Controls. Haga clic en el botón de la bandeja RX en la barra lateral derecha si el applet no está visible.
- Seleccione la franja que desea ajustar usando las pestañas de franja (A..H) en la parte superior del applet, si hay más de una franja activa.

## Pasos

1. En el applet RX Controls, localice la fila RIT cerca de la parte inferior del applet.
2. Haga clic en RIT para habilitar Receive Incremental Tuning. El botón se ilumina cuando está activo.
3. Use los botones `<` y `>` junto al control giratorio de desplazamiento RIT, o desplace la rueda del ratón sobre el control giratorio, para ajustar el desplazamiento. Cada paso mueve la frecuencia de recepción en 10 Hz. El control giratorio muestra el desplazamiento actual (valor predeterminado: `+0 Hz`).
4. Continúe ajustando hasta que la estación que se desvía esté centrada en la banda pasante.
5. Para volver al desplazamiento cero sin deshabilitar RIT, haga clic en RIT 0. El desplazamiento se restablece a `+0 Hz`.
6. Para desactivar RIT por completo, haga clic en RIT nuevamente. La frecuencia de recepción vuelve a la frecuencia del VFO.

## Qué hace cada control

| Control      | Tipo          | Valor predeterminado |
|--------------|---------------|----------------------|
| RIT          | Botón de alternancia | Off                  |
| RIT offset   | Control giratorio | `+0 Hz`              |
| RIT 0        | Botón pulsador | —                    |

## Consejos

- RIT afecta solo la frecuencia de recepción. Su frecuencia de transmisión permanece en el VFO. Si también necesita desplazar su frecuencia de transmisión, use XIT en lugar de o junto con RIT.
- El paso mínimo de 10 Hz es adecuado para trabajo en SSB y CW. Para una estación que se desvía lentamente, unas pocas pulsaciones de `>` o un breve desplazamiento de la rueda del ratón suelen ser suficientes.
- Hacer clic en RIT 0 antes de desactivar RIT es una buena práctica. Esto significa que RIT ya está puesto a cero si lo vuelve a habilitar más tarde.

## Color de las pestañas de franja y la insignia (v0.9.3)

Desde v0.9.3, los botones de las pestañas de franja (A..H) y la insignia de franja (Slice badge) en la esquina superior izquierda del applet toman su color del singleton SliceColorManager en lugar de una tabla de colores fija. Esto significa:

- Los colores por franja son personalizables y persisten entre sesiones.
- El mismo color se refleja en los botones de las pestañas de franja, la insignia de franja, los widgets VFO y las barras de medidor dondequiera que se muestre la franja.
- No se requiere ninguna acción de su parte; los colores se actualizan automáticamente cuando una franja se conecta o se cambia su color.

## Formato de texto de la insignia de franja (v26.5.2.1)

Desde v26.5.2.1, la etiqueta de la insignia de franja utiliza formato de texto enriquecido para que la letra de la franja pueda mostrarse como HTML. Esto permite caracteres de color o estilo especiales si es necesario. La insignia aún muestra la letra de la franja actualmente vinculada (A..H).

## Comportamiento de las pestañas de franja al reconectar (v0.9.5.1)

Desde v0.9.5.1, la fila de pestañas de franja se reconstruye correctamente cada vez que el número de franjas disponibles cambia durante un ciclo de desconexión y reconexión. Específicamente:

- Cuando el radio informa un número diferente de franjas al reconectar, los botones de pestaña existentes se eliminan por completo antes de crear otros nuevos. La insignia de franja estática se restaura y es visible mientras no haya pestañas presentes.
- Los manejadores de señal de clic se conectan solo una vez por duración del applet, independientemente de cuántas veces el radio se conecte o reconecte. Esto evita que se disparen eventos duplicados cuando se hace clic en una pestaña de franja después de una reconexión.

No se requiere ninguna acción de su parte. Si se reconecta a un radio con una configuración de franja diferente, la fila de pestañas se actualiza automáticamente.

## Comportamiento del modo RADE

Cuando selecciona RADE del combo de modo, la franja se coloca en modo RADE (Rapid Automatic Detection and Excitation). Tenga en cuenta que RADE es un modo solo del lado del cliente: el radio retransmite el modo real (DIGL/DIGU) inmediatamente después de la selección. Cuando cambia de RADE a otro modo, no se emite ninguna señal de desactivación de RADE porque el modo de la franja nunca es `"RADE"` en el lado del radio. Esto evita desactivaciones espurias al cambiar de modo.

## Corrección en el cambio de modo RADE (v26.5.3)

Desde v26.5.3, al cambiar del modo RADE a través del combo de modo, el applet emite `radeActivated(false)` solo si la franja estaba realmente en modo RADE. Esto evita señales de desactivación obsoletas al cambiar de modo en una franja que no está en RADE (#2376).

## Demodulador WFM por software (v26.6.3)

Desde v26.6.3, aparece un botón WFM junto al combo de modo en la fila de frecuencia. Este botón activa un demodulador FM por software que enruta el audio a través de DAX IQ a un cable de alta fidelidad (Hi-Fi Cable). El botón WFM es distinto del combo de modo: WFM nunca es una selección de modo en el combo.

Haga clic en el botón **WFM** para activar o desactivar el demodulador FM por software para la franja actual. El botón se ilumina en verde cuando está activo. Cuando selecciona un modo de radio real desde el combo de modo mientras WFM está activo, la superposición WFM se desactiva automáticamente. Esto evita conflictos entre el demodulador por software y el procesamiento de modo propio del radio.

## Comportamiento del modo NT

Desde v0.9.3, el modo NT se trata como un modo digital en todo el applet RX Controls:

- **Valores preestablecidos de ancho de filtro** aplican la lista preestablecida digital (DIG) a las franjas NT, igual que para DIGU y DIGL.
- **Visualización del ancho de filtro** calcula el ancho de filtro NT usando el borde superior (hi), de manera consistente con el manejo de DIGU y FDV.
- **El squelch** está deshabilitado para franjas NT. Debido a que el audio se enruta a través de DAX en modos digitales, el control de squelch no tiene sentido. El botón SQL y el control deslizante de nivel de squelch están atenuados cuando NT es el modo activo. Si el squelch estaba activado cuando cambió a NT, se desactiva automáticamente y se restaura cuando sale de NT.

## Comportamiento del squelch en modo RTTY (v26.5.1)

Desde v26.5.1, el modo RTTY se agrega a la lista de modos que deshabilitan automáticamente el squelch. Cuando cambia al modo RTTY:

- El botón **SQL** y el control deslizante **Nivel de squelch** están deshabilitados.
- Si el squelch estaba activado, se desactiva automáticamente y el estado guardado se restaura cuando sale de RTTY.

Esto evita que el squelch elimine los caracteres FSK y rompa la decodificación (#2504).

## Persistencia del nivel de squelch manual (v26.5.2.1)

Desde v26.5.2.1, el umbral de squelch manual que establece con el control deslizante de nivel de squelch se guarda y restaura entre sesiones. Cuando el modo de squelch automático está activo, el radio puede cambiar el nivel de squelch internamente; el cliente ahora recuerda su última preferencia manual para que se conserve cuando regrese al control de squelch manual. La configuración se almacena en `LastManualSquelchLevel` con un valor predeterminado de 20.

## Menú de antena RX (v26.5.2.1)

Desde v26.5.2.1, el menú de antena RX se completa desde el `rxAntennaList()` dedicado de la franja cuando está disponible, recurriendo al `ant_list` general del estado del panadapter. Esto asegura que solo vea antenas válidas para la franja actual. Los elementos del menú muestran el nombre de la antena con información sobre herramientas y sugerencia de estado que muestra el identificador de antena sin procesar. La selección de un elemento llama a `setRxAntenna()` con la cadena de datos de la antena en lugar del texto de la etiqueta del menú.

## Menú de antena TX (v26.5.2.1)

Desde v26.5.2.1, el menú de antena TX utiliza un algoritmo de filtrado refinado. Una función de respaldo `likelyTxAntennaFallbackToken()` acepta tokens de antena que comienzan con `ANT`, `TX`, o son exactamente `XVTR`. Los puertos que comienzan con `RX` se excluyen. Los elementos del menú muestran el nombre de la antena con información sobre herramientas y sugerencia de estado. La selección de un elemento llama a `setTxAntenna()` con la cadena de datos de la antena.

## Valores preestablecidos de ancho de filtro (v0.9.5.1)

Desde v0.9.5.1, las entradas de valores preestablecidos de filtro pueden almacenar un valor de ancho simple o un par de banda pasante lo:hi explícito. Esto coincide con el formato de almacenamiento utilizado por VfoWidget (#2259). El comportamiento desde su perspectiva es:

- Los valores preestablecidos que guardó en versiones anteriores (valores de ancho simple) continúan cargándose y funcionando sin ningún cambio.
- Cuando se guarda un valor preestablecido desde una posición de banda pasante personalizada, se almacenan los bordes de filtro tanto bajo como alto. Cuando se recupera ese valor preestablecido, la banda pasante se restaura exactamente a la misma posición, no solo al mismo ancho.
- La configuración `FilterPresets` en AppSettings utiliza el formato `lo:hi` para entradas conscientes de la banda pasante y un entero simple para entradas solo de ancho. Las entradas múltiples están separadas por comas, por ejemplo: `300:3000,100:2900,2700`.
- Se muestran como máximo seis valores preestablecidos en el applet RX Controls, independientemente de cuántos estén almacenados.

Haga clic derecho en un botón de valor preestablecido de filtro para guardar el ancho de filtro actual (y la posición de la banda pasante, si corresponde) como ese valor preestablecido. Haga clic en un botón de valor preestablecido para aplicarlo.

## Escalonamiento del ancho de filtro (v0.9.8)

Desde v0.9.8, el método `stepFilterWidth()` recorre la lista de valores preestablecidos por modo para encontrar el siguiente valor preestablecido de filtro más estrecho o más ancho. Esto significa que los atajos de ampliar/reducir (si están disponibles) producen una geometría de borde correcta para el modo para todos los modos (LSB, CWL, DIGL, RTTY, AM, CW, USB) en lugar de aplicar un desplazamiento fijo simple. La lectura del ancho de filtro, compartida con el panel VFO a través de `RxApplet::formatFilterWidth()`, utiliza lógica consciente del modo para que los modos SSB y digitales muestren el ancho etiquetado correcto.

Si tiene atajos de teclado para ampliar o reducir vinculados a `stepFilterWidth()`:

- Al presionar el atajo de ampliar se selecciona el siguiente valor preestablecido más ancho en la lista de valores preestablecidos de filtro del modo actual que sea más ancho que el ancho actual.
- Al presionar el atajo de reducir se selecciona el siguiente valor preestablecido más estrecho.
- Si no existe un valor preestablecido más ancho/estrecho, se ignora la pulsación de tecla.

No se requiere ninguna acción de su parte; el comportamiento de escalonamiento se actualiza automáticamente en v0.9.8.

## Comportamiento del botón de silencio (v26.5.3)

Desde v26.5.3, el botón de silencio utiliza un sistema de discriminación de clics:

- **Un solo clic** silencia o restaura el sonido solo de la franja actual. La acción se difiere por el intervalo de doble clic de la plataforma (aproximadamente 400 ms) para que un doble clic pueda anularla.
- **Doble clic** silencia o restaura el sonido de todas las franjas propiedad de este cliente, emitido a través de la señal `muteAllToggled`.
- El icono visual (🔊/🔇) se actualiza solo cuando el radio confirma el cambio de estado de silencio a través de `SliceModel::audioMuteChanged`. Esto sigue la Política de Ajustes de Autoridad del Radio (#2489): el radio es la fuente de verdad para el silencio de audio.
- El estado de silencio NO se guarda ni se restaura al reconectar.

## Analizador de entrada de frecuencia (v26.5.3)

Desde v26.5.3, la entrada de frecuencia utiliza un `FrequencyEntryParser` dedicado para la normalización y validación de texto:

- Cuando escribe una frecuencia en MHz y presiona Enter, el analizador normaliza el texto eliminando cualquier punto después del primer punto decimal. Por ejemplo, `14.200.000` se convierte en `14.200000`.
- El analizador detecta si ingresó un valor explícito en MHz (contiene un punto decimal) o un número sin procesar. Si ingresa un valor superior a 54.0 MHz como una entrada explícita en MHz (ej., `144.0`), se aplica el límite de frecuencia XVTR de 50000.0 MHz, lo que permite la operación en VHF/UHF sin requerir una antena XVTR.
- Si ingresa un valor superior a 54.0 MHz sin un punto decimal, el sistema divide el valor por 1000 (tratando kHz como Hz) o por 1e6 (tratando Hz como MHz) según corresponda.
- En cualquier entrada válida (0.001 a maxMhz), se emite la señal `directEntryCommitted(freqMhz, QStringLiteral("rx-direct-entry"))` para re-centrar el panadapter.

## Editor de frecuencia (v26.6.3)

Desde v26.6.3, el campo de texto del editor de frecuencia es un `FreqLineEdit` en lugar de un `QLineEdit` simple. El texto de marcador de posición ahora muestra "MHz" como texto de sugerencia en lugar de un marcador de posición atenuado. El comportamiento de edición es por lo demás idéntico: ingrese una frecuencia en MHz y presione Enter para sintonizar, o presione Escape para cancelar y restaurar la frecuencia anterior.

## Etiquetas de los controles deslizantes de ganancia AF y panorámico (v26.5.3)

Desde v26.5.3, los controles deslizantes de ganancia AF y panorámico muestran etiquetas de porcentaje y posición:

- **Control deslizante de ganancia AF**: Muestra el valor actual como un porcentaje (ej., `70%`) usando `percentText()`.
- **Control deslizante panorámico**: Muestra `C` en el centro (50), `Lx` para desplazamiento a la izquierda (ej., `L
