# Comprensión de Slices y VFOs

En AetherSDR, un slice es un receptor independiente dentro de un panadapter. Cada slice tiene su propia frecuencia de VFO, modo, filtro y configuración de audio. El FLEX-8600 admite hasta ocho slices simultáneos (etiquetados de la A a la H), lo que le permite monitorear múltiples frecuencias a la vez dentro del mismo panadapter o de diferentes.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Los slices solo existen cuando hay una conexión de radio activa.
- El applet **RX Controls** debe estar visible. Si no lo está, haga clic en el botón de bandeja **RX** en la barra lateral derecha.

## Cómo funcionan los slices

Cada slice es un canal de recepción completamente independiente. Tiene:

- Una **frecuencia de VFO** — la frecuencia de sintonización central para ese slice, mostrada en la **Frequency label** en el applet **RX Controls**.
- Un **modo** — USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL o RTTY — configurado con el **Mode combo**.
- Una **banda de paso del filtro** — ajustable mediante ajustes preestablecidos de ancho de filtro o arrastrando el **Filter passband widget**.
- Su propia **ganancia de AF**, **AGC**, **squelch**, **RIT** y **XIT**.
- Antenas de RX y TX asignadas.

Un slice siempre está vinculado a un panadapter. El panadapter muestra el espectro FFT para el segmento de banda del slice, y el marcador de VFO del slice aparece como una línea en ese espectro.

## Slices y el panadapter

La pantalla **Spectrum / waterfall** del panadapter muestra la posición actual del VFO del slice. Al hacer clic o arrastrar en el espectro se sintoniza el slice activo. La barra de título del panadapter muestra qué slice está vinculado a él (por ejemplo, **Slice A**).

En el modo de múltiples slices, cada panadapter puede contener uno o más marcadores de slice. Al hacer clic en el espectro de un panadapter diferente, se activa ese panadapter y su slice asociado.

## Cambio entre slices

El applet **RX Controls** muestra una fila de pestañas etiquetadas de la **A** a la **H** (hasta el número máximo de slices de la radio). Haga clic en una pestaña para vincular el applet **RX Controls** a ese slice. El indicador **Slice badge** en el applet se actualiza para mostrar la letra del slice activo, coloreada según la identidad del slice. La insignia admite representación de texto enriquecido para la letra del slice.

La fila de pestañas está oculta cuando solo se usa un slice. Cuando la radio se desconecta, `clearSliceButtons()` elimina todos los botones de las pestañas y restaura la insignia de slice estática.

## El slice de TX

Solo un slice transmite a la vez. El slice que transmite actualmente es el slice de TX. Para convertir un slice en el slice de TX, haga clic en su botón **TX (badge)** en el applet **RX Controls**. Esto enruta la transmisión a través de la frecuencia, el modo y la antena de TX de ese slice.

## RIT y XIT

RIT (Receive Incremental Tuning) desplaza la frecuencia de recepción sin mover el VFO. Actívelo con el botón **RIT**; ajústelo con el spinbox **RIT offset** (pasos de 10 Hz); reinícielo con **RIT 0**.

XIT (Transmit Incremental Tuning) desplaza la frecuencia de transmisión sin cambiar la frecuencia de recepción. Actívelo con el botón **XIT**; ajústelo con el spinbox **XIT offset** (pasos de 10 Hz); reinícielo con **XIT 0**.

Ambos son independientes por slice.

## Bloqueo de un slice

Para evitar una resintonización accidental, haga clic en el botón 🔓 en el applet **RX Controls**. El ícono cambia a 🔒 y el slice ignora los cambios de frecuencia hasta que se desbloquee.

## Ganancia de AF y panorámico

Ajuste el control deslizante de **AF gain** (0–100) para configurar el volumen de salida de audio del slice. Use el control deslizante de **L / R pan** (0–100) para posicionar el audio del slice en el campo estéreo: 0 es completamente a la izquierda, 50 es al centro, 100 es completamente a la derecha. Haga doble clic en el control deslizante de panorámico para reiniciarlo al centro.

## Squelch

Active el squelch haciendo clic en el botón **SQL**, luego ajuste el control deslizante de **Squelch level** (0–100) para configurar el umbral. El squelch solo surte efecto cuando SQL está activado.

