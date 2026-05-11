# Comprensión de Slices y VFOs

En AetherSDR, un slice es un receptor independiente dentro de un panadapter. Cada slice tiene su propia frecuencia de VFO, modo, filtro y configuración de audio. La FLEX-8600 admite hasta ocho slices simultáneos (etiquetados de la A a la H), lo que le permite monitorear múltiples frecuencias a la vez dentro del mismo panadapter o en diferentes panadapters.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Los slices solo existen cuando hay una conexión activa con la radio.
- El applet de Controles de RX debe estar visible. Si no lo está, haga clic en el botón de la bandeja **RX** en la barra lateral derecha.

## Cómo funcionan los slices

Cada slice es un canal de recepción completamente independiente. Dispone de:

- Una **frecuencia de VFO**: la frecuencia de sintonización central para ese slice, que se muestra en la **Etiqueta de frecuencia** en el applet de Controles de RX.
- Un **modo**: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL o RTTY, configurado con el **Combo de modo**.
- Un **pasabanda de filtro**: ajustable mediante ajustes predefinidos de ancho de filtro o arrastrando el **Widget de pasabanda de filtro**.
- Su propia configuración de **ganancia de AF**, **AGC**, **squelch**, **RIT** y **XIT**.
- Antenas de RX y TX asignadas.

Un slice siempre está vinculado a un panadapter. El panadapter muestra el espectro FFT para el segmento de banda del slice, y el marcador de VFO del slice aparece como una línea en ese espectro.

## Slices y el panadapter

La pantalla de **Espectro/Waterfall** del panadapter muestra la posición actual del VFO del slice. Al hacer clic o arrastrar en el espectro se sintoniza el slice activo. La barra de título del panadapter muestra qué slice está vinculado a él (por ejemplo, **Slice A**).

En modo multislice, cada panadapter puede contener uno o más marcadores de slice. Al hacer clic en el espectro de un panadapter diferente, se activa ese panadapter y su slice asociado.

## Cambio entre slices

El applet de Controles de RX muestra una fila de pestañas etiquetadas de la **A** a la **H** (hasta el número máximo de slices de la radio). Haga clic en una pestaña para vincular el applet de Controles de RX a ese slice. El indicador de **Distintivo de slice** en el applet se actualiza para mostrar la letra del slice activo, coloreada según la identidad del slice.

La fila de pestañas se oculta cuando solo se utiliza un slice.

## El slice de TX

Solo un slice transmite a la vez. El slice que está transmitiendo actualmente es el slice de TX. Para convertir un slice en el slice de TX, haga clic en su botón **TX (distintivo)** en el applet de Controles de RX. Esto enruta la transmisión a través de la frecuencia, el modo y la antena de TX de ese slice.

## RIT y XIT

RIT (Sintonización Incremental de Recepción) desplaza la frecuencia de recepción sin mover el VFO. Actívelo con el botón **RIT**; ajústelo con el cuadro de giro **Desplazamiento de RIT** (pasos de 10 Hz); restáurelo con **RIT 0**.

XIT (Sintonización Incremental de Transmisión) desplaza la frecuencia de transmisión sin cambiar la frecuencia de recepción. Actívelo con el botón **XIT**; ajústelo con el cuadro de giro **Desplazamiento de XIT** (pasos de 10 Hz); restáurelo con **XIT 0**.

Ambos son independientes por slice.

## Bloqueo de un slice

Para evitar una resintonización accidental, haga clic en el botón 🔓 en el applet de Controles de RX. El icono cambia a 🔒 y el slice ignora los cambios de frecuencia hasta que se desbloquee.

## Ganancia de AF y panorámico

Ajuste el control deslizante de **Ganancia de AF** (0–100) para configurar el volumen de salida de audio del slice. Use el control deslizante de **Panorámico L / R** (0–100) para posicionar el audio del slice en el campo estéreo: 0 es completamente a la izquierda, 50 es el centro, 100 es completamente a la derecha. Haga doble clic en el control deslizante de panorámico para restablecerlo al centro.

## Squelch

Active el squelch haciendo clic en el botón **SQL**, luego ajuste el control deslizante de **Nivel de squelch** (0–100) para configurar el umbral. El squelch solo tiene efecto cuando SQL está activado.

## AGC

Seleccione el modo AGC en el cuadro combinado **Modo AGC**: Off, Slow, Med o Fast. El control deslizante de **Umbral de AGC** ajusta el nivel de umbral de AGC. Cuando el modo AGC está en Off, el control deslizante configura el nivel de apagado. El cuadro combinado de modo se oculta en los modos de la familia FM (FM, NFM, DFM).

## Dúplex de repetidor FM

Cuando se opera en modo FM, NFM o DFM, aparecen los controles de dúplex FM:

- **Modo de tono (FM)**: seleccione "CTCSS TX" para habilitar la transmisión de tono CTCSS.
- **Valor de tono CTCSS**: seleccione la frecuencia de tono CTCSS entre los 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz). Solo está habilitado cuando el Modo de tono está configurado en CTCSS TX.
- **Desplazamiento (FM)**: configure la frecuencia de desplazamiento del repetidor (0.0–100.0 MHz en pasos de 0.1 MHz).
- **− (desplazamiento hacia abajo)**: haga clic para establecer la frecuencia de TX por debajo de RX.
- **Simplex**: haga clic para establecer la frecuencia de TX igual a RX (predeterminado).
- **+ (desplazamiento hacia arriba)**: haga clic para establecer la frecuencia de TX por encima de RX.
- **REV**: haga clic para invertir el signo del desplazamiento de TX para un par de repetidor invertido.

