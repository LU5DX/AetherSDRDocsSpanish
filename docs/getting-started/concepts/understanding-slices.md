# Comprensión de los slices y los VFO

En AetherSDR, un slice (receptor independiente) es un receptor autónomo dentro de un panadapter. Cada slice tiene su propia frecuencia de VFO, modo, filtro y configuración de audio. El FLEX-8600 admite hasta ocho slices simultáneos (etiquetados de A a H), lo que permite monitorear múltiples frecuencias a la vez dentro del mismo panadapter o en panadapters diferentes.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. Los slices solo existen cuando hay una conexión de radio activa.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón de bandeja **RX** de la barra lateral derecha.

## Cómo funcionan los slices

Cada slice es un canal de recepción completamente independiente. Incluye:

- Una **frecuencia de VFO** — la frecuencia de sintonía central para ese slice, mostrada en la etiqueta **Frequency label** del applet RX Controls.
- Un **modo** — USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL o RTTY — configurado con el combo **Mode combo**.
- Una **banda de paso del filtro** — ajustable mediante preajustes de ancho de filtro o arrastrando el widget **Filter passband widget**.
- Sus propios ajustes de **AF gain**, **AGC**, **squelch**, **RIT** y **XIT**.
- Antenas RX y TX asignadas.

Un slice siempre está vinculado a un panadapter. El panadapter muestra el espectro FFT del segmento de banda del slice, y el marcador de VFO del slice aparece como una línea en ese espectro.

## Los slices y el panadapter

La pantalla **Spectrum / waterfall** del panadapter muestra la posición actual del VFO del slice. Hacer clic o arrastrar en el espectro sintoniza el slice activo. La barra de título del panadapter indica qué slice está vinculado a él (por ejemplo, **Slice A**).

En el modo multislice, cada panadapter puede contener uno o más marcadores de slice. Hacer clic en el espectro de un panadapter diferente activa ese panadapter y su slice asociado.

## Cambio entre slices

El applet RX Controls muestra una fila de pestañas etiquetadas de **A** a **H** (hasta el número máximo de slices del radio). Haga clic en una pestaña para vincular el applet RX Controls a ese slice. El indicador **Slice badge** del applet se actualiza para mostrar la letra del slice activo, con un color según la identidad del slice.

La fila de pestañas se oculta cuando solo hay un slice en uso.

## El slice TX

Solo un slice transmite a la vez. El slice que transmite en ese momento es el slice TX. Para convertir un slice en el slice TX, haga clic en su botón **TX (badge)** en el applet RX Controls. Esto enruta la transmisión a través de la frecuencia, el modo y la antena TX de ese slice.

## RIT y XIT

El RIT (Receive Incremental Tuning) desplaza la frecuencia de recepción sin mover el VFO. Actívelo con el botón **RIT**; ajústelo con el spinbox **RIT offset** (pasos de 10 Hz); restablézcalo con **RIT 0**.

El XIT (Transmit Incremental Tuning) desplaza la frecuencia de transmisión sin cambiar la frecuencia de recepción. Actívelo con el botón **XIT**; ajústelo con el spinbox **XIT offset** (pasos de 10 Hz); restablézcalo con **XIT 0**.

Ambos son independientes por slice.

## Bloqueo de un slice

Para evitar una resintonización accidental, haga clic en el botón 🔓 del applet RX Controls. El ícono cambia a 🔒 y el slice ignora los cambios de frecuencia hasta que se desbloquee.

## Consejos

- La etiqueta **Frequency label** muestra la frecuencia del VFO con agrupación por puntos (por ejemplo, `14.225.000`). Haga clic en ella para activar el modo de edición, escriba una frecuencia en MHz y presione Enter para sintonizar y recentrar el panadapter.
- El spinbox **STEP** controla cuánto se mueve el VFO por cada clic de la rueda de desplazamiento o por cada pulsación de los botones **<** / **>**. Los tamaños de paso son por modo — por ejemplo, los pasos en SSB son 1, 10, 50, 100, 500, 1000, 2000 o 3000 Hz; los pasos en CW son 1, 5, 10, 50, 100, 200 o 400 Hz.
- El tamaño de paso predeterminado es 100 Hz (índice 2 en la lista por modo).
- Presionar Escape en el campo de edición de frecuencia cancela la entrada, restaura la frecuencia anterior y cierra el editor.

## Temas relacionados

- [Descripción general de RX Controls](../../features/rx/overview.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](../../features/rx/switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en el indicador)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Bloquear el slice para evitar una resintonización accidental](../../features/rx/lock-the-slice-to-prevent-accidental-retuning.md)
- [Usar el RIT para compensar la frecuencia de recepción de una estación con deriva](../../features/rx/use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Usar el XIT para compensar la frecuencia de transmisión sin cambiar la recepción](../../features/rx/use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Hacer clic en el espectro para activar un panadapter (modo multislice)](../../features/panadapter/click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Descripción general del panadapter](../../features/panadapter/overview.md)
- [Realizar su primer QSO con AetherSDR](../tutorials/first-qso.md)