El squelch se desactiva automáticamente en modos RTTY y digitales (DIGU, DIGL) donde el squelch eliminaría los caracteres FSK e interrumpiría la decodificación.

El umbral de squelch manual se conserva del lado del cliente entre sesiones. Cuando el modo de squelch automático está activo, la radio puede sobrescribir el nivel de squelch del slice con valores sugeridos por el algoritmo, por lo que AetherSDR recuerda su última preferencia manual y la restaura.

## AGC

Seleccione el modo AGC del cuadro combinado **AGC mode**: Off, Slow, Med o Fast. El control deslizante de **AGC threshold** ajusta el nivel del umbral AGC. Cuando el modo AGC es Off, el control deslizante establece el nivel de apagado. El cuadro combinado de modo está oculto en los modos de la familia FM (FM, NFM, DFM).

## Dúplex de repetidor FM

Cuando opera en modo FM, NFM o DFM, aparecen los controles de dúplex FM:

- **Tone mode (FM)** — Seleccione "CTCSS TX" para habilitar la transmisión de tono CTCSS.
- **CTCSS tone value** — Seleccione la frecuencia del tono CTCSS entre 41 tonos estándar EIA/TIA-603 (67,0 Hz a 254,1 Hz). Solo está habilitado cuando el modo de tono está configurado en CTCSS TX.
- **Offset (FM)** — Establezca la frecuencia de desplazamiento del repetidor (0,0–100,0 MHz en pasos de 0,1 MHz).
- **− (offset down)** — Haga clic para establecer la frecuencia de TX por debajo de RX.
- **Simplex** — Haga clic para establecer la frecuencia de TX igual a RX (predeterminado).
- **+ (offset up)** — Haga clic para establecer la frecuencia de TX por encima de RX.
- **REV** — Haga clic para invertir el signo del desplazamiento de TX para un par de repetidor invertido.

## Selección de antena

### Antena RX

Haga clic en el botón **ANT1 (RX antenna)** para abrir un menú que enumera las antenas de recepción disponibles. Seleccionar una antena llama a `setRxAntenna()` en el slice. El menú se completa desde `rxAntennaList()` del slice cuando está disponible; de lo contrario, desde la lista de antenas del panadapter. Cada elemento del menú lleva el token de la antena como su valor de datos y muestra una etiqueta de visualización con información sobre herramientas y estado.

### Antena TX

Haga clic en el botón **ANT1 (TX antenna)** para abrir un menú que enumera las antenas con capacidad de TX. Los puertos de antena solo de RX (prefijo "RX") se filtran. Seleccionar una antena llama a `setTxAntenna()` en el slice. Cada elemento del menú lleva el token de la antena como su valor de datos y muestra una etiqueta de visualización con información sobre herramientas y estado.

## Ajustes preestablecidos de ancho de filtro

Haga clic en un botón de **Filter width presets** para aplicar un ancho de filtro preestablecido. Haga clic con el botón derecho en un botón preestablecido para guardar el ancho de filtro actual como preestablecido. Los ajustes preestablecidos son por modo y están ocultos para los modos FM/NFM/DFM.

El indicador **Filter width label** muestra el ancho de banda del filtro actual (por ejemplo, "2.7K", "3.3K", "500", "6.0K"). La lectura del ancho del filtro se comparte con el panel VFO para una visualización coherente, utilizando una lógica que reconoce el modo para que los modos SSB/digitales muestren el ancho etiquetado correcto.

Use el **Filter passband widget** para arrastrar los bordes inferior y superior y ajustar la banda de paso del filtro manualmente.

## Ancho de filtro por pasos

Use los comandos **Widen** y **Narrow** para recorrer la lista de ajustes preestablecidos de filtro por modo. Cada pulsación avanza al ajuste preestablecido más ancho o más angosto siguiente en la lista. El comando recorre la lista de ajustes preestablecidos por modo, por lo que siempre produce bordes de banda de paso correctos para el modo.

## Silencio

Haga clic en el botón 🔊 / 🔇 para silenciar o reactivar la salida de audio del slice. Según la Radio-Authoritative Settings Policy, el estado de silencio NO se guarda ni se restaura al reconectar: la radio es la fuente de verdad para el silencio de audio.

