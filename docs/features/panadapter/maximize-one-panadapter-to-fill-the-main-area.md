# Maximizar un panadapter para ocupar el área principal

Cuando tiene más de un panadapter abierto, puede expandir uno solo para que ocupe toda el área principal, desplazando temporalmente los demás.

## Antes de comenzar

- Debe estar conectado a una radio FLEX-8600.
- Debe haber al menos dos panadapters abiertos. En el modo de un solo panadapter, el botón de maximizar está oculto.

## Pasos

1. Localice la barra de título del panadapter que desea expandir. Contiene el nombre del slice (por ejemplo, "Slice A"), seguido de los botones ⬈, □ y × a la derecha.
2. Haga clic en □ en la barra de título de ese panadapter.

El panadapter seleccionado se expande para ocupar toda el área principal.

## Consejos

- Para restaurar el diseño con múltiples panadapters, haga clic en □ nuevamente sobre el panadapter maximizado.

## Relacionado

- [Descripción general del panadapter](overview.md)
- [Haga clic en el espectro para activar un panadapter (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Abrir un panadapter en su propia ventana](pop-a-panadapter-out-into-its-own-window.md)


# Panel de decodificación CW

El panel de decodificación CW aparece debajo del espectro y del waterfall cuando está habilitado. Muestra el texto Morse decodificado y proporciona controles para ajustar el decodificador.

## Menú contextual del área de texto de decodificación CW

Al hacer clic derecho en cualquier parte del área de texto decodificado se abre un menú contextual. Además de las acciones de texto estándar (Select All, Copy, entre otras), el menú contiene una entrada **Clear**. Haga clic en **Clear** para borrar todo el búfer de decodificación CW sin salir del área de texto. Esto es equivalente a hacer clic en el botón **CLR** de la barra de herramientas del panel.

## Referencia de controles

| Control | Tipo | Predeterminado | Descripción |
|---|---|---|---|
| Etiqueta de estadísticas CW | Indicador | — | Muestra el tono y la velocidad CW detectados en el formato `<hz> Hz  <wpm> WPM`. |
| Sens | Deslizador | 30 (rango 0–100) | Filtra las decodificaciones de baja confianza. Los valores más altos son más estrictos. Asigna 0–100 a un umbral de costo de 1.0–0.1. Clave de configuración: `CwDecoderSensitivity`. |
| 🔒P (Lock Pitch) | Botón de alternancia | — | Fija el tono del decodificador CW a la frecuencia sintonizada actual. |
| 🔒S (Lock Speed) | Botón de alternancia | — | Fija la velocidad del decodificador CW al WPM actual. |
| Lo (tono mínimo) | Deslizador | 500 Hz (rango 300–1200 Hz) | Establece el tono mínimo que busca el decodificador CW. Limitado a no ser mayor que el valor Hi. |
| Hi (tono máximo) | Deslizador | 700 Hz (rango 300–1200 Hz) | Establece el tono máximo que busca el decodificador CW. Limitado a no ser menor que el valor Lo. |
| CPY ALL | Botón | — | Copia el texto decodificado completo al portapapeles. |
| CPY VIS | Botón | — | Copia al portapapeles solo el texto visible actualmente en el área de desplazamiento. |
| CLR | Botón | — | Borra el búfer de decodificación CW. |
| ✕ (cerrar CW) | Botón | — | Oculta el panel de decodificación CW. |
| Texto de decodificación CW | Campo de texto de solo lectura | — | Visualización continua del CW decodificado con color según la confianza: verde (costo < 0.15), amarillo (< 0.35), naranja (< 0.60), rojo (≥ 0.60). Haga clic derecho para el menú contextual. |

## Notas

- El panel de decodificación CW requiere enrutamiento de audio por PC para funcionar. Si el audio no está configurado, el panel muestra el recordatorio `(requires PC Audio)`.

## Relacionado

- [Descripción general del panadapter](overview.md)
- [Haga clic en el espectro para activar un panadapter (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Abrir un panadapter en su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
