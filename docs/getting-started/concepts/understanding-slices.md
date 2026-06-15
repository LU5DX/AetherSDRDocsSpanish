# Comprensión de los Slices y VFOs

En AetherSDR, un slice es un receptor independiente dentro de un panadapter. Cada slice tiene su propia frecuencia VFO, modo, filtro y configuración de audio. La FLEX-8600 admite hasta ocho slices simultáneos (etiquetados de la A a la H), lo que le permite monitorear múltiples frecuencias a la vez dentro del mismo panadapter o de diferentes.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Los slices solo existen cuando hay una conexión activa con la radio.
- El applet de Controles de RX debe estar visible. Si no lo está, haga clic en el botón **RX** de la bandeja en la barra lateral derecha.

## Cómo funcionan los slices

Cada slice es un canal de recepción completamente independiente. Tiene:

- Una **frecuencia VFO** — la frecuencia de sintonización central para ese slice, mostrada en la **Etiqueta de frecuencia** en el applet de Controles de RX.
- Un **modo** — USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL o RTTY — configurado con el **Combo de modo**.
- Un **ancho de banda de filtro** — ajustable mediante valores predefinidos de ancho de filtro o arrastrando el **Widget de ancho de banda de filtro**.
- Su propia **ganancia AF**, **CAG**, **squelch**, **RIT** y **XIT**.
- Antenas de RX y TX asignadas.

Un slice siempre está vinculado a un panadapter. El panadapter muestra el espectro FFT para el segmento de banda del slice, y el marcador VFO del slice aparece como una línea en ese espectro.

## Slices y el panadapter

La visualización de **Espectro / Waterfall** del panadapter muestra la posición actual del VFO del slice. Al hacer clic o arrastrar en el espectro, se sintoniza el slice activo. La barra de título del panadapter muestra qué slice está vinculado a él (por ejemplo, **Slice A**).

En el modo de múltiples slices, cada panadapter puede contener uno o más marcadores de slice. Al hacer clic en el espectro de un panadapter diferente, se activa ese panadapter y su slice asociado.

## Cambio entre slices

El applet de Controles de RX muestra una fila de pestañas etiquetadas de la **A** a la **H** (hasta el número máximo de slices de la radio). Haga clic en una pestaña para vincular el applet de Controles de RX a ese slice. El indicador de **Insignia de slice** en el applet se actualiza para mostrar la letra del slice activo, coloreada según la identidad del slice. La insignia admite representación de texto enriquecido para la letra del slice.

La fila de pestañas se oculta cuando solo se utiliza un slice. Cuando la radio se desconecta, `clearSliceButtons()` elimina todos los botones de pestaña y restaura la insignia de slice estática.

## El slice de TX

Solo un slice transmite a la vez. El slice que está transmitiendo actualmente es el slice de TX. Para convertir un slice en el slice de TX, haga clic en su botón **TX (insignia)** en el applet de Controles de RX. Esto enruta la transmisión a través de la frecuencia, el modo y la antena TX de ese slice.

## RIT y XIT

El RIT (Sintonización Incremental de Recepción) desplaza la frecuencia de recepción sin mover el VFO. Actívelo con el botón **RIT**; ajústelo con el cuadro giratorio **Desplazamiento RIT** (pasos de 10 Hz); restablezca con **RIT 0**.

El XIT (Sintonización Incremental de Transmisión) desplaza la frecuencia de transmisión sin cambiar la frecuencia de recepción. Actívelo con el botón **XIT**; ajústelo con el cuadro giratorio **Desplazamiento XIT** (pasos de 10 Hz); restablezca con **XIT 0**.

Ambos son independientes por slice.

## Bloqueo de un slice

Para evitar una resintonización accidental, haga clic en el botón 🔓 en el applet de Controles de RX. El icono cambia a 🔒 y el slice ignora los cambios de frecuencia hasta que se desbloquee.

## Ganancia AF y panorámico

Ajuste el control deslizante de **Ganancia AF** (0–100) para configurar el volumen de salida de audio del slice. Use el control deslizante **Panorámico L / R** (0–100) para posicionar el audio del slice en el campo estéreo: 0 es totalmente a la izquierda, 50 es al centro, 100 es totalmente a la derecha. Haga doble clic en el control deslizante panorámico para restablecer al centro. El control deslizante panorámico ahora muestra un indicador de texto: "C" para centro, "L{n}" para desplazamiento izquierdo o "R{n}" para desplazamiento derecho.

## Squelch

Active el squelch haciendo clic en el botón **SQL**, luego ajuste el control deslizante de **Nivel de squelch** (0–100) para configurar el umbral. El squelch solo tiene efecto cuando SQL está activado.

El squelch se desactiva automáticamente en modo RTTY y modos digitales (DIGU, DIGL), donde el squelch eliminaría los caracteres FSK e interrumpiría la decodificación.

