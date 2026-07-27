# Extraer un panadaptador a su propia ventana

Cuando tiene más de un panadaptador abierto, puede desacoplar cualquiera de ellos en una ventana flotante separada. Esto es útil para colocar el panadaptador en un segundo monitor o redimensionarlo independientemente del diseño principal de AetherSDR.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El botón de extracción solo está disponible cuando hay una conexión activa con la radio.
- Abra al menos un panadaptador adicional. En el modo de un solo panadaptador, el botón de extracción está oculto.

## Pasos

1. Localice la barra de título en la parte superior del panadaptador que desea desacoplar. Muestra la etiqueta del slice (por ejemplo, **Slice A**) y una fila de botones pequeños a la derecha.
2. Haga clic en el botón **⬈** en esa barra de título.

   El panadaptador se desacopla en una ventana flotante sin marco.

3. Para mover la ventana flotante, haga clic y arrastre la barra de título en la parte superior de la ventana flotante.
4. Para redimensionar la ventana flotante, arrastre el control de tamaño en su esquina inferior derecha.
5. Para acoplar la ventana de nuevo al diseño principal, haga clic en el botón **↩** en la barra de título de la ventana flotante.

## Qué hace cada control

| Control           | Descripción                                                                               | Predeterminado |
|-------------------|-------------------------------------------------------------------------------------------|----------------|
| **⬈** (extraer)   | Desacopla el panadaptador en una ventana flotante.                                        | —              |
| **↩** (acoplar)   | Devuelve el panadaptador flotante al diseño principal.                                    | —              |
| **□** (maximizar) | Expande este panadaptador para llenar el área principal.                                  | —              |
| **×** (cerrar)    | Cierra este panadaptador.                                                                 | —              |
| Título del slice  | Indicador que muestra qué slice está vinculado a este panadaptador (Slice A hasta Slice H). | Slice A        |

> **Nota para sesiones Multi-Flex:** Cuando se usan múltiples clientes, el título del slice coincide con la letra de índice proporcionada por la radio, de modo que el título corresponda a la insignia del slice.

## Panel de decodificación CW

Cuando el panel de decodificación CW está abierto, aparece debajo del espectro y el waterfall. El panel decodifica código Morse desde el audio de PC enrutado a AetherSDR. Tanto el CW recibido (RX) como el transmitido (TX) se decodifican y muestran en el mismo panel, con diferentes colores para distinguirlos.

> **Nota:** La decodificación CW requiere que el enrutamiento de audio de PC esté activo. Si no hay audio enrutado, el panel muestra la sugerencia **(requires PC Audio)**.

### Controles del panel de decodificación CW

