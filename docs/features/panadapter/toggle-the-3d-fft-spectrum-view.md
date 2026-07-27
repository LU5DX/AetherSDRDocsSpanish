# Alternar la vista de espectro FFT 3D

Cambie la visualización del espectro desde la vista por defecto en cascada FFT 2D a una vista de superficie 3D que muestra el historial de señales desplazándose hacia adelante en el tiempo, con sombras de elevación para los marcadores de segmento.

## Antes de comenzar

- Su radio debe estar conectada y el panadapter visible en la ventana principal.
- El panadapter debe estar en estado normal (acoplado) — la alternancia 3D es parte del SpectrumWidget integrado en cada Panadapter.

## Pasos

1. Localice el área de visualización del espectro del panadapter (la región FFT / en cascada).
2. Haga clic en el botón de alternancia **3D FFT view** en el panadapter. Este botón alterna entre la vista de espectro 2D por defecto y la vista de superficie 3D.
   - La etiqueta del botón dice **3D FFT view** (un botón de alternancia en el SpectrumWidget).
   - El estado por defecto es **Disabled**.
3. Para volver a la vista 2D, haga clic nuevamente en la alternancia **3D FFT view**.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Botón de alternancia **3D FFT view** | Alterna entre el espectro/cascada 2D y la vista de superficie 3D. Cuando está habilitado, el historial de señales se muestra como una superficie 3D que se desplaza hacia adelante con sombras de elevación proyectadas por las banderas de segmento. El piso se resincroniza después del zoom de ancho de banda. |

## Consejos

- La vista FFT 3D incluye límites de historial con desplazamiento suave y sombras de elevación en caché para los marcadores de segmento.
- El zoom de ancho de banda funciona normalmente — el piso se resincroniza automáticamente.
- Esta funcionalidad es nueva en la versión 26.7.x y es parte del SpectrumWidget.

## Relacionado

- [Leer el historial de señales como una superficie 3D desplazable](read-signal-history-as-a-scrolling-3d-surface.md)
