# Comprensión de slices y VFOs

En AetherSDR, un slice es un receptor independiente dentro de un panadapter. Cada slice tiene su propia frecuencia de VFO, modo, filtro y configuración de audio. El FLEX-8600 soporta hasta ocho slices simultáneos (etiquetados de A a H), lo que le permite monitorear múltiples frecuencias a la vez dentro del mismo panadapter o en diferentes panadapters.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Los slices solo existen cuando hay una conexión de radio activa.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón **RX** de la barra lateral derecha.

## Cómo funcionan los slices

Cada slice es un canal de recepción totalmente independiente. Tiene:

- Una **frecuencia de VFO** — la frecuencia de sintonización central para ese slice, mostrada en la **etiqueta de frecuencia** en el applet RX Controls.
- Un **modo** — USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL o RTTY — configurado con el **combo de modo**.
- Una **banda de paso del filtro** — ajustable mediante presets de ancho de filtro o arrastrando el **widget de banda de paso del filtro**.
- Su propia configuración de **ganancia de AF**, **AGC**, **squelch**, **RIT** y **XIT**.
- Antenas de RX y TX asignadas.

Un slice siempre está vinculado a un panadapter. El panadapter muestra el espectro FFT para el segmento de banda del slice, y el marcador de VFO del slice aparece como una línea en ese espectro.

## Slices y el panadapter

La visualización de **espectro / waterfall** del panadapter muestra la posición actual del VFO del slice. Al hacer clic o arrastrar sobre el espectro se sintoniza el slice activo. La barra de título del panadapter muestra qué slice está vinculado a él (por ejemplo, **Slice A**).

En modo multi-slice, cada panadapter puede contener uno o más marcadores de slice. Hacer clic en el espectro de un panadapter diferente activa ese panadapter y su slice asociado.

## Cambio entre slices

El applet RX Controls muestra una fila de pestañas etiquetadas de **A** a **H** (hasta el número máximo de slices de la radio). Haga clic en una pestaña para vincular el applet RX Controls a ese slice. El indicador **Slice badge** en el applet se actualiza para mostrar la letra del slice activo, coloreada según la identidad del slice. La insignia soporta renderizado de texto enriquecido para la letra del slice.

La fila de pestañas se oculta cuando solo se usa un slice. Cuando la radio está desconectada, `clearSliceButtons()` elimina todos los botones de pestaña y restaura la insignia de slice estática.

## El slice de TX

Solo un slice transmite a la vez. El slice que transmite actualmente es el slice de TX. Para hacer que un slice sea el slice de TX, haga clic en su botón **TX (badge)** en el applet RX Controls. Esto enruta la transmisión a través de la frecuencia, el modo y la antena de TX de ese slice.

## RIT y XIT

El RIT (Receive Incremental Tuning) desplaza la frecuencia de recepción sin mover el VFO. Actívelo con el botón **RIT**; ajústelo con la caja de giro **RIT offset** (pasos de 10 Hz); restablézcalo con **RIT 0**.

El XIT (Transmit Incremental Tuning) desplaza la frecuencia de transmisión sin cambiar la frecuencia de recepción. Actívelo con el botón **XIT**; ajústelo con la caja de giro **XIT offset** (pasos de 10 Hz); restablézcalo con **XIT 0**.

Ambos son independientes por slice.

## Bloqueo de un slice

Para evitar resintonizaciones accidentales, haga clic en el botón 🔓 en el applet RX Controls. El ícono cambia a 🔒 y el slice ignora los cambios de frecuencia hasta que se desbloquee.

## Ganancia de AF y balance

Ajuste el control deslizante **AF gain** (0–100) para configurar el volumen de salida de audio del slice. Use el control deslizante **L / R pan** (0–100) para posicionar el audio del slice en el campo estéreo: 0 es totalmente a la izquierda, 50 es el centro, 100 es totalmente a la derecha. Haga doble clic en el control deslizante de balance para restablecerlo al centro. El control deslizante de balance ahora muestra un indicador de texto: "C" para centro, "L{n}" para desplazamiento a la izquierda, o "R{n}" para desplazamiento a la derecha.

## Squelch

Active el squelch haciendo clic en el botón **SQL**, luego ajuste el control deslizante **Squelch level** (0–100) para configurar el umbral. El squelch solo tiene efecto cuando SQL está activado.

El squelch se desactiva automáticamente en modos RTTY y digitales (DIGU, DIGL), donde el squelch recortaría los caracteres FSK y rompería la decodificación.

El umbral manual de squelch se conserva en el lado del cliente entre sesiones. Cuando el modo de squelch automático está activo, la radio puede sobrescribir el nivel de squelch del slice con valores sugeridos por el algoritmo, por lo que AetherSDR recuerda su última preferencia manual y la restaura.

## AGC

