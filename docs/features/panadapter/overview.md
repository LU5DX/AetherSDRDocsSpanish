# Descripción general del panadapter

El panadapter es la pantalla principal de AetherSDR. Muestra un espectro FFT en vivo y un waterfall para un único slice (ranura de frecuencia), y opcionalmente un panel decodificador de CW fuera del aire debajo de él. Esta página describe cada control del panadapter y enlaza a páginas de tareas específicas.

## Cómo funciona

Cada panadapter está vinculado a un slice (mostrado en la barra de título como "Slice A" hasta "Slice H"). La parte superior es la pantalla de espectro y waterfall; hacer clic o arrastrar sobre ella sintoniza el slice vinculado. Desplazar la rueda del ratón amplía o reduce el rango de frecuencias.

En el modo de panadapter único, la barra de título muestra solo la etiqueta del slice y el control de arrastre. En el modo multi-slice, aparecen los botones de ventana flotante (⬈), maximizar (□) y cerrar (×) en la barra de título para reorganizar el diseño.

El panel decodificador de CW está oculto de forma predeterminada. Cuando está activo, se sitúa debajo del waterfall y ejecuta un decodificador Morse fuera del aire sobre el audio del PC enrutado a AetherSDR. El panel muestra el texto decodificado, el tono y la velocidad, y proporciona controles para sintonizar y bloquear el decodificador.

## Qué hace cada control

### Barra de título

| Control | Tipo | Comportamiento | Notas |
|---|---|---|---|
| Título del slice | Indicador | Muestra qué slice está vinculado (p. ej., "Slice A"). Rango: Slice A–Slice H. | — |
| ⬈ / ↩ (ventana flotante/acoplar) | Botón | Saca el panadapter a una ventana flotante; haga clic de nuevo para acoplarlo. | Oculto en el modo de panadapter único. |
| □ (maximizar) | Botón | Maximiza este panadapter para llenar el área principal. | Oculto en el modo de panadapter único. |
| × (cerrar) | Botón | Cierra este panadapter. | Oculto en el modo de panadapter único. |

### Espectro / waterfall

| Control | Tipo | Comportamiento |
|---|---|---|
| Espectro / waterfall | Control de arrastre | Haga clic para activar el panadapter (modo multi-slice); arrastre para desplazar la frecuencia; desplace la rueda para ampliar o reducir. |

### Panel decodificador de CW

| Control | Tipo | Valor predeterminado | Rango | Clave persistida | Comportamiento |
|---|---|---|---|---|---|
| Etiqueta de estadísticas CW | Indicador | — | `<hz> Hz  <wpm> WPM` | — | Muestra el tono y la velocidad detectados por el decodificador. |
| Sens | Control deslizante | 30 | 0–100 | `CwDecoderSensitivity` | Filtra decodificaciones de baja confianza. Valores más altos son más estrictos. Mapea 0–100 a un umbral de costo interno de 1.0–0.1. |
| 🔒P (Lock Pitch) | Botón de alternancia | Off | On/Off | — | Bloquea el tono del decodificador en la frecuencia sintonizada actual. |
| 🔒S (Lock Speed) | Botón de alternancia | Off | On/Off | — | Bloquea la velocidad del decodificador en el WPM actual. |
| Lo (tono mínimo) | Control deslizante | 500 Hz | 300–1200 Hz | — | Tono mínimo en el que busca el decodificador. Limitado a ≤ Hi. |
| Hi (tono máximo) | Control deslizante | 700 Hz | 300–1200 Hz | — | Tono máximo en el que busca el decodificador. Limitado a ≥ Lo. |
| CPY ALL | Botón | — | — | — | Copia el búfer completo de texto decodificado al portapapeles. |
| CPY VIS | Botón | — | — | — | Copia solo el texto visible actualmente en el área de desplazamiento al portapapeles. |
| CLR | Botón | — | — | — | Borra el búfer de decodificación CW. |
| ✕ (cerrar CW) | Botón | — | — | — | Oculta el panel decodificador de CW. |
| Texto decodificado CW | Campo de texto (solo lectura) | — | — | — | Pantalla continua de CW decodificado. El texto se colorea según la confianza de decodificación: verde (mayor confianza), pasando por amarillo y naranja, hasta rojo (menor confianza). |

## Consejos

- El decodificador CW requiere que el audio del PC esté enrutado a AetherSDR. Si el panel muestra "(requires PC Audio)", el enrutamiento de audio aún no está configurado.
- Lo y Hi están limitados entre sí: arrastrar Lo por encima de Hi ajusta Lo al valor de Hi, y viceversa. Establezca Lo primero y luego Hi.
- El color del texto decodificado refleja la confianza. El texto verde es el más fiable; el texto rojo debe tratarse con precaución.

## Relacionados

- [Activar el decodificador CW para leer Morse fuera del aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
- [Sacar un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Maximizar un panadapter para llenar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Hacer clic en el espectro para activar un panadapter (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Comprensión de los slices y los VFO](../../getting-started/concepts/understanding-slices.md)
