# Comprensión de los slices y los VFOs

Un slice (canal de recepción independiente) es un canal de recepción —y opcionalmente de transmisión— dentro de un único panadapter. Comprender la relación entre los slices y los VFOs le ayudará a usar la capacidad multicanal de AetherSDR sin confusión.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Los controles de slice no están disponibles sin una conexión de radio.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón RX del panel lateral derecho para mostrarlo.

## Qué es un slice

La FLEX-8600 puede ejecutar hasta ocho canales de recepción simultáneos dentro de uno o más panadapters. Cada canal se denomina **slice** y se identifica con una letra: de la A a la H. Cada slice tiene su propia:

- Frecuencia de VFO (mostrada en la **Frequency label** del applet RX Controls)
- Modo de recepción (USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY)
- Banda de paso del filtro
- Configuración de AGC, ganancia de AF, squelch, RIT y XIT
- Asignación de antena RX y TX

La letra del slice aparece en el indicador **Slice badge** en la parte superior del applet RX Controls, con un color que corresponde a la identidad de ese slice.

## Qué es un VFO

En AetherSDR, el VFO es la frecuencia asignada a un slice. No existe un concepto separado de "VFO A / VFO B" distinto de los slices. Cada slice lleva su propio VFO. La frecuencia del Slice A es el VFO A; la frecuencia del Slice B es el VFO B, y así sucesivamente.

La frecuencia actual del VFO se muestra en la **Frequency label** (formato: `0.000.000`). Haga clic en la etiqueta para entrar en modo de edición, escriba una frecuencia en MHz y presione Enter para sintonizar el VFO de ese slice a la nueva frecuencia.

## Relación entre los slices y los panadapters

Cada panadapter muestra un segmento del espectro. Los slices aparecen como marcadores dentro del rango de frecuencias de ese panadapter. El indicador **Slice title** en la parte superior de cada panadapter (por ejemplo, `Slice A`) muestra qué slice está vinculado a esa vista.

En el modo de slice único, solo hay un slice activo y su panadapter ocupa la ventana principal. En el modo multislice, los slices adicionales pueden compartir el mismo panadapter u ocupar panadapters separados. Los botones ⬈ (pop-out), □ (maximize) y × (close) en la barra de título de cada panadapter solo están disponibles en configuraciones multipanel.

## Cambio entre slices

La fila **Slice tabs (A..H)** en la parte superior del applet RX Controls muestra una pestaña por cada slice activo. Haga clic en una pestaña para vincular el applet RX Controls a ese slice. La fila de pestañas se oculta cuando la radio opera con un solo slice.

Solo un slice a la vez es el slice de TX. Haga clic en el botón **TX (badge)** del applet RX Controls para el slice deseado y conviértalo en el canal de transmisión.

## Bloqueo del VFO de un slice

Para evitar que un slice sea resintonizado accidentalmente, haga clic en el botón 🔓 del applet RX Controls. El ícono cambia a 🔒 y el slice ignora los cambios de frecuencia hasta que haga clic nuevamente para desbloquearlo.

## Consejos

- RIT desplaza la frecuencia de recepción del slice activo sin mover su VFO. XIT desplaza la frecuencia de transmisión sin modificar la recepción. Ambos ajustes son independientes por slice.
- El control deslizante **L / R pan** (valor predeterminado 50, centro) permite ubicar el audio de cada slice en una posición diferente en el campo estéreo al monitorear varios slices simultáneamente. Haga doble clic en el control para restablecer el valor central.
- El tamaño de paso del slice depende del modo. Por ejemplo, los pasos en SSB son 1, 10, 50, 100, 500, 1000, 2000 y 3000 Hz; los pasos en CW son 1, 5, 10, 50, 100, 200 y 400 Hz. Recórralos con los botones **STEP** `<` y `>` o con la rueda del ratón.

## Temas relacionados

- [Cambiar entre múltiples slices usando la fila de pestañas A..H](../../features/rx/switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar la radio a una frecuencia (escribir MHz en el indicador)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Bloquear el slice para evitar resintonizaciones accidentales](../../features/rx/lock-the-slice-to-prevent-accidental-retuning.md)
- [Usar RIT para desplazar la frecuencia de recepción de una estación con deriva](../../features/rx/use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Usar XIT para desplazar la frecuencia de transmisión sin modificar la recepción](../../features/rx/use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Descripción general del panadapter](../../features/panadapter/overview.md)
- [Descripción general de RX Controls](../../features/rx/overview.md)
- [Hacer clic en el espectro para activar un panadapter (modo multislice)](../../features/panadapter/click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
