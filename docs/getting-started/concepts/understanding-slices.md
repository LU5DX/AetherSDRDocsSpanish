# Comprensión de los slices y los VFOs

Un slice es un canal de recepción (y opcionalmente de transmisión) independiente dentro de un único panadapter. Cada slice tiene su propia frecuencia de VFO, modo, filtro y ruta de audio. Comprender cómo se relacionan los slices con los VFOs le ayuda a gestionar múltiples señales simultáneas en el FLEX-8600.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El applet RX Controls debe estar visible. Actívelo con el botón RX de la barra lateral derecha.

## Cómo funcionan los slices

El FLEX-8600 admite hasta ocho slices simultáneos, etiquetados de A a H. Cada slice es un receptor independiente con su propio:

- **Frecuencia de VFO** — mostrada en la etiqueta Frequency del applet RX Controls.
- **Modo** — configurado con el selector Mode (USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY).
- **Banda de paso del filtro** — mostrada en el indicador de ancho de filtro (por ejemplo, `2.7K`) y ajustable mediante el widget Filter passband o los preajustes Filter width.
- **Ruta de audio** — controles independientes de ganancia AF, panorama L/R y squelch.
- **CAG** — modo de CAG y umbral de CAG independientes por slice.

Los slices dentro de un panadapter comparten el mismo rango de FFT, por lo que todos los slices visibles sintonizarán la misma porción del espectro. Es posible ver todos los marcadores de slice activos simultáneamente en la pantalla Spectrum / waterfall.

## El slice de TX

Solo un slice transmite a la vez. Ese slice es el slice de TX. El botón TX (badge) del applet RX Controls designa el slice actual como slice de TX. La etiqueta Frequency del slice de TX determina la frecuencia de transmisión.

## Selección y cambio de slices

El applet RX Controls muestra una fila de pestañas de slice etiquetadas de A a H (la fila se oculta cuando solo hay un slice activo). Haga clic en una pestaña para vincular el applet a ese slice. El badge Slice se actualiza para reflejar la letra del slice actualmente vinculado.

En el panadapter, cada slice aparece como un marcador independiente en el Spectrum / waterfall. Al hacer clic en el espectro se activa el panadapter; en modo multislice, hacer clic cerca de un marcador de slice sintoniza o selecciona ese slice.

## RIT y XIT

El RIT (Sintonización Incremental de Recepción) desplaza la frecuencia de recepción sin mover el VFO. Actívelo con el botón de alternancia RIT y ajuste el desplazamiento mediante el spinbox RIT offset (pasos de 10 Hz). Haga clic en RIT 0 para poner el desplazamiento a cero.

El XIT (Sintonización Incremental de Transmisión) desplaza la frecuencia de transmisión sin modificar la frecuencia de recepción. Actívelo con el botón de alternancia XIT y ajústelo con el spinbox XIT offset (pasos de 10 Hz). Haga clic en XIT 0 para poner el desplazamiento a cero.

Tanto el RIT como el XIT tienen el valor predeterminado de `+0 Hz`.

## Bloqueo de un slice

El alternador 🔓 / 🔒 del applet RX Controls bloquea la frecuencia del slice. Un slice bloqueado ignora los cambios de frecuencia producidos al hacer clic en el panadapter o mediante comandos CAT externos. El icono alterna entre candado abierto y cerrado para indicar el estado actual.

## Consejos

- La etiqueta Frequency muestra la frecuencia del VFO con separación por puntos. Haga clic en ella para activar el modo de edición, escriba una frecuencia en MHz y presione Enter para sintonizar y recentrar el panadapter. Presione Escape para cancelar y restaurar la frecuencia anterior.
- Si tiene el RIT activo y la estación suena en frecuencia pero aparece descentrada, ponga el RIT a cero con RIT 0 y vuelva a sintonizar.
- Haga doble clic en el deslizador de panorama L / R para restablecerlo al centro (50).

## Relacionados

- [Cambiar entre múltiples slices usando la fila de pestañas A..H](../../features/rx/switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar la radio a una frecuencia (escribir MHz en el indicador)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](../../features/rx/change-mode-usb-lsb-cw-am-fm-etc.md)
- [Bloquear el slice para evitar una resintonización accidental](../../features/rx/lock-the-slice-to-prevent-accidental-retuning.md)
- [Usar el RIT para desplazar la frecuencia de recepción ante una estación con deriva](../../features/rx/use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Usar el XIT para desplazar la frecuencia de transmisión sin modificar la recepción](../../features/rx/use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Hacer clic en el espectro para activar un panadapter (modo multislice)](../../features/panadapter/click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Descripción general de RX Controls](../../features/rx/overview.md)
