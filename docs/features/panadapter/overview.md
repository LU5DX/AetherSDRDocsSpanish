# Descripción general del panadapter

El panadapter muestra un espectro FFT en tiempo real y un waterfall (cascada) para un slice de radio, permitiéndole visualizar la actividad en la banda y sintonizar haciendo clic o arrastrando. Cada panadapter también puede mostrar un panel opcional de decodificación CW que lee el código Morse directamente en la aplicación.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panadapter requiere una conexión activa con la radio.
- Para la decodificación CW, se debe configurar el enrutamiento de audio del PC a AetherSDR. El panel muestra un recordatorio "(requires PC Audio)" cuando esto no está configurado.

## Cómo funciona

AetherSDR se abre con un panadapter visible en el centro de la ventana principal. Siempre está presente; no puede cerrar el último panadapter. En modo multislices, aparecen panadapters adicionales, cada uno en su propio contenedor con título. Cada panadapter está vinculado a un slice (Slice A a Slice H), que se muestra en la barra de título.

**Espectro y waterfall.** La parte superior del panadapter muestra la traza del espectro FFT; debajo está el waterfall. Haga clic en cualquier lugar del espectro o waterfall para activar ese panadapter. Arrastre para desplazarse por la banda. Desplace la rueda del ratón para hacer zoom. Los elementos de menú `View > Single-Click to Tune` y `View > Pan Follows VFO` afectan cómo interactúan los clics y el desplazamiento con el VFO.

**Barra de título.** La barra de título de 16 píxeles en la parte superior de cada panadapter contiene la etiqueta del slice, un asa de arrastre y (en modo multislices) los botones de desacoplar, maximizar y cerrar. En modo de un solo panadapter, esos tres botones están ocultos.

**Panel de decodificación CW.** Un panel opcional puede aparecer debajo del waterfall. Ejecuta un decodificador Morse fuera del aire y muestra el texto decodificado en un campo de solo lectura con desplazamiento, codificado por colores según la confianza del decodificador. El panel está oculto por defecto y se habilita desde los controles del modo CW. Consulte [Activar el decodificador CW para leer Morse fuera del aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).

## Función de cada control

### Barra de título

| Control | Tipo | Comportamiento | Notas |
|---|---|---|---|
| Título del slice | Indicador | Muestra el slice vinculado a este panadapter. Valores: Slice A – Slice H. | — |
| ⬈ / ↩ (desacoplar/acoplar) | Botón | Desacopla el panadapter en una ventana flotante, o lo vuelve a acoplar. | Oculto en modo de un solo panadapter. La ventana flotante no tiene marco; arrastre mediante la barra de título dentro de la aplicación, redimensione mediante el asa de tamaño en la esquina inferior derecha. |
| □ (maximizar) | Botón | Maximiza este panadapter para llenar el área de diseño principal. | Oculto en modo de un solo panadapter. |
| × (cerrar) | Botón | Cierra este panadapter. | Oculto en modo de un solo panadapter. |

### Espectro / waterfall

| Control | Tipo | Comportamiento |
|---|---|---|
| Espectro / waterfall | Área de visualización y arrastre | Haga clic para activar el panadapter. Arrastre para desplazarse. Desplace la rueda para hacer zoom. |

### Panel de decodificación CW

| Control | Tipo | Valor predet. | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|---|
| Etiqueta de estadísticas CW | Indicador | — | `<hz> Hz  <wpm> WPM` | — | Muestra el tono y la velocidad detectados actualmente por el decodificador. |
| Sens | Deslizador | 30 | 0 – 100 | `CwDecoderSensitivity` | Filtra decodificaciones de baja confianza. Los valores más altos son más estrictos. Internamente asigna el rango 0 – 100 a un umbral de costo de 1.0 – 0.1. |
| 🔒P (Bloquear tono) | Botón de alternancia | Desactivado | Activado / Desactivado | — | Bloquea el tono del decodificador en la frecuencia actualmente sintonizada. |
| 🔒S (Bloquear velocidad) | Botón de alternancia | Desactivado | Activado / Desactivado | — | Bloquea la velocidad del decodificador en la lectura actual de WPM. |
| Lo (tono mínimo) | Deslizador | 500 Hz | 300 – 1200 Hz | — | Establece el tono mínimo que busca el decodificador. Se limita para no superar a Hi. |
| Hi (tono máximo) | Deslizador | 700 Hz | 300 – 1200 Hz | — | Establece el tono máximo que busca el decodificador. Se limita para no ser inferior a Lo. |
| CPY ALL | Botón | — | — | — | Copia todo el búfer de texto decodificado al portapapeles. |
| CPY VIS | Botón | — | — | — | Copia solo el texto actualmente visible en el área de desplazamiento al portapapeles. |
| CLR | Botón | — | — | — | Limpia el búfer de decodificación CW. |
| × (cerrar CW) | Botón | — | — | — | Oculta el panel de decodificación CW. |
| Texto de decodificación CW | Campo de texto de solo lectura | — | — | — | Visualización continua del Morse decodificado, coloreado según la confianza: verde (mayor confianza) pasando por amarillo y naranja hasta rojo (menor confianza). Haga clic derecho en el área de texto para abrir un menú contextual; el menú incluye acciones de texto estándar y un elemento **Clear** que limpia el búfer de decodificación. |

## Consejos

- Los deslizadores de tono Lo y Hi limitan el rango de frecuencia que busca el decodificador. Reducir este rango alrededor del tono CW esperado reduce las falsas decodificaciones en una banda ocupada.
- El color del texto decodificado refleja la confianza del decodificador. El texto verde es el más fiable; el texto rojo debe tratarse con precaución. Ajuste Sens hacia arriba para suprimir los caracteres rojos y naranjas si el ruido produce salida no deseada.
- `CwDecoderSensitivity` se conserva entre sesiones. No necesita reajustarlo cada vez que abre la aplicación.
- Puede limpiar el búfer de decodificación desde el menú contextual con clic derecho (sin teclado) en el área de texto decodificado, como alternativa a hacer clic en CLR.

## Relacionados

- [Activar el decodificador CW para leer Morse fuera del aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento es bueno](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
- [Desacoplar un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Maximizar un panadapter para llenar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Hacer clic en el espectro para activar un panadapter (modo multislices)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Comprender los slices y los VFO](../../getting-started/concepts/understanding-slices.md)
