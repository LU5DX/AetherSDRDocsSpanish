# Vista general del panadapter

El panadapter (visualizador panorámico de espectro) es la pantalla principal de AetherSDR para visualizar la actividad del espectro de RF. Combina un gráfico de espectro FFT y una cascada (*waterfall*) desplazable, y opcionalmente muestra un panel de decodificación CW debajo de la pantalla para leer código Morse fuera del aire.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El panadapter requiere una conexión de radio activa.
- Si desea utilizar el decodificador CW, primero debe configurar el enrutamiento de audio del PC hacia AetherSDR. El panel muestra un recordatorio "(requires PC Audio)" hasta que el audio esté disponible.

## Cómo funciona

Cada panadapter está vinculado a un slice (Slice A hasta Slice H). El título del slice se muestra en la barra de título del panadapter. En el modo de panadapter único, los botones de la barra de título para desprender, maximizar y cerrar están ocultos. Aparecen cuando hay más de un panadapter abierto.

**Interacción con el espectro y la cascada**

Hacer clic en cualquier lugar del área de espectro/cascada activa ese panadapter. Puede arrastrar para sintonizar y desplazar la rueda del ratón para hacer zoom. De forma predeterminada, se requiere un doble clic para resintonizar; active `View > Single-Click to Tune` para cambiar este comportamiento. Cuando `View > Pan Follows VFO` está activado (valor predeterminado), la pantalla se desplaza automáticamente para mantener visible el marcador VFO activo.

**Panel de decodificación CW**

El panel de decodificación CW aparece debajo del espectro cuando el decodificador CW está activado. Ejecuta un decodificador de código Morse fuera del aire sobre el audio del PC y muestra el texto decodificado en forma continua. Cada carácter se colorea según el nivel de confianza de la decodificación: verde (mayor confianza), amarillo, naranja y rojo (menor confianza). El panel puede ocultarse en cualquier momento con ✕.

## Qué hace cada control

### Barra de título

| Control | Tipo | Comportamiento | Notas |
|---|---|---|---|
| Título del slice | Indicador | Muestra el slice vinculado a este panadapter (p. ej., "Slice A"). | — |
| ⬈ / ↩ (desprender/acoplar) | Botón | Desprende el panadapter en una ventana flotante o lo acopla de nuevo. | Oculto en modo de panadapter único. |
| □ (maximizar) | Botón | Maximiza este panadapter para llenar el área del diseño principal. | Oculto en modo de panadapter único. |
| × (cerrar) | Botón | Cierra este panadapter. | Oculto en modo de panadapter único. |

### Espectro / cascada

| Control | Tipo | Comportamiento |
|---|---|---|
| Espectro / cascada | Pantalla y controlador de arrastre | Haga clic para activar; arrastre para sintonizar; desplace para hacer zoom. |

### Panel de decodificación CW

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|---|
| Etiqueta de estadísticas CW | Indicador | — | `<hz> Hz  <wpm> WPM` | — | Muestra el tono y la velocidad detectados actualmente por el decodificador. |
| Sens | Control deslizante | 30 | 0–100 | `CwDecoderSensitivity` | Filtra las decodificaciones de baja confianza. Los valores más altos son más estrictos. Mapea 0–100 a un umbral de costo de 1.0–0.1. |
| 🔒P (Lock Pitch) | Botón de alternancia | Off | — | — | Fija el tono del decodificador a la frecuencia sintonizada actual. |
| 🔒S (Lock Speed) | Botón de alternancia | Off | — | — | Fija la velocidad del decodificador a los WPM actuales. |
| Lo (tono mínimo) | Control deslizante | 500 Hz | 300–1200 Hz | — | Establece el tono mínimo en el que busca el decodificador. Limitado a ≤ Hi. |
| Hi (tono máximo) | Control deslizante | 700 Hz | 300–1200 Hz | — | Establece el tono máximo en el que busca el decodificador. Limitado a ≥ Lo. |
| CPY ALL | Botón | — | — | — | Copia el buffer completo de texto decodificado al portapapeles. |
| CPY VIS | Botón | — | — | — | Copia solo el texto visible actualmente en el área de desplazamiento al portapapeles. |
| CLR | Botón | — | — | — | Borra el buffer de decodificación CW. |
| ✕ (cerrar CW) | Botón | — | — | — | Oculta el panel de decodificación CW. |
| Texto decodificado CW | Área de texto de solo lectura | — | — | — | Visualización continua del código Morse decodificado. Los caracteres se colorean según la confianza: verde (<0.15), amarillo (<0.35), naranja (<0.60), rojo (≥0.60). |

## Consejos

- Lo y Hi definen la ventana de búsqueda de tono. Reducir el rango alrededor del tono conocido de una señal disminuye las decodificaciones falsas causadas por interferencias adyacentes.
- Establecer Sens en 0 muestra todos los intentos de decodificación, incluidos los de baja confianza. Auméntelo gradualmente hasta que desaparezca el ruido generado por señales no deseadas.
- Use 🔒P y 🔒S una vez que el decodificador haya capturado la señal con claridad. Esto evita que el decodificador se desplace si la señal se debilita temporalmente.

## Relacionados

- [Activar el decodificador CW para leer código Morse fuera del aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Fijar el tono o la velocidad del decodificador CW una vez que el seguimiento es estable](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
- [Desprender un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Maximizar un panadapter para llenar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Hacer clic en el espectro para activar un panadapter (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Comprender los slices y los VFOs](../../getting-started/concepts/understanding-slices.md)
