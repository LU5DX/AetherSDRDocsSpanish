# Maximizar un panadapter para llenar el área principal

Cuando tiene más de un panadapter abierto, puede expandir uno solo para que ocupe todo el área principal, apartando temporalmente los demás.

## Antes de comenzar

- Debe estar conectado a una radio FLEX-8600.
- Debe haber al menos dos panadapters abiertos. En el modo de un solo pan, el botón de maximizar está oculto.

## Pasos

1. Localice la barra de título del panadapter que desea expandir. Contiene el nombre del slice (por ejemplo, "Slice A"), seguido de los botones ⬈, □ y × en el lado derecho.
2. Haga clic en □ en la barra de título de ese panadapter.

El panadapter seleccionado se expande para llenar el área principal.

## Consejos

- Para restaurar la distribución de varios pan, haga clic nuevamente en □ en el panadapter maximizado.

## Relacionado

- [Descripción general del panadapter](overview.md)
- [Haga clic en el espectro para activar un panadapter (modo de múltiples slices)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Extraer un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)

# Panel de decodificación CW

El panel de decodificación CW aparece debajo del espectro y el waterfall cuando está habilitado. Muestra el texto Morse decodificado y proporciona controles para ajustar el decodificador.

## Menú contextual del área de texto de decodificación CW

Al hacer clic con el botón derecho en cualquier lugar del área de texto decodificado se abre un menú contextual. Además de las acciones de texto estándar (Select All, Copy, etc.), el menú contiene una entrada **Clear**. Haga clic en **Clear** para borrar todo el búfer de decodificación CW sin salir del área de texto. Esto equivale a hacer clic en el botón **CLR** en la barra de herramientas del panel.

## Texto decodificado del lado de TX

Cuando tanto la manipulación transmitida por la radio como el audio recibido se enrutan al mismo panel de decodificación CW, su propio envío aparece en cian (`#5fc8ff`) mientras que el CW entrante aparece en los colores estándar basados en confianza. Un solo espacio separa las secuencias de texto de Tx y Rx para que no se fusionen visualmente. No se agrega espacio inicial cuando el panel está vacío o cuando el primer texto decodificado proviene del transmisor.

## Redimensionar el panel de decodificación CW

En v26.7.4, puede redimensionar verticalmente el panel de decodificación CW para mostrar más o menos historial de texto decodificado. Una delgada empuñadura de arrastre horizontal aparece en el borde superior del panel.

1. Mueva el cursor sobre la delgada franja horizontal en la parte superior del panel de decodificación CW. El cursor cambia a un cursor de redimensionamiento vertical.
2. Haga clic y arrastre hacia abajo para hacer el panel más alto, o hacia arriba para hacerlo más bajo. La altura está limitada entre 60 y 600 píxeles.
3. Suelte el mouse. La nueva altura se guarda en la configuración y se restaurará la próxima vez que abra el panel.

El tamaño de fuente del texto decodificado también se puede ajustar de forma independiente (consulte Controles de tamaño de fuente a continuación).

## Controles de tamaño de fuente

En v26.7.4, dos nuevos botones le permiten cambiar el tamaño de fuente del texto decodificado:

| Control | Tipo | Comportamiento |
|---------|------|----------------|
| A- (Disminuir) | Botón | Disminuye el tamaño de fuente del texto decodificado en 1 píxel, limitado entre 8 y 32 píxeles. |
| A+ (Aumentar) | Botón | Aumenta el tamaño de fuente del texto decodificado en 1 píxel, limitado entre 8 y 32 píxeles. |

1. Haga clic en **A-** para hacer el texto decodificado más pequeño.
2. Haga clic en **A+** para hacer el texto decodificado más grande.

El tamaño de fuente se guarda en la configuración y se restaurará la próxima vez que abra el panel.

## Referencia de controles

| Control            | Tipo                 | Predeterminado             | Notas                          |
|--------------------|----------------------|----------------------------|--------------------------------|
| Etiqueta de estadísticas CW | Indicador     | —                          | Muestra el tono y la velocidad detectados |
| Sens               | Control deslizante   | 30 (rango 0–100)           |                                |
| 🔒P (Lock Pitch)   | Botón de alternancia | —                          |                                |
| 🔒S (Lock Speed)   | Botón de alternancia | —                          |                                |
| Pitch (rango)      | Control deslizante de rango | 500–700 Hz (rango 300–1200 Hz) | Reemplaza el par Lo/Hi |
| WPM (rango)        | Control deslizante de rango | 15–40 WPM (rango 5–60 WPM) |                                |
| A- (Disminuir)     | Botón                | —                          | Nuevo en v26.7.4               |
| A+ (Aumentar)      | Botón                | —                          | Nuevo en v26.7.4               |
| CPY ALL            | Botón                | —                          |                                |
| CPY VIS            | Botón                | —                          |                                |
| CLR                | Botón                | —                          |                                |
| ✕ (cerrar CW)      | Botón                | —                          |                                |
| Texto de decodificación CW | Campo de texto de solo lectura | —                |                                |

