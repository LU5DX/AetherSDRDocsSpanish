# Comprensión de Slices y VFOs

En AetherSDR, un slice es un receptor independiente dentro de un panadapter. Cada slice tiene su propia frecuencia de VFO, modo, filtro y configuración de audio. El FLEX-8600 admite hasta ocho slices simultáneos (etiquetados de la A a la H), lo que le permite monitorear múltiples frecuencias a la vez dentro del mismo panadapter o de diferentes panadapters.

## Antes de empezar

- AetherSDR debe estar conectado a una radio FLEX-8600. Los slices solo existen cuando hay una conexión de radio activa.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón de la bandeja **RX** en la barra lateral derecha.

## Cómo funcionan los slices

Cada slice es un canal de recepción completamente independiente. Tiene:

- Una **frecuencia de VFO**: la frecuencia de sintonización central para ese slice, que se muestra en la **Frequency label** del applet RX Controls.
- Un **modo**: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL o RTTY, que se configura con el **Mode combo**.
- Un **pasabanda de filtro**: ajustable mediante presets de ancho de filtro o arrastrando el **Filter passband widget**.
- Su propia configuración de **AF gain**, **AGC**, **squelch**, **RIT** y **XIT**.
- Antenas de RX y TX asignadas.

Un slice está siempre vinculado a un panadapter. El panadapter muestra el espectro FFT para el segmento de banda del slice, y el marcador de VFO del slice aparece como una línea en ese espectro.

## Slices y el panadapter

La pantalla de **Spectrum / waterfall** del panadapter muestra la posición actual del VFO del slice. Al hacer clic o arrastrar en el espectro se sintoniza el slice activo. La barra de título del panadapter muestra qué slice está vinculado a él (por ejemplo, **Slice A**).

En modo multislice, cada panadapter puede contener uno o más marcadores de slice. Al hacer clic en el espectro de un panadapter diferente, se activa ese panadapter y su slice asociado.

## Cambio entre slices

El applet RX Controls muestra una fila de pestañas etiquetadas de la **A** a la **H** (hasta el número máximo de slices de la radio). Haga clic en una pestaña para vincular el applet RX Controls a ese slice. El indicador **Slice badge** en el applet se actualiza para mostrar la letra del slice activo, coloreada según la identidad del slice. La insignia admite renderizado de texto enriquecido para la letra del slice.

La fila de pestañas se oculta cuando solo se usa un slice. Cuando la radio se desconecta, `clearSliceButtons()` elimina todos los botones de pestañas y restaura la insignia de slice estática.

## El slice de TX

Solo un slice transmite a la vez. El slice que está transmitiendo actualmente es el slice de TX. Para convertir un slice en el slice de TX, haga clic en su botón **TX (badge)** en el applet RX Controls. Esto enruta la transmisión a través de la frecuencia, el modo y la antena de TX de ese slice.

## RIT y XIT

RIT (Receive Incremental Tuning) desplaza la frecuencia de recepción sin mover el VFO. Actívelo con el botón **RIT**; ajústelo con el spinbox **RIT offset** (pasos de 10 Hz); restablezca con **RIT 0**.

XIT (Transmit Incremental Tuning) desplaza la frecuencia de transmisión sin cambiar la frecuencia de recepción. Actívelo con el botón **XIT**; ajústelo con el spinbox **XIT offset** (pasos de 10 Hz); restablezca con **XIT 0**.

Ambos son independientes por slice.

## Bloqueo de un slice

Para evitar una resintonización accidental, haga clic en el botón 🔓 en el applet RX Controls. El icono cambia a 🔒 y el slice ignora los cambios de frecuencia hasta que se desbloquee.

## AF gain y pan

Ajuste el deslizador **AF gain** (0–100) para establecer el volumen de salida de audio del slice. Use el deslizador **L / R pan** (0–100) para posicionar el audio del slice en el campo estéreo: 0 es completamente a la izquierda, 50 es el centro, 100 es completamente a la derecha. Haga doble clic en el deslizador de pan para restablecerlo al centro. El deslizador de pan ahora muestra un indicador de texto: "C" para centro, "L{n}" para desplazamiento a la izquierda o "R{n}" para desplazamiento a la derecha.

## Squelch

Active el squelch haciendo clic en el botón **SQL**, luego ajuste el deslizador **Squelch level** (0–100) para establecer el umbral. El squelch solo tiene efecto cuando SQL está activado.

El squelch se desactiva automáticamente en modos RTTY y digitales (DIGU, DIGL) donde el squelch eliminaría los caracteres FSK e interrumpiría la decodificación.

El umbral de squelch manual se conserva del lado del cliente entre sesiones. Cuando el modo de squelch automático está activo, la radio puede sobrescribir el nivel de squelch del slice con valores sugeridos por el algoritmo, por lo que AetherSDR recuerda su última preferencia manual y la restaura.

## AGC

