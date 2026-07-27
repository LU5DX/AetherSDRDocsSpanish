# Resumen del Panadapter

El panadapter muestra un espectro FFT en tiempo real y un waterfall para un slice de radio, permitiéndole visualizar la actividad de la banda y sintonizar haciendo clic o arrastrando. Cada panadapter también puede mostrar un panel opcional de decodificación CW que lee el código Morse al aire directamente en la aplicación, y un panel opcional de decodificación RTTY para modos RTTY/DIGL.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panadapter requiere una conexión de radio activa.
- Para la decodificación CW, se debe configurar el enrutamiento de audio del PC a AetherSDR. El panel muestra un recordatorio "(requires PC Audio)" cuando esto no está configurado.

## Cómo funciona

AetherSDR se abre con un panadapter visible en el centro de la ventana principal. Siempre está presente; no puede cerrar el último panadapter. En modo multislices, aparecen panadapters adicionales, cada uno en su propio contenedor con título. Cada panadapter está vinculado a un slice (Slice A a Slice H), que se muestra en la barra de título. En sesiones Multi-Flex, el título usa la letra de índice proporcionada por la radio para que coincida con la insignia del slice.

**Espectro y waterfall.** La parte superior del panadapter muestra la traza del espectro FFT; debajo está el waterfall. Haga clic en cualquier lugar del espectro o del waterfall para activar ese panadapter. Arrastre para desplazarse por la banda. Desplace la rueda del ratón para hacer zoom. Los elementos de menú `View > Single-Click to Tune` y `View > Pan Follows VFO` afectan cómo el clic y el desplazamiento interactúan con el VFO.

**Barra de título.** La barra de título de 16 píxeles en la parte superior de cada panadapter lleva la etiqueta del slice, un asa de arrastre y (en modo multislices) los botones de desacoplar, maximizar y cerrar. En modo de un solo pan, estos tres botones están ocultos. La barra de título utiliza tokens de color conscientes del tema para el fondo degradado y las etiquetas de texto.

**Comportamiento de congelación del waterfall.** Cuando cualquier cliente conectado comienza a transmitir, el waterfall se congela automáticamente. Se descongela cuando la transmisión se detiene, eliminando el artefacto de estela de TX de 10 a 23 segundos que aparecía anteriormente después de desactivar la tecla.

**Comportamiento de reconexión.** Al reconectar la radio, los FPS del panadapter y la duración de la línea del waterfall se reafirman para evitar caer silenciosamente al valor predeterminado de 10 Hz de la radio. Además, los panadapters secundarios (Slices B–H) tienen su rango de dBm preparado en la reconexión para que el ajuste automático del piso de ruido comience desde la línea base correcta en lugar del rango predeterminado [-50, +50] que causaba un espectro plano en la reconexión.

**Panel de decodificación CW.** Un panel opcional puede aparecer debajo del waterfall. Ejecuta un decodificador Morse al aire y muestra el texto decodificado en un campo rodante de solo lectura, con código de colores según la confianza del decodificador. El panel está oculto de forma predeterminada y se habilita desde los controles del modo CW. Consulte [Activar el decodificador CW para leer Morse al aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).

**Panel de decodificación RTTY.** Un panel opcional puede aparecer debajo del waterfall cuando el modo del slice es RTTY o DIGL. Muestra el texto RTTY decodificado en un campo rodante de solo lectura. El panel está oculto de forma predeterminada y se habilita desde los controles del modo RTTY/DIGL.

## Qué hace cada control

### Barra de título

| Control | Tipo | Comportamiento | Notas |
|---|---|---|---|
| Título del slice | Indicador | Muestra el slice vinculado a este panadapter. Valores: Slice A – Slice H. En sesiones Multi-Flex, usa la letra de índice proporcionada por la radio. | — |
| ⬈ / ↩ (desacoplar/acoplar) | Botón | Desacopla el panadapter en una ventana flotante, o lo acopla de nuevo. | Oculto en modo de un solo pan. La ventana flotante no tiene marco; arrastre mediante la tira de título interna de la aplicación, redimensione mediante el asa de redimensionamiento en la parte inferior derecha. En macOS, los recursos de GPU se reinician en cada ciclo de flotación/acoplamiento para mantener el espectro activo. |
| □ (maximizar) | Botón | Maximiza este panadapter para llenar el área de diseño principal. | Oculto en modo de un solo pan. |
| × (cerrar) | Botón | Cierra este panadapter. | Oculto en modo de un solo pan. |

