# Extraiga un panadapter a su propia ventana

Cuando tiene más de un panadapter abierto, puede desacoplar cualquiera de ellos en una ventana flotante separada. Esto es útil para colocar el panadapter en un segundo monitor o para redimensionarlo de forma independiente del diseño principal de AetherSDR.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El botón de extracción solo está disponible cuando hay una conexión de radio activa.
- Abra al menos un panadapter adicional. En el modo de un solo panadapter, el botón de extracción está oculto. Sin embargo, cuando un panadapter está colocado en el lienzo del espacio de trabajo, el botón de extracción está siempre disponible, sin importar cuántos panadapters estén abiertos.

## Pasos

1. Localice la barra de título en la parte superior del panadapter que desea desacoplar. Muestra la etiqueta del slice (por ejemplo, **Slice A**) y una fila de botones pequeños a la derecha.
2. Haga clic en el botón **⬈** en esa barra de título.

   El panadapter se desacopla en una ventana flotante sin marco.

3. Para mover la ventana flotante, haga clic y arrastre la franja de título en la parte superior de la ventana flotante.
4. Para redimensionar la ventana flotante, arrastre el controlador de tamaño en su esquina inferior derecha.
5. Para acoplar la ventana de nuevo al diseño principal, haga clic en el botón **↩** en la barra de título de la ventana flotante.

## Qué hace cada control

| Control           | Descripción                                                                          | Predeterminado |
|-------------------|--------------------------------------------------------------------------------------|----------------|
| **⬈** (extraer)   | Desacopla el panadapter en una ventana flotante.                                     | —              |
| **↩** (acoplar)   | Devuelve el panadapter flotante al diseño principal.                                 | —              |
| **□** (maximizar) | Expande este panadapter para llenar el área principal.                               | —              |
| **×** (cerrar)    | Cierra este panadapter.                                                              | —              |
| Título del slice  | Indicador que muestra qué slice está vinculado a este panadapter (Slice A a Slice H). | Slice A        |

> **Nota para sesiones Multi-Flex:** Al usar múltiples clientes, el título del slice coincide con la letra de índice proporcionada por la radio, de modo que el título corresponde a la insignia del slice.

## Modo lienzo del espacio de trabajo

Cuando un panadapter está colocado en el lienzo del espacio de trabajo (en lugar del diseño acoplado estándar), su barra de título se comporta de manera diferente:

- **Arrastrar para mover** — Haga clic y arrastre la barra de título para mover el panadapter por el lienzo. Un umbral de 6 píxeles separa un clic de un arrastre; después de ese umbral, el gesto es consumido por el lienzo y mueve el panadapter como un todo.
- **Clic para activar** — Un clic simple en la barra de título (sin arrastrar más allá del umbral de 6 píxeles) activa el panadapter.
- **Extracción siempre disponible** — El botón **⬈** (extraer) está siempre visible mientras un panadapter está en el lienzo, incluso si es el único panadapter abierto. Esto se debe a que la ocultación del botón en modo de un solo panadapter es una economía del diseño, no una restricción para flotar.
- **Mutualmente excluyente con flotación** — El modo de arrastre en lienzo solo se aplica cuando el panadapter no está flotando. Las ventanas flotantes usan el mecanismo de movimiento sin marco en su lugar.

## Panel de decodificación CW

Cuando el panel de decodificación CW está abierto, aparece debajo del espectro y el waterfall. El panel decodifica código Morse del audio de PC enrutado a AetherSDR. Tanto el CW recibido (RX) como el transmitido (TX) se decodifican y se muestran en el mismo panel, con diferentes colores para distinguirlos.

> **Nota:** La decodificación CW requiere que el enrutamiento de audio de PC esté activo. Si no se enruta audio, el panel muestra la pista **(requires PC Audio)**.

### Controles del panel de decodificación CW

