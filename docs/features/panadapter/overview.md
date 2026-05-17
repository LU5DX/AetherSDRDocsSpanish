# Descripción general del panadapter

El panadapter muestra un espectro FFT en tiempo real y un waterfall para un slice de radio, permitiéndole visualizar la actividad en la banda y sintonizar haciendo clic o arrastrando. Cada panadapter también puede mostrar un panel opcional de decodificación CW que lee el código Morse directamente en la aplicación.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panadapter requiere una conexión de radio activa.
- Para la decodificación CW, se debe configurar el enrutamiento de audio del PC a AetherSDR. El panel muestra un recordatorio "(requires PC Audio)" cuando esto no está configurado.

## Cómo funciona

AetherSDR se abre con un panadapter visible en el centro de la ventana principal. Siempre está presente; no puede cerrar el último panadapter. En el modo de múltiples slices, aparecen panadapters adicionales, cada uno en su propio contenedor con título. Cada panadapter está vinculado a un slice (Slice A a Slice H), que se muestra en la barra de título. En sesiones Multi-Flex, el título usa la letra de índice proporcionada por la radio para que coincida con la etiqueta del slice.

**Espectro y waterfall.** La parte superior del panadapter muestra la traza del espectro FFT; debajo se encuentra el waterfall. Haga clic en cualquier parte del espectro o del waterfall para activar ese panadapter. Arrastre para desplazarse por la banda. Use la rueda del ratón para hacer zoom. Los elementos de menú `View > Single-Click to Tune` y `View > Pan Follows VFO` afectan la forma en que los clics y el desplazamiento interactúan con el VFO.

**Barra de título.** La barra de título de 16 píxeles en la parte superior de cada panadapter contiene la etiqueta del slice, un asa de arrastre y (en modo de múltiples slices) los botones de desacoplar, maximizar y cerrar. En el modo de un solo pan, estos tres botones están ocultos.

**Comportamiento de congelación del waterfall.** Cuando cualquier cliente conectado comienza a transmitir, el waterfall se congela automáticamente. Se descongela cuando la transmisión se detiene, eliminando el artefacto de la estela de TX de 10 a 23 segundos que aparecía anteriormente después de soltar la tecla.

**Comportamiento de reconexión.** Al reconectar la radio, se reafirman los FPS del panadapter y la duración de la línea del waterfall para evitar que se reduzcan silenciosamente al valor predeterminado de 10 Hz de la radio.

**Panel de decodificación CW.** Un panel opcional puede aparecer debajo del waterfall. Ejecuta un decodificador Morse fuera del aire y muestra el texto decodificado en un campo de solo lectura con desplazamiento, codificado por colores según la confianza del decodificador. El panel está oculto por defecto y se habilita desde los controles del modo CW. Consulte [Activar el decodificador CW para leer Morse fuera del aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).

## Qué hace cada control

### Barra de título

| Control | Tipo | Comportamiento | Notas |
|---|---|---|---|
| Título del slice | Indicador | Muestra el slice vinculado a este panadapter. Valores: Slice A – Slice H. En sesiones Multi-Flex, usa la letra de índice proporcionada por la radio. | — |
| ⬈ / ↩ (desacoplar/acoplar) | Botón | Desacopla el panadapter en una ventana flotante, o lo vuelve a acoplar. | Oculto en modo de un solo pan. La ventana flotante no tiene marco; arrastre mediante la barra de título dentro de la aplicación, redimensione mediante el asa de tamaño en la esquina inferior derecha. En macOS, los recursos de GPU se restablecen en cada ciclo de flotación/acoplamiento para mantener el espectro activo. |
| □ (maximizar) | Botón | Maximiza este panadapter para llenar el área de diseño principal. | Oculto en modo de un solo pan. |
| × (cerrar) | Botón | Cierra este panadapter. | Oculto en modo de un solo pan. |

### Espectro / waterfall

| Control | Tipo | Comportamiento |
|---|---|---|
| Espectro / waterfall | Área de visualización y arrastre | Haga clic para activar el panadapter. Arrastre para desplazarse. Use la rueda del ratón para hacer zoom. |

