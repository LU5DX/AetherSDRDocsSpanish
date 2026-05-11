# Usar RIT para compensar la frecuencia de recepción de una estación a la deriva

RIT (Receive Incremental Tuning) desplaza la frecuencia de recepción en una pequeña cantidad sin mover la frecuencia de transmisión ni la lectura del VFO. Úselo cuando una estación se desvía ligeramente de su frecuencia de marcación y desea seguirla sin re-sintonizar todo el slice.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles RIT están inactivos sin una conexión de radio.
- Abra el applet RX Controls. Haga clic en el botón de la bandeja RX en la barra lateral derecha si el applet no está visible.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) en la parte superior del applet, si más de un slice está activo.

## Pasos

1. En el applet RX Controls, localice la fila RIT cerca de la parte inferior del applet.
2. Haga clic en RIT para habilitar Receive Incremental Tuning. El botón se ilumina cuando está activo.
3. Use los botones `<` y `>` junto al control numérico de compensación RIT, o gire la rueda del ratón sobre el control numérico, para ajustar la compensación. Cada paso mueve la frecuencia de recepción en 10 Hz. El control numérico muestra la compensación actual (por defecto: `+0 Hz`).
4. Continúe ajustando hasta que la estación a la deriva esté centrada en la banda pasante.
5. Para volver a la compensación cero sin desactivar RIT, haga clic en RIT 0. La compensación se restablece a `+0 Hz`.
6. Para desactivar RIT por completo, haga clic nuevamente en RIT. La frecuencia de recepción vuelve a la frecuencia del VFO.

## Qué hace cada control

| Control      | Tipo                | Por defecto |
|--------------|---------------------|-------------|
| RIT          | Botón de alternancia | Apagado     |
| RIT offset   | Control numérico    | `+0 Hz`     |
| RIT 0        | Botón pulsador      | —           |

## Consejos

- RIT afecta solo la frecuencia de recepción. Su frecuencia de transmisión permanece en el VFO. Si también necesita compensar su frecuencia de transmisión, use XIT en lugar de o junto con RIT.
- El paso mínimo de 10 Hz es adecuado para trabajo en SSB y CW. Para una estación que se desplaza lentamente, unos pocos toques en `>` o un breve giro de la rueda del ratón suelen ser suficientes.
- Hacer clic en RIT 0 antes de desactivar RIT es una buena práctica. Significa que RIT ya está en cero si lo vuelve a habilitar más tarde.

## Pestañas de slice y colores de insignia (v0.9.3)

A partir de v0.9.3, los botones de pestaña de slice (A..H) y la insignia Slice en la esquina superior izquierda del applet toman su color del singleton SliceColorManager en lugar de una tabla de colores fija. Esto significa:

- Los colores por slice son personalizables y persisten entre sesiones.
- El mismo color se refleja en los botones de pestaña de slice, la insignia Slice, los widgets VFO y las tiras de medidor dondequiera que se muestre el slice.
- No se requiere ninguna acción de su parte; los colores se actualizan automáticamente cuando un slice se conecta o cambia su color.

## Comportamiento de pestañas de slice al reconectar (v0.9.5.1)

A partir de v0.9.5.1, la fila de pestañas de slice se reconstruye correctamente cada vez que el número de slices disponibles cambia en un ciclo de desconexión y reconexión. Específicamente:

- Cuando el radio reporta un recuento de slices diferente al reconectar, los botones de pestaña existentes se eliminan por completo antes de crear otros nuevos. La insignia Slice estática se restaura y es visible mientras no haya pestañas presentes.
- Los manejadores de señales de clic se conectan solo una vez por vida útil del applet, independientemente de cuántas veces el radio se conecte o reconecte. Esto evita que se activen eventos duplicados al hacer clic en una pestaña de slice después de una reconexión.

No se requiere ninguna acción de su parte. Si se reconecta a un radio con una configuración de slices diferente, la fila de pestañas se actualiza automáticamente.

## Comportamiento del modo RADE

Cuando selecciona RADE del combo de modos, el slice se coloca en modo RADE (Rapid Automatic Detection and Excitation). Si el mismo slice estaba previamente en RADE y cambia a otro modo, la señal de desactivación de RADE solo se emite si ese slice estaba realmente en RADE antes del cambio. Esto evita desactivaciones espurias cuando:

- Se cambian modos en un slice que no está en RADE
- Se carga un perfil al inicio
- Se activa RADE desde una fuente externa como el widget VFO

## Comportamiento del modo NT

A partir de v0.9.3, el modo NT se trata como un modo digital en todo el applet RX Controls:

- Los **preajustes de ancho de filtro** aplican la lista de preajustes digital (DIG) a los slices NT, igual que DIGU y DIGL.
- La **visualización del ancho de filtro** calcula el ancho de filtro NT usando el borde superior (hi), de manera coherente con el manejo de DIGU y FDV.
- El **squelch** está deshabilitado para slices NT. Debido a que el audio se enruta a través de DAX en modos digitales, el control de squelch no es significativo. El botón SQL y el control deslizante de nivel de squelch se atenúan cuando NT es el modo activo. Si el squelch estaba activo cuando cambió a NT, se desactiva automáticamente y se restaura cuando sale de NT.

## Comportamiento de squelch en modo RTTY (v26.5.1)

A partir de v26.5.1, el modo RTTY se agrega a la lista de modos que deshabilitan automáticamente el squelch. Cuando cambia al modo RTTY:

- El botón **SQL** y el control deslizante **Nivel de squelch** se deshabilitan.
- Si el squelch estaba activo, se desactiva automáticamente y el estado guardado se restaura cuando sale de RTTY.

Esto evita que el squelch elimine los caracteres FSK e interrumpa la decodificación (#2504).

## Preajustes de ancho de filtro (v0.9.5.1)

A partir de v0.9.5.1, las entradas de preajuste de filtro pueden almacenar ya sea un valor de ancho simple o un par explícito de banda pasante lo:hi. Esto coincide con el formato de almacenamiento utilizado por VfoWidget (#2259). El comportamiento desde su perspectiva es:

- Los preajustes que guardó en versiones anteriores (valores de ancho simples) continúan cargándose y funcionando sin ningún cambio.
- Cuando se guarda un preajuste desde una posición de banda pasante personalizada, se almacenan tanto el borde inferior como el superior del filtro. Cuando se recupera ese preajuste, la banda pasante se restaura exactamente a la misma posición, no solo al mismo ancho.
- La configuración `FilterPresets` en AppSettings usa el formato `lo:hi` para entradas con conocimiento de banda pasante y un entero simple para entradas solo de ancho. Las múltiples entradas están separadas por comas, por ejemplo: `300:3000,100:2900,2700`.
- Se muestran como máximo seis preajustes en el applet RX Controls, independientemente de cuántos estén almacenados.

Haga clic derecho en un botón de preajuste de filtro para guardar el ancho de filtro actual (y la posición de la banda pasante, si corresponde) como ese preajuste. Haga clic en un botón de preajuste para aplicarlo.

## Escalonado de ancho de filtro (v0.9.8)

A partir de v0.9.8, el método `stepFilterWidth()` recorre la lista de preajustes por modo para encontrar el siguiente preajuste de filtro más angosto o más ancho. Esto significa que los atajos de ampliar/reducir (si están disponibles) producen geometría de borde correcta según el modo para todos los modos (LSB, CWL, DIGL, RTTY, AM, CW, USB) en lugar de aplicar un desplazamiento fijo simple. La lectura del ancho de filtro, compartida con el panel VFO a través de `RxApplet::formatFilterWidth()`, utiliza lógica consciente del modo para que los modos SSB y digitales muestren el ancho etiquetado correcto.

Si tiene atajos de teclado de ampliar o reducir vinculados a `stepFilterWidth()`:

- Al presionar el atajo de ampliar se selecciona el siguiente preajuste más ancho en la lista de preajustes de filtro del modo actual que sea más ancho que el ancho actual.
- Al presionar el atajo de reducir se selecciona el siguiente preajuste más angosto.
- Si no existe un preajuste más ancho/más angosto, se ignora la pulsación de tecla.

No se requiere ninguna acción de su parte; el comportamiento de escalonado se actualiza automáticamente en v0.9.8.

## Relacionado

- [Use XIT to offset the transmit frequency without changing RX](use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Tune the radio to a frequency (type MHz in the readout)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Pick a filter width preset for the current mode](pick-a-filter-width-preset-for-the-current-mode.md)