## Indicador QSK

El indicador **QSK** se ilumina en ámbar cuando el break-in (QSK) de CW está activo. Es de solo lectura y se controla a través del botón **Breakin** en el applet de CW.

## Superposición de barrido SWR

La versión V0.9.4 agrega una superposición de barrido SWR que dibuja datos de SWR versus frecuencia directamente en el espectro del panadapter. Cuando un barrido está activo, cada punto de datos asigna su frecuencia (en MHz) a una posición horizontal en el espectro y traza el valor SWR correspondiente como una superposición de línea. La superposición se dibuja tanto en las rutas de pintado aceleradas por GPU como en las procesadas por software.

La superposición tiene tres estados:

| Estado            | Descripción                                                                                                                                                          | Notas |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------|
| Sin datos         | La superposición no se dibuja. Llame a `clearSwrSweepPoints()` para volver a este estado.                                                                            |       |
| Barrido en curso  | La superposición se dibuja y un cursor marca la frecuencia de barrido actual. Establezca `running = true` y proporcione `currentFreqMhz` al llamar a `setSwrSweepPoints()`. |       |
| Barrido completo  | La superposición se dibuja sin un marcador de cursor. Establezca `running = false` al llamar a `setSwrSweepPoints()`.                                                  |       |

Se puede pasar una etiqueta de origen opcional (por ejemplo, el nombre del sintonizador de antena o analizador que proporciona los datos) a través del parámetro `sourceLabel` y se muestra en la superposición.

Para actualizar la superposición, llame a `setSwrSweepPoints()` con un vector de valores `SwrSweepPoint`. Cada punto lleva:

- `freqMhz` — frecuencia de la medición, en MHz (predeterminado `0.0`).
- `swr` — valor SWR en esa frecuencia (predeterminado `1.0`).

Los puntos con valores no finitos de `freqMhz` o `swr` se omiten silenciosamente. Los puntos cuya coordenada x mapeada queda fuera del área visible del espectro no se dibujan.

Para eliminar la superposición, llame a `clearSwrSweepPoints()`.

## Consejos

- La **Frequency label** muestra la frecuencia del VFO con agrupación de puntos (por ejemplo, `14.225.000`). Haga clic en ella para ingresar al modo de edición y escribir una frecuencia en MHz, luego presione Enter para sintonizar y volver a centrar el panadapter. El editor de frecuencia admite hasta 450 MHz cuando el slice está en una antena XVTR.
- El spinbox **STEP** controla cuánto se mueve el VFO por cada clic de la rueda de desplazamiento o por cada pulsación de los botones **<** / **>**. Los tamaños de paso son por modo — por ejemplo, los pasos de SSB son 1, 10, 50, 100, 500, 1000, 2000 o 3000 Hz; los pasos de CW son 1, 5, 10, 50, 100, 200 o 400 Hz.
- El tamaño de paso predeterminado es 100 Hz (índice 2 en la lista por modo).
- Presionar Escape en el campo de edición de frecuencia cancela la entrada, restaura la frecuencia anterior y descarta el editor.
- Los controles deslizantes de **AF gain** y **L / R pan** tienen un valor predeterminado de 70 y 50 (centro) respectivamente.
- El valor predeterminado de **Squelch level** es 20. El nivel de squelch manual se recuerda entre sesiones.
- El valor predeterminado de **AGC threshold** es 65.

## Relacionados

- [RX Controls overview](../../features/rx/overview.md)
- [Switch between multiple slices using the A..H tab row](../../features/rx/switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Tune the radio to a frequency (type MHz in the readout)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Lock the slice to prevent accidental retuning](../../features/rx/lock-the-slice-to-prevent-accidental-retuning.md)
- [Use RIT to offset the receive frequency for a drifting station](../../features/rx/use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Use XIT to offset the transmit frequency without changing RX](../../features/rx/use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Click the spectrum to activate a panadapter (multi-slice mode)](../../features/panadapter/click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Panadapter overview](../../features/panadapter/overview.md)
- [Make your first QSO with AetherSDR](../tutorials/first-qso.md)
<!-- docmesh:llm version=v0.9.8 date=2026-06-01 -->
