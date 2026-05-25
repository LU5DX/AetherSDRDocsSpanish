# Entender Slices y VFOs

En AetherSDR, un slice es un receptor independiente dentro de un panadapter. Cada slice tiene su propia frecuencia de VFO, modo, filtro y configuración de audio. El FLEX-8600 admite hasta ocho slices simultáneos (etiquetados de la A a la H), lo que le permite monitorear múltiples frecuencias a la vez dentro del mismo panadapter o de diferentes panadapters.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. Los slices solo existen cuando hay una conexión activa con el radio.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón de la bandeja **RX** en la barra lateral derecha.

## Cómo funcionan los slices

Cada slice es un canal de recepción completamente independiente. Tiene:

- Una **frecuencia de VFO** — la frecuencia de sintonización central para ese slice, que se muestra en la **Frequency label** del applet RX Controls.
- Un **modo** — USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL o RTTY — configurado con el **Mode combo**.
- Una **banda de paso del filtro** — ajustable mediante presets de ancho de filtro o arrastrando el **Filter passband widget**.
- Sus propios ajustes de **AF gain**, **AGC**, **squelch**, **RIT** y **XIT**.
- Antenas de RX y TX asignadas.

Un slice siempre está vinculado a un panadapter. El panadapter muestra el espectro FFT para el segmento de banda del slice, y el marcador del VFO del slice aparece como una línea en ese espectro.

## Slices y el panadapter

La visualización de **Spectrum / waterfall** del panadapter muestra la posición actual del VFO del slice. Al hacer clic o arrastrar en el espectro se sintoniza el slice activo. La barra de título del panadapter muestra qué slice está vinculado a él (por ejemplo, **Slice A**).

En el modo multislice, cada panadapter puede contener uno o más marcadores de slice. Al hacer clic en el espectro de un panadapter diferente, se activa ese panadapter y su slice asociado.

## Cambiar entre slices

El applet RX Controls muestra una fila de pestañas etiquetadas de la **A** a la **H** (hasta el número máximo de slices del radio). Haga clic en una pestaña para vincular el applet RX Controls a ese slice. El indicador **Slice badge** en el applet se actualiza para mostrar la letra del slice activo, coloreada según la identidad del slice. La badge admite renderizado de texto enriquecido para la letra del slice.

La fila de pestañas se oculta cuando solo se usa un slice. Cuando el radio se desconecta, `clearSliceButtons()` elimina todos los botones de pestañas y restaura la badge de slice estática.

## El slice de TX

Solo un slice transmite a la vez. El slice que está transmitiendo actualmente es el slice TX. Para convertir un slice en el slice TX, haga clic en su botón **TX (badge)** en el applet RX Controls. Esto enruta la transmisión a través de la frecuencia, el modo y la antena TX de ese slice.

## RIT y XIT

RIT (Receive Incremental Tuning) desplaza la frecuencia de recepción sin mover el VFO. Actívelo con el botón **RIT**; ajústelo con el spinbox **RIT offset** (pasos de 10 Hz); restablézcalo con **RIT 0**.

XIT (Transmit Incremental Tuning) desplaza la frecuencia de transmisión sin cambiar la frecuencia de recepción. Actívelo con el botón **XIT**; ajústelo con el spinbox **XIT offset** (pasos de 10 Hz); restablézcalo con **XIT 0**.

Ambos son independientes por slice.

## Bloquear un slice

Para evitar una resintonización accidental, haga clic en el botón 🔓 en el applet RX Controls. El icono cambia a 🔒 y el slice ignora los cambios de frecuencia hasta que se desbloquee.

## Ganancia de AF y paneo

Ajuste el control deslizante **AF gain** (0–100) para establecer el volumen de salida de audio del slice. Use el control deslizante **L / R pan** (0–100) para posicionar el audio del slice en el campo estéreo: 0 es completamente a la izquierda, 50 es el centro, 100 es completamente a la derecha. Haga doble clic en el control deslizante de paneo para restablecerlo al centro. El control deslizante de paneo ahora muestra un indicador de texto: "C" para centro, "L{n}" para desplazamiento a la izquierda, o "R{n}" para desplazamiento a la derecha.

## Squelch

Active el squelch haciendo clic en el botón **SQL**, luego ajuste el control deslizante **Squelch level** (0–100) para establecer el umbral. El squelch solo tiene efecto cuando SQL está activado.

