# Usar RIT para desplazar la frecuencia de recepción de una estación con deriva

RIT (Receive Incremental Tuning, Sintonización Incremental de Recepción) desplaza la frecuencia de recepción en una pequeña cantidad sin mover la frecuencia de transmisión ni la lectura del VFO. Utilícelo cuando una estación se desvía ligeramente de su frecuencia de marcación y desea seguirla sin reajustar toda la franja (slice).

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. Los controles de RIT están inactivos sin conexión al equipo.
- Abra el applet de Controles de RX. Haga clic en el botón de la bandeja de RX en la barra lateral derecha si el applet no está visible.
- Seleccione la franja (slice) que desea ajustar usando las pestañas de franja (A..H) en la parte superior del applet, si hay más de una franja activa.

## Pasos

1. En el applet de Controles de RX, localice la fila de RIT cerca de la parte inferior del applet.
2. Haga clic en RIT para habilitar la Sintonización Incremental de Recepción. El botón se ilumina cuando está activo.
3. Use los botones `<` y `>` junto al cuadro de desplazamiento del desplazamiento de RIT, o desplace la rueda del ratón sobre el cuadro de desplazamiento, para ajustar el desplazamiento. Cada paso mueve la frecuencia de recepción en 10 Hz. El cuadro de desplazamiento muestra el desplazamiento actual (valor predeterminado: `+0 Hz`).
4. Continúe ajustando hasta que la estación con deriva esté centrada en la banda pasante.
5. Para volver al desplazamiento cero sin deshabilitar RIT, haga clic en RIT 0. El desplazamiento se restablece a `+0 Hz`.
6. Para desactivar RIT por completo, haga clic en RIT nuevamente. La frecuencia de recepción vuelve a la frecuencia del VFO.

## Qué hace cada control

| Control      | Tipo            | Valor predeterminado |
|--------------|-----------------|----------------------|
| RIT          | Botón de alternancia | Off (Desactivado)    |
| Despl. RIT   | Cuadro de desplazamiento | `+0 Hz`              |
| RIT 0        | Botón pulsador  | —                    |

## Consejos

- RIT afecta solo la frecuencia de recepción. Su frecuencia de transmisión permanece en el VFO. Si también necesita desplazar su frecuencia de transmisión, use XIT en lugar de o junto con RIT.
- El paso mínimo de 10 Hz es adecuado para trabajos en SSB y CW. Para una estación que se desvía lentamente, unas pocas pulsaciones de `>` o un breve desplazamiento de la rueda del ratón suele ser suficiente.
- Hacer clic en RIT 0 antes de desactivar RIT es una buena práctica. Significa que RIT ya está en cero si lo vuelve a habilitar más tarde.

## Colores de las pestañas de franja y la insignia (v0.9.3)

A partir de v0.9.3, los botones de las pestañas de franja (A..H) y la insignia de franja en la esquina superior izquierda del applet toman su color del singleton SliceColorManager en lugar de una tabla de colores fija. Esto significa:

- Los colores por franja son personalizables y persisten entre sesiones.
- El mismo color se refleja en los botones de las pestañas de franja, la insignia de franja, los widgets de VFO y las tiras de medidor dondequiera que se muestre la franja.
- No se requiere ninguna acción de su parte; los colores se actualizan automáticamente cuando una franja se conecta o se cambia su color.

## Formato del texto de la insignia de franja (v26.5.2.1)

A partir de v26.5.2.1, la etiqueta de la insignia de franja utiliza formato de texto enriquecido para que la letra de la franja pueda representarse como HTML. Esto permite caracteres especiales de color o estilo si es necesario. La insignia aún muestra la letra de la franja vinculada actualmente (A..H).

## Comportamiento de las pestañas de franja al reconectar (v0.9.5.1)

A partir de v0.9.5.1, la fila de pestañas de franja se reconstruye correctamente siempre que el número de franjas disponibles cambia a través de un ciclo de desconexión y reconexión. Específicamente:

- Cuando el equipo informa un recuento de franjas diferente al reconectar, los botones de pestañas existentes se eliminan por completo antes de crear otros nuevos. La insignia de franja estática se restaura y es visible mientras no hay pestañas presentes.
- Los controladores de señales de clic se conectan solo una vez por vida útil del applet, independientemente de cuántas veces se conecte o reconecte el equipo. Esto evita que se activen eventos duplicados cuando se hace clic en una pestaña de franja después de una reconexión.

No se requiere ninguna acción de su parte. Si se reconecta a un equipo con una configuración de franja diferente, la fila de pestañas se actualiza automáticamente.

## Comportamiento del modo RADE