Seleccione el modo AGC del cuadro combinado **AGC mode**: Off, Slow, Med o Fast. El deslizador **AGC threshold** ajusta el nivel de umbral del AGC. Cuando el modo AGC está en Off, el deslizador establece el nivel de apagado en su lugar. El cuadro combinado de modo se oculta en los modos de la familia FM (FM, NFM, DFM).

### Calibración de ruido AGC-T

Haga clic derecho en el deslizador **AGC threshold** para abrir un menú contextual, luego seleccione **Calibrate AGC-T against noise floor…** para iniciar el panel de calibración de ruido AGC-T para el slice actual. El panel de calibración utiliza la medición del piso de ruido para calcular un umbral óptimo. La información sobre herramientas del deslizador anuncia esta función.

## Dúplex de repetidor FM

Cuando opera en modo FM, NFM o DFM, aparecen los controles de dúplex de FM:

- **Tone mode (FM)** — Seleccione "CTCSS TX" para habilitar la transmisión de tono CTCSS.
- **CTCSS tone value** — Seleccione la frecuencia de tono CTCSS entre 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz). Solo está habilitado cuando Tone mode está configurado en CTCSS TX.
- **Offset (FM)** — Establezca la frecuencia de desplazamiento del repetidor (0.0–100.0 MHz en pasos de 0.1 MHz).
- **− (offset down)** — Haga clic para establecer la frecuencia de TX por debajo de la de RX.
- **Simplex** — Haga clic para establecer la frecuencia de TX igual a la de RX (predeterminado).
- **+ (offset up)** — Haga clic para establecer la frecuencia de TX por encima de la de RX.
- **REV** — Haga clic para invertir el signo del desplazamiento de TX para un par de repetidor invertido.

## Selección de antena

### Antena RX

Haga clic en el botón **ANT1 (RX antenna)** para abrir un menú que lista las antenas de recepción disponibles. Seleccionar una antena llama a `setRxAntenna()` en el slice. El menú se completa con `rxAntennaList()` del slice cuando está disponible; de lo contrario, con la lista de antenas del panadapter. Cada elemento del menú lleva el token de antena como su valor de datos y muestra una etiqueta con información sobre herramientas y sugerencia de estado.

### Antena TX

Haga clic en el botón **ANT1 (TX antenna)** para abrir un menú que lista las antenas capaces de TX. Los puertos de antena solo de RX (prefijo "RX") se filtran. Seleccionar una antena llama a `setTxAntenna()` en el slice. Cada elemento del menú lleva el token de antena como su valor de datos y muestra una etiqueta con información sobre herramientas y sugerencia de estado.

## Presets de ancho de filtro

Haga clic en un botón de **Filter width presets** para aplicar un ancho de filtro preestablecido. Haga clic derecho en un botón de preset para guardar el ancho de filtro actual como un preset. Los presets son por modo y están ocultos para los modos FM/NFM/DFM.

El indicador **Filter width label** muestra el ancho de banda del filtro actual (por ejemplo, "2.7K", "3.3K", "500", "6.0K"). La lectura del ancho de filtro se comparte con el panel VFO para una visualización coherente, utilizando lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto.

Use el **Filter passband widget** para arrastrar los bordes bajo y alto y ajustar el pasabanda del filtro manualmente.

## Ancho de filtro por pasos

Use los comandos **Widen** y **Narrow** para recorrer la lista de presets de filtro por modo. Cada pulsación pasa al siguiente preset más ancho o más estrecho en la lista. El comando recorre la lista de presets por modo, por lo que siempre produce bordes de pasabanda correctos para el modo.

## Silencio

Haga clic en el botón 🔊 / 🔇 para silenciar o reactivar el audio del slice. Un solo clic silencia/reactiva el slice actual. Un doble clic silencia/reactiva todos los slices propietarios a la vez. El botón de silencio no es seleccionable: el icono se actualiza solo cuando la radio confirma el cambio de estado de silencio a través del modelo de slice, lo que garantiza que el estado mostrado coincida siempre con la radio.

