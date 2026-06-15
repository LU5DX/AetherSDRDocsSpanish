# Maximizar un panadapter para que ocupe el área principal

Cuando tiene más de un panadapter abierto, puede expandir uno solo para que ocupe toda el área principal, apartando temporalmente los demás.

## Antes de empezar

- Debe estar conectado a una radio FLEX-8600.
- Debe tener al menos dos panadapters abiertos. En modo de un solo panadapter, el botón de maximizar está oculto.

## Pasos

1. Localice la barra de título del panadapter que desea expandir. Contiene el nombre del slice (por ejemplo, "Slice A"), seguido de los botones ⬈, □ y × a la derecha.
2. Haga clic en □ en la barra de título de ese panadapter.

El panadapter seleccionado se expande para ocupar el área principal.

## Consejos

- Para restaurar la disposición de múltiples panadapters, vuelva a hacer clic en □ en el panadapter maximizado.

## Relacionado

- [Panadapter overview](overview.md)
- [Click the spectrum to activate a panadapter (multi-slice mode)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Close an extra panadapter](close-an-extra-panadapter.md)
- [Pop a panadapter out into its own window](pop-a-panadapter-out-into-its-own-window.md)

# Panel de decodificación CW

El panel de decodificación CW aparece debajo del espectro y el waterfall cuando está habilitado. Muestra el texto Morse decodificado y proporciona controles para sintonizar el decodificador.

## Menú contextual del área de texto de decodificación CW

Al hacer clic derecho en cualquier parte del área de texto decodificado, se abre un menú contextual. Además de las acciones de texto estándar (Seleccionar todo, Copiar, etc.), el menú contiene una entrada **Clear**. Haga clic en **Clear** para borrar todo el búfer de decodificación CW sin salir del área de texto. Esto es equivalente a hacer clic en el botón **CLR** en la barra de herramientas del panel.

## Texto decodificado del lado TX

Cuando tanto la clave transmitida de la radio como el audio recibido se enrutan al mismo panel de decodificación CW, su propia transmisión aparece en cian (`#5fc8ff`), mientras que la CW entrante aparece en los colores estándar basados en confianza. Un solo espacio separa las secuencias de texto Tx y Rx para que no se fusionen visualmente. No se agrega un espacio inicial cuando el panel está vacío o cuando el primer texto decodificado proviene del transmisor.

## Referencia de controles

| Control            | Tipo                 | Valor predeterminado      | Notas                          |
|--------------------|----------------------|----------------------------|--------------------------------|
| Etiqueta de estadísticas CW | Indicador            | —                          | Muestra el tono y la velocidad detectados |
| Sens               | Deslizador           | 30 (rango 0–100)          |                                |
| 🔒P (Bloquear tono) | Botón de alternancia  | —                          |                                |
| 🔒S (Bloquear velocidad) | Botón de alternancia  | —                          |                                |
| Tono (rango)       | Deslizador de rango   | 500–700 Hz (rango 300–1200 Hz) | Reemplaza el par Lo/Hi       |
| WPM (rango)        | Deslizador de rango   | 15–40 WPM (rango 5–60 WPM)  | Nuevo en v26.6.3               |
| CPY ALL            | Botón                | —                          |                                |
| CPY VIS            | Botón                | —                          |                                |
| CLR                | Botón                | —                          |                                |
| ✕ (cerrar CW)      | Botón                | —                          |                                |
| Texto de decodificación CW | Campo de texto de solo lectura | —                          |                                |

## Notas

- El panel de decodificación CW requiere enrutamiento de audio de PC para funcionar. Si el audio no está configurado, el panel muestra el recordatorio `(requires PC Audio)`.
- El deslizador de sensibilidad asigna valores de 0–100 a un umbral de costo de 1.0–0.1. Los valores más altos filtran las decodificaciones de menor confianza.
- El deslizador de rango de tono reemplaza los dos deslizadores Lo y Hi separados anteriores. Proporciona un control de doble manija (rango 300–1200 Hz) con el extremo inferior predeterminado en 500 Hz y el extremo superior predeterminado en 700 Hz. La etiqueta "Pitch" está integrada dentro del widget.
- El deslizador de rango WPM (nuevo en v26.6.3) limita el rango de búsqueda de velocidad del decodificador. Proporciona un control de doble manija (rango 5–60 WPM) con el extremo inferior predeterminado en 15 WPM y el extremo superior predeterminado en 40 WPM. La etiqueta "WPM" está integrada dentro del widget.
- Los botones de alternancia Bloquear tono y Bloquear velocidad congelan el decodificador al tono o velocidad actualmente detectados, impidiendo que el decodificador rastree los cambios.
- Cuando la radio está transmitiendo, la congelación del waterfall es impulsada por el estado de interbloqueo TRANSMITTING de la radio en todos los clientes conectados (Multi-Flex), eliminando el artefacto de estela de transmisión de 10–23 segundos después de soltar la clave.
- Al reconectar la radio, se reafirman los FPS deseados del panadapter y la duración de la línea del waterfall para evitar que disminuyan silenciosamente al valor predeterminado de 10 Hz de la radio.
- La barra de título del panadapter y el panel CW ahora usan colores conscientes del tema a través de `ThemeManager::applyStyleSheet()` en lugar de valores hexadecimales codificados. El degradado de la barra de título referencia `{{color.text.disabled}}` y `{{color.background.1}}`, el asa de arrastre usa `{{color.text.label}}`, y el título del slice usa `{{color.text.secondary}}`. El fondo y el borde del panel CW usan `{{color.background.0}}` y `{{color.background.1}}` respectivamente. El deslizador de sensibilidad usa el ayudante `applyPrimarySliderStyle()` para una temática consistente.

## Relacionado

- [Panadapter overview](overview.md)
- [Click the spectrum to activate a panadapter (multi-slice mode)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Close an extra panadapter](close-an-extra-panadapter.md)
- [Pop a panadapter out into its own window](pop-a-panadapter-out-into-its-own-window.md)
