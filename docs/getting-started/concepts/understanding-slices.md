# Comprensión de los slices y los VFOs

Un slice es un canal de recepción (y opcionalmente de transmisión) independiente dentro de un panadapter. Comprender la relación entre los slices y los VFOs es la base para usar AetherSDR de manera efectiva: cada operación de sintonía, modo y filtro actúa sobre un slice específico.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón RX tray en la barra lateral derecha.

## Qué es un slice

El FLEX-8600 puede ejecutar hasta ocho slices de recepción simultáneos, etiquetados de A hasta H. Cada slice es un canal de radio independiente con su propio:

- Frecuencia de VFO
- Modo (USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY)
- Banda de paso del filtro
- Asignación de antena RX y TX
- Configuraciones de AGC, ganancia AF, squelch, RIT y XIT

Cada slice ocupa un segmento del espectro cubierto por su panadapter. En el Panadapter, el indicador de título Slice muestra qué slice está asociado a esa vista; por ejemplo, "Slice A".

## Qué es el VFO

El VFO es la frecuencia sintonizada de un slice. En el applet RX Controls, la etiqueta Frequency muestra la frecuencia actual del VFO con separación por puntos (por ejemplo, `14.225.000`). Al hacer clic en la etiqueta Frequency, esta cambia al campo de edición Frequency edit field, donde puede escribir una frecuencia en MHz y presionar Enter para resintonizar.

Existe un VFO por slice. Los slices son independientes: sintonizar el Slice A no afecta al Slice B.

## Los slices y el applet RX Controls

El applet RX Controls está vinculado a un slice a la vez. El indicador Slice badge (A, B, C, D, E, F, G, H) en el encabezado del applet muestra qué slice afectan actualmente los controles. Cuando hay más de un slice activo, aparece una fila de pestañas Slice tabs (A..H) en la parte superior del applet. Haga clic en una pestaña para vincular el applet a ese slice.

Todos los controles del applet — modo, frecuencia, ancho de filtro, AGC, ganancia AF, squelch, RIT, XIT — operan sobre el slice que se muestra en ese momento en el Slice badge.

## El slice TX

Solo un slice transmite a la vez. El indicador TX badge en el applet RX Controls señala cuál es el slice TX. Haga clic en TX en cualquier slice para convertirlo en el slice de transmisión.

## Bloqueo de sintonía

Para evitar la resintonización accidental de un slice, haga clic en el botón 🔓 del applet RX Controls. El ícono cambia a 🔒 y el slice ignora los cambios de frecuencia hasta que lo desbloquee.

## Slices y panadapters

Cada panadapter muestra el espectro y el waterfall de su slice asociado. En una disposición de múltiples slices, cada panadapter tiene su propia barra de título que indica "Slice A", "Slice B", y así sucesivamente. Al hacer clic en el espectro o el waterfall de un panadapter, se activa el slice de ese panadapter.

## RIT y XIT

El RIT (Receive Incremental Tuning) desplaza la frecuencia de recepción del slice activo sin cambiar el VFO mostrado. El XIT (Transmit Incremental Tuning) desplaza la frecuencia de transmisión sin cambiar la frecuencia RX. Ambos son independientes por slice y ajustables en pasos de 10 Hz mediante los cuadros de giro RIT offset y XIT offset.

## Consejos

- La fila de pestañas Slice tabs se oculta cuando solo hay un slice activo, ya que no hay nada entre qué cambiar.
- Hacer doble clic en el control deslizante L / R pan lo restablece a 50 (centro).
- El cuadro de giro STEP recorre los tamaños de paso por modo. Para SSB los pasos son 1, 10, 50, 100, 500, 1000, 2000 y 3000 Hz. Para CW los pasos son 1, 5, 10, 50, 100, 200 y 400 Hz. El paso predeterminado es 100 Hz.

## Relacionados

- [Cambiar entre múltiples slices usando la fila de pestañas A..H](../../features/rx/switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar la radio a una frecuencia (escribir MHz en el indicador)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](../../features/rx/change-mode-usb-lsb-cw-am-fm-etc.md)
- [Bloquear el slice para evitar una resintonización accidental](../../features/rx/lock-the-slice-to-prevent-accidental-retuning.md)
- [Usar RIT para desplazar la frecuencia de recepción de una estación con deriva](../../features/rx/use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Usar XIT para desplazar la frecuencia de transmisión sin cambiar RX](../../features/rx/use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Hacer clic en el espectro para activar un panadapter (modo multi-slice)](../../features/panadapter/click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Realizar su primer QSO con AetherSDR](../tutorials/first-qso.md)