### Espectro / waterfall

| Control | Tipo | Comportamiento |
|---|---|---|
| Espectro / waterfall | Área de visualización y arrastre | Haga clic para activar el panadapter. Arrastre para desplazarse. Desplace la rueda del ratón para hacer zoom. |

### Panel de decodificación CW

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|---|
| Etiqueta de estadísticas CW | Indicador | — | `<hz> Hz  <wpm> WPM` | — | Muestra el tono y la velocidad detectados actualmente por el decodificador. |
| Asa de redimensionamiento | Área de arrastre | — | 60–600 px (altura del panel) | — | Una tira delgada de 4 píxeles en la parte superior del panel de decodificación CW. Arrastre hacia arriba o hacia abajo para redimensionar el panel y revelar más historial de texto decodificado. Reemplaza la altura fija anterior de 80 píxeles. |
| Sens | Deslizador | 30 | 0 – 100 | `CwDecoderSensitivity` | Filtra decodificaciones de baja confianza. Los valores más altos son más estrictos. Internamente asigna el rango 0 – 100 a un umbral de costo de 1.0 – 0.1. Utiliza estilo de deslizador temático mediante `applyPrimarySliderStyle`. |
| 🔒P (Lock Pitch) | Botón de alternancia | Desactivado | Activado / Desactivado | — | Bloquea el tono del decodificador en la frecuencia actualmente sintonizada. |
| 🔒S (Lock Speed) | Botón de alternancia | Desactivado | Activado / Desactivado | — | Bloquea la velocidad del decodificador en la lectura actual de WPM. |
| Pitch (deslizador de rango) | Deslizador de rango | 500 – 700 Hz | 300 – 1200 Hz | — | Establece el tono mínimo y máximo que busca el decodificador. Utiliza un deslizador de dos mangos; Lo y Hi se ajustan juntos. |
| WPM (deslizador de rango) | Deslizador de rango | 15 – 40 WPM | 5 – 60 WPM | — | Establece la velocidad mínima y máxima (WPM) que busca el decodificador. Utiliza un deslizador de dos mangos. |
| A- (Disminuir fuente) | Botón | — | — | — | Disminuye el tamaño de fuente del texto decodificado en un paso. Los valores se conservan entre sesiones. |
| A+ (Aumentar fuente) | Botón | — | — | — | Aumenta el tamaño de fuente del texto decodificado en un paso. Los valores se conservan entre sesiones. |
| CPY ALL | Botón | — | — | — | Copia todo el búfer de texto decodificado al portapapeles. |
| CPY VIS | Botón | — | — | — | Copia solo el texto actualmente visible en el área de desplazamiento al portapapeles. |
| CLR | Botón | — | — | — | Limpia el búfer de decodificación CW. |
| × (cerrar CW) | Botón | — | — | — | Oculta el panel de decodificación CW. |
| Texto de decodificación CW | Campo de texto de solo lectura | — | — | — | Visualización rodante de código Morse decodificado, con código de colores según la confianza. El tamaño de fuente es ajustable por el usuario (consulte los botones A- / A+). Haga clic derecho en el área de texto para abrir un menú contextual; el menú incluye acciones de texto estándar y un elemento **Clear** que limpia el búfer de decodificación. |

### Colores de confianza de decodificación CW

| Color | Rango de costo | Significado |
|---|---|---|
| Verde | <0.15 | Alta confianza |
| Amarillo | 0.15–0.34 | Confianza moderada |
| Naranja | 0.35–0.59 | Confianza baja |
| Rojo | >=0.60 | Confianza muy baja, tratar con precaución |

### Decodificación CW del lado de TX