El umbral de squelch manual se conserva del lado del cliente entre sesiones. Cuando el modo de squelch automático está activo, la radio puede sobrescribir el nivel de squelch del slice con valores sugeridos por el algoritmo, por lo que AetherSDR recuerda su última preferencia manual y la restaura.

## CAG

Seleccione el modo CAG en el cuadro combinado **Modo CAG**: Apagado, Lento, Medio o Rápido. El control deslizante de **Umbral CAG** ajusta el nivel del umbral CAG. Cuando el modo CAG está en Apagado, el control deslizante establece el nivel de apagado en su lugar. El combo de modo se oculta en los modos de la familia FM (FM, NFM, DFM).

### Calibración de ruido CAG-T

Haga clic derecho en el control deslizante de **Umbral CAG** para abrir un menú contextual, luego seleccione **Calibrar CAG-T contra el piso de ruido…** para iniciar el panel de calibración de ruido CAG-T para el slice actual. El panel de calibración utiliza la medición del piso de ruido para calcular un umbral óptimo. La información sobre herramientas del control deslizante anuncia esta función.

## Dúplex de repetidor FM

Cuando se opera en modo FM, NFM o DFM, aparecen los controles de dúplex FM:

- **Modo de tono (FM)** — Seleccione "CTCSS TX" para habilitar la transmisión de tono CTCSS.
- **Valor de tono CTCSS** — Seleccione la frecuencia de tono CTCSS de entre 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz). Solo está habilitado cuando el Modo de tono está configurado en CTCSS TX.
- **Desplazamiento (FM)** — Configure la frecuencia de desplazamiento del repetidor (0.0–100.0 MHz en pasos de 0.1 MHz).
- **− (desplazamiento hacia abajo)** — Haga clic para establecer la frecuencia de TX por debajo de la de RX.
- **Símplex** — Haga clic para establecer la frecuencia de TX igual a la de RX (predeterminado).
- **+ (desplazamiento hacia arriba)** — Haga clic para establecer la frecuencia de TX por encima de la de RX.
- **REV** — Haga clic para invertir el signo del desplazamiento de TX para un par de repetidor invertido.

## Selección de antena

### Antena RX

Haga clic en el botón **ANT1 (antena RX)** para abrir un menú que enumera las antenas de recepción disponibles. Seleccionar una antena llama a `setRxAntenna()` en el slice. El menú se completa desde `rxAntennaList()` del slice cuando está disponible; de lo contrario, desde la lista de antenas del panadapter. Cada elemento del menú lleva el token de la antena como su valor de datos y muestra una etiqueta con información sobre herramientas y sugerencia de estado.

### Antena TX

Haga clic en el botón **ANT1 (antena TX)** para abrir un menú que enumera las antenas con capacidad TX. Los puertos de antena solo RX (prefijo "RX") se filtran. Seleccionar una antena llama a `setTxAntenna()` en el slice. Cada elemento del menú lleva el token de la antena como su valor de datos y muestra una etiqueta con información sobre herramientas y sugerencia de estado.

## Valores predefinidos de ancho de filtro

Haga clic en un botón de **Valores predefinidos de ancho de filtro** para aplicar un ancho de filtro predefinido. Haga clic derecho en un botón predefinido para guardar el ancho de filtro actual como un valor predefinido. Los valores predefinidos son por modo y están ocultos para los modos FM/NFM/DFM.

El indicador de **Etiqueta de ancho de filtro** muestra el ancho de banda del filtro actual (por ejemplo, "2.7K", "3.3K", "500", "6.0K"). La lectura del ancho de filtro se comparte con el panel VFO para una visualización coherente, utilizando lógica sensible al modo para que los modos SSB/digitales muestren el ancho etiquetado correcto.

Use el **Widget de ancho de banda de filtro** para arrastrar los bordes inferior y superior y ajustar el ancho de banda del filtro manualmente.

## Ancho de filtro por pasos

Use los comandos **Ampliar** y **Reducir** para recorrer la lista de valores predefinidos de filtro por modo. Cada pulsación avanza al siguiente valor predefinido más ancho o más estrecho en la lista. El comando recorre la lista de valores predefinidos por modo, por lo que siempre produce bordes de paso de banda correctos para el modo.

## Silencio

Haga clic en el botón 🔊 / 🔇 para silenciar o reactivar la salida de audio del slice. Un solo clic silencia/reactiva el slice actual. Un doble clic silencia/reactiva todos los slices propiedad del usuario a la vez. El botón de silencio no es seleccionable: el icono se actualiza solo cuando la radio confirma el cambio de estado de silencio a través del modelo del slice, asegurando que el estado mostrado siempre coincida con la radio.

