# Maximizar un panadapter para que ocupe toda el área principal

Cuando tiene más de un panadapter abierto, puede expandir uno de ellos para que ocupe toda el área principal, apartando temporalmente los demás.

## Antes de comenzar

- Debe estar conectado a una radio FLEX-8600.
- Debe tener al menos dos panadapters abiertos. En el modo de un solo panadapter, el botón de maximizar está oculto.

## Pasos

1. Ubique la barra de título del panadapter que desea expandir. Contiene el nombre del slice (por ejemplo, "Slice A"), seguido de los botones ⬈, □ y × en la parte derecha.
2. Haga clic en □ en la barra de título de ese panadapter.

El panadapter seleccionado se expande para ocupar toda el área principal.

## Consejos

- Para restaurar la distribución de múltiples panadapters, haga clic nuevamente en □ en el panadapter maximizado.

## Relacionados

- [Panadapter overview](overview.md)
- [Click the spectrum to activate a panadapter (multi-slice mode)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Close an extra panadapter](close-an-extra-panadapter.md)
- [Pop a panadapter out into its own window](pop-a-panadapter-out-into-its-own-window.md)

# Panel de decodificación CW

El panel de decodificación CW aparece debajo del espectro y el waterfall cuando está habilitado. Muestra el texto Morse decodificado y proporciona controles para ajustar el decodificador.

## Menú contextual del área de texto de decodificación CW

Al hacer clic derecho en cualquier lugar del área de texto decodificado, se abre un menú contextual. Además de las acciones de texto estándar (Seleccionar Todo, Copiar, etc.), el menú contiene una entrada **Clear**. Haga clic en **Clear** para borrar todo el búfer de decodificación CW sin salir del área de texto. Esto es equivalente a hacer clic en el botón **CLR** en la barra de herramientas del panel.

## Referencia de controles

| Control                    | Tipo                 | Valor predeterminado       |
|----------------------------|----------------------|-----------------------------|
| Etiqueta de estadísticas CW | Indicador            | —                           |
| Sens                       | Control deslizante   | 30 (rango 0–100)            |
| 🔒P (Lock Pitch)           | Botón de alternancia  | —                           |
| 🔒S (Lock Speed)           | Botón de alternancia  | —                           |
| Lo (pitch mínimo)          | Control deslizante   | 500 Hz (rango 300–1200 Hz)  |
| Hi (pitch máximo)          | Control deslizante   | 700 Hz (rango 300–1200 Hz)  |
| CPY ALL                    | Botón                | —                           |
| CPY VIS                    | Botón                | —                           |
| CLR                        | Botón                | —                           |
| ✕ (cerrar CW)             | Botón                | —                           |
| Texto de decodificación CW | Campo de texto de solo lectura | —              |

## Notas

- El panel de decodificación CW requiere enrutamiento de audio de PC para funcionar. Si el audio no está configurado, el panel muestra el recordatorio `(requires PC Audio)`.

## Relacionados

- [Panadapter overview](overview.md)
- [Click the spectrum to activate a panadapter (multi-slice mode)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Close an extra panadapter](close-an-extra-panadapter.md)
- [Pop a panadapter out into its own window](pop-a-panadapter-out-into-its-own-window.md)
