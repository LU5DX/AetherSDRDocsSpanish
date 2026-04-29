# Usar RIT para desplazar la frecuencia de recepción de una estación que deriva

RIT (Receive Incremental Tuning) desplaza la frecuencia de recepción una pequeña cantidad sin mover la frecuencia de transmisión ni el indicador del VFO. Úselo cuando una estación se aleje ligeramente de su frecuencia sintonizada y desee seguirla sin resintonizar todo el slice (canal de recepción).

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles RIT están inactivos sin una conexión de radio.
- Abra el applet RX Controls. Haga clic en el botón RX del panel lateral derecho si el applet no está visible.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) en la parte superior del applet, si hay más de un slice activo.

## Pasos

1. En el applet RX Controls, ubique la fila RIT cerca de la parte inferior del applet.
2. Haga clic en RIT para habilitar Receive Incremental Tuning. El botón se ilumina cuando está activo.
3. Use los botones `<` y `>` junto al spinbox de desplazamiento RIT, o desplace la rueda del ratón sobre el spinbox, para ajustar el desplazamiento. Cada paso mueve la frecuencia de recepción 10 Hz. El spinbox muestra el desplazamiento actual (predeterminado: `+0 Hz`).
4. Continúe ajustando hasta que la estación que deriva quede centrada en la banda de paso.
5. Para volver a desplazamiento cero sin deshabilitar RIT, haga clic en RIT 0. El desplazamiento se restablece a `+0 Hz`.
6. Para desactivar RIT por completo, haga clic en RIT nuevamente. La frecuencia de recepción vuelve a la frecuencia del VFO.

## Qué hace cada control

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| RIT | Botón de alternancia | Desactivado | Habilita o deshabilita Receive Incremental Tuning. |
| Desplazamiento RIT | Spinbox | `+0 Hz` | Muestra el desplazamiento RIT actual. Use `<` / `>` o la rueda del ratón para ajustar en pasos de 10 Hz. |
| RIT 0 | Botón de acción | — | Pone a cero el desplazamiento RIT sin deshabilitarlo. |

## Consejos

- RIT afecta únicamente la frecuencia de recepción. Su frecuencia de transmisión permanece en el VFO. Si también necesita desplazar la frecuencia de transmisión, use XIT en lugar de RIT o junto con él.
- El paso mínimo de 10 Hz es adecuado para trabajo en SSB y CW. Para una estación que deriva lentamente, unos pocos presses de `>` o un desplazamiento corto de la rueda del ratón suelen ser suficientes.
- Es una buena práctica hacer clic en RIT 0 antes de desactivar RIT. Así el desplazamiento ya estará en cero si lo reactiva más adelante.

## Relacionado

- [Usar XIT para desplazar la frecuencia de transmisión sin cambiar la recepción](use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
