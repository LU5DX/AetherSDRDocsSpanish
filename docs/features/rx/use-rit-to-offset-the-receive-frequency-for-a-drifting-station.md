# Usar RIT para desplazar la frecuencia de recepción de una estación que se desvía

RIT (Receive Incremental Tuning) desplaza la frecuencia de recepción una pequeña cantidad sin mover la frecuencia de transmisión ni la lectura del VFO. Úsalo cuando una estación se desvía ligeramente de tu frecuencia de sintonia y deseas seguirla sin resintonizar toda la slice.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Los controles de RIT están inactivos sin conexión a la radio.
- Abre el applet RX Controls. Haz clic en el botón RX en la barra lateral derecha si el applet no es visible.
- Selecciona la slice que deseas ajustar usando las pestañas de slice (A..H) en la parte superior del applet, si hay más de una slice activa.

## Pasos

1. En el applet RX Controls, localiza la fila RIT cerca de la parte inferior del applet.
2. Haz clic en RIT para habilitar Receive Incremental Tuning. El botón se ilumina cuando está activo.
3. Usa los botones `<` y `>` junto a la casilla de desplazamiento RIT offset, o desplaza la rueda del ratón sobre la casilla, para ajustar el desplazamiento. Cada paso mueve la frecuencia de recepción 10 Hz. La casilla muestra el desplazamiento actual (predeterminado: `+0 Hz`).
4. Continúa ajustando hasta que la estación que se desvía esté centrada en la banda de paso.
5. Para volver al desplazamiento cero sin desactivar RIT, haz clic en RIT 0. El desplazamiento se reinicia a `+0 Hz`.
6. Para desactivar RIT por completo, haz clic en RIT nuevamente. La frecuencia de recepción vuelve a la frecuencia del VFO.

## Qué hace cada control

| Control      | Tipo          | Predeterminado |
|--------------|---------------|----------------|
| RIT          | Botón de alternancia | Desactivado |
| RIT offset   | Casilla de desplazamiento | `+0 Hz` |
| RIT 0        | Botón de pulsación | — |

## Consejos

- RIT afecta solo la frecuencia de recepción. Tu frecuencia de transmisión permanece en el VFO. Si también necesitas desplazar tu frecuencia de transmisión, usa XIT en lugar de RIT o junto con RIT.
- El paso mínimo de 10 Hz es adecuado para trabajo en SSB y CW. Para una estación que se desvía lentamente, unos pocos pulsaciones de `>` o un breve desplazamiento de la rueda del ratón suele ser suficiente.
- Es una buena práctica hacer clic en RIT 0 antes de desactivar RIT. Significa que RIT ya estará en cero si lo vuelves a habilitar más tarde.

## Colores de pestañas y insignia de slice (v0.9.3)

A partir de v0.9.3, los botones de pestañas de slice (A..H) y la insignia Slice en la esquina superior izquierda del applet obtienen su color del singleton SliceColorManager en lugar de una tabla de colores fija. Esto significa:

- Los colores por slice son personalizables y se mantienen entre sesiones.
- El mismo color se refleja en los botones de pestañas de slice, la insignia Slice, los widgets VFO y las tiras de medidor donde quiera que se muestre la slice.
- No se requiere ninguna acción de tu parte; los colores se actualizan automáticamente cuando se conecta una slice o se cambia su color.

## Comportamiento del modo NT

A partir de v0.9.3, el modo NT se trata como un modo digital en todo el applet RX Controls:

- **Preajustes de ancho de filtro** aplican la lista de preajustes digital (DIG) a slices NT, igual que DIGU y DIGL.
- **Visualización de ancho de filtro** calcula el ancho de filtro de NT usando el borde superior (hi), consistente con el manejo de DIGU y FDV.
- **Silenciador** está desactivado para slices NT. Como el audio se enruta a través de DAX en modos digitales, el control de silenciador no tiene sentido. El botón SQL y el deslizador de nivel de silenciador se atenúan cuando NT es el modo activo. Si el silenciador estaba activado cuando cambiaste a NT, se desactiva automáticamente y se restaura cuando sales de NT.

## Relacionado

- [Usar XIT para desplazar la frecuencia de transmisión sin cambiar RX](use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Sintonizar la radio a una frecuencia (escribir MHz en la lectura)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Elegir un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