| Control | Descripción | Predeterminado | Notas |
|---|---|---|---|
| **Etiqueta de estadísticas CW** | Muestra el tono y la velocidad detectados, por ejemplo `750 Hz  20 WPM`. | — | Solo lectura; se actualiza continuamente mediante el decodificador. |
| **Control deslizante Sens** | Filtra decodificaciones de baja confianza. Los valores más altos son más estrictos. | 30 | Asigna el rango 0–100 a un umbral de costo de 1.0–0.1. Se guarda como `CwDecoderSensitivity`. |
| **🔒P (Lock Pitch)** | Bloquea el tono del decodificador en la frecuencia sintonizada actual. | Off | Alternable. |
| **🔒S (Lock Speed)** | Bloquea la velocidad del decodificador en la lectura de WPM actual. | Off | Alternable. |
| **Control deslizante de rango Pitch** | Establece el tono mínimo y máximo que busca el decodificador. | 500–700 Hz | Rango: 300–1200 Hz. Control deslizante de doble manija que reemplaza los controles separados **Lo** y **Hi**. |
| **Control deslizante de rango WPM** | Establece la velocidad mínima y máxima que busca el decodificador. | 15–40 WPM | Rango: 5–60 WPM. |
| **CPY ALL** | Copia todo el texto decodificado al portapapeles. | — | — |
| **CPY VIS** | Copia solo el texto actualmente visible en el área de desplazamiento. | — | — |
| **A-** | Disminuye el tamaño de fuente del texto decodificado en 1 píxel. | — | Se conserva entre sesiones mediante `CwDecodeSettings::fontPx`. Rango: 8–32 px. |
| **A+** | Aumenta el tamaño de fuente del texto decodificado en 1 píxel. | — | Se conserva entre sesiones mediante `CwDecodeSettings::fontPx`. Rango: 8–32 px. |
| **CLR** | Limpia el búfer de decodificación CW. | — | — |
| **✕ (cerrar CW)** | Oculta el panel de decodificación CW. | — | — |
| **Texto de decodificación CW** | Visualización continua de solo lectura del CW decodificado, coloreado según la confianza de decodificación. | — | Verde: costo < 0.15; Amarillo: costo < 0.35; Naranja: costo < 0.60; Rojo: costo ≥ 0.60. El texto originado en TX aparece en cian (#5fc8ff). |
| **Control de arrastre** (tira delgada en la parte superior del panel CW) | Arrastre hacia arriba o hacia abajo para redimensionar la altura del panel de decodificación CW. | — | Cursor de tamaño vertical. La altura del panel se conserva mediante `CwDecodeSettings::panelHeight`. Rango: 60–600 px. |

### Comportamiento del texto de decodificación CW

El panel de decodificación CW ahora muestra tanto la decodificación Morse recibida (RX) como la transmitida (TX) en una sola área de texto continuo:

- **Texto RX** — Coloreado según la confianza como se describió anteriormente (verde, amarillo, naranja, rojo).
- **Texto TX** — Renderizado en cian (#5fc8ff) para que pueda distinguir su propio envío del CW entrante.
- **Manejo de límites** — Al alternar entre TX y RX, se inserta un espacio automáticamente para que las ejecuciones de color no se fusionen visualmente.
- **Seguimiento de fuente** — El decodificador rastrea si el último texto decodificado provino de TX o RX para aplicar la lógica de separador correcta.

### Menú contextual del texto de decodificación CW

Al hacer clic derecho dentro del área de **CW decode text**, se abre un menú contextual. El menú contiene las acciones estándar de edición de texto (Select All, Copy, etc.) seguidas de un separador y un elemento **Clear**. Al hacer clic en **Clear** en el menú contextual, se obtiene el mismo efecto que al hacer clic en el botón **CLR**: vacía el búfer de decodificación inmediatamente.

### Tamaño de fuente del panel de decodificación CW

El tamaño de fuente del texto decodificado es de 13 píxeles de forma predeterminada. Use los botones **A-** y **A+** para disminuir o aumentar el tamaño de fuente en 1 píxel por clic. El tamaño está limitado al rango de 8 a 32 píxeles y se conserva entre sesiones mediante la configuración `CwDecodeSettings`.

### Altura del panel de decodificación CW

Arrastre el delgado control de agarre horizontal en la parte superior del panel de decodificación CW hacia arriba o hacia abajo para redimensionar la altura del panel. La altura está limitada al rango de 60 a 600 píxeles y se conserva entre sesiones mediante la configuración `CwDecodeSettings`. Un panel más alto revela más historial de texto decodificado.

## Congelación del waterfall durante la transmisión

Cuando cualquier cliente en una sesión Multi-Flex comienza a transmitir, el waterfall en este panadaptador se congela automáticamente. Se reanuda la actualización cuando finaliza la transmisión. Esto elimina el artefacto de estela de TX de 10 a 23 segundos que aparecía anteriormente después de dejar de transmitir.

Al reconectar la radio, el panadaptador reafirma la frecuencia de cuadro deseada y la duración de la línea del waterfall para evitar caer silenciosamente a los 10 Hz predeterminados de la radio.

Los panadaptadores secundarios (Slices B–H) tienen su rango de dBm preparado al reconectarse, de modo que el ajuste automático del piso de ruido comience desde la línea base correcta en lugar del rango predeterminado [-50, +50] que causaba un espectro plano al reconectar.

## Panel de decodificación RTTY

Cuando el modo del slice activo es RTTY o DIGL, aparece un panel de decodificación RTTY debajo del espectro y el waterfall. Este panel decodifica señales RTTY desde el audio de PC enrutado a AetherSDR. El panel tiene una altura fija de 90 píxeles y está oculto cuando el modo del slice no es RTTY o DIGL.

> **Nota:** La decodificación RTTY requiere que el enrutamiento de audio de PC esté activo.

## Compatibilidad con temas

La barra de título del panadaptador, el panel de decodificación CW, el panel de decodificación RTTY y todos los controles asociados ahora utilizan tokens de color compatibles con temas (sujetos a cambios en versiones futuras). La apariencia visual se adapta al tema activo sin necesidad de anulaciones de estilo manuales.

## Consejos

- La ventana flotante no tiene marco. Use la barra de título dentro de la aplicación para arrastrarla y el control de tamaño en la esquina inferior derecha para redimensionarla. No hay borde de ventana del sistema operativo.
- Las etiquetas de los botones ⬈ y ↩ cambian para reflejar el estado actual: ⬈ cuando está acoplado, ↩ cuando está flotando.
- Use el control deslizante de rango **Pitch** para acotar el rango de tono de la señal que está copiando. Reducir el rango reduce las decodificaciones falsas cuando hay múltiples señales CW presentes.
- Use el control deslizante de rango **WPM** para acotar el rango de velocidad de la señal que está copiando. Reducir el rango reduce las decodificaciones falsas cuando hay múltiples señales CW presentes.
- Para borrar el texto decodificado rápidamente, haga clic derecho en el área de texto de decodificación y seleccione **Clear** en lugar de buscar el botón **CLR**.
- El texto decodificado del lado TX aparece en cian para ayudarle a distinguir su propio envío del CW entrante, sin necesidad de un prefijo textual.
- Use los botones **A-** y **A+** para ajustar el tamaño de fuente del texto decodificado para una mejor legibilidad.
- Arrastre el delgado control de agarre en la parte superior del panel de decodificación CW para revelar más historial de texto decodificado.

## Solución de problemas

- **El botón ⬈ no es visible** — Solo tiene un panadaptador abierto. Los botones de extraer, maximizar y cerrar están ocultos en el modo de un solo panadaptador. Abra un panadaptador adicional para que aparezcan.
- **La ventana flotante no se puede mover** — Haga clic y arrastre la barra de título dentro de la ventana flotante, no el área del espectro. El área del espectro se utiliza para la sintonización.
- **El área de texto de decodificación CW no muestra texto** — Verifique que el audio de PC esté enrutado a AetherSDR. El panel muestra **(requires PC Audio)** cuando el audio no está disponible.

## Relacionados

- [Maximizar un panadaptador para llenar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cerrar un panadaptador adicional](close-an-extra-panadapter.md)
- [Hacer clic en el espectro para activar un panadaptador (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Descripción general del panadaptador](overview.md)
