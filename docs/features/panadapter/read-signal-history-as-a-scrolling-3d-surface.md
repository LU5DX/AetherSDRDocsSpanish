# Leer el historial de señales como una superficie 3D desplazable

Active la vista de espectro FFT 3D para ver el historial de señales representado como una superficie 3D que se desplaza hacia adelante, en lugar de la cascada 2D tradicional. La superficie muestra sombras de elevación de los indicadores de slice y resincroniza su base después de un zoom de ancho de banda.

## Antes de comenzar

- Su AetherSDR debe estar conectado a una radio FLEX-8600 (consulte [Radio Setup...] en el menú Settings).
- Debe haber un panadapter visible en la ventana principal que muestre datos de espectro y cascada.

## Pasos

1. Localice el botón de conmutación **3D FFT view** en el panadapter: está etiquetado con el icono de FFT 3D y se encuentra junto con los otros controles de espectro en el área SpectrumWidget.
2. Haga clic una vez en el botón de conmutación **3D FFT view** para activar la vista de superficie 3D. La visualización del espectro cambia de la cascada 2D plana a una superficie 3D desplazable.
3. Para volver a la vista 2D estándar, haga clic de nuevo en el mismo botón de conmutación **3D FFT view** para desactivarlo.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento | Clave de configuración |
|---------|---------------------|----------------|------------------------|
| Conmutador 3D FFT view | Desactivado | Activa/desactiva la vista de espectro FFT 3D que muestra el historial de señales como una superficie que se desplaza hacia adelante con sombras de elevación y límites de desplazamiento suave. | Ninguna |

## Consejos

- Los indicadores de slice proyectan sombras de elevación almacenadas en caché sobre la superficie 3D, lo que facilita identificar las posiciones de los slices activos de un vistazo.
- La base de la superficie 3D se resincroniza automáticamente después de cambiar el nivel de zoom del ancho de banda, evitando una línea de base plana o desalineada.
- La vista FFT 3D comparte el mismo comportamiento de congelación del panadapter que la cascada 2D: durante la transmisión (desde cualquier cliente), la visualización se congela y se reanuda cuando termina la transmisión.

## Relacionados

- [Toggle the 3D FFT spectrum view](toggle-the-3d-fft-spectrum-view.md)
- [Panadapter overview](overview.md)
