# Lea el historial de señales como una superficie 3D en desplazamiento

Active la vista de espectro FFT 3D para ver el historial de señales representado como una superficie 3D que avanza en desplazamiento, en lugar de la cascada 2D tradicional. La superficie muestra sombras de elevación de los indicadores de slice y resincroniza su base después de un zoom de ancho de banda.

## Antes de comenzar

- Su AetherSDR debe estar conectado a una radio FLEX-8600 (consulte [Radio Setup...] en el menú Settings).
- Debe haber un panadapter visible en la ventana principal que muestre datos de espectro y waterfall.

## Pasos

1. Localice el botón de conmutación **3D FFT view** en el panadapter: está etiquetado con el icono de FFT 3D y se encuentra junto con los demás controles de espectro en el área SpectrumWidget.
2. Haga clic una vez en el botón de conmutación **3D FFT view** para activar la vista de superficie 3D. La pantalla de espectro cambia de la waterfall 2D plana a una superficie 3D en desplazamiento.
3. Para volver a la vista 2D estándar, haga clic nuevamente en el mismo botón de conmutación **3D FFT view** para desactivarlo.

## Función de cada control

| Control | Valor predeterminado | Comportamiento | Clave de configuración |
|---------|---------|----------|-------------|
| Conmutador de vista FFT 3D | Desactivado | Activa/desactiva la vista de espectro FFT 3D que muestra el historial de señales como una superficie en desplazamiento hacia adelante con sombras de elevación y límites de desplazamiento suave. | Ninguna |
| Título de slice | Slice A | Muestra qué slice está vinculado a este panadapter (Slice A..Slice H). | Ninguna |
| ⬈ / ↩ (pop-out/dock) | — | Extrae el panadapter a una ventana flotante o lo vuelve a acoplar. Oculto en modo de pan único; siempre disponible cuando el panadapter está alojado en el lienzo del espacio de trabajo. | Ninguna |
| □ (maximizar) | — | Maximiza este panadapter en una distribución de múltiples pan. Oculto en modo de pan único. | Ninguna |
| × (cerrar) | — | Cierra este panadapter. Oculto en modo de pan único. | Ninguna |
| Espectro / waterfall | — | Haga clic para activar el panadapter; arrastre para sintonizar, desplácese para hacer zoom. | Ninguna |
| Etiqueta de estadísticas CW | — | Muestra el tono y la velocidad CW detectados como `<hz> Hz  <wpm> WPM`. | Ninguna |
| Sens | 30 | Filtra decodificaciones de baja confianza; mayor = más estricto. Asigna 0-100 al umbral de costo 1.0-0.1. | `CwDecoderSensitivity` |
| 🔒P (Lock Pitch) | — | Bloquea el tono del decodificador CW en la frecuencia sintonizada actual. | Ninguna |
| 🔒S (Lock Speed) | — | Bloquea la velocidad del decodificador CW en las WPM actuales. | Ninguna |
| Lo (mín. de tono) | 500 | Tono mínimo que busca el decodificador CW; limitado a ≤ Hi. Rango 300-1200 Hz. | Ninguna |
| Hi (máx. de tono) | 700 | Tono máximo que busca el decodificador CW; limitado a ≥ Lo. Rango 300-1200 Hz. | Ninguna |
| CPY ALL | — | Copia todo el texto decodificado al portapapeles. | Ninguna |
| CPY VIS | — | Copia solo el texto actualmente visible en el área de desplazamiento. | Ninguna |
| CLR | — | Borra el búfer de decodificación CW. | Ninguna |
| ✕ (cerrar CW) | — | Oculta el panel de decodificación CW. | Ninguna |
| Texto de decodificación CW | — | Pantalla de solo lectura en desplazamiento del CW decodificado, coloreado por confianza (verde <0.15, amarillo <0.35, naranja <0.60, rojo ≥0.60). | Ninguna |

## Comportamiento de congelación de waterfall y reconexión

- La waterfall se congela cada vez que cualquier cliente (incluido un segundo cliente FlexRadio) transmite, y se reanuda cuando finaliza la transmisión. Esto es controlado por el estado de interbloqueo TRANSMITTING de la radio, lo que elimina el artefacto de cola de TX de 10-23 s después de desactivar la tecla.
- Al reconectar la radio, el FPS deseado del panadapter y la duración de línea de la waterfall se restablecen automáticamente, evitando que caigan silenciosamente al valor predeterminado de 10 Hz de la radio.
- Los panadapters secundarios (Slices B-H) tienen su rango de dBm preestablecido al reconectar, de modo que el ajuste automático del piso de ruido comience desde la línea base correcta en lugar del rango predeterminado [-50, +50] que causaba un espectro plano al reconectar.

## Consejos

- Los indicadores de slice proyectan sombras de elevación almacenadas en caché sobre la superficie 3D, lo que facilita identificar las posiciones de slice activas de un vistazo.
- La base de la superficie 3D se resincroniza automáticamente después de cambiar el nivel de zoom de ancho de banda, evitando una línea base plana o desalineada.
- La vista FFT 3D comparte el mismo comportamiento de congelación del panadapter que la waterfall 2D: durante la transmisión (de cualquier cliente), la pantalla se congela y se reanuda cuando finaliza la transmisión.

## Alojamiento en lienzo

Cuando el panadapter está alojado como un elemento en el lienzo del espacio de trabajo (en lugar de la distribución estándar en pila):

- La franja de título muestra un gesto de movimiento en vivo que puede arrastrar para reposicionar el panadapter en el lienzo.
- Un umbral de arrastre de 6 px separa un clic (que activa el panadapter) de un arrastre.
- El botón de pop-out permanece disponible incluso en modo de pan único mientras está en el lienzo, de modo que siempre puede flotar un panadapter alojado en el lienzo.

## Relacionado

- [Toggle the 3D FFT spectrum view](toggle-the-3d-fft-spectrum-view.md)
- [Panadapter overview](overview.md)
