# Resumen del panadapter

El panadapter muestra un espectro FFT en tiempo real y un waterfall para un slice de radio, lo que le permite visualizar la actividad de la banda y sintonizar haciendo clic o arrastrando. Cada panadapter también puede mostrar un panel opcional de decodificación de CW que lee el código Morse directamente de la señal, y un panel opcional de decodificación de RTTY para modos RTTY/DIGL.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panadapter requiere una conexión activa con la radio.
- Para la decodificación de CW, se debe configurar el enrutamiento de audio de la PC a AetherSDR. El panel muestra un recordatorio "(requires PC Audio)" cuando esto no está configurado.

## Cómo funciona

AetherSDR se abre con un panadapter visible en el centro de la ventana principal. Siempre está presente; no puede cerrar el último panadapter. En el modo de múltiples slices, aparecen panadapters adicionales, cada uno en su propio contenedor con título. Cada panadapter está vinculado a un slice (Slice A a Slice H), que se muestra en la barra de título. En sesiones Multi-Flex, el título usa la letra de índice proporcionada por la radio para que coincida con la insignia del slice.

**Espectro y waterfall.** La parte superior del panadapter muestra la traza del espectro FFT; debajo está el waterfall. Haga clic en cualquier parte del espectro o del waterfall para activar ese panadapter. Arrastre para desplazarse por la banda. Desplace la rueda del ratón para hacer zoom. Los elementos de menú `View > Single-Click to Tune` y `View > Pan Follows VFO` afectan cómo los clics y el desplazamiento interactúan con el VFO.