El squelch se desactiva automáticamente en modos RTTY y digitales (DIGU, DIGL) donde el squelch eliminaría los caracteres FSK e interrumpiría la decodificación.

El umbral de squelch manual se conserva del lado del cliente entre sesiones. Cuando el modo de squelch automático está activo, el radio puede sobrescribir el nivel de squelch del slice con valores sugeridos por el algoritmo, por lo que AetherSDR recuerda su última preferencia manual y la restaura.

## AGC

Seleccione el modo AGC del cuadro combinado **AGC mode**: Off, Slow, Med o Fast. El control deslizante **AGC threshold** ajusta el nivel de umbral del AGC. Cuando el modo AGC es Off, el control deslizante establece el nivel de apagado en su lugar. El cuadro combinado de modo se oculta en los modos de la familia FM (FM, NFM, DFM).

## Dúplex de repetidor FM

Cuando opera en modo FM, NFM o DFM, aparecen los controles de dúplex FM:

- **Tone mode (FM)** — Seleccione "CTCSS TX" para habilitar la transmisión de tono CTCSS.
- **CTCSS tone value** — Seleccione la frecuencia del tono CTCSS de entre 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz). Solo está habilitado cuando Tone mode está configurado en CTCSS TX.
- **Offset (FM)** — Establezca la frecuencia de desplazamiento del repetidor (0.0–100.0 MHz en pasos de 0.1 MHz).
- **− (offset down)** — Haga clic para establecer la frecuencia de TX por debajo de la de RX.
- **Simplex** — Haga clic para establecer la frecuencia de TX igual a la de RX (predeterminado).
- **+ (offset up)** — Haga clic para establecer la frecuencia de TX por encima de la de RX.
- **REV** — Haga clic para invertir el signo del desplazamiento de TX para un par de repetidor invertido.

## Selección de antena

### Antena RX

Haga clic en el botón **ANT1 (RX antenna)** para abrir un menú que enumera las antenas de recepción disponibles. Seleccionar una antena llama a `setRxAntenna()` en el slice. El menú se completa desde `rxAntennaList()` del slice cuando está disponible; de lo contrario, desde la lista de antenas del panadapter. Cada elemento del menú lleva el token de la antena como su valor de datos y muestra una etiqueta con información sobre herramientas e información de estado.

### Antena TX

Haga clic en el botón **ANT1 (TX antenna)** para abrir un menú que enumera las antenas capaces de TX. Los puertos de antena solo de RX (prefijo "RX") se filtran. Seleccionar una antena llama a `setTxAntenna()` en el slice. Cada elemento del menú lleva el token de la antena como su valor de datos y muestra una etiqueta con información sobre herramientas e información de estado.

## Presets de ancho de filtro

Haga clic en un botón **Filter width presets** para aplicar un ancho de filtro preestablecido. Haga clic con el botón derecho en un botón de preset para guardar el ancho de filtro actual como un preset. Los presets son por modo y están ocultos para los modos FM/NFM/DFM.

El indicador **Filter width label** muestra el ancho de banda del filtro actual (por ejemplo, "2.7K", "3.3K", "500", "6.0K"). La lectura del ancho del filtro se comparte con el panel VFO para una visualización coherente, utilizando lógica consciente del modo para que los modos SSB/digitales muestren la anchura etiquetada correcta.

Use el **Filter passband widget** para arrastrar los bordes inferior y superior y ajustar la banda de paso del filtro manualmente.

## Ancho de filtro por pasos

Use los comandos **Widen** y **Narrow** para recorrer la lista de presets de filtro por modo. Cada pulsación pasa al preset siguiente más ancho o más estrecho en la lista. El comando recorre la lista de presets por modo, por lo que siempre produce bordes de banda de paso correctos para el modo.

## Silenciar

Haga clic en el botón 🔊 / 🔇 para silenciar o reactivar el audio del slice. Un solo clic silencia/reactiva el slice actual. Un doble clic silencia/reactiva todos los slices propietarios a la vez. El botón de silencio no es marcable: el icono se actualiza solo cuando el radio confirma el cambio de estado de silencio a través del modelo del slice, lo que garantiza que el estado mostrado siempre coincida con el del radio.

