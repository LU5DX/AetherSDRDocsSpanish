# Maximizar un panadapter para ocupar el área principal

Cuando hay más de un panadapter abierto, puede expandir uno solo para que ocupe toda el área principal, desplazando temporalmente los demás.

## Antes de comenzar

- Debe estar conectado a una radio FLEX-8600.
- Deben estar abiertos al menos dos panadapters. En el modo de panel único, el botón de maximizar está oculto.

## Pasos

1. Ubique la barra de título del panadapter que desea expandir. Contiene el nombre del slice (por ejemplo, "Slice A"), seguido de los botones ⬈, □ y × a la derecha.
2. Haga clic en □ en la barra de título de ese panadapter.

El panadapter seleccionado se expande para ocupar toda el área principal.

## Sugerencias

- Para restaurar el diseño de múltiples paneles, haga clic en □ nuevamente sobre el panadapter maximizado.

## Relacionado

- [Descripción general del panadapter](overview.md)
- [Haga clic en el espectro para activar un panadapter (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Extraer un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)


# Panel de decodificación CW

El panel de decodificación CW aparece debajo del espectro y el waterfall cuando está habilitado. Muestra el texto Morse decodificado y proporciona controles para ajustar el decodificador.

## Menú contextual del área de texto decodificado CW

Al hacer clic derecho en cualquier parte del área de texto decodificado se abre un menú contextual. Además de las acciones de texto estándar (Select All, Copy, entre otras), el menú contiene una entrada **Clear**. Haga clic en **Clear** para borrar todo el búfer de decodificación CW sin salir del área de texto. Esto equivale a hacer clic en el botón **CLR** de la barra de herramientas del panel.

## Referencia de controles

| Control         | Tipo                 | Valor predeterminado       |
|-----------------|----------------------|----------------------------|
| CW stats label  | Indicador            | —                          |
| Sens            | Control deslizante   | 30 (rango 0–100)           |
| 🔒P (Lock Pitch) | Botón de alternancia | —                          |
| 🔒S (Lock Speed) | Botón de alternancia | —                          |
| Lo (pitch min)  | Control deslizante   | 500 Hz (rango 300–1200 Hz) |
| Hi (pitch max)  | Control deslizante   | 700 Hz (rango 300–1200 Hz) |
| CPY ALL         | Botón                | —                          |
| CPY VIS         | Botón                | —                          |
| CLR             | Botón                | —                          |
| ✕ (close CW)    | Botón                | —                          |
| CW decode text  | Campo de texto de solo lectura | —             |

## Notas

- El panel de decodificación CW requiere enrutamiento de audio por PC para funcionar. Si el audio no está configurado, el panel muestra el aviso `(requires PC Audio)`.

## Relacionado

- [Descripción general del panadapter](overview.md)
- [Haga clic en el espectro para activar un panadapter (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Extraer un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