## Alojamiento en el lienzo

Cuando un panadapter se coloca en el lienzo del espacio de trabajo (en lugar de en la distribución estándar de divisor), su barra de título entra en un modo de lienzo que transmite un gesto de movimiento en vivo. Este es el mismo mecanismo que utilizan las barras de título de los contenedores en modo lienzo: un gesto real que la sesión del lienzo sigue, no un fantasma de arrastrar y soltar.

Mientras está en el lienzo, la barra de título maneja la entrada del mouse de la siguiente manera:

- Una pulsación con el botón izquierdo y liberación sin movimiento activa el panadapter (igual que hacer clic en el espectro).
- Arrastrar más allá de un umbral de 6 píxeles comienza un movimiento en vivo del panadapter a través del lienzo. Todos los eventos del mouse son consumidos por la barra de título durante el arrastre para que el mecanismo de arrastre de ventana flotante nunca interfiera.
- La liberación finaliza el movimiento y actualiza la posición del panadapter en el lienzo.

El botón de extracción (⬈) permanece visible mientras está en el lienzo, incluso si este es el único panadapter. El comportamiento de ocultar botones en modo de un solo pan solo se aplica en la distribución de pila, no en el lienzo.

## Notas

- El panel de decodificación CW requiere enrutamiento de audio de PC para funcionar. Si el audio no está configurado, el panel muestra el recordatorio `(requires PC Audio)`.
- El control deslizante de sensibilidad asigna valores de 0–100 a un umbral de costo de 1.0–0.1. Los valores más altos filtran las decodificaciones de menor confianza.
- El control deslizante de rango de Pitch reemplaza los dos controles deslizantes separados anteriores Lo y Hi. Proporciona un solo control de doble manija (rango 300–1200 Hz) con el extremo bajo predeterminado en 500 Hz y el extremo alto predeterminado en 700 Hz. La etiqueta "Pitch" está incorporada dentro del widget.
- El control deslizante de rango de WPM limita el rango de búsqueda de velocidad del decodificador. Proporciona un solo control de doble manija (rango 5–60 WPM) con el extremo bajo predeterminado en 15 WPM y el extremo alto predeterminado en 40 WPM. La etiqueta "WPM" está incorporada dentro del widget.
- Los botones de alternancia Lock Pitch y Lock Speed congelan el decodificador en el tono o la velocidad actualmente detectados, impidiendo que el decodificador siga los cambios.
- Cuando la radio está transmitiendo, la congelación del waterfall está impulsada por el estado TRANSMITTING del interlock de la radio en todos los clientes conectados (Multi-Flex), eliminando el artefacto de rastro de TX de 10–23 segundos después de desactivar la manipulación.
- Al reconectarse a la radio, el FPS deseado del panadapter y la duración de línea del waterfall se vuelven a afirmar para evitar caer silenciosamente al valor predeterminado de 10 Hz de la radio. Los panadapters secundarios (Slices B–H) también tienen su rango de dBm preparado al reconectarse para que el ajuste automático del piso de ruido comience desde la línea base correcta en lugar del rango predeterminado [-50, +50].
- La barra de título del panadapter y el panel CW ahora usan colores conscientes del tema mediante `ThemeManager::applyStyleSheet()` en lugar de valores hexadecimales codificados. El degradado de la barra de título referencia `{{color.text.disabled}}` y `{{color.background.1}}`, la empuñadura de arrastre usa `{{color.text.label}}`, y el título del slice usa `{{color.text.secondary}}`. El fondo y el borde del panel CW usan `{{color.background.0}}` y `{{color.background.1}}` respectivamente. El control deslizante de sensibilidad usa el asistente `applyPrimarySliderStyle()` para un tematizado consistente.

## Relacionado

- [Descripción general del panadapter](overview.md)
- [Haga clic en el espectro para activar un panadapter (modo de múltiples slices)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Extraer un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
