# Usar RIT para compensar la frecuencia de recepción de una estación que se desvía

RIT (Receive Incremental Tuning) desplaza la frecuencia de recepción en una pequeña cantidad sin mover la frecuencia de transmisión ni la lectura del VFO. Úselo cuando una estación se desvía ligeramente de su frecuencia de sintonía y desea seguirla sin reajustar toda la slice.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles de RIT están inactivos sin conexión al radio.
- Abra el applet RX Controls. Haga clic en el botón RX de la barra lateral derecha si el applet no está visible.
- Seleccione la slice que desea ajustar usando las pestañas de slice (A..H) en la parte superior del applet, si hay más de una slice activa.

## Pasos

1. En el applet RX Controls, localice la fila RIT cerca de la parte inferior del applet.
2. Haga clic en RIT para habilitar Receive Incremental Tuning. El botón se ilumina cuando está activo.
3. Use los botones `<` y `>` junto al cuadro de compensación de RIT, o desplace la rueda del ratón sobre el cuadro, para ajustar la compensación. Cada paso mueve la frecuencia de recepción en 10 Hz. El cuadro muestra la compensación actual (predeterminado: `+0 Hz`).
4. Continúe ajustando hasta que la estación que se desvía esté centrada en la banda pasante.
5. Para volver a la compensación cero sin desactivar RIT, haga clic en RIT 0. La compensación se restablece a `+0 Hz`.
6. Para desactivar RIT por completo, haga clic nuevamente en RIT. La frecuencia de recepción vuelve a la frecuencia del VFO.

## Función de cada control

| Control    | Tipo           | Predeterminado |
|------------|----------------|----------------|
| RIT        | Botón de alternancia | Apagado       |
| Compensación RIT | Cuadro       | `+0 Hz`       |
| RIT 0      | Botón pulsador | —              |

## Consejos

- RIT afecta solo la frecuencia de recepción. Su frecuencia de transmisión permanece en el VFO. Si también necesita compensar su frecuencia de transmisión, use XIT en lugar de o junto con RIT.
- El paso mínimo de 10 Hz es adecuado para trabajo en SSB y CW. Para una estación que se desvía lentamente, unos pocos toques de `>` o un breve desplazamiento de la rueda del ratón suelen ser suficientes.
- Hacer clic en RIT 0 antes de desactivar RIT es una buena práctica. Así, RIT ya estará en cero si lo vuelve a activar más tarde.

## Colores de pestañas de slice y de la placa (v0.9.3)

A partir de v0.9.3, los botones de las pestañas de slice (A..H) y la placa Slice en la esquina superior izquierda del applet toman su color de la clase singleton SliceColorManager en lugar de una tabla de colores fija. Esto significa:

- Los colores por slice son personalizables y persisten entre sesiones.
- El mismo color se refleja en los botones de las pestañas de slice, la placa Slice, los widgets del VFO y las barras de medidor dondequiera que se muestre la slice.
- No es necesario que realice ninguna acción; los colores se actualizan automáticamente cuando se conecta una slice o se cambia su color.

## Comportamiento de las pestañas de slice al reconectar (v0.9.5.1)

A partir de v0.9.5.1, la fila de pestañas de slice se reconstruye correctamente siempre que el número de slices disponibles cambia en un ciclo de desconexión y reconexión. Específicamente:

- Cuando el radio informa un número diferente de slices al reconectar, los botones de pestaña existentes se eliminan por completo antes de crear otros nuevos. La placa Slice estática se restaura y permanece visible mientras no haya pestañas presentes.
- Los controladores de señal de clic se conectan solo una vez por vida útil del applet, independientemente de cuántas veces se conecte o reconecte el radio. Esto evita que se disparen eventos duplicados al hacer clic en una pestaña de slice después de una reconexión.

No es necesario que realice ninguna acción. Si se reconecta a un radio con una configuración de slices diferente, la fila de pestañas se actualiza automáticamente.

## Comportamiento del modo NT

A partir de v0.9.3, el modo NT se trata como un modo digital en todo el applet RX Controls:

- **Los preajustes de ancho de filtro** aplican la lista de preajustes digital (DIG) a las slices NT, igual que para DIGU y DIGL.
- **La visualización del ancho de filtro** calcula el ancho de filtro NT usando el borde superior (hi), de forma coherente con el manejo de DIGU y FDV.
- **El squelch** está deshabilitado para las slices NT. Dado que el audio se enruta a través de DAX en los modos digitales, el control de squelch no tiene sentido. El botón SQL y el control deslizante de nivel de squelch se atenúan cuando NT es el modo activo. Si el squelch estaba activado al cambiar a NT, se desactiva automáticamente y se restaura al salir de NT.

## Preajustes de ancho de filtro (v0.9.5.1)

A partir de v0.9.5.1, las entradas de preajuste de filtro pueden almacenar un valor de ancho simple o un par explícito de banda pasante lo:hi. Esto coincide con el formato de almacenamiento usado por VfoWidget (#2259). El comportamiento desde su perspectiva es:

- Los preajustes que guardó en versiones anteriores (valores de ancho simple) siguen cargando y funcionando sin cambios.
- Cuando se guarda un preajuste desde una posición de banda pasante personalizada, se almacenan tanto el borde inferior como el superior del filtro. Cuando se recupera ese preajuste, la banda pasante se restaura exactamente a la misma posición, no solo al mismo ancho.
- La configuración `FilterPresets` en AppSettings usa el formato `lo:hi` para entradas con banda pasante y un entero simple para entradas solo de ancho. Las entradas múltiples están separadas por comas, por ejemplo: `300:3000,100:2900,2700`.
- Se muestran como máximo seis preajustes en el applet RX Controls, independientemente de cuántos estén almacenados.

Haga clic con el botón derecho en un botón de preajuste de filtro para guardar el ancho de filtro actual (y la posición de la banda pasante, si corresponde) como ese preajuste. Haga clic en un botón de preajuste para aplicarlo.

## Escalonamiento del ancho de filtro (v0.9.8)

A partir de v0.9.8, el método `stepFilterWidth()` recorre la lista de preajustes por modo para encontrar el preajuste de filtro más estrecho o más ancho siguiente. Esto significa que los atajos de ampliar/reducir (si están disponibles) producen una geometría de bordes correcta para el modo en todos los modos (LSB, CWL, DIGL, RTTY, AM, CW, USB) en lugar de aplicar un desplazamiento fijo simple. La lectura del ancho de filtro, compartida con el panel VFO a través de `RxApplet::formatFilterWidth()`, utiliza lógica consciente del modo para que los modos SSB y digitales muestren el ancho etiquetado correcto.

Si tiene atajos de teclado de ampliar o reducir asignados a `stepFilterWidth()`:

- Al presionar el atajo de ampliar se selecciona el siguiente preajuste más ancho en la lista de preajustes de filtro del modo actual que sea más ancho que el ancho actual.
- Al presionar el atajo de reducir se selecciona el siguiente preajuste más estrecho.
- Si no existe un preajuste más ancho/más estrecho, se ignora la pulsación de tecla.

No es necesario que realice ninguna acción; el comportamiento de escalonamiento se actualiza automáticamente en v0.9.8.

## Relacionado

- [Use XIT to offset the transmit frequency without changing RX](use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Tune the radio to a frequency (type MHz in the readout)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Pick a filter width preset for the current mode](pick-a-filter-width-preset-for-the-current-mode.md)
