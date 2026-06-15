# Visión general del panadapter

El panadapter muestra un espectro FFT en tiempo real y un waterfall para un slice de radio, permitiéndole visualizar la actividad de la banda y sintonizar haciendo clic o arrastrando. Cada panadapter también puede mostrar un panel opcional de decodificación CW que lee el código Morse directamente en la aplicación, y un panel opcional de decodificación RTTY para modos RTTY/DIGL.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panadapter requiere una conexión de radio activa.
- Para la decodificación CW, se debe configurar el enrutamiento de audio del PC a AetherSDR. El panel muestra un recordatorio "(requires PC Audio)" cuando esto no está configurado.

## Cómo funciona

AetherSDR se abre con un panadapter visible en el centro de la ventana principal. Siempre está presente; no puede cerrar el último panadapter. En el modo de múltiples slices, aparecen panadapters adicionales, cada uno en su propio contenedor con título. Cada panadapter está vinculado a un slice (Slice A a Slice H), que se muestra en la barra de título. En sesiones Multi-Flex, el título utiliza la letra de índice proporcionada por la radio para que coincida con la etiqueta del slice.

**Espectro y waterfall.** La parte superior del panadapter muestra la traza del espectro FFT; debajo está el waterfall. Haga clic en cualquier lugar del espectro o del waterfall para activar ese panadapter. Arrastre para desplazarse por la banda. Desplace la rueda del ratón para hacer zoom. Los elementos del menú `View > Single-Click to Tune` y `View > Pan Follows VFO` afectan la forma en que los clics y el desplazamiento interactúan con el VFO.

**Barra de título.** La barra de título de 16 píxeles en la parte superior de cada panadapter lleva la etiqueta del slice, un asa de arrastre y (en el modo de múltiples slices) los botones de desacoplar, maximizar y cerrar. En el modo de un solo pan, esos tres botones están ocultos. La barra de título utiliza tokens de color según el tema para el fondo degradado y las etiquetas de texto.

**Comportamiento de congelación del waterfall.** Cuando cualquier cliente conectado comienza a transmitir, el waterfall se congela automáticamente. Se descongela cuando la transmisión se detiene, eliminando el artefacto de estela de TX de 10 a 23 segundos que antes aparecía después de desactivar la transmisión.

**Comportamiento en reconexión.** Tras una reconexión de la radio, se reafirman los FPS del panadapter y la duración de la línea del waterfall para evitar que caigan silenciosamente al valor predeterminado de 10 Hz de la radio.

**Panel de decodificación CW.** Un panel opcional puede aparecer debajo del waterfall. Ejecuta un decodificador Morse fuera del aire y muestra el texto decodificado en un campo de solo lectura con desplazamiento, codificado por colores según la confianza del decodificador. El panel está oculto por defecto y se habilita desde los controles del modo CW. Consulte [Turn on the CW decoder to read Morse off-air](turn-on-the-cw-decoder-to-read-morse-off-air.md).

**Panel de decodificación RTTY.** Un panel opcional puede aparecer debajo del waterfall cuando el modo del slice es RTTY o DIGL. Muestra el texto RTTY decodificado en un campo de solo lectura con desplazamiento. El panel está oculto por defecto y se habilita desde los controles del modo RTTY/DIGL.

## Qué hace cada control

### Barra de título

| Control | Tipo | Comportamiento | Notas |
|---|---|---|---|
| Título del slice | Indicador | Muestra el slice vinculado a este panadapter. Valores: Slice A – Slice H. En sesiones Multi-Flex, utiliza la letra de índice proporcionada por la radio. | — |
| ⬈ / ↩ (desacoplar/acoplar) | Botón | Desacopla el panadapter en una ventana flotante, o lo acopla de nuevo. | Oculto en el modo de un solo pan. La ventana flotante no tiene marco; arrastre mediante la barra de título dentro de la aplicación, redimensione mediante el asa de tamaño en la esquina inferior derecha. En macOS, los recursos de la GPU se reinician en cada ciclo de flotación/acoplamiento para mantener el espectro activo. |
| □ (maximizar) | Botón | Maximiza este panadapter para llenar el área de diseño principal. | Oculto en el modo de un solo pan. |
| × (cerrar) | Botón | Cierra este panadapter. | Oculto en el modo de un solo pan. |

### Espectro / waterfall

| Control | Tipo | Comportamiento |
|---|---|---|
| Espectro / waterfall | Área de visualización y arrastre | Haga clic para activar el panadapter. Arrastre para desplazarse. Desplace la rueda del ratón para hacer zoom. |

### Panel de decodificación CW

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|---|
| Etiqueta de estadísticas CW | Indicador | — | `<hz> Hz  <wpm> WPM` | — | Muestra el tono y la velocidad detectados actualmente por el decodificador. |
| Sens | Deslizador | 30 | 0 – 100 | `CwDecoderSensitivity` | Filtra decodificaciones de baja confianza. Los valores más altos son más estrictos. Internamente asigna el rango 0 – 100 a un umbral de coste de 1.0 – 0.1. Utiliza el estilo de deslizador del tema mediante `applyPrimarySliderStyle`. |
| 🔒P (Lock Pitch) | Botón de alternancia | Apagado | On / Off | — | Bloquea el tono del decodificador a la frecuencia actualmente sintonizada. |
| 🔒S (Lock Speed) | Botón de alternancia | Apagado | On / Off | — | Bloquea la velocidad del decodificador a la lectura actual de WPM. |
| Pitch (deslizador de rango) | Deslizador de rango | 500 – 700 Hz | 300 – 1200 Hz | — | Establece el tono mínimo y máximo que busca el decodificador. Utiliza un deslizador de dos asas; Lo y Hi se ajustan juntos. |
| WPM (deslizador de rango) | Deslizador de rango | 15 – 40 WPM | 5 – 60 WPM | — | Establece la velocidad mínima y máxima (WPM) que busca el decodificador. Utiliza un deslizador de dos asas. |
| CPY ALL | Botón | — | — | — | Copia todo el búfer de texto decodificado al portapapeles. |
| CPY VIS | Botón | — | — | — | Copia solo el texto actualmente visible en el área de desplazamiento al portapapeles. |
| CLR | Botón | — | — | — | Borra el búfer de decodificación CW. |
| × (cerrar CW) | Botón | — | — | — | Oculta el panel de decodificación CW. |
| Texto de decodificación CW | Campo de texto de solo lectura | — | — | — | Visualización continua de Morse decodificado, codificado por colores según la confianza: verde (<0.15 de coste), amarillo (<0.35), naranja (<0.60), rojo (>=0.60). Haga clic derecho en el área de texto para abrir un menú contextual; el menú incluye acciones de texto estándar y un elemento **Clear** que borra el búfer de decodificación. |