Seleccione el modo AGC en el cuadro combinado **AGC mode**: Off, Slow, Med o Fast. El control deslizante **AGC threshold** ajusta el nivel de umbral del AGC. Cuando el modo AGC está en Off, el control deslizante configura el nivel de off en su lugar. El cuadro combinado de modo se oculta en los modos de la familia FM (FM, NFM, DFM).

### Calibración de ruido AGC-T

Haga clic derecho en el control deslizante **AGC threshold** para abrir un menú contextual, luego seleccione **Calibrate AGC-T against noise floor…** para iniciar el panel de calibración de ruido AGC-T para el slice actual. El panel de calibración utiliza la medición del piso de ruido para calcular un umbral óptimo. La información sobre herramientas del control deslizante anuncia esta función.

## Duplex de repetidor FM

Cuando opera en modo FM, NFM o DFM, aparecen los controles de duplex FM:

- **Tone mode (FM)** — Seleccione "CTCSS TX" para habilitar la transmisión de tono CTCSS.
- **CTCSS tone value** — Seleccione la frecuencia de tono CTCSS entre los 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz). Solo se habilita cuando Tone mode está configurado en CTCSS TX.
- **Offset (FM)** — Configure la frecuencia de desplazamiento del repetidor (0.0–100.0 MHz en pasos de 0.1 MHz).
- **− (offset down)** — Haga clic para configurar la frecuencia de TX por debajo de la de RX.
- **Simplex** — Haga clic para configurar la frecuencia de TX igual a la de RX (predeterminado).
- **+ (offset up)** — Haga clic para configurar la frecuencia de TX por encima de la de RX.
- **REV** — Haga clic para invertir el signo del desplazamiento de TX para un par de repetidor invertido.

## Selección de antena

### Antena de RX

Haga clic en el botón **ANT1 (RX antenna)** para abrir un menú que enumera las antenas de recepción disponibles. Al seleccionar una antena se llama a `setRxAntenna()` en el slice. El menú se completa con la `rxAntennaList()` del slice cuando está disponible; de lo contrario, con la lista de antenas del panadapter. Cada elemento del menú lleva el token de antena como su valor de datos y muestra una etiqueta de visualización con información sobre herramientas y sugerencia de estado.

### Antena de TX

Haga clic en el botón **ANT1 (TX antenna)** para abrir un menú que enumera las antenas capaces de transmitir. Los puertos de antena de solo RX (prefijo "RX") se filtran. Al seleccionar una antena se llama a `setTxAntenna()` en el slice. Cada elemento del menú lleva el token de antena como su valor de datos y muestra una etiqueta de visualización con información sobre herramientas y sugerencia de estado.

## Presets de ancho de filtro

Haga clic en un botón de **Filter width presets** para aplicar un ancho de filtro preestablecido. Haga clic derecho en un botón de preset para guardar el ancho de filtro actual como preset. Los presets son por modo y se ocultan para los modos FM/NFM/DFM.

El indicador **Filter width label** muestra el ancho de banda del filtro actual (por ejemplo, "2.7K", "3.3K", "500", "6.0K"). La lectura del ancho de filtro se comparte con el panel de VFO para una visualización consistente, utilizando lógica sensible al modo para que los modos SSB/digitales muestren el ancho etiquetado correcto.

Use el **widget de banda de paso del filtro** para arrastrar los bordes inferior y superior y ajustar la banda de paso del filtro manualmente.

## Ancho de filtro por pasos

Use los comandos **Widen** y **Narrow** para recorrer la lista de presets de filtro por modo. Cada pulsación se mueve al preset siguiente más ancho o más estrecho en la lista. El comando recorre la lista de presets por modo para que siempre produzca bordes de banda de paso correctos para el modo.

## Silencio (Mute)

Haga clic en el botón 🔊 / 🔇 para silenciar o reactivar la salida de audio del slice. Un solo clic silencia/reactiva el slice actual. Doble clic silencia/reactiva todos los slices propiedad de una vez. El botón de silencio no es marcable: el ícono se actualiza solo cuando la radio confirma el cambio de estado de silencio a través del modelo de slice, asegurando que el estado mostrado siempre coincida con la radio.

