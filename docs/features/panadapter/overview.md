# Descripción general del panadapter

El panadapter muestra un espectro FFT en tiempo real y un waterfall para un slice vinculado, y opcionalmente decodifica código Morse desde audio. Esta página describe cada control del panadapter y su panel de decodificación CW; siga los enlaces al final para instrucciones paso a paso.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El panadapter requiere una conexión de radio activa.
- El audio de la PC debe estar enrutado hacia AetherSDR para que el decodificador CW produzca salida.

## Cómo funciona

Cada panadapter es una pantalla independiente vinculada a un slice (Slice A hasta Slice H). El área principal muestra el espectro FFT en la parte superior y el waterfall debajo, dibujados por el SpectrumWidget. Haga clic en cualquier punto del espectro o el waterfall para activar ese panadapter; arrastre para sintonizar; desplace la rueda del mouse para hacer zoom.

En el diseño predeterminado de un solo panadapter, únicamente un panadapter es visible y los botones de su barra de título (desprender, maximizar, cerrar) están ocultos. Al agregar slices, cada panadapter obtiene su propia barra de título y esos botones quedan disponibles.

Debajo del espectro se encuentra un panel opcional de decodificación CW. Está oculto de forma predeterminada y aparece cuando se habilita la decodificación CW. El decodificador escucha el audio de la PC y utiliza el motor ggmorse para identificar el Morse; el texto decodificado se desplaza en una pantalla de solo lectura y se codifica por colores según el nivel de confianza.

## Qué hace cada control

### Barra de título

| Control | Tipo | Comportamiento |
|---|---|---|
| Título del slice | Indicador | Muestra el slice vinculado a este panadapter. Valor predeterminado: `Slice A`. Rango: Slice A–Slice H. |
| ⬈ / ↩ (desprender/acoplar) | Botón | Desprende el panadapter en una ventana flotante, o lo acopla de vuelta. Oculto en el modo de un solo panadapter. |
| □ (maximizar) | Botón | Maximiza este panadapter para llenar el área principal en un diseño de múltiples panadapters. Oculto en el modo de un solo panadapter. |
| × (cerrar) | Botón | Cierra este panadapter. Oculto en el modo de un solo panadapter. |

### Espectro y waterfall

| Control | Tipo | Comportamiento |
|---|---|---|
| Espectro / waterfall | Pantalla / controlador de arrastre | Haga clic para activar este panadapter. Arrastre hacia la izquierda o la derecha para sintonizar. Desplace la rueda del mouse para acercar o alejar. |

### Panel de decodificación CW

| Control | Tipo | Predeterminado | Rango | Clave de ajuste | Comportamiento |
|---|---|---|---|---|---|
| Etiqueta de estadísticas CW | Indicador | — | `<hz> Hz  <wpm> WPM` | — | Muestra el tono y la velocidad detectados actualmente por el decodificador. |
| Sens | Control deslizante | 30 | 0–100 | `CwDecoderSensitivity` | Filtra las decodificaciones de baja confianza. Valores más altos son más estrictos. Internamente mapea 0–100 a un umbral de costo de 1.0–0.1. |
| 🔒P (Lock Pitch) | Botón de alternancia | Off | On / Off | — | Fija el tono del decodificador a la frecuencia sintonizada actualmente. |
| 🔒S (Lock Speed) | Botón de alternancia | Off | On / Off | — | Fija la velocidad del decodificador al valor WPM actual. |
| Lo (tono mínimo) | Control deslizante | 500 Hz | 300–1200 Hz | — | Establece el tono mínimo que busca el decodificador. Limitado a no ser mayor que Hi. |
| Hi (tono máximo) | Control deslizante | 700 Hz | 300–1200 Hz | — | Establece el tono máximo que busca el decodificador. Limitado a no ser menor que Lo. |
| CPY ALL | Botón | — | — | — | Copia todo el buffer de texto decodificado al portapapeles. |
| CPY VIS | Botón | — | — | — | Copia al portapapeles solo el texto visible actualmente en el área de desplazamiento. |
| CLR | Botón | — | — | — | Borra el buffer de decodificación CW. |
| × (cerrar CW) | Botón | — | — | — | Oculta el panel de decodificación CW. |
| Texto decodificado CW | Pantalla de solo lectura | — | — | — | Pantalla continua del Morse decodificado. El texto se codifica por colores según el nivel de confianza de la decodificación: verde (mejor) pasando por amarillo y naranja hasta rojo (peor). |

## Consejos

- Lo y Hi definen la ventana de búsqueda de tono. Reducir este rango alrededor del tono real de la señal disminuye las decodificaciones falsas.
- La etiqueta de estadísticas CW muestra `(requires PC Audio)` cuando el audio aún no está enrutado. Si solo ve esta indicación y no hay tono ni WPM, verifique el enrutamiento de audio de su PC antes de ajustar Sens.
- El color del texto decodificado permite una verificación rápida de la calidad sin leer los caracteres sin procesar. Una cadena de texto en verde indica que el decodificador está siguiendo bien la señal.

## Relacionados

- [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Fijar el tono o la velocidad del decodificador CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
- [Desprender un panadapter en su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Maximizar un panadapter para llenar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Hacer clic en el espectro para activar un panadapter (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Comprensión de slices y VFOs](../../getting-started/concepts/understanding-slices.md)