Según la Política de Ajustes Autoritativos del Radio (#2489), el estado de silencio NO se guarda ni restaura al reconectar: el radio es la fuente de verdad para el silencio de audio.

## Indicador QSK

El indicador **QSK** se ilumina en ámbar cuando el break-in de CW (QSK) está activo. Es de solo lectura y se controla mediante el botón Breakin del applet CW.

## Ingreso de frecuencia

El campo **Frequency edit** ahora usa `FrequencyEntryParser::normalizedMhzText()` para limpiar los valores en MHz ingresados por el usuario. Ingresar una frecuencia superior a 54.0 MHz sin notación explícita de MHz (por ejemplo, "144600000" para 144.6 MHz) se trata como una entrada de banda VHF/UHF y se escala automáticamente en consecuencia. La notación explícita de MHz por encima de 54.0 MHz (por ejemplo, "144.600") otorga acceso a frecuencias de hasta 50000.0 MHz sin necesidad de una antena XVTR.

## Indicadores de texto en controles deslizantes

Tanto los controles deslizantes de AF gain como de paneo ahora muestran lecturas de texto en vivo:
- **AF gain**: Muestra "X%" (por ejemplo, "70%")
- **Pan**: Muestra "C" para centro, "L{n}" para desplazamiento a la izquierda o "R{n}" para desplazamiento a la derecha (por ejemplo, "L20", "R15")

## Superposición de barrido SWR

La versión V0.9.4 añade una superposición de barrido SWR que dibuja los datos de SWR versus frecuencia directamente en el espectro del panadapter. Cuando un barrido está activo, cada punto de datos asigna su frecuencia (en MHz) a una posición horizontal en el espectro y traza el valor de SWR correspondiente como una línea superpuesta. La superposición se dibuja tanto en las rutas de pintado aceleradas por GPU como en las de software.

La superposición tiene tres estados:

| Estado            | Descripción                                                                                                                                                      | Notas |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------|
| Sin datos         | La superposición no se dibuja. Llame a `clearSwrSweepPoints()` para volver a este estado.                                                                        |       |
| Barrido en curso  | La superposición se dibuja y un cursor marca la frecuencia de barrido actual. Establezca `running = true` y proporcione `currentFreqMhz` al llamar a `setSwrSweepPoints()`. |       |
| Barrido completo  | La superposición se dibuja sin un marcador de cursor. Establezca `running = false` al llamar a `setSwrSweepPoints()`.                                                  |       |

Se puede pasar una etiqueta de origen opcional (por ejemplo, el nombre del sintonizador de antena o analizador que proporciona los datos) a través del parámetro `sourceLabel` y se muestra en la superposición.

Para actualizar la superposición, llame a `setSwrSweepPoints()` con un vector de valores `SwrSweepPoint`. Cada punto contiene:

- `freqMhz` — frecuencia de la medición, en MHz (predeterminado `0.0`).
- `swr` — valor de SWR en esa frecuencia (predeterminado `1.0`).

Los puntos con valores `freqMhz` o `swr` no finitos se omiten silenciosamente. Los puntos cuya coordenada x asignada cae fuera del área visible del espectro no se dibujan.

Para eliminar la superposición, llame a `clearSwrSweepPoints()`.

## Consejos

- La **Frequency label** muestra la frecuencia del VFO con agrupación de puntos (por ejemplo, `14.225.000`). Haga clic en ella para entrar en modo de edición y escriba una frecuencia en MHz, luego presione Enter para sintonizar y volver a centrar el panadapter. El editor de frecuencias admite hasta 450 MHz cuando el slice está en una antena XVTR, y hasta 50000.0 MHz cuando se ingresa una entrada explícita en MHz superior a 54.0 MHz.
- El spinbox **STEP** controla cuánto se mueve el VFO por clic de la rueda de desplazamiento o por cada pulsación de los botones **<** / **>**. Los tamaños de paso son por modo; por ejemplo, los pasos de SSB son 1, 10, 50, 100, 500, 1000, 2000 o 3000 Hz; los pasos de CW son 1, 5, 10, 50, 100, 200 o 400 Hz.
- El tamaño de paso predeterminado es 100 Hz (índice 2 en la lista por modo).
- Presionar Escape en el campo de edición de frecuencia cancela la entrada, restaura la frecuencia anterior y descarta el editor.
- El valor predeterminado del control deslizante **AF gain** es 70. El valor predeterminado del control deslizante **L / R pan** es 50 (centro).
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
