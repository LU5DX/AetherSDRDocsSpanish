# Maximizar un panadaptador para que ocupe el área principal

Cuando tiene más de un panadaptador abierto, puede expandir uno solo para que ocupe toda el área principal, apartando temporalmente los demás.

## Antes de comenzar

- Debe estar conectado a una radio FLEX-8600.
- Deben haber al menos dos panadaptadores abiertos. En el modo de un solo panadaptador, el botón de maximizar está oculto.

## Pasos

1. Localice la barra de título del panadaptador que desea expandir. Contiene el nombre del slice (por ejemplo, "Slice A"), seguido de los botones ⬈, □ y × a la derecha.
2. Haga clic en □ en la barra de título de ese panadaptador.

El panadaptador seleccionado se expande para ocupar toda el área principal.

## Consejos

- Para restaurar la distribución de múltiples panadaptadores, vuelva a hacer clic en □ en el panadaptador maximizado.

## Relacionado

- [Descripción general del panadaptador](overview.md)
- [Haga clic en el espectro para activar un panadaptador (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Cerrar un panadaptador adicional](close-an-extra-panadapter.md)
- [Extraer un panadaptador a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)

# Panel de decodificación CW

El panel de decodificación CW aparece debajo del espectro y el waterfall cuando está habilitado. Muestra texto Morse decodificado y proporciona controles para sintonizar el decodificador.

## Menú contextual del área de texto de decodificación CW

Al hacer clic derecho en cualquier lugar del área de texto decodificado, se abre un menú contextual. Además de las acciones de texto estándar (Seleccionar todo, Copiar, etc.), el menú contiene una entrada **Clear**. Haga clic en **Clear** para borrar todo el búfer de decodificación CW sin salir del área de texto. Esto equivale a hacer clic en el botón **CLR** en la barra de herramientas del panel.

## Texto decodificado del lado de transmisión

Cuando tanto la clave transmitida por la radio como el audio recibido se enrutan al mismo panel de decodificación CW, su propia transmisión aparece en cian (`#5fc8ff`) mientras que la CW entrante aparece en los colores estándar basados en confianza. Un solo espacio separa las secuencias de texto de Tx y Rx para que no se fusionen visualmente. No se agrega un espacio al inicio cuando el panel está vacío o cuando el primer texto decodificado proviene del transmisor.

## Cambiar el tamaño del panel de decodificación CW

En v26.7.4, puede cambiar el tamaño vertical del panel de decodificación CW para mostrar más o menos historial de texto decodificado. Aparece una delgada barra de arrastre horizontal en el borde superior del panel.

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

| Control            | Tipo                 | Predeterminado            | Notas                         |
|--------------------|----------------------|---------------------------|-------------------------------|
| Etiqueta de estadísticas CW | Indicador | —                         | Muestra el tono y la velocidad detectados |
| Sens               | Deslizador           | 30 (rango 0–100)          |                               |
| 🔒P (Bloquear tono) | Botón de alternancia | —                         |                               |
| 🔒S (Bloquear velocidad) | Botón de alternancia | —                     |                               |
| Pitch (rango)      | Deslizador de rango  | 500–700 Hz (rango 300–1200 Hz) | Reemplaza el par Lo/Hi       |
| WPM (rango)        | Deslizador de rango  | 15–40 WPM (rango 5–60 WPM)                               |
| A- (Disminuir)     | Botón                | —                         | Nuevo en v26.7.4              |
| A+ (Aumentar)      | Botón                | —                         | Nuevo en v26.7.4              |
| CPY ALL            | Botón                | —                         |                               |
| CPY VIS            | Botón                | —                         |                               |
| CLR                | Botón                | —                         |                               |
| ✕ (cerrar CW)     | Botón                | —                         |                               |
| Texto de decodificación CW | Campo de texto de solo lectura | —                   |                               |

## Notas

- El panel de decodificación CW requiere enrutamiento de audio de PC para funcionar. Si el audio no está configurado, el panel muestra el recordatorio `(requires PC Audio)`.
- El deslizador de Sensibilidad asigna valores de 0–100 a un umbral de costo de 1.0–0.1. Los valores más altos filtran las decodificaciones de menor confianza.
- El deslizador de rango de Pitch reemplaza los dos deslizadores separados anteriores Lo y Hi. Proporciona un único control de doble manija (rango 300–1200 Hz) con el extremo inferior predeterminado en 500 Hz y el extremo superior predeterminado en 700 Hz. La etiqueta "Pitch" está integrada dentro del widget.
- El deslizador de rango de WPM limita el rango de búsqueda de velocidad del decodificador. Proporciona un único control de doble manija (rango 5–60 WPM) con el extremo inferior predeterminado en 15 WPM y el extremo superior predeterminado en 40 WPM. La etiqueta "WPM" está integrada dentro del widget.
- Los botones de alternancia de Bloquear tono y Bloquear velocidad congelan el decodificador en el tono o la velocidad detectados actualmente, evitando que el decodificador rastree cambios.
- Cuando la radio está transmitiendo, la congelación del waterfall es impulsada por el estado de interbloqueo TRANSMITTING de la radio en todos los clientes conectados (Multi-Flex), eliminando el artefacto de estela de transmisión de 10 a 23 segundos después de soltar la clave.
- Al reconectar la radio, se restablecen los FPS deseados del panadaptador y la duración de la línea del waterfall para evitar una caída silenciosa al valor predeterminado de 10 Hz de la radio.
- La barra de título del panadaptador y el panel CW ahora usan colores conscientes del tema a través de `ThemeManager::applyStyleSheet()` en lugar de valores hexadecimales codificados. El degradado de la barra de título hace referencia a `{{color.text.disabled}}` y `{{color.background.1}}`, la barra de arrastre usa `{{color.text.label}}`, y el título del slice usa `{{color.text.secondary}}`. El fondo y el borde del panel CW usan `{{color.background.0}}` y `{{color.background.1}}` respectivamente. El deslizador de Sensibilidad usa el ayudante `applyPrimarySliderStyle()` para un tema consistente.

## Relacionado

- [Descripción general del panadaptador](overview.md)
- [Haga clic en el espectro para activar un panadaptador (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Cerrar un panadaptador adicional](close-an-extra-panadapter.md)
- [Extraer un panadaptador a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