| Control | Descripción | Predeterminado | Notas |
|---|---|---|---|
| **Etiqueta de estadísticas CW** | Muestra el tono y la velocidad detectados, por ejemplo `750 Hz  20 WPM`. | — | Solo lectura; actualizado continuamente por el decodificador. |
| **Control deslizante Sens** | Filtra decodificaciones de baja confianza. Los valores más altos son más estrictos. | 30 | Mapea el rango 0–100 a un umbral de costo de 1.0–0.1. Se guarda como `CwDecoderSensitivity`. |
| **🔒P** (Bloquear tono) | Bloquea el tono del decodificador a la frecuencia sintonizada actual. | Desactivado | Alternar. |
| **🔒S** (Bloquear velocidad) | Bloquea la velocidad del decodificador a la lectura actual de WPM. | Desactivado | Alternar. |
| **Control deslizante de rango Pitch** | Establece el tono mínimo y máximo que busca el decodificador. | 500–700 Hz | Rango: 300–1200 Hz. El control deslizante de doble manija reemplaza los controles separados **Lo** y **Hi**. |
| **Control deslizante de rango WPM** | Establece la velocidad mínima y máxima que busca el decodificador. | 15–40 WPM | Rango: 5–60 WPM. |
| **CPY ALL** | Copia todo el texto decodificado al portapapeles. | — | — |
| **CPY VIS** | Copia solo el texto actualmente visible en el área de desplazamiento. | — | — |
| **A-** | Disminuye el tamaño de fuente del texto decodificado en 1 píxel. | — | Se conserva entre sesiones mediante `CwDecodeSettings::fontPx`. Rango: 8–32 px. |
| **A+** | Aumenta el tamaño de fuente del texto decodificado en 1 píxel. | — | Se conserva entre sesiones mediante `CwDecodeSettings::fontPx`. Rango: 8–32 px. |
| **CLR** | Borra el búfer de decodificación CW. | — | — |
| **✕** (cerrar CW) | Oculta el panel de decodificación CW. | — | — |
| **Texto de decodificación CW** | Visualización continua de solo lectura del CW decodificado, coloreado según la confianza de decodificación. | — | Verde: costo < 0.15; amarillo: costo < 0.35; naranja: costo < 0.60; rojo: costo ≥ 0.60. El texto originado en TX aparece en cian (#5fc8ff). |
| **Controlador de arrastre** (franja delgada en la parte superior del panel CW) | Arrastre hacia arriba o hacia abajo para redimensionar la altura del panel de decodificación CW. | — | Cursor de tamaño vertical. La altura del panel se conserva mediante `CwDecodeSettings::panelHeight`. Rango: 60–600 px. |

### Comportamiento del texto de decodificación CW

El panel de decodificación CW ahora muestra tanto la decodificación Morse recibida (RX) como la transmitida (TX) en un área de texto continuo único:

- **Texto RX** — Coloreado por confianza como se describió anteriormente (verde, amarillo, naranja, rojo).
- **Texto TX** — Renderizado en cian (#5fc8ff) para que pueda distinguir su propio envío del CW entrante.
- **Manejo de límites** — Al cambiar entre TX y RX, se inserta un espacio automáticamente para que las secuencias de colores no se fusionen visualmente.
- **Seguimiento de origen** — El decodificador rastrea si el último texto decodificado provino de TX o RX para aplicar la lógica de separador correcta.

### Menú contextual del texto de decodificación CW

Al hacer clic derecho dentro del área de **texto de decodificación CW**, se abre un menú contextual. El menú contiene las acciones estándar de edición de texto (Select All, Copy, etc.) seguidas de un separador y un elemento **Clear**. Al hacer clic en **Clear** en el menú contextual se produce el mismo efecto que al hacer clic en el botón **CLR**: vacía el búfer de decodificación inmediatamente.

### Tamaño de fuente del panel de decodificación CW

El tamaño de fuente del texto decodificado tiene un valor predeterminado de 13 píxeles. Use los botones **A-** y **A+** para disminuir o aumentar el tamaño de fuente en 1 píxel por clic. El tamaño está limitado al rango de 8–32 píxeles y se conserva entre sesiones mediante la configuración `CwDecodeSettings`.

### Altura del panel de decodificación CW

Arrastre la franja horizontal delgada en la parte superior del panel de decodificación CW hacia arriba o hacia abajo para redimensionar la altura del panel. La altura está limitada al rango de 60–600 píxeles y se conserva entre sesiones mediante la configuración `CwDecodeSettings`. Un panel más alto revela más historial de texto decodificado.

## Vista 3D FFT

El panadapter incluye una vista de espectro 3D FFT opcional que muestra el historial de señales como una superficie 3D que se desplaza hacia adelante. Esta vista incluye:

- **Sombras de elevación** — Las banderas de slice y los picos de señal proyectan sombras de elevación almacenadas en caché sobre la superficie.
- **Límites de desplazamiento suave** — El historial se desplaza suavemente sin saltos de límites.
- **Resincronización del piso con zoom de ancho de banda** — El nivel del piso se resincroniza después de un zoom de ancho de banda para mantener una percepción de profundidad precisa.

Active o desactive la **vista 3D FFT** para habilitar o deshabilitar este modo de visualización. Es parte del widget de espectro y está deshabilitada de forma predeterminada.

## Congelación del waterfall durante la transmisión

Cuando cualquier cliente en una sesión Multi-Flex comienza a transmitir, el waterfall en este panadapter se congela automáticamente. Reanuda la actualización cuando finaliza la transmisión. Esto elimina el artefacto de rastro TX de 10–23 segundos que aparecía anteriormente después de soltar la tecla. La congelación es impulsada por el interlock (TRANSMITTING) de la radio, por lo que se aplica sin importar qué cliente inicie la transmisión.

Al reconectarse la radio, el panadapter reafirma la frecuencia de cuadros deseada y la duración de línea del waterfall para evitar caer silenciosamente a los 10 Hz predeterminados de la radio.

Los panadapters secundarios (Slices B–H) tienen su rango de dBm preparado al reconectarse para que el ajuste automático del piso de ruido comience desde la línea base correcta en lugar del rango predeterminado [-50, +50] que causaba un espectro plano al reconectarse.

## Panel de decodificación RTTY

Cuando el modo del slice activo es RTTY o DIGL, aparece un panel de decodificación RTTY debajo del espectro y el waterfall. Este panel decodifica señales RTTY del audio de PC enrutado a AetherSDR. El panel tiene una altura fija de 90 píxeles y se oculta cuando el modo del slice no es RTTY o DIGL.

> **Nota:** La decodificación RTTY requiere que el enrutamiento de audio de PC esté activo.

## Soporte de temas

La barra de título del panadapter, el panel de decodificación CW, el panel de decodificación RTTY y todos los controles asociados ahora usan tokens de color conscientes del tema (sujetos a cambios en futuras versiones). La apariencia visual se adapta al tema activo sin necesidad de anulaciones de estilo manuales.

## Consejos

- La ventana flotante no tiene marco. Use la franja de título dentro de la aplicación para arrastrarla y el controlador de tamaño en la esquina inferior derecha para redimensionarla. No hay borde de ventana del sistema operativo.
- Las etiquetas de los botones ⬈ y ↩ cambian para reflejar el estado actual: ⬈ cuando está acoplado, ↩ cuando está flotando.
- Use el **control deslizante de rango Pitch** para acotar el rango de tono de la señal que está copiando. Reducir el rango disminuye las decodificaciones falsas cuando hay múltiples señales CW presentes.
- Use el **control deslizante de rango WPM** para acotar el rango de velocidad de la señal que está copiando. Reducir el rango disminuye las decodificaciones falsas cuando hay múltiples señales CW presentes.
- Para borrar el texto decodificado rápidamente, haga clic derecho en el área de texto decodificado y seleccione **Clear** en lugar de buscar el botón **CLR**.
- El texto decodificado del lado TX aparece en cian para ayudarle a distinguir su propio envío del CW entrante, sin necesidad de un prefijo textual.
- Use los botones **A-** y **A+** para ajustar el tamaño de fuente del texto decodificado para una mejor legibilidad.
- Arrastre la franja delgada en la parte superior del panel de decodificación CW para revelar más historial de texto decodificado.
- Cuando esté en el lienzo del espacio de trabajo, haga clic en la barra de título para activar un panadapter o arrástrela para reposicionarlo. Un umbral de 6 píxeles separa el clic del arrastre.
- El botón de extracción **⬈** está siempre disponible mientras un panadapter está en el lienzo, incluso si es el único abierto.

## Solución de problemas

- **El botón ⬈ no es visible** — Solo tiene un panadapter abierto y no está en el lienzo del espacio de trabajo. Los botones de extracción, maximizar y cerrar están todos ocultos en el modo de pila de un solo panadapter. Abra un panadapter adicional o mueva el panadapter al lienzo para que aparezcan.
- **La ventana flotante no se puede mover** — Haga clic y arrastre la franja de título dentro de la ventana flotante, no el área del espectro. El área del espectro se usa para sintonizar.
- **Un panadapter en el lienzo no se puede arrastrar** — Haga clic y arrastre la barra de título, no el área del espectro. Debe superarse un umbral de arrastre de 6 píxeles antes de que el panadapter comience a moverse. Si el panadapter está flotando, el modo de arrastre en lienzo está deshabilitado; acóplelo primero.
- **El área de texto de decodificación CW no muestra texto** — Verifique que el audio de PC esté enrutado a AetherSDR. El panel muestra **(requires PC Audio)** cuando el audio no está disponible.

## Relacionados

- [Maximice un panadapter para llenar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cierre un panadapter adicional](close-an-extra-panadapter.md)
- [Haga clic en el espectro para activar un panadapter (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Descripción general del panadapter](overview.md)
