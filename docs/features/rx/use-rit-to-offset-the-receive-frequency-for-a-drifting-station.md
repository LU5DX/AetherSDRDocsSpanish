# Usar RIT para desplazar la frecuencia de recepción hacia una estación con deriva

RIT (Receive Incremental Tuning) desplaza la frecuencia de recepción en una pequeña cantidad sin mover la frecuencia de transmisión ni el indicador del VFO. Úselo cuando una estación deriva ligeramente de su frecuencia marcada y desea seguirla sin resintonizar todo el slice (receptor parcial).

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Los controles RIT están inactivos sin una conexión de radio.
- Abra el applet RX Controls. Haga clic en el botón RX del panel lateral derecho si el applet no está visible.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) en la parte superior del applet, si hay más de un slice activo.

## Pasos

1. En el applet RX Controls, localice la fila RIT cerca de la parte inferior del applet.
2. Haga clic en RIT para activar Receive Incremental Tuning. El botón se ilumina cuando está activo.
3. Use los botones `<` y `>` junto al cuadro de valores del desplazamiento RIT, o gire la rueda del ratón sobre el cuadro de valores, para ajustar el desplazamiento. Cada paso mueve la frecuencia de recepción 10 Hz. El cuadro de valores muestra el desplazamiento actual (por defecto: `+0 Hz`).
4. Continúe ajustando hasta que la estación con deriva quede centrada en la banda de paso.
5. Para volver a cero sin desactivar RIT, haga clic en RIT 0. El desplazamiento se restablece a `+0 Hz`.
6. Para desactivar RIT por completo, haga clic nuevamente en RIT. La frecuencia de recepción vuelve a la frecuencia del VFO.

## Qué hace cada control

| Control          | Tipo             | Valor por defecto |
|------------------|------------------|-------------------|
| RIT              | Botón de alternancia | Off          |
| Desplazamiento RIT | Cuadro de valores | `+0 Hz`       |
| RIT 0            | Botón pulsador   | —                 |

## Consejos

- RIT afecta únicamente a la frecuencia de recepción. Su frecuencia de transmisión permanece en el VFO. Si también necesita desplazar la frecuencia de transmisión, use XIT en lugar de RIT o junto con él.
- El paso mínimo de 10 Hz es adecuado para trabajo en SSB y CW. Para una estación que deriva lentamente, unos pocos toques en `>` o un giro corto de la rueda del ratón suelen ser suficientes.
- Es una buena práctica hacer clic en RIT 0 antes de desactivar RIT. Así, RIT ya estará en cero si lo reactiva más adelante.

## Colores de pestañas y etiqueta de slice (v0.9.3)

A partir de v0.9.3, los botones de pestaña de slice (A..H) y la etiqueta Slice en la esquina superior izquierda del applet toman su color del singleton SliceColorManager en lugar de una tabla de colores fija. Esto significa que:

- Los colores por slice son personalizables y se conservan entre sesiones.
- El mismo color se refleja en los botones de pestaña de slice, la etiqueta Slice, los widgets de VFO y las tiras de medidor en todos los lugares donde se muestra el slice.
- No se requiere ninguna acción de su parte; los colores se actualizan automáticamente cuando se conecta un slice o se cambia su color.

## Comportamiento de las pestañas de slice al reconectar (v0.9.5.1)

A partir de v0.9.5.1, la fila de pestañas de slice se reconstruye correctamente cada vez que el número de slices disponibles cambia a lo largo de un ciclo de desconexión y reconexión. Específicamente:

- Cuando la radio informa un número de slices diferente al reconectar, los botones de pestaña existentes se eliminan por completo antes de crear los nuevos. La etiqueta estática Slice se restaura y permanece visible mientras no hay pestañas presentes.
- Los manejadores de señal de clic se conectan solo una vez durante la vida útil del applet, independientemente de cuántas veces la radio se conecte o reconecte. Esto evita que se disparen eventos duplicados al hacer clic en una pestaña de slice tras una reconexión.

No se requiere ninguna acción de su parte. Si se reconecta a una radio con una configuración de slice diferente, la fila de pestañas se actualiza automáticamente.

## Comportamiento del modo NT

A partir de v0.9.3, el modo NT se trata como un modo digital en todo el applet RX Controls:

- **Preajustes de ancho de filtro**: aplican la lista de preajustes digital (DIG) a los slices NT, igual que DIGU y DIGL.
- **Visualización del ancho de filtro**: calcula el ancho de filtro NT usando el borde superior (hi), de forma coherente con el manejo de DIGU y FDV.
- **Silenciador (Squelch)**: está desactivado para los slices NT. Dado que el audio se enruta a través de DAX en modos digitales, el control de squelch no es significativo. El botón SQL y el deslizador de nivel de squelch aparecen en gris cuando NT es el modo activo. Si el squelch estaba activado al cambiar a NT, se desactiva automáticamente y se restaura al salir de NT.

## Preajustes de ancho de filtro (v0.9.5.1)

A partir de v0.9.5.1, las entradas de preajuste de filtro pueden almacenar un valor de ancho simple o un par explícito de banda de paso lo:hi. Esto coincide con el formato de almacenamiento usado por VfoWidget (#2259). El comportamiento desde su perspectiva es:

- Los preajustes guardados en versiones anteriores (valores de ancho simple) continúan cargándose y funcionando sin ningún cambio.
- Cuando se guarda un preajuste desde una posición de banda de paso personalizada, se almacenan tanto el borde inferior como el superior del filtro. Al recuperar ese preajuste, la banda de paso se restaura a exactamente la misma posición, no solo al mismo ancho.
- El ajuste `FilterPresets` en AppSettings usa el formato `lo:hi` para entradas con banda de paso definida y un entero simple para entradas de solo ancho. Las entradas múltiples se separan con comas; por ejemplo: `300:3000,100:2900,2700`.
- Se muestran como máximo seis preajustes en el applet RX Controls, independientemente de cuántos estén almacenados.

Haga clic derecho en un botón de preajuste de filtro para guardar el ancho de filtro actual (y la posición de la banda de paso, si corresponde) como ese preajuste. Haga clic en un botón de preajuste para aplicarlo.

## Relacionado

- [Usar XIT para desplazar la frecuencia de transmisión sin cambiar la recepción](use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Sintonizar la radio a una frecuencia (introducir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