Según la Política de Configuración Autoritativa de la Radio (#2489), el estado de silencio NO se guarda ni se restaura al reconectar: la radio es la fuente de verdad para el silencio de audio.

## Indicador QSK

El indicador **QSK** se enciende en ámbar cuando el break-in de CW (QSK) está activo. Es de solo lectura y se controla mediante el botón Breakin del applet CW.

## Entrada de frecuencia

El campo **Frequency edit** ahora usa `FreqLineEdit` (un widget derivado de `FrequencyEntryParser`) con texto de sugerencia "MHz". Ingresar una frecuencia superior a 54.0 MHz sin notación explícita de MHz (por ejemplo, "144600000" para 144.6 MHz) se trata como una entrada de banda VHF/UHF y se escala automáticamente en consecuencia. La notación explícita de MHz superior a 54.0 MHz (por ejemplo, "144.600") otorga acceso a frecuencias de hasta 50000.0 MHz sin requerir una antena XVTR.

## Demodulador de software WFM

El botón de conmutación **WFM** habilita un demodulador FM por software para el slice actual. Cuando está habilitado, el botón se ilumina en verde. El demodulador procesa señales FM de banda ancha recibidas a través de DAX IQ mediante el Cable Hi-Fi. Active el botón para activar la superposición WFM, o desactívelo para desactivarla.

La superposición WFM se elimina automáticamente cuando cambia el modo del slice mediante el **combo de modo** — seleccionar cualquier modo de radio real (USB, LSB, CW, etc.) desactiva WFM en ese slice. El estado del botón WFM se sincroniza con la radio: cuando otra parte de la aplicación activa o desactiva WFM en el mismo slice, el botón se actualiza en consecuencia.

## Indicadores de texto en controles deslizantes

Tanto los controles deslizantes de AF gain como de balance ahora muestran lecturas de texto en vivo:
- **AF gain**: Muestra "X%" (por ejemplo, "70%")
- **Pan**: Muestra "C" para centro, "L{n}" para desplazamiento a la izquierda, o "R{n}" para desplazamiento a la derecha (por ejemplo, "L20", "R15")

## Superposición de barrido SWR

V0.9.4 agrega una superposición de barrido SWR que dibuja datos de SWR versus frecuencia directamente en el espectro del panadapter. Cuando hay un barrido activo, cada punto de datos mapea su frecuencia (en MHz) a una posición horizontal en el espectro y traza el valor de SWR correspondiente como una superposición de línea. La superposición se dibuja tanto en la ruta de pintado acelerada por GPU como en la renderizada por software.

La superposición tiene tres estados:

| Estado             | Descripción                                                                                                                                           | Notas |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|-------|
| Sin datos          | La superposición no se dibuja. Llame a `clearSwrSweepPoints()` para volver a este estado.                                                              |       |
| Barrido en curso   | La superposición se dibuja y un cursor marca la frecuencia de barrido actual. Configure `running = true` y proporcione `currentFreqMhz` al llamar a `setSwrSweepPoints()`. |       |
| Barrido completo   | La superposición se dibuja sin marcador de cursor. Configure `running = false` al llamar a `setSwrSweepPoints()`.                                      |       |

Una etiqueta de origen opcional (por ejemplo, el nombre del acoplador de antena o analizador que proporciona los datos) se puede pasar mediante el parámetro `sourceLabel` y se muestra en la superposición.

Para actualizar la superposición, llame a `setSwrSweepPoints()` con un vector de valores `SwrSweepPoint`. Cada punto contiene:

- `freqMhz` — frecuencia de la medición, en MHz (predeterminado `0.0`).
- `swr` — valor de SWR en esa frecuencia (predeterminado `1.0`).

Los puntos con valores `freqMhz` o `swr` no finitos se omiten silenciosamente. Los puntos cuya coordenada x mapeada cae fuera del área visible del espectro no se dibujan.

Para eliminar la superposición, llame a `clearSwrSweepPoints()`.

## Congelación del panadapter durante TX

Cuando la radio entra en el estado TRANSMITTING (cualquier cliente en la red transmite), el waterfall en este panadapter se congela automáticamente. Reanuda el desplazamiento cuando la radio vuelve a recepción. Esto reemplaza la lógica anterior de congelación basada en el borde MOX, eliminando un artefacto de estela de TX de 10–23 segundos después de desactivar la transmisión.

## Reconciliación de reconexión del panadapter

Al reconectar la radio, la velocidad de cuadros deseada del panadapter y la duración de la línea del waterfall se reafirman a la radio. Esto evita que el panadapter caiga silenciosamente a la velocidad de cuadros predeterminada de 10 Hz de la radio. Los panadapters secundarios también tienen su rango dBm preparado al reconectar para que el ajuste automático del piso de ruido comience desde la línea base correcta en lugar del rango predeterminado [-50, +50] que podría causar un espectro plano.

## Alojamiento del panadapter en el lienzo

Cuando un panadapter se aloja como un elemento en el lienzo del espacio de trabajo, su franja de título proporciona un gesto de movimiento en vivo para reposicionarlo. Un clic (movimiento inferior a 6 px antes de soltar) activa el panadapter; un arrastre más allá de 6 px inicia el gesto de movimiento del lienzo. El botón de ventana emergente permanece visible en los elementos del lienzo incluso en modo de un solo panadapter, ya que un elemento del lienzo siempre puede flotar.

## Vista de espectro FFT 3D

El conmutador **3D FFT view** (en el panadapter) alterna entre el espectro 2