Cuando su propia señal transmitida se enruta de vuelta a través del audio del PC a AetherSDR, el decodificador también puede mostrar su código Morse transmitido. Su texto transmitido aparece en un color cian distintivo (#5fc8ff) para diferenciarlo de las señales recibidas. Se inserta automáticamente un espacio separador entre el texto de recepción y el de transmisión, y entre el texto de transmisión y el de recepción, para evitar que las ejecuciones de color se fusionen visualmente.

| Comportamiento | Detalle |
|---|---|
| Color del texto TX | Cian (#5fc8ff) |
| Inserción de separador | Espacio automático añadido en las transiciones TX→RX y RX→TX |
| Filtro de confianza | El mismo umbral del deslizador `Sens` se aplica a las rutas de recepción y transmisión |

### Panel de decodificación RTTY

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|---|
| CPY ALL | Botón | — | — | — | Copia todo el búfer de texto RTTY decodificado al portapapeles. |
| CPY VIS | Botón | — | — | — | Copia solo el texto RTTY actualmente visible en el área de desplazamiento al portapapeles. |
| CLR | Botón | — | — | — | Limpia el búfer de decodificación RTTY. |
| × (cerrar RTTY) | Botón | — | — | — | Oculta el panel de decodificación RTTY. |
| Texto de decodificación RTTY | Campo de texto de solo lectura | — | — | — | Visualización rodante de caracteres RTTY decodificados. Haga clic derecho en el área de texto para abrir un menú contextual; el menú incluye acciones de texto estándar y un elemento **Clear** que limpia el búfer de decodificación. |

## Integración de temas

Todos los elementos visuales del panadapter ahora utilizan tokens de color conscientes del tema en lugar de valores hexadecimales codificados:

- **Contenedor:** El widget del panadapter está registrado con el sistema de temas como `applet/panadapter`.
- **Degradado de la barra de título:** Utiliza tokens `{{color.text.disabled}}`, `{{color.background.1}}`.
- **Puntos del asa de arrastre:** Utiliza el token `{{color.text.label}}`.
- **Título del slice:** Utiliza el token `{{color.text.secondary}}`.
- **Fondo del panel CW:** Utiliza tokens `{{color.background.0}}` y `{{color.background.1}}`.
- **Asa de redimensionamiento CW:** Utiliza el token `{{color.background.2}}`.
- **Título CW:** Utiliza el token `{{color.accent}}`.
- **Sugerencia CW:** Utiliza el token `{{color.meter.bar.fill}}`.
- **Etiqueta de estadísticas CW:** Utiliza el token `{{color.text.label}}`.
- **Deslizador de sensibilidad:** Estilizado mediante `applyPrimarySliderStyle()`.

Esto asegura que la apariencia del panadapter se adapte al tema seleccionado sin necesidad de anulaciones manuales de color.

## Consejos

- El deslizador de rango de Pitch limita el rango de frecuencia que busca el decodificador. Reducir este rango alrededor del tono CW esperado reduce las falsas decodificaciones en una banda concurrida.
- El deslizador de rango de WPM limita el rango de velocidad que busca el decodificador. Reducir este rango alrededor de la velocidad de envío esperada reduce las falsas decodificaciones.
- El color del texto decodificado refleja la confianza del decodificador. El texto verde es el más fiable; el texto rojo debe tratarse con precaución. Ajuste Sens hacia arriba para suprimir los caracteres rojos y naranjas si el ruido produce salida basura.
- `CwDecoderSensitivity` se conserva entre sesiones. No necesita reajustarlo cada vez que abre la aplicación.
- La altura del panel de decodificación CW y el tamaño de fuente se conservan entre sesiones. Use el asa de redimensionamiento en la parte superior del panel para ajustar la altura, y los botones A- / A+ para ajustar el tamaño de fuente.
- Puede limpiar el búfer de decodificación desde el menú contextual de clic derecho sin teclado en el área de texto decodificado, como alternativa a hacer clic en CLR.
- Al ver tanto CW transmitido como recibido en el mismo panel, el texto TX en cian le ayuda a identificar su propia manipulación. No se añade ningún prefijo textual "[TX]" — el color solo distingue la fuente.
- El panel de decodificación RTTY aparece automáticamente cuando el modo del slice se establece en RTTY o DIGL.

## Relacionados

- [Activar el decodificador CW para leer Morse al aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento es bueno](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
- [Desacoplar un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Maximizar un panadapter para llenar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Hacer clic en el espectro para activar un panadapter (modo multislices)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Comprender los slices y VFOs](../../getting-started/concepts/understanding-slices.md)
