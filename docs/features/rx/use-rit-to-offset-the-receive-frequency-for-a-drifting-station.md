# Use RIT para compensar la frecuencia de recepción de una estación a la deriva

RIT (Receive Incremental Tuning) desplaza la frecuencia de recepción en una pequeña cantidad sin mover la frecuencia de transmisión ni la lectura del VFO. Úselo cuando una estación se desvía ligeramente de su frecuencia de marcación y desea seguirla sin re-sintonizar toda la slice.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Los controles RIT están inactivos sin conexión a la radio.
- Abra el applet RX Controls. Haga clic en el botón de la bandeja RX en la barra lateral derecha si el applet no está visible.
- Seleccione la slice que desea ajustar usando las pestañas de slice (A..H) en la parte superior del applet, si hay más de una slice activa.

## Pasos

1. En el applet RX Controls, localice la fila RIT cerca de la parte inferior del applet.
2. Haga clic en RIT para habilitar Receive Incremental Tuning. El botón se ilumina cuando está activo.
3. Use los botones `<` y `>` junto al cuadro giratorio de compensación RIT, o desplace la rueda del mouse sobre el cuadro giratorio, para ajustar la compensación. Cada paso mueve la frecuencia de recepción en 10 Hz. El cuadro giratorio muestra la compensación actual (predeterminado: `+0 Hz`).
4. Continúe ajustando hasta que la estación a la deriva esté centrada en la banda de paso.
5. Para volver a compensación cero sin deshabilitar RIT, haga clic en RIT 0. La compensación se restablece a `+0 Hz`.
6. Para desactivar RIT por completo, haga clic en RIT nuevamente. La frecuencia de recepción vuelve a la frecuencia del VFO.

## Qué hace cada control

