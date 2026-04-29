# Descripción general del panadapter

El panadapter muestra un espectro FFT en tiempo real y un waterfall para un slice de radio, lo que permite visualizar la actividad de banda y sintonizar haciendo clic o arrastrando. Cada panadapter también puede mostrar un panel opcional de decodificación CW que lee el código Morse del aire directamente en la aplicación.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panadapter requiere una conexión de radio activa.
- Para la decodificación CW, el enrutamiento de audio de PC hacia AetherSDR debe estar configurado. El panel muestra un recordatorio "(requires PC Audio)" cuando esto no está configurado.

## Cómo funciona

AetherSDR se abre con un panadapter visible en el centro de la ventana principal. Siempre está presente; no es posible cerrar el último panadapter. En el modo multi-slice, aparecen panadapters adicionales, cada uno en su propio contenedor con título. Cada panadapter está vinculado a un slice (Slice A hasta Slice H), que se muestra en la barra de título.

**Espectro y waterfall.** La parte superior del panadapter muestra la traza del espectro FFT; debajo se encuentra el waterfall. Haga clic en cualquier punto del espectro o del waterfall para activar ese panadapter. Arrastre para desplazarse por la banda. Use la rueda del ratón para hacer zoom. Los elementos de menú `View > Single-Click to Tune` y `View > Pan Follows VFO` afectan la forma en que los clics y el desplazamiento interactúan con el VFO.

**Barra de título.** La barra de título de 16 píxeles en la parte superior de cada panadapter muestra la etiqueta del slice, un control de arrastre y (en modo multi-slice) los botones de ventana flotante, maximizar y cerrar. En el modo de panel único, esos tres botones están ocultos.

**Panel de decodificación CW.** Un panel opcional puede aparecer debajo del waterfall. Ejecuta un decodificador de código Morse del aire y muestra el texto decodificado en un campo de solo lectura con desplazamiento, con código de color según la confianza del decodificador. El panel está oculto de forma predeterminada y se activa desde los controles del modo CW. Consulte [Activar el decodificador CW para leer código Morse del aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).

## Qué hace cada control

### Barra de título

| Control | Tipo | Comportamiento | Notas |
|---|---|---|---|
| Título del slice | Indicador | Muestra el slice vinculado a este panadapter. Valores: Slice A – Slice H. | — |
| ⬈ / ↩ (ventana flotante/acoplar) | Botón | Mueve el panadapter a una ventana flotante o lo vuelve a acoplar. | Oculto en modo de panel único. La ventana flotante no tiene marco; arrastre mediante la barra de título interna de la aplicación y cambie el tamaño mediante el control de tamaño en la esquina inferior derecha. |
| □ (maximizar) | Botón | Maximiza este panadapter para ocupar el área de diseño principal. | Oculto en modo de panel único. |
| × (cerrar) | Botón | Cierra este panadapter. | Oculto en modo de panel único. |

### Espectro / waterfall

| Control | Tipo | Comportamiento |
|---|---|---|
| Espectro / waterfall | Área de visualización y arrastre | Haga clic para activar el panadapter. Arrastre para desplazarse. Use la rueda del ratón para hacer zoom. |

### Panel de decodificación CW

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|---|
| Etiqueta de estadísticas CW | Indicador | — | `<hz> Hz  <wpm> WPM` | — | Muestra el tono y la velocidad detectados actualmente por el decodificador. |
| Sens | Control deslizante | 30 | 0 – 100 | `CwDecoderSensitivity` | Filtra las decodificaciones de baja confianza. Los valores más altos son más estrictos. Internamente asigna el rango 0 – 100 a un umbral de costo de 1.0 – 0.1. |
| 🔒P (Lock Pitch) | Botón de alternancia | Off | On / Off | — | Bloquea el tono del decodificador en la frecuencia sintonizada actualmente. |
| 🔒S (Lock Speed) | Botón de alternancia | Off | On / Off | — | Bloquea la velocidad del decodificador en la lectura WPM actual. |
| Lo (tono mínimo) | Control deslizante | 500 Hz | 300 – 1200 Hz | — | Establece el tono mínimo que busca el decodificador. Limitado para no ser mayor que Hi. |
| Hi (tono máximo) | Control deslizante | 700 Hz | 300 – 1200 Hz | — | Establece el tono máximo que busca el decodificador. Limitado para no ser menor que Lo. |
| CPY ALL | Botón | — | — | — | Copia el buffer completo de texto decodificado al portapapeles. |
| CPY VIS | Botón | — | — | — | Copia solo el texto visible actualmente en el área de desplazamiento al portapapeles. |
| CLR | Botón | — | — | — | Borra el buffer de decodificación CW. |
| × (cerrar CW) | Botón | — | — | — | Oculta el panel de decodificación CW. |
| Texto decodificado CW | Campo de texto de solo lectura | — | — | — | Visualización con desplazamiento del código Morse decodificado, con color según la confianza: verde (mayor confianza) pasando por amarillo y naranja hasta rojo (menor confianza). Haga clic derecho en el área de texto para abrir un menú contextual; el menú incluye acciones de texto estándar y un elemento **Clear** que borra el buffer de decodificación. |

## Consejos

- Los controles deslizantes de tono Lo y Hi limitan el rango de frecuencia que busca el decodificador. Estrechar este rango alrededor del tono CW esperado reduce las decodificaciones falsas en una banda con mucha actividad.
- El color del texto decodificado refleja la confianza del decodificador. El texto en verde es el más confiable; el texto en rojo debe tratarse con precaución. Aumente Sens para suprimir los caracteres rojos y naranja si el ruido está generando salida incorrecta.
- `CwDecoderSensitivity` se conserva entre sesiones. No es necesario reajustarlo cada vez que abra la aplicación.
- Puede borrar el buffer de decodificación desde el menú contextual del clic derecho en el área de texto decodificado, como alternativa a hacer clic en CLR.

## Relacionados

- [Activar el decodificador CW para leer código Morse del aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Bloquear el tono o la velocidad del decodificador CW cuando el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
- [Mover un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Maximizar un panadapter para ocupar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Hacer clic en el espectro para activar un panadapter (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Comprensión de slices y VFOs](../../getting-started/concepts/understanding-slices.md)
