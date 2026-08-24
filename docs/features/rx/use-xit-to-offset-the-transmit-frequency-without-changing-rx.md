# Applet de Controles de RX — Referencia Completa

El applet de Controles de RX proporciona controles de recepción por segmento (slice) para el segmento actualmente vinculado. Se muestra como un panel en la barra lateral derecha cuando se hace clic en el botón de la bandeja RX.

## Uso de XIT

XIT (Sintonización Incremental de Transmisión) le permite desplazar su frecuencia de transmisión por un número fijo de hercios mientras su frecuencia de recepción permanece en el VFO. Esto es útil cuando se opera en división (split), para compensar un desplazamiento de TX solicitado por la otra estación, o para igualar una frecuencia de red sin reajustar el panadapter.

### Pasos

1. En el applet de Controles de RX, desplácese hacia abajo hasta la sección RIT/XIT.
2. Haga clic en XIT para habilitar la Sintonización Incremental de Transmisión. El botón se ilumina cuando está activo.
3. Ajuste el desplazamiento de XIT usando uno de estos métodos:
   - Haga clic en los botones **<** o **>** que flanquean la caja de desplazamiento de XIT para avanzar en incrementos de 10 Hz.
   - Coloque el cursor sobre la caja de desplazamiento de XIT y gire la rueda del ratón para avanzar en incrementos de 10 Hz.
4. Para devolver el desplazamiento de TX a cero sin deshabilitar XIT, haga clic en XIT 0.
5. Para apagar XIT, haga clic en XIT nuevamente para que el botón deje de estar iluminado.

### Consejos

- RIT y XIT son independientes. Puede ejecutar ambos simultáneamente: RIT desplaza su frecuencia de recepción, XIT desplaza su frecuencia de transmisión, y la lectura del VFO permanece sin cambios.
- Para poner el desplazamiento a cero rápidamente antes de una transmisión, haga clic en XIT 0 en lugar de alternar XIT entre apagado y encendido.

### Solución de problemas

- **Los controles de XIT están atenuados** — La radio no está conectada. Use `Settings > Connect to Radio...` para establecer una conexión y luego intente nuevamente.
- **La frecuencia de TX no se desplaza como se espera** — Confirme que el segmento correcto esté seleccionado usando las pestañas de segmento (A..H). XIT actúa solo sobre el segmento actualmente vinculado.

---

## Pestañas de segmento (A..H)

La fila de pestañas de segmento en la parte superior del applet le permite seleccionar a qué segmento está vinculado el applet. Cada segmento tiene su propio color que persiste entre sesiones. El mismo color se refleja en los widgets de VFO y las tiras de medidor para ese segmento.

- Haga clic en un botón de pestaña (A..H) para vincular el applet a ese segmento.
- La fila de pestañas se oculta si la radio admite solo un segmento.
- Al reconectar, la fila de pestañas se reconstruye correctamente cuando cambia el número de segmentos disponibles. El controlador de clic que emite `sliceActivationRequested` se conecta solo una vez por instancia del applet, independientemente de cuántas veces se reconstruya la fila de pestañas.
- Las conexiones de clic de los botones de segmento están protegidas contra manejadores de señales duplicados entre reconexiones. `clearSliceButtons()` desmantela todos los botones de pestaña generados y restaura la insignia de segmento estática al desconectarse.

## Insignia de segmento

La insignia de segmento en la esquina superior izquierda del applet muestra la letra del segmento actualmente vinculado (A a H) con su color de identidad de segmento. La insignia admite renderizado de texto enriquecido (HTML) para accesibilidad o requisitos de visualización especiales.

## 🔓 / 🔒 (Bloqueo de sintonía)

Alterna el bloqueo de sintonía en el segmento. Cuando está bloqueado, el segmento ignora los cambios de frecuencia.

## ANT1 (Antena de RX)

Abre un menú que lista las antenas de recepción disponibles. El menú usa la lista dedicada `rxAntennaList()` del segmento cuando está disponible, recurriendo a la lista global de antenas del panadapter. Si un administrador de KiwiSDR está activo, los tokens de antena virtual del KiwiSDR se agregan a las opciones del menú — estos se verifican contra el perfil de KiwiSDR asignado al segmento actual. Seleccionar una antena virtual emite una señal `kiwiRxAntennaSelected` con el ID del segmento y el ID del perfil; seleccionar una antena Flex real emite `flexRxAntennaSelected` y llama a `setRxAntenna()` en el segmento. Etiqueta de color azul.

## ANT1 (Antena de TX)

Abre un menú que lista las antenas con capacidad de TX. Los puertos de antena solo-RX (prefijo "RX") se filtran. Etiqueta de color rojo.

## 2.7K (Ancho de filtro)

Muestra el ancho de banda del filtro del segmento actual. La lectura se comparte con el panel de VFO y usa lógica consciente del modo para que los modos SSB y digitales muestren el ancho etiquetado correcto. El método `stepFilterWidth()` recorre la lista de presets de filtro por modo para ensanchar o estrechar la banda pasante, produciendo una geometría de bordes correcta según el modo.

