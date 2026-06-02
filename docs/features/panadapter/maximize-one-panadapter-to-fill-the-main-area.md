# Maximizar un panadapter para que ocupe el área principal

Cuando tiene más de un panadapter abierto, puede expandir uno solo para que ocupe toda el área principal, apartando temporalmente los demás.

## Antes de comenzar

- Debe estar conectado a una radio FLEX-8600.
- Al menos dos panadapters deben estar abiertos. En modo de un solo panadapter, el botón de maximizar está oculto.

## Pasos

1. Localice la barra de título del panadapter que desea expandir. Contiene el nombre del slice (por ejemplo, "Slice A"), seguido de los botones ⬈, □ y × a la derecha.
2. Haga clic en □ en la barra de título de ese panadapter.

El panadapter seleccionado se expande para llenar el área principal.

## Consejos

- Para restaurar la distribución de múltiples panadapters, haga clic nuevamente en □ en el panadapter maximizado.

## Relacionado

- [Panadapter overview](overview.md)
- [Click the spectrum to activate a panadapter (multi-slice mode)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Close an extra panadapter](close-an-extra-panadapter.md)
- [Pop a panadapter out into its own window](pop-a-panadapter-out-into-its-own-window.md)

# Panel de decodificación CW

El panel de decodificación CW aparece debajo del espectro y el waterfall cuando está habilitado. Muestra texto Morse decodificado y proporciona controles para ajustar el decodificador.

## Menú contextual del área de texto decodificado CW

Haciendo clic derecho en cualquier lugar del área de texto decodificado se abre un menú contextual. Además de las acciones de texto estándar (Seleccionar todo, Copiar, etc.), el menú contiene una entrada **Clear**. Haga clic en **Clear** para borrar todo el búfer de decodificación CW sin salir del área de texto. Esto es equivalente a hacer clic en el botón **CLR** en la barra de herramientas del panel.

## Texto decodificado del lado de TX

Cuando tanto el keying transmitido de la radio como el audio recibido se enrutan al mismo panel de decodificación CW, su propia transmisión aparece en cian (`#5fc8ff`) mientras que el CW entrante aparece en los colores estándar basados en confianza. Un solo espacio separa las secuencias de texto de Tx y Rx para que no se fusionen visualmente. No se agrega espacio inicial cuando el panel está vacío o cuando el primer texto decodificado proviene del transmisor.

## Referencia de controles

| Control              | Tipo                | Valor predeterminado       |
|----------------------|---------------------|----------------------------|
| Etiqueta de estadísticas CW | Indicador      | —                          |
| Sens                 | Deslizador          | 30 (rango 0–100)           |
| 🔒P (Lock Pitch)      | Botón de alternancia | —                          |
| 🔒S (Lock Speed)      | Botón de alternancia | —                          |
| Lo (tono mínimo)     | Deslizador          | 500 Hz (rango 300–1200 Hz) |
| Hi (tono máximo)     | Deslizador          | 700 Hz (rango 300–1200 Hz) |
| CPY ALL              | Botón               | —                          |
| CPY VIS              | Botón               | —                          |
| CLR                  | Botón               | —                          |
| ✕ (cerrar CW)        | Botón               | —                          |
| Texto decodificado CW | Campo de texto solo lectura | —                    |

## Notas

- El panel de decodificación CW requiere enrutamiento de audio por PC para funcionar. Si el audio no está configurado, el panel muestra el recordatorio `(requires PC Audio)`.
- El deslizador de sensibilidad mapea valores 0–100 a un umbral de costo de 1.0–0.1. Los valores más altos filtran las decodificaciones de menor confianza.
- Los deslizadores de tono Lo y Hi se limitan para que Lo nunca pueda exceder a Hi, y Hi nunca pueda ser menor que Lo.
- Los botones de alternancia Lock Pitch y Lock Speed congelan el decodificador en el tono o velocidad actualmente detectados, evitando que el decodificador rastree cambios.
- Cuando la radio está transmitiendo, la congelación del waterfall es controlada por el estado TRANSMITIENDO del interlock de la radio en todos los clientes conectados (Multi-Flex), eliminando el artefacto de estela de TX de 10–23 segundos después de deskeyear.
- Al reconectar la radio, se reafirman los FPS deseados del panadapter y la duración de la línea del waterfall para evitar una caída silenciosa al valor predeterminado de 10 Hz de la radio.
- La barra de título del panadapter y el panel CW ahora usan colores conscientes del tema mediante `ThemeManager::applyStyleSheet()` en lugar de valores hexadecimales fijos. El degradado de la barra de título referencia `{{color.text.disabled}}` y `{{color.background.1}}`, el asa de arrastre usa `{{color.text.label}}`, y el título del slice usa `{{color.text.secondary}}`. El fondo y borde del panel CW usan `{{color.background.0}}` y `{{color.background.1}}` respectivamente. El deslizador de sensibilidad usa el auxiliar `applyPrimarySliderStyle()` para un tematizado consistente.

## Relacionado

- [Panadapter overview](overview.md)
- [Click the spectrum to activate a panadapter (multi-slice mode)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Close an extra panadapter](close-an-extra-panadapter.md)
- [Pop a panadapter out into its own window](pop-a-panadapter-out-into-its-own-window.md)
