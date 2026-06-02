# Resumen del panadaptador

El panadaptador muestra un espectro FFT en tiempo real y un waterfall para una slice de radio, permitiéndole visualizar la actividad en la banda y sintonizar haciendo clic o arrastrando. Cada panadaptador también puede mostrar un panel opcional de decodificación CW que lee el código Morse directamente en la aplicación.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panadaptador requiere una conexión de radio activa.
- Para la decodificación CW, se debe configurar el enrutamiento de audio del PC a AetherSDR. El panel muestra un recordatorio "(requires PC Audio)" cuando esto no está configurado.

## Cómo funciona

AetherSDR se abre con un panadaptador visible en el centro de la ventana principal. Siempre está presente; no puede cerrar el último panadaptador. En modo multi-slice, aparecen panadaptadores adicionales, cada uno en su propio contenedor con título. Cada panadaptador está vinculado a una slice (Slice A a Slice H), que se muestra en la barra de título. En sesiones Multi-Flex, el título usa la letra de índice proporcionada por la radio para que coincida con la insignia de la slice.

**Espectro y waterfall.** La parte superior del panadaptador muestra la traza del espectro FFT; debajo está el waterfall. Haga clic en cualquier lugar del espectro o del waterfall para activar ese panadaptador. Arrastre para desplazarse por la banda. Desplace la rueda del ratón para acercar o alejar. Los elementos de menú `View > Single-Click to Tune` y `View > Pan Follows VFO` afectan cómo el clic y el desplazamiento interactúan con el VFO.

**Barra de título.** La barra de título de 16 píxeles en la parte superior de cada panadaptador lleva la etiqueta de la slice, un asa de arrastre y (en modo multi-slice) los botones de desacoplar, maximizar y cerrar. En modo de un solo panel, esos tres botones están ocultos. La barra de título utiliza tokens de color conscientes del tema para el fondo degradado y las etiquetas de texto.

**Comportamiento de congelación del waterfall.** Cuando cualquier cliente conectado comienza a transmitir, el waterfall se congela automáticamente. Se descongela cuando la transmisión se detiene, eliminando el artefacto de la estela de TX de 10 a 23 segundos que aparecía anteriormente después de desactivar la transmisión.

**Comportamiento de reconexión.** Al reconectar la radio, los FPS del panadaptador y la duración de la línea del waterfall se reafirman para evitar que se reduzcan silenciosamente al valor predeterminado de 10 Hz de la radio.

**Panel de decodificación CW.** Un panel opcional puede aparecer debajo del waterfall. Ejecuta un decodificador Morse fuera del aire y muestra el texto decodificado en un campo de solo lectura con desplazamiento, codificado por colores según la confianza del decodificador. El panel está oculto por defecto y se habilita desde los controles del modo CW. Consulte [Turn on the CW decoder to read Morse off-air](turn-on-the-cw-decoder-to-read-morse-off-air.md).

## Qué hace cada control

### Barra de título

| Control | Tipo | Comportamiento | Notas |
|---|---|---|---|
| Título de la slice | Indicador | Muestra la slice vinculada a este panadaptador. Valores: Slice A – Slice H. En sesiones Multi-Flex, usa la letra de índice proporcionada por la radio. | — |
| ⬈ / ↩ (desacoplar/acoplar) | Botón | Desacopla el panadaptador en una ventana flotante, o lo acopla de nuevo. | Oculto en modo de un solo panel. La ventana flotante no tiene marco; arrastre mediante la barra de título de la aplicación, redimensione mediante el asa de tamaño en la esquina inferior derecha. En macOS, los recursos de GPU se restablecen en cada ciclo de desacoplamiento/acoplamiento para mantener el espectro activo. |
| □ (maximizar) | Botón | Maximiza este panadaptador para llenar el área de diseño principal. | Oculto en modo de un solo panel. |
| × (cerrar) | Botón | Cierra este panadaptador. | Oculto en modo de un solo panel. |

### Espectro / waterfall

| Control | Tipo | Comportamiento |
|---|---|---|
| Espectro / waterfall | Área de visualización y arrastre | Haga clic para activar el panadaptador. Arrastre para desplazarse. Desplace la rueda para acercar/alejar. |

### Panel de decodificación CW

