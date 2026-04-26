# Descripción general del panadapter

El panadapter es la pantalla principal de AetherSDR: un espectro FFT en tiempo real y un waterfall que muestra la actividad de radiofrecuencia en la banda sintonizada. Un panel opcional de decodificación CW, ubicado debajo, puede decodificar código Morse en tiempo real desde el aire.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El panadapter requiere una conexión de radio activa.
- Si desea usar el decodificador CW, el enrutamiento de audio del PC hacia AetherSDR debe estar activo. El panel muestra el recordatorio "(requires PC Audio)" hasta que el audio esté disponible.

## Cómo funciona

AetherSDR se abre con un panadapter visible en el centro de la ventana principal. La barra de título en la parte superior del panadapter indica qué slice está vinculado a él (por defecto: "Slice A", desde Slice A hasta Slice H). En el modo multi-slice, cada slice tiene su propio panadapter con su propia barra de título y controles.

### Espectro y waterfall

El área de espectro y waterfall ocupa el cuerpo principal del panadapter. Al hacer clic en él, se activa ese panadapter. Arrastrar sintoniza el VFO; desplazar con la rueda amplía o reduce el rango de frecuencia. Con `View > Pan Follows VFO` habilitado (la opción predeterminada), la pantalla se desplaza automáticamente para mantener el marcador del VFO en vista.

### Controles de la barra de título

En el modo de un solo panel, los botones ⬈ / ↩, □ y × están ocultos. Se vuelven visibles cuando se agrega un segundo panadapter.

| Control | Función |
|---|---|
| Título del slice | Indicador que muestra qué slice (Slice A–Slice H) está vinculado a este panadapter. |
| ⬈ / ↩ (separar/acoplar) | Extrae el panadapter a una ventana flotante o lo vuelve a acoplar. Oculto en el modo de un solo panel. |
| □ (maximizar) | Expande este panadapter para ocupar el área principal en un diseño de múltiples paneles. Oculto en el modo de un solo panel. |
| × (cerrar) | Cierra este panadapter. Oculto en el modo de un solo panel. |

### Panel de decodificación CW

El panel de decodificación CW aparece debajo del espectro cuando el decodificador CW está activado. Utiliza el audio del PC para detectar y decodificar código Morse desde el aire, y muestra el texto decodificado con colores según el nivel de confianza: verde (mayor confianza), amarillo, naranja y rojo (menor confianza). El tono y la velocidad detectados se muestran en la etiqueta de estadísticas CW con el formato `<hz> Hz  <wpm> WPM`.

## Qué hace cada control

### Controles del panel de decodificación CW

| Control | Valor predeterminado | Rango válido | Clave persistida | Función |
|---|---|---|---|---|
| Etiqueta de estadísticas CW | — | `<hz> Hz  <wpm> WPM` | — | Muestra el tono (Hz) y la velocidad (WPM) detectados por el decodificador. |
| Sens | 30 | 0–100 | `CwDecoderSensitivity` | Filtra decodificaciones de baja confianza. Los valores más altos son más estrictos. Asigna el rango 0–100 a un umbral de costo interno de 1.0–0.1. |
| 🔒P (Lock Pitch) | Desactivado | Activado / Desactivado | — | Bloquea el decodificador al tono detectado actualmente en lugar de seguirlo automáticamente. |
| 🔒S (Lock Speed) | Desactivado | Activado / Desactivado | — | Bloquea el decodificador a los WPM actuales en lugar de seguirlos automáticamente. |
| Lo (tono mínimo) | 500 Hz | 300–1200 Hz | — | Establece el límite inferior del rango de tono que busca el decodificador. Se limita para no superar el valor de Hi. |
| Hi (tono máximo) | 700 Hz | 300–1200 Hz | — | Establece el límite superior del rango de tono que busca el decodificador. Se limita para no ser inferior al valor de Lo. |
| CPY ALL | — | — | — | Copia el buffer completo de texto decodificado al portapapeles. |
| CPY VIS | — | — | — | Copia solo el texto visible actualmente en el área de desplazamiento al portapapeles. |
| CLR | — | — | — | Borra el buffer de decodificación CW. |
| × (close CW) | — | — | — | Oculta el panel de decodificación CW. |

## Consejos

- Los controles deslizantes de tono Lo y Hi limitan el rango de frecuencia en el que busca el decodificador. Reducir este rango alrededor del tono real de la señal (visible en el espectro) disminuye las detecciones falsas.
- El nivel de confianza del texto decodificado se indica por color: verde corresponde a un umbral de costo inferior a 0.15, amarillo inferior a 0.35, naranja inferior a 0.60, y rojo en 0.60 o superior. Aumentar el valor de Sens descarta el texto rojo y naranja.
- Con `View > Single-Click to Tune` habilitado, un solo clic en el espectro resintoniza el VFO. Sin esta opción, se requiere un doble clic.

## Relacionados

- [Activar el decodificador CW para leer Morse desde el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
- [Extraer un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Maximizar un panadapter para ocupar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Hacer clic en el espectro para activar un panadapter (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Comprender los slices y los VFOs](../../getting-started/concepts/understanding-slices.md)