### Panel de decodificación CW

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|---|
| Etiqueta de estadísticas CW | Indicador | — | `<hz> Hz  <wpm> WPM` | — | Muestra el tono y la velocidad detectados actualmente por el decodificador. |
| Sens | Deslizador | 30 | 0 – 100 | `CwDecoderSensitivity` | Filtra las decodificaciones de baja confianza. Los valores más altos son más estrictos. Internamente, asigna el rango de 0 – 100 a un umbral de costo de 1.0 – 0.1. |
| 🔒P (Bloquear tono) | Botón de alternancia | Apagado | Encendido / Apagado | — | Bloquea el tono del decodificador a la frecuencia sintonizada actualmente. |
| 🔒S (Bloquear velocidad) | Botón de alternancia | Apagado | Encendido / Apagado | — | Bloquea la velocidad del decodificador a la lectura actual de WPM. |
| Lo (tono mínimo) | Deslizador | 500 Hz | 300 – 1200 Hz | — | Establece el tono mínimo que busca el decodificador. Se limita para no ser mayor que Hi. |
| Hi (tono máximo) | Deslizador | 700 Hz | 300 – 1200 Hz | — | Establece el tono máximo que busca el decodificador. Se limita para no ser menor que Lo. |
| CPY ALL | Botón | — | — | — | Copia todo el búfer de texto decodificado al portapapeles. |
| CPY VIS | Botón | — | — | — | Copia solo el texto actualmente visible en el área de desplazamiento al portapapeles. |
| CLR | Botón | — | — | — | Borra el búfer de decodificación CW. |
| × (cerrar CW) | Botón | — | — | — | Oculta el panel de decodificación CW. |
| Texto de decodificación CW | Campo de texto de solo lectura | — | — | — | Visualización rodante del Morse decodificado, codificado por colores según la confianza: verde (costo <0.15), amarillo (<0.35), naranja (<0.60), rojo (>=0.60). Haga clic derecho en el área de texto para abrir un menú contextual; el menú incluye acciones de texto estándar y un elemento **Clear** que borra el búfer de decodificación. |

### Decodificación CW del lado de TX

Cuando su propia señal transmitida se enruta de vuelta a través del audio del PC a AetherSDR, el decodificador también puede mostrar su Morse transmitido. Su texto transmitido aparece en un color cian distintivo (#5fc8ff) para diferenciarlo de las señales recibidas. Se inserta automáticamente un espacio separador entre el texto de recepción y el de transmisión, y entre el texto de transmisión y el de recepción, para evitar que las secuencias de colores se fusionen visualmente.

| Comportamiento | Detalle |
|---|---|
| Color del texto TX | Cian (#5fc8ff) |
| Inserción de separador | Espacio automático añadido en las transiciones TX→RX y RX→TX |
| Filtro de confianza | El mismo umbral del deslizador `Sens` se aplica tanto a las rutas de recepción como a las de transmisión |

## Consejos

- Los deslizadores de tono Lo y Hi limitan el rango de frecuencias que busca el decodificador. Reducir este rango alrededor del tono CW esperado reduce las decodificaciones falsas en una banda ocupada.
- El color del texto decodificado refleja la confianza del decodificador. El texto verde es el más fiable; el texto rojo debe tratarse con precaución. Ajuste Sens hacia arriba para suprimir los caracteres rojos y naranjas si el ruido produce resultados basura.
- `CwDecoderSensitivity` se conserva entre sesiones. No es necesario reajustarlo cada vez que abra la aplicación.
- Puede borrar el búfer de decodificación desde el menú contextual con clic derecho (sin teclado) en el área de texto decodificado, como alternativa a hacer clic en CLR.
- Al visualizar tanto CW transmitido como recibido en el mismo panel, el texto TX en color cian le ayuda a identificar su propia manipulación. No se añade ningún prefijo textual "[TX]": el color por sí solo distingue la fuente.

## Relacionados

- [Activar el decodificador CW para leer Morse fuera del aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento sea bueno](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
- [Desacoplar un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Maximizar un panadapter para llenar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Hacer clic en el espectro para activar un panadapter (modo de múltiples slices)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Comprender los slices y los VFO](../../getting-started/concepts/understanding-slices.md)