| Control    | Tipo                                                                                                                                                                                                                                                                                                                                                      | Predeterminado                                                                                                                                                                                                                             |
|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| RIT        | Botón de alternancia                                                                                                                                                                                                                                                                                                                                      | Apagado                                                                                                                                                                                                                                    |
| Compensación RIT | Cuadro giratorio                                                                                                                                                                                                                                                                                                                                          | `+0 Hz`                                                                                                                                                                                                                                    |
| RIT 0      | Botón pulsador                                                                                                                                                                                                                                                                                                                                            | —                                                                                                                                                                                                                                          |
| REV / XFC  | Para operación de repetidora FM, REV invierte el signo de la compensación TX para trabajar un par de repetidora invertido. En backends que admiten una verificación de frecuencia de transmisión, el botón se etiqueta nuevamente como XFC: al presionarlo, mantiene la verificación de frecuencia de transmisión durante la duración de la pulsación, y mientras está presionado, fuerza brevemente la radio hacia la frecuencia de transmisión para confirmar cobertura. | El botón alterna REV (marcable) normalmente, o se convierte en un botón momentáneo XFC hacia abajo cuando el backend de radio conectado anuncia hasTransmitFrequencyCheck. El XFC mantenido se libera al ocultar, desactivar, cambio de capacidad o desconexión. |
| SQL / AUTO | Botón de ciclo de tres posiciones: cada clic avanza Apagado → SQL (umbral manual) → AUTO (el algoritmo rastrea el piso de ruido) → Apagado. En modo AUTO, el botón muestra 'AUTO' en ámbar; en modo manual, 'SQL' en verde. Deshabilitado (y apagado automáticamente) en modos RTTY y digitales (DIGU, DIGL) donde el squelch recortaría los caracteres FSK (#2504). | Manual y Auto activan el squelch de la radio. El algoritmo de squelch automático reside en el panadapter; el nivel es el margen en dB por encima del piso de ruido medido. Reflejado por un botón idéntico en la pestaña Audio del panel VFO. |

## Consejos

- RIT afecta solo la frecuencia de recepción. Su frecuencia de transmisión permanece en el VFO. Si también necesita compensar su frecuencia de transmisión, use XIT en lugar de o junto con RIT.
- El paso mínimo de 10 Hz es adecuado para trabajo en SSB y CW. Para una estación que se desplaza lentamente, unas pocas pulsaciones de `>` o un breve desplazamiento de la rueda del mouse suele ser suficiente.
- Hacer clic en RIT 0 antes de desactivar RIT es una buena práctica. Significa que RIT ya está en cero si lo vuelve a habilitar más tarde.

## Colores de pestañas de slice y distintivo (v0.9.3)

Desde v0.9.3, los botones de pestaña de slice (A..H) y el distintivo Slice en la esquina superior izquierda del applet toman su color del singleton SliceColorManager en lugar de una tabla de colores fija. Esto significa:

- Los colores por slice son personalizables y persisten entre sesiones.
- El mismo color se refleja en los botones de pestaña de slice, el distintivo Slice, los widgets VFO y las tiras de medidores dondequiera que se muestre la slice.
- No se requiere ninguna acción de su parte; los colores se actualizan automáticamente cuando una slice se conecta o se cambia su color.

## Formato de texto del distintivo Slice (v26.5.2.1)

Desde v26.5.2.1, la etiqueta del distintivo de slice usa formato de texto enriquecido para que la letra de la slice pueda representarse como HTML. Esto permite caracteres especiales de color o estilo si es necesario. El distintivo aún muestra la letra de la slice actualmente vinculada (A..H).

## Comportamiento de pestañas de slice en reconexión (v0.9.5.1)

Desde v0.9.5.1, la fila de pestañas de slice se reconstruye correctamente cuando el número de slices disponibles cambia en un ciclo de desconexión y reconexión. Específicamente:

- Cuando la radio informa una cantidad diferente de slices al reconectar, los botones de pestaña existentes se eliminan por completo antes de crear otros nuevos. El distintivo Slice estático se restaura y es visible mientras no hay pestañas presentes.
- Los manejadores de señal de clic se conectan solo una vez por vida del applet, independientemente de cuántas veces se conecte o reconecte la radio. Esto evita que se disparen eventos duplicados al hacer clic en una pestaña de slice después de una reconexión.

No se requiere ninguna acción de su parte. Si se reconecta a una radio con una configuración de slices diferente, la fila de pestañas se actualiza automáticamente.

## Comportamiento del modo RADE

Cuando selecciona RADE del combo de modos, la slice se coloca en modo RADE (Rapid Automatic Detection and Excitation). Tenga en cuenta que RADE es un modo solo del lado del cliente: la radio refleja el modo real (DIGL/DIGU) inmediatamente después de la selección. Cuando cambia de RADE a otro modo, no se emite una señal de desactivación de RADE porque el modo de la slice nunca es `"RADE"` en el lado de la radio. Esto evita desactivaciones espurias al cambiar de modos.

## Corrección de cambio de modo RADE (v26.5.3)

Desde v26.5.3, al cambiar fuera del modo RADE mediante el combo de modos, el applet emite `radeActivated(false)` solo si la slice estaba realmente en modo RADE. Esto evita señales de desactivación obsoletas al cambiar de modos en una slice que no es RADE (#2376).

## Demodulador de software WFM (v26.6.3)

Desde v26.6.3, aparece un botón WFM junto al combo de modos en la fila de frecuencia. Este botón activa un demodulador FM por software que enruta el audio a través de DAX IQ a un Cable Hi-Fi. El botón WFM es distinto del combo de modos: WFM nunca es una selección de modo en el combo.

Haga clic en el botón **WFM** para alternar el demodulador FM por software activado o desactivado para la slice actual. El botón se ilumina en verde cuando está activo. Cuando selecciona un modo de radio real del combo de modos mientras WFM está activo, la superposición WFM se desactiva automáticamente. Esto evita conflictos entre el demodulador por software y el procesamiento de modos de la propia radio.

## Comportamiento del modo NT

Desde v0.9.3, el modo NT se trata como un modo digital en todo el applet RX Controls:

- **Preajustes de ancho de filtro** aplican la lista de preajustes digitales (DIG) a las slices NT, igual que DIGU y DIGL.
- **Visualización del ancho de filtro** calcula el ancho de filtro NT usando el borde superior (hi), consistente con el manejo de DIGU y FDV.
- **Squelch** está deshabilitado para slices NT. Debido a que el audio se enruta a través de DAX en modos digitales, el control de squelch no es significativo. El botón SQL y el control deslizante de nivel de squelch se atenúan cuando NT es el modo activo. Si el squelch estaba activado cuando cambió a NT, se apaga automáticamente y se restaura cuando sale de NT.

## Comportamiento de squelch en modo RTTY (v26.5.1)

Desde v26.5.1, el modo RTTY se agrega a la lista de modos que deshabilitan automáticamente el squelch. Cuando cambia al modo RTTY:

- El botón **SQL** y el control deslizante de **nivel de squelch** se deshabilitan.
- Si el squelch estaba activado, se apaga automáticamente y el estado guardado se restaura cuando sale de RTTY.

Esto evita que el squelch recorte los caracteres FSK y rompa la decodificación (#2504).

## Persistencia del nivel de squelch manual (v26.5.2.1)

Desde v26.5.2.1, el umbral de squelch manual que establece con el control deslizante de nivel de squelch se guarda y restaura entre sesiones. Cuando el modo de squelch automático está activo, la radio puede cambiar el nivel de squelch internamente: el cliente ahora recuerda su última preferencia manual para que se conserve cuando vuelva al control de squelch manual. La configuración se almacena en `LastManualSquelchLevel` con un valor predeterminado de 20.

## El nivel de squelch manual es autoritativo para la radio (v26.8.4)

Desde v26.8.4, el nivel de squelch manual ya no se siembra desde `LastManualSquelchLevel` al inicio. La radio es la fuente de verdad para las configuraciones de squelch (#4592). El nivel de squelch manual ahora toma su valor predeterminado de clase de 20 como respaldo cuando no hay ninguna slice adjunta; el nivel real proviene de la radio.

## Menú de antena RX (v26.5.2.1)

Desde v26.5.2.1, el menú de antena RX se completa desde la `rxAntennaList()` dedicada de la slice cuando está disponible, recurriendo a la `ant_list` general del estado del panadapter. Esto garantiza que solo vea antenas válidas para la slice actual. Los elementos del menú muestran el nombre de la antena con información sobre herramientas y sugerencia de estado mostrando el identificador de antena sin procesar. Seleccionar un elemento llama a `setRxAntenna()` con la cadena de datos de antena en lugar del texto de la etiqueta del menú.

## Menú de antena TX (v26.5.2.1)

Desde v26.5.2.1, el menú de antena TX usa un algoritmo de filtrado refinado. Una función de respaldo `likelyTxAntennaFallbackToken()` acepta tokens de antena que comienzan con `ANT`, `TX`, o son exactamente `XVTR`. Los puertos que comienzan con `RX` se excluyen. Los elementos del menú muestran el nombre de la antena con información sobre herramientas y sugerencia de estado. Seleccionar un elemento llama a `setTxAntenna()` con la cadena de datos de antena.

## Preajustes de ancho de filtro (v0.9.5.1)

Desde v0.9.5.1, las entradas de preajuste de filtro pueden almacenar un valor de ancho simple o un par de banda de paso lo:hi explícito. Esto coincide con el formato de almacenamiento utilizado por VfoWidget (#2259). El comportamiento desde su perspectiva es:

- Los preajustes que guardó en versiones anteriores (valores de ancho simple) continúan cargándose y funcionando sin ningún cambio.
- Cuando se guarda un preajuste desde una posición de banda de paso personalizada, se almacenan tanto el borde de filtro bajo como el alto. Cuando se recupera ese preajuste, la banda de paso se restaura exactamente a la misma posición, no solo al mismo ancho.
- La configuración `FilterPresets` en AppSettings usa el formato `lo:hi` para entradas con banda de paso y un entero simple para entradas solo de ancho. Varias entradas están separadas por comas, por ejemplo: `300:3000,100:2900,2700`.
- Se muestran como máximo seis preajustes en el applet RX Controls independientemente de cuántos estén almacenados.

Haga clic derecho en un botón de preajuste de filtro para guardar el ancho de filtro actual (y la posición de banda de paso, si corresponde) como ese preajuste. Haga clic en un botón de preajuste para aplicarlo.

## Incremento de ancho de filtro (v0.9.8)

Desde v0.9.8, el método `stepFilterWidth()` recorre la lista de preajustes por modo para encontrar el siguiente preajuste de filtro más estrecho o más ancho. Esto significa que los atajos de ensanchar/estrechar (si están disponibles) producen geometría de borde correcta para el modo en todos los modos (LSB, CWL, DIGL, RTTY, AM, CW, USB) en lugar de aplicar un desplazamiento fijo simple. La lectura del ancho de filtro, compartida con el panel VFO mediante `RxApplet::formatFilterWidth()`, usa lógica consciente del modo para que los modos SSB y digitales muestren el ancho etiquetado correcto.

Si tiene atajos de teclado de ensanchar o estrechar vinculados a `stepFilterWidth()`:

- Presionar el atajo de ensanchar selecciona el siguiente preajuste más ancho en la lista de preajustes de filtro del modo actual que sea más ancho que el ancho actual.
- Presionar el atajo de estrechar selecciona el siguiente preajuste más estrecho.
- Si no existe ningún preajuste más ancho/estrecho, se ignora la pulsación de tecla.

No se requiere ninguna acción de su parte; el comportamiento de incremento se actualiza automáticamente en v0.9.8.

## Comportamiento del botón de silencio (v26.5.3)

Desde v26.5.3, el botón de silencio usa un sistema de discriminación de clics:

- **Un solo clic** silencia o reactiva solo la slice actual. La acción se difiere por el intervalo de doble clic de la plataforma (aproximadamente 400 ms) para que un doble clic pueda anularla.
- **Doble clic** silencia o reactiva todas las slices propiedad de este cliente, emitido a través de la señal `muteAllToggled`.
- El icono visual (🔊/🔇) se actualiza solo cuando la radio confirma el cambio de estado de silencio mediante `SliceModel::audioMuteChanged`. Esto sigue la Política de Configuración Autoritativa de la Radio (#2489): la radio es la fuente de verdad para el silencio de audio.
- El estado de silencio NO se guarda ni se restaura en la reconexión.

## Analizador de entrada de frecuencia (v26.5.3)

Desde v26.5.3, la entrada de frecuencia usa un `FrequencyEntryParser` dedicado para la normalización y validación de texto:

- Cuando escribe una frecuencia en MHz y presiona Enter, el analizador normaliza el texto eliminando cualquier punto después del primer decimal. Por ejemplo, `14.200.000` se convierte en `14.200000`.
- El analizador detecta si ingresó un valor MHz explícito (contiene un punto