### Decodificación CW del lado de TX

Cuando su propia señal transmitida se reenvía a través del audio del PC a AetherSDR, el decodificador también puede mostrar su Morse transmitido. Su texto transmitido aparece en un color cian distintivo (#5fc8ff) para diferenciarlo de las señales recibidas. Se inserta automáticamente un espacio separador entre el texto de recepción y el de transmisión, y entre el de transmisión y el de recepción, para evitar que las secuencias de colores se fusionen visualmente.

| Comportamiento | Detalle |
|---|---|
| Color del texto de TX | Cian (#5fc8ff) |
| Inserción de separador | Espacio automático añadido en las transiciones TX→RX y RX→TX |
| Filtro de confianza | El mismo umbral del deslizador `Sens` se aplica tanto a la recepción como a la transmisión |

### Panel de decodificación RTTY

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|---|
| CPY ALL | Botón | — | — | — | Copia todo el búfer de texto RTTY decodificado al portapapeles. |
| CPY VIS | Botón | — | — | — | Copia solo el texto RTTY actualmente visible en el área de desplazamiento al portapapeles. |
| CLR | Botón | — | — | — | Borra el búfer de decodificación RTTY. |
| × (cerrar RTTY) | Botón | — | — | — | Oculta el panel de decodificación RTTY. |
| Texto de decodificación RTTY | Campo de texto de solo lectura | — | — | — | Visualización continua de caracteres RTTY decodificados. Haga clic derecho en el área de texto para abrir un menú contextual; el menú incluye acciones de texto estándar y un elemento **Clear** que borra el búfer de decodificación. |

## Integración con temas

Todos los elementos visuales del panadapter ahora utilizan tokens de color según el tema en lugar de valores hexadecimales fijos:

- **Contenedor:** El widget del panadapter está registrado en el sistema de temas como `applet/panadapter`.
- **Degradado de la barra de título:** Utiliza tokens `{{color.text.disabled}}`, `{{color.background.1}}`.
- **Puntos del asa de arrastre:** Utiliza el token `{{color.text.label}}`.
- **Título del slice:** Utiliza el token `{{color.text.secondary}}`.
- **Fondo del panel CW:** Utiliza los tokens `{{color.background.0}}` y `{{color.background.1}}`.
- **Título CW:** Utiliza el token `{{color.accent}}`.
- **Indicación CW:** Utiliza el token `{{color.meter.bar.fill}}`.
- **Etiqueta de estadísticas CW:** Utiliza el token `{{color.text.label}}`.
- **Deslizador de sensibilidad:** Con estilo mediante `applyPrimarySliderStyle()`.

Esto asegura que la apariencia del panadapter se adapte al tema seleccionado sin anulaciones de color manuales.

## Consejos

- El deslizador de rango Pitch limita el rango de frecuencia que busca el decodificador. Reducir este rango alrededor del tono CW esperado reduce las decodificaciones falsas en una banda ocupada.
- El deslizador de rango WPM limita el rango de velocidad que busca el decodificador. Reducir este rango alrededor de la velocidad de envío esperada reduce las decodificaciones falsas.
- El color del texto decodificado refleja la confianza del decodificador. El texto verde es el más fiable; el texto rojo debe tratarse con precaución. Ajuste Sens hacia arriba para suprimir caracteres rojos y naranjas si el ruido produce resultados basura.
- `CwDecoderSensitivity` se conserva entre sesiones. No necesita reajustarlo cada vez que abre la aplicación.
- Puede borrar el búfer de decodificación desde el menú contextual con clic derecho (sin teclado) en el área de texto decodificado, como alternativa a hacer clic en CLR.
- Cuando visualice tanto CW transmitido como recibido en el mismo panel, el texto TX en cian le ayuda a identificar su propia manipulación. No se añade ningún prefijo textual "[TX]": el color solo distingue el origen.
- El panel de decodificación RTTY aparece automáticamente cuando el modo del slice se establece en RTTY o DIGL.

## Relacionados

- [Turn on the CW decoder to read Morse off-air](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Tune CW decoder sensitivity to reject noise](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Lock CW decoder pitch or speed once tracking is good](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copy decoded CW text to the clipboard](copy-decoded-cw-text-to-the-clipboard.md)
- [Pop a panadapter out into its own window](pop-a-panadapter-out-into-its-own-window.md)
- [Maximize one panadapter to fill the main area](maximize-one-panadapter-to-fill-the-main-area.md)
- [Close an extra panadapter](close-an-extra-panadapter.md)
- [Click the spectrum to activate a panadapter (multi-slice mode)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Understanding slices and VFOs](../../getting-started/concepts/understanding-slices.md)
