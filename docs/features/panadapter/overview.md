# Descripción general del panadapter

El panadapter muestra un espectro FFT en tiempo real y un waterfall para una slice de radio, lo que permite visualizar la actividad de la banda y sintonizar haciendo clic o arrastrando. Cada panadapter también puede mostrar un panel opcional de decodificación CW que lee el código Morse directamente del aire dentro de la aplicación.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panadapter requiere una conexión de radio activa.
- Para la decodificación CW, el enrutamiento de audio del PC hacia AetherSDR debe estar configurado. El panel muestra el aviso "(requires PC Audio)" cuando esto no está configurado.

## Cómo funciona

AetherSDR se abre con un panadapter visible en el centro de la ventana principal. Siempre está presente; no es posible cerrar el último panadapter. En el modo multi-slice, aparecen panadapters adicionales, cada uno en su propio contenedor con título. Cada panadapter está vinculado a una slice (Slice A hasta Slice H), indicada en la barra de título.

**Espectro y waterfall.** La parte superior del panadapter muestra la traza del espectro FFT; debajo se encuentra el waterfall. Haga clic en cualquier parte del espectro o del waterfall para activar ese panadapter. Arrastre para desplazarse por la banda. Use la rueda de desplazamiento para hacer zoom. Los elementos de menú `View > Single-Click to Tune` y `View > Pan Follows VFO` afectan la forma en que los clics y el desplazamiento interactúan con el VFO.

**Barra de título.** La barra de título de 16 píxeles en la parte superior de cada panadapter contiene la etiqueta de la slice, un control de arrastre y (en el modo multi-slice) los botones para desacoplar, maximizar y cerrar. En el modo de panadapter único, esos tres botones están ocultos.

**Panel de decodificación CW.** Un panel opcional puede aparecer debajo del waterfall. Ejecuta un decodificador Morse fuera del aire y muestra el texto decodificado en un campo de solo lectura con desplazamiento continuo, con código de colores según la confianza del decodificador. El panel está oculto de forma predeterminada y se habilita desde los controles del modo CW. Consulte [Activar el decodificador CW para leer código Morse del aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).

## Qué hace cada control

### Barra de título

| Control | Tipo | Comportamiento | Notas |
|---|---|---|---|
| Título de la slice | Indicador | Muestra la slice vinculada a este panadapter. Valores: Slice A – Slice H. | — |
| ⬈ / ↩ (desacoplar/acoplar) | Botón | Extrae el panadapter a una ventana flotante o lo vuelve a acoplar. | Oculto en el modo de panadapter único. La ventana flotante no tiene marco; arrástrela mediante la barra de título interna y redimensiónela mediante el control de tamaño en la esquina inferior derecha. |
| □ (maximizar) | Botón | Maximiza este panadapter para ocupar el área del diseño principal. | Oculto en el modo de panadapter único. |
| × (cerrar) | Botón | Cierra este panadapter. | Oculto en el modo de panadapter único. |

### Espectro / waterfall

| Control | Tipo | Comportamiento |
|---|---|---|
| Espectro / waterfall | Área de visualización y arrastre | Haga clic para activar el panadapter. Arrastre para desplazarse. Use la rueda para hacer zoom. |

### Panel de decodificación CW

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|---|
| Etiqueta de estadísticas CW | Indicador | — | `<hz> Hz  <wpm> WPM` | — | Muestra el tono y la velocidad detectados actualmente por el decodificador. |
| Sens | Control deslizante | 30 | 0 – 100 | `CwDecoderSensitivity` | Filtra las decodificaciones de baja confianza. Los valores más altos son más estrictos. Internamente asigna el rango 0 – 100 a un umbral de costo de 1,0 – 0,1. |
| 🔒P (Lock Pitch) | Botón de alternancia | Off | On / Off | — | Fija el tono del decodificador en la frecuencia sintonizada actualmente. |
| 🔒S (Lock Speed) | Botón de alternancia | Off | On / Off | — | Fija la velocidad del decodificador en la lectura WPM actual. |
| Lo (tono mínimo) | Control deslizante | 500 Hz | 300 – 1200 Hz | — | Establece el tono mínimo que busca el decodificador. Se limita para no ser mayor que Hi. |
| Hi (tono máximo) | Control deslizante | 700 Hz | 300 – 1200 Hz | — | Establece el tono máximo que busca el decodificador. Se limita para no ser menor que Lo. |
| CPY ALL | Botón | — | — | — | Copia el búfer completo de texto decodificado al portapapeles. |
| CPY VIS | Botón | — | — | — | Copia únicamente el texto visible actualmente en el área de desplazamiento al portapapeles. |
| CLR | Botón | — | — | — | Borra el búfer de decodificación CW. |
| × (cerrar CW) | Botón | — | — | — | Oculta el panel de decodificación CW. |
| Texto decodificado CW | Campo de texto de solo lectura | — | — | — | Visualización continua del código Morse decodificado, con color según la confianza: verde (mayor confianza), amarillo y naranja hasta rojo (menor confianza). Haga clic derecho en el área de texto para abrir un menú contextual; el menú incluye acciones de texto estándar y un elemento **Clear** que borra el búfer de decodificación. |

## Consejos

- Los controles deslizantes de tono Lo y Hi delimitan el rango de frecuencias que busca el decodificador. Reducir este rango alrededor del tono CW esperado disminuye las decodificaciones falsas en una banda con mucha actividad.
- El color del texto decodificado refleja la confianza del decodificador. El texto verde es el más fiable; el texto rojo debe tratarse con precaución. Aumente Sens para suprimir los caracteres rojos y naranja si el ruido genera salida incorrecta.
- `CwDecoderSensitivity` se conserva entre sesiones. No es necesario ajustarlo cada vez que abra la aplicación.
- Puede borrar el búfer de decodificación desde el menú contextual del clic derecho en el área de texto decodificado, como alternativa a hacer clic en CLR.

## Relacionados

- [Activar el decodificador CW para leer código Morse del aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar el ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Fijar el tono o la velocidad del decodificador CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
- [Extraer un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Maximizar un panadapter para ocupar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Hacer clic en el espectro para activar un panadapter (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Comprensión de las slices y los VFO](../../getting-started/concepts/understanding-slices.md)
