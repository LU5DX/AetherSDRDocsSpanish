# Comprensión de Slices y VFOs

En AetherSDR, un slice es un receptor independiente dentro de un panadapter. Cada slice tiene su propia frecuencia VFO, modo, filtro y configuración de audio. El FLEX-8600 soporta hasta ocho slices simultáneos (etiquetados A a H), lo que le permite monitorear múltiples frecuencias a la vez dentro del mismo o de diferentes panadapters.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. Los slices solo existen cuando hay una conexión de radio activa.
- El applet de Controles RX debe estar visible. Si no lo está, haga clic en el botón de la bandeja **RX** en la barra lateral derecha.

## Cómo funcionan los slices

Cada slice es un canal de recepción completamente independiente. Tiene:

- Una **frecuencia VFO**: la frecuencia de sintonización central para ese slice, que se muestra en la **Etiqueta de frecuencia** en el applet de Controles RX.
- Un **modo**: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL o RTTY, configurado con el **Combo de modo**.
- Un **pasabanda de filtro**: ajustable mediante preajustes de ancho de filtro o arrastrando el **Widget de pasabanda de filtro**.
- Su propia **ganancia AF**, **AGC**, **squelch**, **RIT** y **XIT**.
- Antenas RX y TX asignadas.

Un slice siempre está vinculado a un panadapter. El panadapter muestra el espectro FFT para el segmento de banda del slice, y el marcador VFO del slice aparece como una línea en ese espectro.

## Slices y el panadapter

La visualización de **Espectro / Waterfall** del panadapter muestra la posición VFO actual del slice. Al hacer clic o arrastrar en el espectro se sintoniza el slice activo. La barra de título del panadapter muestra qué slice está vinculado a él (por ejemplo, **Slice A**).

En modo multislice, cada panadapter puede contener uno o más marcadores de slice. Al hacer clic en el espectro de un panadapter diferente se activa ese panadapter y su slice asociado.

## Cambio entre slices

El applet de Controles RX muestra una fila de pestañas etiquetadas como **A** a **H** (hasta el número máximo de slices del radio). Haga clic en una pestaña para vincular el applet de Controles RX a ese slice. El indicador de **Insignia de slice** en el applet se actualiza para mostrar la letra del slice activo, coloreada por identidad de slice.

La fila de pestañas está oculta cuando solo se usa un slice.

## El slice TX

Solo un slice transmite a la vez. El slice que transmite actualmente es el slice TX. Para convertir un slice en el slice TX, haga clic en su botón **TX (insignia)** en el applet de Controles RX. Esto enruta la transmisión a través de la frecuencia, modo y antena TX de ese slice.

## RIT y XIT

RIT (Sintonización Incremental de Recepción) desplaza la frecuencia de recepción sin mover el VFO. Actívelo con el botón **RIT**; ajústelo con el cuadro giratorio **Desplazamiento RIT** (pasos de 10 Hz); restablézcalo con **RIT 0**.

XIT (Sintonización Incremental de Transmisión) desplaza la frecuencia de transmisión sin cambiar la frecuencia de recepción. Actívelo con el botón **XIT**; ajústelo con el cuadro giratorio **Desplazamiento XIT** (pasos de 10 Hz); restablézcalo con **XIT 0**.

Ambos son independientes por slice.

## Bloqueo de un slice

Para evitar resintonizaciones accidentales, haga clic en el botón 🔓 en el applet de Controles RX. El icono cambia a 🔒 y el slice ignora los cambios de frecuencia hasta que se desbloquee.

## Ganancia AF y paneo

Ajuste el control deslizante de **Ganancia AF** (0–100) para establecer el volumen de salida de audio del slice. Use el control deslizante **Paneo L / R** (0–100) para posicionar el audio del slice en el campo estéreo: 0 es completamente a la izquierda, 50 es centro, 100 es completamente a la derecha. Haga doble clic en el control deslizante de paneo para restablecerlo al centro.

## Squelch

Active el squelch haciendo clic en el botón **SQL**, luego ajuste el control deslizante **Nivel de squelch** (0–100) para establecer el umbral. El squelch solo tiene efecto cuando SQL está activado.

## AGC

Seleccione el modo AGC del cuadro combinado **Modo AGC**: Off, Slow, Med o Fast. El control deslizante **Umbral AGC** ajusta el nivel de umbral del AGC. Cuando el modo AGC está en Off, el control deslizante establece el nivel de apagado en su lugar. El combo de modo está oculto en modos de la familia FM (FM, NFM, DFM).

## Dúplex de repetidor FM

Cuando opera en modo FM, NFM o DFM, aparecen los controles de dúplex FM:

- **Modo de tono (FM)**: seleccione "CTCSS TX" para habilitar la transmisión de tono CTCSS.
- **Valor de tono CTCSS**: seleccione la frecuencia de tono CTCSS entre 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz). Solo se habilita cuando el Modo de tono está configurado en CTCSS TX.
- **Desplazamiento (FM)**: establezca la frecuencia de desplazamiento del repetidor (0.0–100.0 MHz en pasos de 0.1 MHz).
- **− (desplazamiento hacia abajo)**: haga clic para establecer la frecuencia TX por debajo de la RX.
- **Simplex**: haga clic para establecer la frecuencia TX igual a la RX (predeterminado).
- **+ (desplazamiento hacia arriba)**: haga clic para establecer la frecuencia TX por encima de la RX.
- **REV**: haga clic para invertir el signo del desplazamiento TX para un par de repetidores invertido.