Según la Política de Configuración Autoritativa de la Radio (#2489), el estado de silencio NO se guarda ni restaura al reconectar: la radio es la fuente de verdad para el silencio de audio.

## Indicador QSK

El indicador **QSK** se enciende en ámbar cuando el break-in de CW (QSK) está activo. Es de solo lectura y se controla mediante el botón Breakin del applet CW.

## Entrada de frecuencia

El campo **Frequency edit** ahora usa `FreqLineEdit` (un widget derivado de `FrequencyEntryParser`) con texto de sugerencia "MHz". Ingresar una frecuencia superior a 54.0 MHz sin notación explícita de MHz (por ejemplo, "144600000" para 144.6 MHz) se trata como una entrada de banda VHF/UHF y se escala automáticamente en consecuencia. La notación explícita de MHz superior a 54.0 MHz (por ejemplo, "144.600") otorga acceso a frecuencias de hasta 50000.0 MHz sin necesidad de una antena XVTR.

## Demodulador de software WFM

El botón de alternancia **WFM** habilita un demodulador de FM por software para el slice actual. Cuando está habilitado, el botón se ilumina en verde. El demodulador procesa señales de FM de banda ancha recibidas a través de DAX IQ por el Cable Hi-Fi. Active el botón para encender la superposición WFM o desactívelo para desactivarla.

La superposición WFM se elimina automáticamente cuando cambia el modo del slice mediante el **Mode combo**: seleccionar cualquier modo de radio real (USB, LSB, CW, etc.) desactiva WFM en ese slice. El estado del botón WFM se sincroniza con la radio: cuando otra parte de la aplicación activa o desactiva WFM en el mismo slice, el botón se actualiza en consecuencia.

## Indicadores de texto en deslizadores

Tanto los deslizadores de AF gain como de pan muestran ahora lecturas de texto en vivo:
- **AF gain**: Muestra "X%" (por ejemplo, "70%")
- **Pan**: Muestra "C" para centro, "L{n}" para desplazamiento a la izquierda o "R{n}" para desplazamiento a la derecha (por ejemplo, "L20", "R15")

## Superposición de barrido SWR

La versión V0.9.4 añade una superposición de barrido SWR que dibuja datos de SWR frente a frecuencia directamente en el espectro del panadapter. Cuando un barrido está activo, cada punto de datos asigna su frecuencia (en MHz) a una posición horizontal en el espectro y traza el valor de SWR correspondiente como una línea superpuesta. La superposición se dibuja tanto en las rutas de renderizado aceleradas por GPU como en las de software.

La superposición tiene tres estados:

| Estado | Descripción | Notas |
|--------|-------------|-------|
| Sin datos | La superposición no se dibuja. Llame a `clearSwrSweepPoints()` para volver a este estado. | |
| Barrido en curso | La superposición se dibuja y un cursor marca la frecuencia de barrido actual. Establezca `running = true` y proporcione `currentFreqMhz` al llamar a `setSwrSweepPoints()`. | |
| Barrido completo | La superposición se dibuja sin un marcador de cursor. Establezca `running = false` al llamar a `setSwrSweepPoints()`. | |

Una etiqueta de origen opcional (por ejemplo, el nombre del sintonizador de antena o analizador que proporciona los datos) se puede pasar mediante el parámetro `sourceLabel` y se muestra en la superposición.

Para actualizar la superposición, llame a `setSwrSweepPoints()` con un vector de valores `SwrSweepPoint`. Cada punto lleva:

- `freqMhz`: frecuencia de la medición, en MHz (predeterminado `0.0`).
- `swr`: valor de SWR en esa frecuencia (predeterminado `1.0`).

Los puntos con valores `freqMhz` o `swr` no finitos se omiten silenciosamente. Los puntos cuya coordenada x asignada cae fuera del área visible del espectro no se dibujan.

Para eliminar la superposición, llame a `clearSwrSweepPoints()`.

## Congelación del panadapter durante TX

Cuando la radio entra en el estado TRANSMITTING (cualquier cliente en la red transmite), el waterfall de este panadapter se congela automáticamente. Se reanuda el desplazamiento cuando la radio vuelve a recepción. Esto reemplaza la lógica de congelación basada en el borde MOX anterior, eliminando un artefacto de cola de TX de 10 a 23 segundos después de desactivar la transmisión.

## Panel de decodificación CW

Cada panadapter puede mostrar un panel de decodificación CW debajo del espectro para la decodificación Morse fuera del aire. El panel aparece solo en modo CW cuando el audio de PC está enrutado al decodificador CW.

### Sintonización y controles

- **Sens**: un deslizador (0–100) que filtra decodificaciones de baja confianza. Los valores más altos son más estrictos. La configuración se guarda en `CwDecoderSensitivity`.
- **🔒P (Lock Pitch)**: activa/desactiva el bloqueo del tono del decodificador a la frecuencia sintonizada actual.
- **🔒S (Lock Speed)**: activa/desactiva el bloqueo de la velocidad del decodificador a las WPM actuales.
- **Lo (pitch min)**: establece el tono mínimo a buscar (300–1200 Hz). Limitado a ≤ Hi.
- **Hi (pitch max)**: establece el tono máximo a buscar (300–1200 Hz). Limitado a ≥ Lo.

### Copiar y limpiar

- **CPY ALL**: copia todo el texto decodificado al portapapeles.
- **CPY VIS**: copia solo el texto actualmente visible en el área de desplazamiento.
- **CLR**: limpia el búfer de decodificación CW.
- **✕ (close CW)**: oculta el panel de decodificación CW.

### Ajuste de tamaño de fuente (#3628)

Dos botones ajustan el tamaño de fuente del texto decodificado para facilitar la lectura:

- **A-**: disminuye el tamaño de fuente (mínimo