## QSK

Se ilumina en ámbar cuando el break-in de CW (QSK) está activo. Solo lectura; controlado mediante el botón Breakin del applet de CW.

## TX (insignia)

Haga clic para establecer este segmento como el segmento de TX.

## Combo de modo

Selecciona el modo del segmento entre las opciones disponibles: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY. Si la compilación tiene soporte RADE, RADE también está disponible. Los modos DSTR y FreeDV se filtran cuando el modelo no los admite.

Al cambiar de modo:
- Cambiar a RTTY o modos digitales (DIGU, DIGL) desactiva automáticamente el squelch, que de otro modo recortaría los caracteres FSK y rompería la decodificación.
- Al salir del modo RADE, el applet emite una señal de desactivación solo si el segmento estaba realmente en modo RADE, evitando señales de desactivación obsoletas al cambiar de modo en un segmento sin RADE.
- Seleccionar cualquier modo de radio real desmantela automáticamente la superposición del demodulador de software WFM si estaba ejecutándose en este segmento (consulte la sección del botón WFM).
- La configuración del modo CW ahora usa una lista única de modos CW mediante `isCwMode()`, por lo que el modo CWL recibe correctamente los mismos presets de filtro CW y tamaños de paso que CW. Anteriormente solo coincidía la cadena literal de modo "CW".

## Botón WFM

Un botón de alternancia etiquetado "WFM" aparece inmediatamente después del combo de modo. Activa o desactiva el demodulador de FM por software, que usa audio DAX IQ enrutado a través del cable Hi-Fi. Esto no es un modo de radio sino una superposición del lado del cliente.

- Haga clic para alternar el demodulador WFM entre encendido y apagado.
- Cuando está activo, el botón se resalta con un fondo verde.
- Información sobre herramientas: "Software FM demodulator via DAX IQ → Hi-Fi Cable"
- Seleccionar cualquier modo del combo de modo desactiva automáticamente WFM en ese segmento.
- El estado de WFM se sincroniza entre reconexiones: si la conexión de radio se cae y se restablece, el botón refleja el estado de WFM previamente activo.

## Etiqueta de frecuencia

Muestra la frecuencia actual del VFO con agrupación de puntos. Haga clic para cambiar al modo de edición. Accesibilidad: la etiqueta de frecuencia emite eventos de cambio de valor accesibles cuando la frecuencia mostrada cambia, permitiendo que los lectores de pantalla anuncien la nueva frecuencia.

## Edición de frecuencia

Ingrese una frecuencia en MHz y presione Enter para sintonizar y re-centrar. Admite auto-escalado de kHz/Hz. La entrada se normaliza de modo que solo el primer punto se conserva como separador decimal; cualquier punto adicional se elimina. Escape cancela la entrada, restaura la frecuencia anterior y cierra el editor. Consciente de XVTR: acepta hasta 50,000 MHz cuando el segmento está en una antena XVTR. El campo de texto es un widget `FreqLineEdit` con una etiqueta de sugerencia "MHz" en lugar de texto de marcador de posición. En 2m/70cm (100–999 MHz), una conveniencia de inserción de dígitos formatea valores como 1446 como 144.6.

## STEP

Cicla a través de los tamaños de paso por modo usando los botones < / > o la rueda del ratón. La lista de pasos depende del modo del segmento. La señal `stepSizeChangedByUser` se emite junto con `stepSizeChanged` para distinguir los cambios de paso iniciados por el usuario de los programáticos.

## Presets de ancho de filtro

Haga clic para aplicar un ancho de filtro preset. Haga clic derecho para guardar el ancho actual como preset. Los botones se ocultan para los modos FM/NFM/DFM. Los presets son por modo.

El método `stepFilterWidth()` recorre la lista de presets de filtro por modo para ensanchar o estrechar la banda pasante, produciendo una geometría de bordes correcta según el modo. El modo CW tiene seis presets (50, 100, 250, 400, 500, 600 Hz).

Los presets de filtro guardados pueden almacenar un valor de ancho de banda simple o un par explícito de borde bajo/borde alto (por ejemplo, `300:3000`).

## Widget de banda pasante del filtro

Arrastre los bordes lo/hi para ajustar la banda pasante del filtro.

## Modo de tono (FM)

Selecciona el modo de tono CTCSS en FM/NFM/DFM. Visible solo en modos de la familia FM.

## Valor de tono CTCSS

Selecciona la frecuencia de tono CTCSS enviada con la transmisión. Habilitado solo cuando el modo de tono es CTCSS TX.

La lista de tonos ahora incluye los 41 tonos estándar EIA/TIA-603. Los tonos que no tienen una letra de designación CTCSS estándar se muestran solo por frecuencia (por ejemplo, "69.3") en lugar de omitirse. Esto incluye 69.3, 159.8, 165.5, 171.3, 177.3, 183.5, 189.9, 196.6 y 199.5 Hz.