## Preajustes de ancho de filtro

Haga clic en un botón de **Preajustes de ancho de filtro** para aplicar un ancho de filtro preestablecido. Haga clic derecho en un botón de preajuste para guardar el ancho de filtro actual como un preajuste. Los preajustes son por modo y están ocultos para modos FM/NFM/DFM.

El indicador de **Etiqueta de ancho de filtro** muestra el ancho de banda del filtro actual (por ejemplo, "2.7K", "3.3K", "500", "6.0K"). La lectura del ancho de filtro se comparte con el panel VFO para una visualización coherente.

Use el **Widget de pasabanda de filtro** para arrastrar los bordes bajo y alto y ajustar el pasabanda del filtro manualmente.

## Ancho de filtro por pasos

Use los comandos **Ampliar** y **Reducir** para recorrer la lista de preajustes de filtro por modo. Cada pulsación avanza al siguiente preajuste más ancho o más estrecho en la lista. El comando recorre la lista de preajustes por modo, por lo que siempre produce bordes de pasabanda correctos para el modo.

## Silencio

Haga clic en el botón 🔊 / 🔇 para silenciar o reactivar la salida de audio del slice.

## Indicador QSK

El indicador **QSK** se ilumina en ámbar cuando el break-in CW (QSK) está activo. Es de solo lectura y se controla mediante el botón Breakin del applet CW.

## Superposición de barrido SWR

La versión V0.9.4 añade una superposición de barrido SWR que dibuja datos de SWR frente a frecuencia directamente en el espectro del panadapter. Cuando un barrido está activo, cada punto de datos asigna su frecuencia (en MHz) a una posición horizontal en el espectro y traza el valor SWR correspondiente como una superposición de línea. La superposición se dibuja tanto en las rutas de pintado aceleradas por GPU como en las renderizadas por software.

La superposición tiene tres estados:

| Estado | Descripción | Notas |
|---|---|---|
| Sin datos | No se dibuja la superposición. Llame a `clearSwrSweepPoints()` para volver a este estado. | |
| Barrido en curso | Se dibuja la superposición y un cursor marca la frecuencia de barrido actual. Establezca `running = true` y proporcione `currentFreqMhz` al llamar a `setSwrSweepPoints()`. | |
| Barrido completo | Se dibuja la superposición sin un marcador de cursor. Establezca `running = false` al llamar a `setSwrSweepPoints()`. | |

Se puede pasar una etiqueta de origen opcional (por ejemplo, el nombre del acoplador de antena o analizador que proporciona los datos) a través del parámetro `sourceLabel` y se muestra en la superposición.

Para actualizar la superposición, llame a `setSwrSweepPoints()` con un vector de valores `SwrSweepPoint`. Cada punto lleva:

- `freqMhz`: frecuencia de la medición, en MHz (predeterminado `0.0`).
- `swr`: valor SWR en esa frecuencia (predeterminado `1.0`).

Los puntos con valores no finitos de `freqMhz` o `swr` se omiten silenciosamente. Los puntos cuya coordenada x mapeada cae fuera del área de espectro visible no se dibujan.

Para eliminar la superposición, llame a `clearSwrSweepPoints()`.

## Consejos

- La **Etiqueta de frecuencia** muestra la frecuencia VFO con agrupación por puntos (por ejemplo, `14.225.000`). Haga clic en ella para entrar en modo de edición y escribir una frecuencia en MHz, luego presione Enter para sintonizar y recentrar el panadapter.
- El cuadro giratorio **PASO** controla cuánto se mueve el VFO por cada clic de rueda de desplazamiento o por cada pulsación de los botones **<** / **>**. Los tamaños de paso son por modo; por ejemplo, los pasos SSB son 1, 10, 50, 100, 500, 1000, 2000 o 3000 Hz; los pasos CW son 1, 5, 10, 50, 100, 200 o 400 Hz.
- El tamaño de paso predeterminado es 100 Hz (índice 2 en la lista por modo).
- Presionar Escape en el campo de edición de frecuencia cancela la entrada, restaura la frecuencia anterior y cierra el editor.
- Los controles deslizantes de **Ganancia AF** y **Paneo L / R** tienen un valor predeterminado de 70 y 50 (centro) respectivamente.
- El valor predeterminado del **Nivel de squelch** es 20.
- El valor predeterminado del **Umbral AGC** es 65.

## Relacionados

- [Visión general de Controles RX](../../features/rx/overview.md)
- [Cambie entre múltiples slices usando la fila de pestañas A..H](../../features/rx/switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonice el radio a una frecuencia (escriba MHz en la lectura)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Bloquee el slice para evitar resintonizaciones accidentales](../../features/rx/lock-the-slice-to-prevent-accidental-retuning.md)
- [Use RIT para desplazar la frecuencia de recepción para una estación a la deriva](../../features/rx/use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Use XIT para desplazar la frecuencia de transmisión sin cambiar RX](../../features/rx/use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Haga clic en el espectro para activar un panadapter (modo multislice)](../../features/panadapter/click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Visión general del panadapter](../../features/panadapter/overview.md)
- [Haga su primer QSO con AetherSDR](../tutorials/first-qso.md)
<!-- docmesh:llm version=v0.9.8 date=2026-06-01 -->