## Ajustes predefinidos de ancho de filtro

Haga clic en un botón de **Ajustes predefinidos de ancho de filtro** para aplicar un ancho de filtro predefinido. Haga clic con el botón derecho en un botón predefinido para guardar el ancho de filtro actual como un preajuste. Los ajustes predefinidos son específicos por modo y están ocultos para los modos FM/NFM/DFM.

El indicador de **Etiqueta de ancho de filtro** muestra el ancho de banda del filtro actual (por ejemplo, "2.7K", "3.3K", "500", "6.0K"). La lectura del ancho de filtro se comparte con el panel de VFO para una visualización coherente.

Use el **Widget de pasabanda de filtro** para arrastrar los bordes inferior y superior y ajustar el pasabanda del filtro manualmente.

## Ancho de filtro por pasos

Use los comandos **Ampliar** y **Reducir** para recorrer la lista de ajustes predefinidos de filtro por modo. Cada pulsación avanza al siguiente preajuste más ancho o más estrecho en la lista. El comando recorre la lista de preajustes por modo, por lo que siempre produce bordes de pasabanda correctos para el modo.

## Silencio

Haga clic en el botón 🔊 / 🔇 para silenciar o reactivar el audio del slice.

## Indicador QSK

El indicador **QSK** se ilumina en ámbar cuando la sintonización de inserción CW (QSK) está activa. Es de solo lectura y se controla mediante el botón de Inserción en el applet CW.

## Superposición de barrido SWR

La versión V0.9.4 añade una superposición de barrido SWR que dibuja los datos de SWR frente a la frecuencia directamente en el espectro del panadapter. Cuando un barrido está activo, cada punto de datos asigna su frecuencia (en MHz) a una posición horizontal en el espectro y traza el valor de SWR correspondiente como una línea de superposición. La superposición se dibuja tanto en las rutas de renderizado aceleradas por GPU como en las de software.

La superposición tiene tres estados:

| Estado            | Descripción                                                                                                                                                       | Notas |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------|
| Sin datos         | La superposición no se dibuja. Llame a `clearSwrSweepPoints()` para volver a este estado.                                                                         |       |
| Barrido en curso  | La superposición se dibuja y un cursor marca la frecuencia de barrido actual. Establezca `running = true` y proporcione `currentFreqMhz` al llamar a `setSwrSweepPoints()`. |       |
| Barrido completo  | La superposición se dibuja sin un marcador de cursor. Establezca `running = false` al llamar a `setSwrSweepPoints()`.                                                   |       |

Se puede pasar una etiqueta de origen opcional (por ejemplo, el nombre del sintonizador de antena o analizador que proporciona los datos) a través del parámetro `sourceLabel` y se muestra en la superposición.

Para actualizar la superposición, llame a `setSwrSweepPoints()` con un vector de valores `SwrSweepPoint`. Cada punto lleva:

- `freqMhz`: frecuencia de la medición, en MHz (predeterminado `0.0`).
- `swr`: valor de SWR en esa frecuencia (predeterminado `1.0`).

Los puntos con valores no finitos de `freqMhz` o `swr` se omiten silenciosamente. Los puntos cuya coordenada x asignada quede fuera del área visible del espectro no se dibujan.

Para eliminar la superposición, llame a `clearSwrSweepPoints()`.

## Consejos

- La **Etiqueta de frecuencia** muestra la frecuencia del VFO con agrupación de puntos (por ejemplo, `14.225.000`). Haga clic en ella para entrar en modo de edición y escriba una frecuencia en MHz, luego presione Enter para sintonizar y volver a centrar el panadapter.
- El cuadro de giro **STEP** controla cuánto se mueve el VFO por cada clic de la rueda de desplazamiento o por cada pulsación de los botones **<** / **>**. Los tamaños de paso son específicos por modo; por ejemplo, los pasos de SSB son 1, 10, 50, 100, 500, 1000, 2000 o 3000 Hz; los pasos de CW son 1, 5, 10, 50, 100, 200 o 400 Hz.
- El tamaño de paso predeterminado es 100 Hz (índice 2 en la lista por modo).
- Presionar Escape en el campo de edición de frecuencia cancela la entrada, restaura la frecuencia anterior y cierra el editor.
- Los controles deslizantes de **Ganancia de AF** y **Panorámico L / R** tienen un valor predeterminado de 70 y 50 (centro), respectivamente.
- El valor predeterminado de **Nivel de squelch** es 20.
- El valor predeterminado de **Umbral de AGC** es 65.

## Relacionado

- [Resumen de Controles de RX](../../features/rx/overview.md)
- [Cambie entre múltiples slices usando la fila de pestañas A..H](../../features/rx/switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonice la radio a una frecuencia (escriba MHz en la lectura)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Bloquee el slice para evitar una resintonización accidental](../../features/rx/lock-the-slice-to-prevent-accidental-retuning.md)
- [Use RIT para desplazar la frecuencia de recepción de una estación a la deriva](../../features/rx/use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Use XIT para desplazar la frecuencia de transmisión sin cambiar RX](../../features/rx/use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Haga clic en el espectro para activar un panadapter (modo multislice)](../../features/panadapter/click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Resumen del panadapter](../../features/panadapter/overview.md)
- [Realice su primer QSO con AetherSDR](../tutorials/first-qso.md)
<!-- docmesh:llm version=v0.9.8 date=2026-06-01 -->