| Control | Tipo | Valor predeterminado | Rango válido | Clave de ajuste | Comportamiento |
|---|---|---|---|---|---|
| Etiqueta de estadísticas CW | Indicador | — | `<hz> Hz  <wpm> WPM` | — | Muestra el tono y la velocidad detectados actualmente por el decodificador. |
| Sens | Deslizador | 30 | 0 – 100 | `CwDecoderSensitivity` | Filtra decodificaciones de baja confianza. Los valores más altos son más estrictos. Internamente asigna el rango 0 – 100 a un umbral de costo de 1.0 – 0.1. Utiliza el estilo de deslizador temático mediante `applyPrimarySliderStyle`. |
| 🔒P (Lock Pitch) | Botón de alternancia | Desactivado | Activado / Desactivado | — | Bloquea el tono del decodificador a la frecuencia sintonizada actualmente. |
| 🔒S (Lock Speed) | Botón de alternancia | Desactivado | Activado / Desactivado | — | Bloquea la velocidad del decodificador a la lectura actual de WPM. |
| Lo (tono mínimo) | Deslizador | 500 Hz | 300 – 1200 Hz | — | Establece el tono mínimo que busca el decodificador. Limitado para no ser mayor que Hi. |
| Hi (tono máximo) | Deslizador | 700 Hz | 300 – 1200 Hz | — | Establece el tono máximo que busca el decodificador. Limitado para no ser menor que Lo. |
| CPY ALL | Botón | — | — | — | Copia todo el búfer de texto decodificado al portapapeles. |
| CPY VIS | Botón | — | — | — | Copia solo el texto actualmente visible en el área de desplazamiento al portapapeles. |
| CLR | Botón | — | — | — | Limpia el búfer de decodificación CW. |
| × (cerrar CW) | Botón | — | — | — | Oculta el panel de decodificación CW. |
| Texto de decodificación CW | Campo de texto de solo lectura | — | — | — | Visualización continua de Morse decodificado, codificado por colores según la confianza: verde (costo <0.15), amarillo (<0.35), naranja (<0.60), rojo (>=0.60). Haga clic derecho en el área de texto para abrir un menú contextual; el menú incluye acciones de texto estándar y un elemento **Clear** que limpia el búfer de decodificación. |

### Decodificación CW del lado TX

Cuando su propia señal transmitida se enruta de vuelta a través del audio del PC a AetherSDR, el decodificador también puede mostrar su Morse transmitido. Su texto transmitido aparece en un color cian distintivo (#5fc8ff) para diferenciarlo de las señales recibidas. Se inserta automáticamente un espacio separador entre el texto recibido y el transmitido, y entre el texto transmitido y el recibido, para evitar que las secuencias de color se fusionen visualmente.

| Comportamiento | Detalle |
|---|---|
| Color del texto TX | Cian (#5fc8ff) |
| Inserción de separador | Espacio automático añadido en las transiciones TX→RX y RX→TX |
| Filtro de confianza | El mismo umbral del deslizador `Sens` se aplica tanto a la ruta de recepción como a la de transmisión |

## Integración con temas

Todos los elementos visuales del panadaptador ahora utilizan tokens de color conscientes del tema en lugar de valores hexadecimales fijos:

- **Contenedor:** El widget del panadaptador está registrado en el sistema de temas como `applet/panadapter`.
- **Degradado de la barra de título:** Utiliza los tokens `{{color.text.disabled}}`, `{{color.background.1}}`.
- **Puntos del asa de arrastre:** Utiliza el token `{{color.text.label}}`.
- **Título de la slice:** Utiliza el token `{{color.text.secondary}}`.
- **Fondo del panel CW:** Utiliza los tokens `{{color.background.0}}` y `{{color.background.1}}`.
- **Título CW:** Utiliza el token `{{color.accent}}`.
- **Indicación CW:** Utiliza el token `{{color.meter.bar.fill}}`.
- **Etiqueta de estadísticas CW:** Utiliza el token `{{color.text.label}}`.
- **Deslizador de sensibilidad:** Diseñado mediante `applyPrimarySliderStyle()`.

Esto asegura que la apariencia del panadaptador se adapte al tema seleccionado sin necesidad de anulaciones de color manuales.

## Consejos

- Los deslizadores de tono Lo y Hi limitan el rango de frecuencia que busca el decodificador. Reducir este rango alrededor del tono CW esperado reduce las falsas decodificaciones en una banda concurrida.
- El color del texto decodificado refleja la confianza del decodificador. El texto verde es el más confiable; el texto rojo debe tratarse con precaución. Ajuste Sens hacia arriba para suprimir caracteres rojos y naranjas si el ruido produce resultados no deseados.
- `CwDecoderSensitivity` se conserva entre sesiones. No es necesario reajustarlo cada vez que abre la aplicación.
- Puede limpiar el búfer de decodificación desde el menú contextual con clic derecho (sin necesidad de teclado) en el área de texto decodificado, como alternativa a hacer clic en CLR.
- Cuando vea CW transmitido y recibido en el mismo panel, el texto TX en color cian le ayuda a identificar su propia clave. No se añade ningún prefijo textual "[TX]"; el color por sí solo distingue la fuente.

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