Según la Política de Configuración Autoritativa de la Radio (#2489), el estado de silencio NO se guarda ni se restablece al reconectar: la radio es la fuente de verdad para el silencio de audio.

## Indicador QSK

El indicador **QSK** se ilumina en ámbar cuando el break-in CW (QSK) está activo. Esto es de solo lectura y se controla mediante el botón Breakin del applet CW.

## Ingreso de frecuencia

El campo **Editar frecuencia** ahora usa `FreqLineEdit` (un widget derivado de `FrequencyEntryParser`) con texto de sugerencia "MHz". Ingresar una frecuencia superior a 54.0 MHz sin notación explícita de MHz (por ejemplo, "144600000" para 144.6 MHz) se trata como una entrada de banda VHF/UHF y se escala automáticamente en consecuencia. La notación explícita de MHz superior a 54.0 MHz (por ejemplo, "144.600") permite el acceso a frecuencias de hasta 50000.0 MHz sin necesidad de una antena XVTR.

## Demodulador de software WFM

El botón de alternancia **WFM** activa un demodulador FM por software para el slice actual. Cuando está activado, el botón se ilumina en verde. El demodulador procesa señales FM de banda ancha recibidas a través de DAX IQ mediante el Cable Hi-Fi. Active el botón para activar la superposición WFM, o desactívelo para desactivarla.

La superposición WFM se elimina automáticamente cuando cambia el modo del slice mediante el **Combo de modo** — seleccionar cualquier modo de radio real (USB, LSB, CW, etc.) desactiva WFM en ese slice. El estado del botón WFM se sincroniza con la radio: cuando otra parte de la aplicación activa o desactiva WFM en el mismo slice, el botón se actualiza en consecuencia.

## Indicadores de texto de los controles deslizantes

Tanto los controles deslizantes de ganancia AF como de panorámico ahora muestran lecturas de texto en vivo:
- **Ganancia AF**: Muestra "X%" (por ejemplo, "70%")
- **Panorámico**: Muestra "C" para centro, "L{n}" para desplazamiento izquierdo o "R{n}" para desplazamiento derecho (por ejemplo, "L20", "R15")

## Superposición de barrido SWR

La versión V0.9.4 añade una superposición de barrido SWR que dibuja los datos de SWR frente a la frecuencia directamente en el espectro del panadapter. Cuando un barrido está activo, cada punto de datos asigna su frecuencia (en MHz) a una posición horizontal en el espectro y traza el valor SWR correspondiente como una línea superpuesta. La superposición se dibuja tanto en las rutas de pintado aceleradas por GPU como en las renderizadas por software.

La superposición tiene tres estados:

| Estado           | Descripción                                                                                                                                               | Notas |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|-------|
| Sin datos        | La superposición no se dibuja. Llame a `clearSwrSweepPoints()` para volver a este estado.                                                                  |       |
| Barrido en curso | La superposición se dibuja y un cursor marca la frecuencia de barrido actual. Establezca `running = true` y proporcione `currentFreqMhz` al llamar a `setSwrSweepPoints()`. |       |
| Barrido completo | La superposición se dibuja sin un marcador de cursor. Establezca `running = false` al llamar a `setSwrSweepPoints()`.                                      |       |

Se puede pasar una etiqueta de origen opcional (por ejemplo, el nombre del sintonizador de antena o analizador que proporciona los datos) a través del parámetro `sourceLabel` y se muestra en la superposición.

Para actualizar la superposición, llame a `setSwrSweepPoints()` con un vector de valores `SwrSweepPoint`. Cada punto contiene:

- `freqMhz` — frecuencia de la medición, en MHz (predeterminado `0.0`).
- `swr` — valor SWR en esa frecuencia (predeterminado `1.0`).

Los puntos con valores no finitos de `freqMhz` o `swr` se omiten silenciosamente. Los puntos cuya coordenada x mapeada cae fuera del área visible del espectro no se dibujan.

Para eliminar la superposición, llame a `clearSwrSweepPoints()`.

## Consejos

- La **Etiqueta de frecuencia** muestra la frecuencia del VFO con agrupación de puntos (por ejemplo, `14.225.000`). Haga clic en ella para ingresar al modo de edición y escribir una frecuencia en MHz, luego presione Enter para sintonizar y re-centrar el panadapter. El editor de frecuencia admite hasta 450 MHz cuando el slice está en una antena XVTR, y hasta 50000.0 MHz cuando se ingresa una entrada explícita de MHz superior a 54.0 MHz.
- El cuadro giratorio **PASO** controla cuánto se mueve el VFO por cada clic de la rueda de desplazamiento o por cada pulsación de los botones **<** / **>**. Los tamaños de paso son por modo — por ejemplo, los pasos de SSB son 1, 10, 50, 100, 500, 1000, 2000 o 3000 Hz; los pasos de CW son 1, 5, 10, 50, 100, 200 o 400 Hz.
- El tamaño de paso predeterminado es 100 Hz (índice 2 en la lista por modo).
- Presionar Escape en el campo de edición de frecuencia cancela la entrada, restaura