Cuando selecciona RADE en el combo de modos, la franja se coloca en modo RADE (Rapid Automatic Detection and Excitation, Detección y Excitación Automática Rápida). Tenga en cuenta que RADE es un modo solo del lado del cliente: el equipo devuelve el modo real (DIGL/DIGU) inmediatamente después de la selección. Cuando cambia de RADE a otro modo, no se emite ninguna señal de desactivación de RADE porque el modo de la franja nunca es `"RADE"` en el lado del equipo. Esto evita desactivaciones espurias al cambiar de modo.

## Corrección de cambio de modo RADE (v26.5.3)

A partir de v26.5.3, al cambiar del modo RADE a través del combo de modos, el applet emite `radeActivated(false)` solo si la franja estaba realmente en modo RADE. Esto evita señales de desactivación obsoletas al cambiar de modo en una franja que no está en RADE (#2376).

## Demodulador de software WFM (v26.6.3)

A partir de v26.6.3, aparece un botón WFM junto al combo de modos en la fila de frecuencia. Este botón activa un demodulador de FM por software que enruta el audio a través de DAX IQ a un cable de alta fidelidad. El botón WFM es distinto del combo de modos: WFM nunca es una selección de modo en el combo.

Haga clic en el botón **WFM** para activar o desactivar el demodulador de FM por software para la franja actual. El botón se ilumina en verde cuando está activo. Cuando selecciona un modo de radio real del combo de modos mientras WFM está activo, la superposición de WFM se desactiva automáticamente. Esto evita conflictos entre el demodulador de software y el procesamiento de modo del propio equipo.

## Comportamiento del modo NT

A partir de v0.9.3, el modo NT se trata como un modo digital en todo el applet de Controles de RX:

- **Los valores preestablecidos de ancho de filtro** aplican la lista de valores preestablecidos digitales (DIG) a las franjas NT, igual que para DIGU y DIGL.
- **La visualización del ancho de filtro** calcula el ancho de filtro NT utilizando el borde superior (hi), de forma coherente con el manejo de DIGU y FDV.
- **El squelch** está deshabilitado para las franjas NT. Debido a que el audio se enruta a través de DAX en modos digitales, el control de squelch no es significativo. El botón SQL y el control deslizante de nivel de squelch se atenúan cuando NT es el modo activo. Si el squelch estaba activado cuando cambió a NT, se desactiva automáticamente y se restaura cuando sale de NT.

## Comportamiento del squelch en modo RTTY (v26.5.1)

A partir de v26.5.1, el modo RTTY se agrega a la lista de modos que deshabilitan automáticamente el squelch. Cuando cambia al modo RTTY:

- El botón **SQL** y el control deslizante **Nivel de squelch** están deshabilitados.
- Si el squelch estaba activado, se desactiva automáticamente y el estado guardado se restaura cuando sale de RTTY.

Esto evita que el squelch elimine los caracteres FSK y rompa la decodificación (#2504).

## Persistencia del nivel de squelch manual (v26.5.2.1)

A partir de v26.5.2.1, el umbral de squelch manual que establece con el control deslizante de nivel de squelch se guarda y restaura entre sesiones. Cuando el modo de squelch automático está activo, el equipo puede cambiar el nivel de squelch internamente; el cliente ahora recuerda su última preferencia manual para que se conserve cuando regrese al control de squelch manual. La configuración se almacena en `LastManualSquelchLevel` con un valor predeterminado de 20.

## Menú de antena RX (v26.5.2.1)

A partir de v26.5.2.1, el menú de antena RX se completa desde el `rxAntennaList()` dedicado de la franja cuando está disponible, recurriendo a la `ant_list` general del estado del panadaptador. Esto garantiza que solo vea antenas válidas para la franja actual. Los elementos del menú muestran el nombre de la antena con información sobre herramientas y una sugerencia de estado que muestra el identificador de antena sin procesar. Seleccionar un elemento llama a `setRxAntenna()` con la cadena de datos de la antena en lugar del texto de la etiqueta del menú.

## Menú de antena TX (v26.5.2.1)

A partir de v26.5.2.1, el menú de antena TX utiliza un algoritmo de filtrado refinado. Una función de respaldo `likelyTxAntennaFallbackToken()` acepta tokens de antena que comienzan con `ANT`, `TX`, o son exactamente `XVTR`. Los puertos que comienzan con `RX` están excluidos. Los elementos del menú muestran el nombre de la antena con información sobre herramientas y sugerencia de estado. Seleccionar un elemento llama a `setTxAntenna()` con la cadena de datos de la antena.

## Valores preestablecidos de ancho de filtro (v0.9.5.1)

A partir de v0.9.5.1, las entradas preestablecidas de filtro pueden almacenar un valor de ancho simple o un par explícito de banda pasante lo:hi. Esto coincide con el formato de almacenamiento utilizado por VfoWidget (#2259). El comportamiento desde su perspectiva es:

- Los valores preestablecidos que guardó en versiones anteriores (valores de ancho simple) continúan cargándose y funcionando sin cambios.
- Cuando se guarda un valor preestablecido desde una posición de banda pasante personalizada, se almacenan tanto el borde de filtro bajo como el alto. Cuando se recupera ese valor preestablecido, la banda pasante se restaura exactamente a la misma posición, no solo al mismo ancho.
- La configuración `FilterPresets` en AppSettings utiliza el formato `lo:hi` para entradas con conocimiento de banda pasante y un entero simple para entradas de solo ancho. Las múltiples entradas están separadas por comas, por ejemplo: `300:3000,100:2900,2700`.
- Se muestran como máximo seis valores preestablecidos en el applet de Controles de RX, independientemente de cuántos estén almacenados.

Haga clic derecho en un botón de valor preestablecido de filtro para guardar el ancho de filtro actual (y la posición de la banda pasante, si corresponde) como ese valor preestablecido. Haga clic en un botón de valor preestablecido para aplicarlo.

## Escalonamiento del ancho de filtro (v0.9.8)

A partir de v0.9.8, el método `stepFilterWidth()` recorre la lista de valores preestablecidos por modo para encontrar el siguiente valor preestablecido de filtro más ancho o más estrecho. Esto significa que los atajos de ampliar/estrechar (si están disponibles) producen una geometría de borde correcta para el modo para todos los modos (LSB, CWL, DIGL, RTTY, AM, CW, USB) en lugar de aplicar un desplazamiento fijo simple. La lectura del ancho de filtro, compartida con el panel VFO a través de `RxApplet::formatFilterWidth()`, utiliza una lógica consciente del modo para que los modos SSB y digitales muestren el ancho etiquetado correcto.

Si tiene atajos de teclado para ampliar o estrechar vinculados a `stepFilterWidth()`:

- Al presionar el atajo de ampliar se selecciona el siguiente valor preestablecido más ancho en la lista de valores preestablecidos de filtro del modo actual que sea más ancho que el ancho actual.
- Al presionar el atajo de estrechar se selecciona el siguiente valor preestablecido más estrecho.
- Si no existe un valor preestablecido más ancho/estrecho, se ignora la pulsación de tecla.

No se requiere ninguna acción de su parte; el comportamiento de escalonamiento se actualiza automáticamente en v0.9.8.

## Comportamiento del botón de silencio (v26.5.3)

A partir de v26.5.3, el botón de silencio utiliza un sistema de discriminación de clics:

- **Un solo clic** silencia o reactiva el sonido solo de la franja actual. La acción se pospone por el intervalo de doble clic de la plataforma (aproximadamente 400 ms) para que un doble clic pueda anularla.
- **Doble clic** silencia o reactiva el sonido de todas las franjas propiedad de este cliente, emitido a través de la señal `muteAllToggled`.
- El icono visual (🔊/🔇) se actualiza solo cuando el equipo confirma el cambio de estado de silencio a través de `SliceModel::audioMuteChanged`. Esto sigue la Política de Configuración Autoritativa del Equipo (Radio-Authoritative Settings Policy) (#2489) — el equipo es la fuente de verdad para el silencio de audio.
- El estado de silencio NO se guarda ni se restaura al reconectar.

## Analizador de entrada de frecuencia (v26.5.3)

A partir de v26.5.3, la entrada de frecuencia utiliza un `FrequencyEntryParser` dedicado para la normalización y validación de texto:

- Cuando escribe una frecuencia en MHz y presiona Enter, el analizador normaliza el texto eliminando cualquier punto después del primer punto decimal. Por ejemplo, `14.200.000` se convierte en `14.200000`.
- El analizador detecta si ingresó un valor explícito en MHz (contiene un punto decimal) o un número sin procesar. Si ingresa un valor superior a 54.0 MHz como una entrada explícita en MHz (por ejemplo, `144.0`), se aplica el límite de frecuencia XVTR de 50000.0 MHz, lo que permite la operación en VHF/UHF sin requerir una antena XVTR.
- Si ingresa un valor superior a 54.0 MHz sin un punto decimal, el sistema divide el valor por 1000 (tratando kHz como Hz) o por 1e6 (tratando Hz como MHz) según corresponda.
- En cualquier entrada válida (0.001 a maxMhz), se emite la señal `directEntryCommitted(freqMhz, QStringLiteral("rx-direct-entry"))` para re-centrar el panadaptador.

## Editor de frecuencia (v26.6.3)

A partir de v26.6.3, el campo de texto del editor de frecuencia es un `FreqLineEdit` en lugar de un `QLineEdit` simple. El texto de marcador de posición ahora dice "MHz" como texto de sugerencia en lugar de un marcador de posición atenuado. El comportamiento de edición es por lo demás idéntico: ingrese una frecuencia en MHz y presione Enter para sintonizar, o presione Escape para cancelar y restaurar la frecuencia anterior.

## Etiquetas de los controles deslizantes de ganancia AF y paneo