## Offset (FM)

Establece la frecuencia de offset del repetidor FM en MHz (0.0–100.0 MHz, paso 0.1).

## −, Símplex, + (dirección del offset)

Establece la dirección del offset del repetidor hacia abajo, símplex o hacia arriba.

## REV / XFC

Para operación de repetidor FM, REV invierte el signo del offset de TX para trabajar un par de repetidor invertido. En backends que admiten una verificación de frecuencia de transmisión, el botón se re-etiqueta como XFC: al presionarlo mantiene la verificación de frecuencia de transmisión durante la duración de la pulsación, y mientras se mantiene presionado fuerza brevemente la radio hacia la frecuencia de transmisión para confirmar la cobertura.

- El botón normalmente alterna REV (marcable).
- Cuando el backend de radio conectado anuncia `hasTransmitFrequencyCheck`, el botón se convierte en un botón momentáneo XFC. Presionarlo emite `setTransmitFrequencyCheck(true)`; soltarlo vuelve a la normalidad.
- El XFC mantenido se libera al ocultar, desactivar, cambio de capacidad o desconexión.

## 🔊 / 🔇 (Silencio)

Un solo clic silencia/activa el sonido de este segmento (diferido por el intervalo de discriminación de clic de la plataforma, configurable en `Radio Setup → Slice Controls`). Doble clic silencia/activa el sonido de todos los segmentos propiedad del usuario. La acción se difiere por el intervalo de doble clic de la plataforma para que un doble clic pueda anular un solo clic.

El estado de silencio NO se guarda ni se restaura al reconectar — la radio es la fuente de verdad para el estado de silencio de audio. El ícono de silencio se actualiza solo cuando la radio confirma el cambio de estado de silencio.

## Ganancia de AF

Ajusta la ganancia de salida de audio del segmento (0-100).

## Pan L / R

Distribuye el audio del segmento entre los canales izquierdo (0) y derecho (100). Doble clic restablece a 50 (centro). El relleno del deslizador se ancla desde el centro hacia afuera para que el operador pueda ver la posición neutral de un vistazo. Un pequeño punto de marca central se dibuja en la ranura.

## SQL / AUTO

Botón de ciclo de tres posiciones: cada clic avanza Apagado → SQL (umbral manual) → AUTO (el algoritmo rastrea el piso de ruido) → Apagado. En modo AUTO el botón muestra "AUTO" en ámbar; en modo manual "SQL" en verde.

- Manual y Auto ambos activan el squelch de la radio.
- El algoritmo de squelch automático reside en el panadapter; el nivel es el margen en dB por encima del piso de ruido medido.
- Reflejado por un botón idéntico en la pestaña Audio del panel de VFO.
- Deshabilitado (y auto-apagado) en modos RTTY y digitales (DIGU, DIGL) donde el squelch recortaría los caracteres FSK.

## Nivel de squelch

Ajusta el umbral de squelch. Solo tiene efecto cuando el squelch está activado. Deshabilitado en modos RTTY y digitales.

- Modo manual: 0-100 (autoritativo por segmento según la radio; el nivel no se persiste en el lado del cliente).
- Modo auto: margen de 5-20 dB por encima del piso de ruido medido; persistido en `AutoSqlMarginDb`.
- Haga clic derecho en el deslizador de umbral AGC para la calibración de ruido AGC-T.

## Modo AGC

Establece el modo AGC del segmento (Off, Slow, Med, Fast). Oculto en modos de la familia FM.

## Umbral AGC

Establece el umbral AGC (o el nivel de apagado de AGC cuando el modo AGC es Off). La información sobre herramientas refleja qué valor se está ajustando. Además, la información sobre herramientas anuncia la función de calibración con clic derecho: "Right-click to calibrate against the noise floor."

Haga clic derecho en el deslizador de umbral AGC para abrir un menú contextual con la opción "Calibrate AGC-T against noise floor…". Seleccionar esto emite una señal `calibrateAgcTRequested` para el segmento actual, que abre el panel de calibración de ruido AGC-T (deshabilitado mientras una recepción de reemplazo Kiwi esté activa).

## Menú contextual de calibración AGC-T

El deslizador de umbral AGC tiene un menú contextual con clic derecho que proporciona acceso al panel de calibración de ruido:

1. Haga clic derecho en el deslizador de umbral AGC.
2. Seleccione "Calibrate AGC-T against noise floor…" del menú contextual.
3. Se abre el panel de calibración, permitiéndole establecer el umbral AGC basado en el piso de ruido medido.

Esta característica le ayuda a establecer el umbral AGC con mayor precisión para su entorno operativo. El menú contextual solo está disponible cuando un segmento está vinculado al applet.

## RIT

Alterna la Sintonización Incremental de Recepción entre encendido y apagado.

## RIT 0

Pone el offset de RIT a cero.

## Offset RIT

Ajusta el offset de RIT en pasos de 10
