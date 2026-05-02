# Entendiendo los slices y los VFO

En AetherSDR, un slice (receptor independiente) es un canal de recepción autónomo dentro de un panadapter. Cada slice tiene su propia frecuencia de VFO, modo, filtro y ajustes de audio. El FLEX-8600 admite hasta ocho slices simultáneos (etiquetados de A a H), lo que permite monitorear múltiples frecuencias a la vez dentro de uno o varios panadapters.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. Los slices solo existen cuando hay una conexión de radio activa.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón **RX** de la bandeja en la barra lateral derecha.

## Cómo funcionan los slices

Cada slice es un canal de recepción completamente independiente. Incluye:

- Una **frecuencia de VFO** — la frecuencia central de sintonía de ese slice, mostrada en la **Frequency label** del applet RX Controls.
- Un **modo** — USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL o RTTY — configurado con el **Mode combo**.
- Una **banda de paso del filtro** — ajustable mediante preajustes de ancho de filtro o arrastrando el **Filter passband widget**.
- Sus propios ajustes de **AF gain**, **AGC**, **squelch**, **RIT** y **XIT**.
- Antenas de RX y TX asignadas.

Un slice siempre está vinculado a un panadapter. El panadapter muestra el espectro FFT del segmento de banda del slice, y el marcador de VFO del slice aparece como una línea sobre ese espectro.

## Slices y el panadapter

La pantalla **Spectrum / waterfall** del panadapter muestra la posición actual del VFO del slice. Al hacer clic o arrastrar sobre el espectro, se sintoniza el slice activo. La barra de título del panadapter indica qué slice está vinculado a él (por ejemplo, **Slice A**).

En el modo multislice, cada panadapter puede contener uno o más marcadores de slice. Al hacer clic en el espectro de un panadapter diferente, se activa ese panadapter y su slice asociado.

## Cambiar entre slices

El applet RX Controls muestra una fila de pestañas etiquetadas de **A** a **H** (hasta el número máximo de slices del radio). Haga clic en una pestaña para vincular el applet RX Controls a ese slice. El indicador **Slice badge** del applet se actualiza para mostrar la letra del slice activo, coloreada según la identidad del slice.

La fila de pestañas se oculta cuando solo hay un slice en uso.

## El slice TX

Solo un slice transmite a la vez. El slice que transmite en ese momento es el slice TX. Para convertir un slice en el slice TX, haga clic en su botón **TX (badge)** en el applet RX Controls. Esto enruta la transmisión a través de la frecuencia, el modo y la antena TX de ese slice.

## RIT y XIT

El RIT (Receive Incremental Tuning) desplaza la frecuencia de recepción sin mover el VFO. Actívelo con el botón **RIT**; ajústelo con el spinbox **RIT offset** (pasos de 10 Hz); restablézcalo con **RIT 0**.

El XIT (Transmit Incremental Tuning) desplaza la frecuencia de transmisión sin cambiar la frecuencia de recepción. Actívelo con el botón **XIT**; ajústelo con el spinbox **XIT offset** (pasos de 10 Hz); restablézcalo con **XIT 0**.

Ambos son independientes por slice.

## Bloquear un slice

Para evitar una resintonización accidental, haga clic en el botón 🔓 del applet RX Controls. El icono cambia a 🔒 y el slice ignora los cambios de frecuencia hasta que se desbloquee.

## Superposición de barrido de ROE

La versión V0.9.4 agrega una superposición de barrido de ROE (Relación de Onda Estacionaria) que dibuja los datos de ROE en función de la frecuencia directamente sobre el espectro del panadapter. Cuando hay un barrido activo, cada punto de datos asigna su frecuencia (en MHz) a una posición horizontal en el espectro y representa el valor de ROE correspondiente como una línea superpuesta. La superposición se dibuja tanto en la ruta de renderizado acelerado por GPU como en la ruta de renderizado por software.

La superposición tiene tres estados:

| Estado               | Descripción                                                                                                                                                                      | Notas |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------|
| Sin datos            | La superposición no se dibuja. Llame a `clearSwrSweepPoints()` para volver a este estado.                                                                                        |       |
| Barrido en curso     | La superposición se dibuja y un cursor marca la frecuencia actual del barrido. Establezca `running = true` e indique `currentFreqMhz` al llamar a `setSwrSweepPoints()`.         |       |
| Barrido completado   | La superposición se dibuja sin marcador de cursor. Establezca `running = false` al llamar a `setSwrSweepPoints()`.                                                               |       |

Se puede pasar una etiqueta de fuente opcional (por ejemplo, el nombre del sintonizador de antena o el analizador que proporciona los datos) mediante el parámetro `sourceLabel`, la cual se muestra sobre la superposición.

Para actualizar la superposición, llame a `setSwrSweepPoints()` con un vector de valores `SwrSweepPoint`. Cada punto contiene:

- `freqMhz` — frecuencia de la medición, en MHz (valor predeterminado: `0.0`).
- `swr` — valor de ROE en esa frecuencia (valor predeterminado: `1.0`).

Los puntos con valores `freqMhz` o `swr` no finitos se omiten silenciosamente. Los puntos cuya coordenada x asignada queda fuera del área de espectro visible no se dibujan.

Para eliminar la superposición, llame a `clearSwrSweepPoints()`.

## Consejos

- La **Frequency label** muestra la frecuencia del VFO con agrupación por puntos (por ejemplo, `14.225.000`). Haga clic en ella para entrar en modo de edición, escriba una frecuencia en MHz y presione Enter para sintonizar y recentrar el panadapter.
- El spinbox **STEP** controla cuánto se mueve el VFO por cada clic de la rueda de desplazamiento o por cada pulsación de los botones **<** / **>**. Los tamaños de paso son por modo — por ejemplo, los pasos en SSB son 1, 10, 50, 100, 500, 1000, 2000 o 3000 Hz; los pasos en CW son 1, 5, 10, 50, 100, 200 o 400 Hz.
- El tamaño de paso predeterminado es 100 Hz (índice 2 en la lista por modo).
- Al presionar Escape en el campo de edición de frecuencia, se cancela la entrada, se restaura la frecuencia anterior y se cierra el editor.

## Relacionados

- [Descripción general de RX Controls](../../features/rx/overview.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](../../features/rx/switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en el indicador)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Bloquear el slice para evitar una resintonización accidental](../../features/rx/lock-the-slice-to-prevent-accidental-retuning.md)
- [Usar RIT para desplazar la frecuencia de recepción de una estación con deriva](../../features/rx/use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Usar XIT para desplazar la frecuencia de transmisión sin cambiar el RX](../../features/rx/use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Hacer clic en el espectro para activar un panadapter (modo multislice)](../../features/panadapter/click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Descripción general del panadapter](../../features/panadapter/overview.md)
- [Realizar su primer QSO con AetherSDR](../tutorials/first-qso.md)
<!-- docmesh:llm version=v0.9.4 date=2026-05-01 -->