**Barra de título.** La barra de título de 16 píxeles en la parte superior de cada panadapter lleva la etiqueta del slice, un asa de arrastre y (en modo de múltiples slices) los botones de desacoplar, maximizar y cerrar. En el modo de un solo panadapter, esos tres botones están ocultos. La barra de título utiliza tokens de color conscientes del tema para el fondo degradado y las etiquetas de texto. Cuando el panadapter está alojado en el lienzo del espacio de trabajo (RFC #4887), la barra de título actúa como el asa de arrastre para el gesto de movimiento en vivo.

**Comportamiento de congelación del waterfall.** La congelación del waterfall está controlada por el estado de transmisión de interbloqueo de la radio, no por el borde local de MOX. Cuando cualquier cliente conectado comienza a transmitir, el waterfall se congela automáticamente. Se descongela cuando la transmisión se detiene, eliminando el artefacto de estela de TX de 10 a 23 segundos que aparecía anteriormente después de desactivar la tecla. En sesiones Multi-Flex, cualquier cliente que transmita activa la congelación.

**Comportamiento de reconexión.** Al reconectar la radio, se reafirman los FPS del panadapter y la duración de línea del waterfall para evitar que caigan silenciosamente al valor predeterminado de 10 Hz de la radio. Además, los panadapters secundarios (Slices B–H) tienen su rango de dBm preparado en la reconexión para que el ajuste automático del piso de ruido comience desde la línea base correcta en lugar del rango predeterminado [-50, +50] que causaba un espectro plano en la reconexión.

**Panel de decodificación de CW.** Un panel opcional puede aparecer debajo del waterfall. Ejecuta un decodificador de Morse de la señal y muestra el texto decodificado en un campo de solo lectura dinámico, con código de colores según la confianza del decodificador. El panel está oculto por defecto y se habilita desde los controles del modo CW. Consulte [Turn on the CW decoder to read Morse off-air](turn-on-the-cw-decoder-to-read-morse-off-air.md).

**Panel de decodificación de RTTY.** Un panel opcional puede aparecer debajo del waterfall cuando el modo del slice es RTTY o DIGL. Muestra el texto RTTY decodificado en un campo de solo lectura dinámico. El panel está oculto por defecto y se habilita desde los controles del modo RTTY/DIGL.

**Vista 3D de FFT.** Una vista de espectro 3D (nueva en v26.7.x) muestra el historial de la señal como una superficie 3D que se desplaza hacia adelante con sombras de elevación, límites de desplazamiento suave y un piso resincronizado después del zoom de ancho de banda. Las banderas de slice proyectan sombras de elevación en caché. Actívela con el botón **3D FFT view** en la barra de título.

## Qué hace cada control

### Barra de título

| Control | Tipo | Comportamiento | Notas |
|---|---|---|---|
| Título del slice | Indicador | Muestra el slice vinculado a este panadapter. Valores: Slice A – Slice H. En sesiones Multi-Flex, usa la letra de índice proporcionada por la radio. | — |
| ⬈ / ↩ (desacoplar/acoplar) | Botón | Desacopla el panadapter en una ventana flotante, o lo vuelve a acoplar. | Oculto en modo de un solo panadapter. Cuando el panadapter está en el lienzo del espacio de trabajo, este botón siempre es visible incluso si es el único panadapter. La ventana flotante no tiene marco; arrastre mediante la tira de título de la aplicación, redimensione mediante el asa de tamaño en la esquina inferior derecha. En macOS, los recursos de GPU se restablecen en cada ciclo de desacoplar/acoplar para mantener el espectro activo. El estado guardado de la ventana flotante no se restaura cuando se agregan panadapters posteriores, lo que evita que aparezca una ventana flotante en blanco. |
| □ (maximizar) | Botón | Maximiza este panadapter para llenar el área de diseño principal. | Oculto en modo de un solo panadapter. |
| × (cerrar) | Botón | Cierra este panadapter. | Oculto en modo de un solo panadapter. |
| 3D FFT view | Botón de alternancia | Alterna la vista de espectro FFT 3D. | Nuevo en v26.7.x. Parte del widget de espectro. |

### Espectro / waterfall

| Control | Tipo | Comportamiento |
|---|---|---|
| Espectro / waterfall | Área de visualización y arrastre | Haga clic para activar el panadapter. Arrastre para desplazarse. Desplace la rueda del ratón para hacer zoom. |

### Arrastre del lienzo de la barra de título

Cuando el panadapter es un elemento en el lienzo del espacio de trabajo (no acoplado en la pila), la barra de título transmite un gesto de movimiento en vivo.

| Comportamiento | Detalle |
|---|---|
| Umbral de arrastre | 6 px separan un clic (que activa el panadapter) de un arrastre |
| Clic | Presionar y soltar sin exceder el umbral activa el panadapter |
| Arrastre | Moverse más allá del umbral inicia el gesto de movimiento en vivo; la sesión del lienzo sigue la barra de título hasta que se suelta |
| Conflicto con modo flotante | Mutuamente excluyente con el modo flotante, cuya maquinaria de movimiento sin marco tiene prioridad |

### Panel de decodificación de CW

| Control | Tipo | Predeterminado | Rango válido | Clave de ajuste | Comportamiento |
|---|---|---|---|---|---|
| Etiqueta de estadísticas de CW | Indicador | — | `<hz> Hz  <wpm> WPM` | — | Muestra el tono y la velocidad detectados actualmente por el decodificador. |
| Asa de redimensionamiento | Área de arrastre | — | 60–600 px (altura del panel) | — | Una tira delgada de 4 píxeles en la parte superior del panel de decodificación de CW. Arrastre hacia arriba o hacia abajo para redimensionar el panel y revelar más historial de texto decodificado. Reemplaza la altura fija anterior de 80 píxeles. |
| Sens | Control deslizante | 30 | 0 – 100 | `CwDecoderSensitivity` | Filtra decodificaciones de baja confianza. Los valores más altos son más estrictos. Internamente mapea el rango de 0 – 100 a un umbral de costo de 1.0 – 0.1. Utiliza el estilo de control deslizante del tema mediante `applyPrimarySliderStyle`. |
| 🔒P (Lock Pitch) | Botón de alternancia | Desactivado | Activado / Desactivado | — | Bloquea el tono del decodificador a la frecuencia sintonizada actualmente. |
| 🔒S (Lock Speed) | Botón de alternancia | Desactivado | Activado / Desactivado | — | Bloquea la velocidad del decodificador a la lectura actual de WPM. |
| Lo (mín. de tono) | Control deslizante | 500 | 300–1200 Hz | — | Tono mínimo que busca el decodificador. Limitado para ser ≤ Hi. |
| Hi (máx. de tono) | Control deslizante | 700 | 300–1200 Hz | — | Tono máximo que busca el decodificador. Limitado para ser ≥ Lo. |
| WPM (control deslizante de rango) | Control deslizante de rango | 15 – 40 WPM | 5 – 60 WPM | — | Establece la velocidad mínima y máxima (WPM) que busca el decodificador. Utiliza un control deslizante de doble asa. |
| A- (Disminuir fuente) | Botón | — | — | — | Disminuye el tamaño de fuente del texto decodificado en un paso. Los valores se conservan entre sesiones. |
| A+ (Aumentar fuente) | Botón | — | — | — | Aumenta el tamaño de fuente del texto decodificado en un paso. Los valores se conservan entre sesiones. |
| CPY ALL | Botón | — | — | — | Copia el búfer completo de texto decodificado al portapapeles. |
| CPY VIS | Botón | — | — | — | Copia solo el texto actualmente visible en el área de desplazamiento al portapapeles. |
| CLR | Botón | — | — | — | Borra el búfer de decodificación de CW. |
| × (cerrar CW) | Botón | — | — | — | Oculta el panel de decodificación de CW. |
| Texto de decodificación de CW | Campo de texto de solo lectura | — | — | — | Visualización dinámica del Morse decodificado, con código de colores según la confianza. El tamaño de fuente es ajustable por el usuario (consulte los botones A- / A+). Haga clic derecho en el área de texto para abrir un menú contextual; el menú incluye acciones de texto estándar y un elemento **Clear** que borra el búfer de decodificación. |

### Colores de confianza de decodificación de CW

| Color | Rango de costo | Significado |
|---|---|---|
| Verde | <0.15 | Confianza alta |
| Amarillo | 0.15–0.34 | Confianza moderada |
| Naranja | 0.35–0.59 | Confianza baja |
| Rojo | >=0.60 | Confianza baja, tratar con precaución |

### Decodificación de CW del lado de TX

Cuando su propia señal transmitida se enruta de vuelta a través del audio de la PC a AetherSDR, el decodificador también puede mostrar su Morse transmitido. Su texto transmitido aparece en un color cian distintivo (#5fc8ff) para diferenciarlo de las señales recibidas. Se inserta automáticamente un espacio separador entre el texto de recepción y el de transmisión, y entre el de transmisión y el de recepción, para evitar que las secuencias de colores se fusionen visualmente.

| Comportamiento | Detalle |
|---|---|
| Color del texto de TX | Cian (#5fc8ff) |
| Inserción de separador | Espacio automático añadido en las transiciones TX→RX y RX→TX |
| Filtro de confianza | El mismo umbral del control deslizante `Sens` se aplica a las rutas de recepción y transmisión |

### Panel de decodificación de RTTY

| Control | Tipo | Predeterminado | Rango válido | Clave de ajuste | Comportamiento |
|---|---|---|---|---|---|
| CPY ALL | Botón | — | — | — | Copia el búfer completo de texto RTTY decodificado al portapapeles. |
| CPY VIS | Botón | — | — | — | Copia solo el texto RTTY actualmente visible en el área de desplazamiento al portapapeles. |
| CLR | Botón | — | — | — | Borra el búfer de decodificación de RTTY. |
| × (cerrar RTTY) | Botón | — | — | — | Oculta el panel de decodificación de RTTY. |
| Texto de decodificación de RTTY | Campo de texto de solo lectura | — | — | — | Visualización dinámica de los caracteres RTTY decodificados. Haga clic derecho en el área de texto para abrir un menú contextual; el menú incluye acciones de texto estándar y un elemento **Clear** que borra el búfer de decodificación. |

## Integración con el tema

Todos los elementos visuales del panadapter ahora utilizan tokens de color conscientes del tema en lugar de valores hex codificados:

- **Contenedor:** El widget del panadapter está registrado en el sistema de temas como `applet/panadapter`.
- **Degradado de la barra de título:** Utiliza los tokens `{{color.text.disabled}}`, `{{color.background.1}}`.
- **Puntos del asa de arrastre:** Utiliza el token `{{color.text.label}}`.
- **Título del slice:** Utiliza el token `{{color.text.secondary}}`.
- **Fondo del panel de CW:** Utiliza los tokens `{{color.background.0}}` y `{{color.background.1}}`.
- **Asa de redimensionamiento de CW:** Utiliza el token `{{color.background.2}}`.
- **Título de CW:** Utiliza el token `{{color.accent}}`.
- **Sugerencia de CW:** Utiliza el token `{{color.meter.bar.fill}}`.
- **Etiqueta de estadísticas de CW:** Utiliza el token `{{color.text.label}}`.
- **Control deslizante de sensibilidad:** Con estilo mediante `applyPrimarySliderStyle()`.

Esto garantiza que la apariencia del panadapter se adapte al tema seleccionado sin anulaciones manuales de color.

## Consejos

- Los controles deslizantes de tono Lo/Hi limitan el rango de frecuencia que busca el decodificador. Estrechar este rango alrededor del tono de CW esperado reduce las decodificaciones falsas en una banda concurrida.
- El control deslizante de rango de WPM limita el rango de velocidad que busca el decodificador. Estrechar este rango alrededor de la velocidad de envío esperada reduce las decodificaciones falsas.
- El color del texto decodificado refleja la confianza del decodificador. El texto verde es el más confiable; el texto rojo debe tratarse con precaución. Ajuste Sens hacia arriba para suprimir los caracteres rojos y naranjas si el ruido está produciendo salida basura.
- `CwDecoderSensitivity` se conserva entre sesiones. No es necesario reajustarlo cada vez que abre la aplicación.
- La altura del panel de decodificación de CW y el tamaño de fuente se conservan entre sesiones. Use el asa de redimensionamiento en la parte superior del panel para ajustar la altura, y los botones A- / A+ para ajustar el tamaño de fuente.
- Puede borrar el búfer de decodificación desde el menú contextual sin teclado con clic derecho en el área de texto decodificado, como alternativa a hacer clic en CLR.
- Al ver CW transmitido y recibido en el mismo panel, el texto de TX en cian le ayuda a identificar su propia manipulación de tecla. No se añade ningún prefijo textual "[TX]" — solo el color distingue la fuente.
- El panel de decodificación de RTTY aparece automáticamente cuando el modo del slice se establece en R
