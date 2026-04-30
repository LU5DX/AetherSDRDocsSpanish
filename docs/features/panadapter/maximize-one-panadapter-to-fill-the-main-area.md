# Maximizar un panadaptador para llenar el área principal

Cuando tiene más de un panadaptador abierto, puede expandir uno solo para llenar toda el área principal, empujando los demás temporalmente a un lado.

## Antes de empezar

- Debe estar conectado a una radio FLEX-8600.
- Al menos dos panadaptadores deben estar abiertos. En modo de un solo panadaptador, el botón de maximizar está oculto.

## Pasos

1. Localice la barra de título del panadaptador que desea expandir. Contiene el nombre del slice (por ejemplo, "Slice A"), seguido de los botones ⬈, □ y × a la derecha.
2. Haga clic en □ en la barra de título de ese panadaptador.

El panadaptador seleccionado se expande para llenar el área principal.

## Consejos

- Para restaurar la disposición de múltiples panadaptadores, haga clic nuevamente en □ en el panadaptador maximizado.

## Relacionado

- [Descripción general del panadaptador](overview.md)
- [Haga clic en el espectro para activar un panadaptador (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Cerrar un panadaptador adicional](close-an-extra-panadapter.md)
- [Sacar un panadaptador a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)


# Panel de decodificación CW

El panel de decodificación CW aparece debajo del espectro y la cascada cuando está habilitado. Muestra texto Morse decodificado y proporciona controles para sintonizar el decodificador.

## Menú contextual del área de texto de decodificación CW

Hacer clic con el botón derecho en cualquier lugar del área de texto decodificado abre un menú contextual. Además de las acciones de texto estándar (Seleccionar todo, Copiar, etc.), el menú contiene una entrada **Clear** (Borrar). Haga clic en **Clear** para borrar todo el búfer de decodificación CW sin salir del área de texto. Esto es equivalente a hacer clic en el botón **CLR** en la barra de herramientas del panel.

## Referencia de controles

| Control         | Tipo                 | Valor predeterminado       |
|-----------------|----------------------|----------------------------|
| Etiqueta de estadísticas CW | Indicador            | —                          |
| Sens            | Deslizador           | 30 (rango 0–100)           |
| 🔒P (Lock Pitch) | Botón de alternancia | —                          |
| 🔒S (Lock Speed) | Botón de alternancia | —                          |
| Lo (mín. tono)  | Deslizador           | 500 Hz (rango 300–1200 Hz) |
| Hi (máx. tono)  | Deslizador           | 700 Hz (rango 300–1200 Hz) |
| CPY ALL         | Botón                | —                          |
| CPY VIS         | Botón                | —                          |
| CLR             | Botón                | —                          |
| ✕ (cerrar CW)   | Botón                | —                          |
| Texto decodificado CW | Campo de texto de solo lectura | —                          |

## Notas

- El panel de decodificación CW requiere enrutamiento de audio de PC para funcionar. Si el audio no está configurado, el panel muestra el recordatorio `(requires PC Audio)`.

## Relacionado

- [Descripción general del panadaptador](overview.md)
- [Haga clic en el espectro para activar un panadaptador (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Cerrar un panadaptador adicional](close-an-extra-panadapter.md)
- [Sacar un panadaptador a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
