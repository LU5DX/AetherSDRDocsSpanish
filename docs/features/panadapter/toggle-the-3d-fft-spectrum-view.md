# Alternar la vista de espectro FFT 3D

Cambie la visualización del espectro de la cascada FFT 2D predeterminada a una vista de superficie 3D que muestra el historial de señales desplazándose hacia adelante en el tiempo, con sombras de elevación para los marcadores de slice.

## Antes de comenzar

- Su radio debe estar conectada y el panadapter debe ser visible en la ventana principal.
- El panadapter debe estar en estado normal (acoplado) — la alternativa 3D es parte del SpectrumWidget integrado en cada panadapter.

## Pasos

1. Localice el área de visualización del espectro del panadapter (la región FFT / cascada).
2. Haga clic en el botón de alternancia **3D FFT view** en el panadapter. Este botón es una alternancia que cambia entre el espectro 2D predeterminado y la vista de superficie 3D.
   - La etiqueta del botón dice **3D FFT view** (un botón de alternancia en el SpectrumWidget).
   - El estado predeterminado es **Disabled**.
3. Para volver a la vista 2D, haga clic nuevamente en la alternancia **3D FFT view**.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Botón de alternancia **3D FFT view** | Cambia entre el espectro/cascada 2D y la vista de superficie 3D. Cuando está habilitado, el historial de señales se muestra como una superficie 3D que se desplaza hacia adelante con sombras de elevación proyectadas por los indicadores de slice. El piso se resincroniza después del zoom de ancho de banda. |
| **Slice title** | Muestra qué slice está vinculado a este panadapter (Slice A a Slice H). |
| **⬈ / ↩ (pop-out/dock)** | Extrae el panadapter a una ventana flotante o lo vuelve a acoplar. Oculto en modo de un solo pan. La ventana flotante no tiene marco — arrástrela mediante la barra de título dentro de la aplicación y redimensione con el mango inferior derecho. En macOS, cada ciclo de extraer/acoplar vuelve a vincular la superficie GPU para que el espectro permanezca activo. El estado guardado de la ventana flotante no se restaura cuando se agregan panadapters posteriores. Al volver a acoplar, se recuperan las ranuras vacías del divisor. |
| **□ (maximizar)** | Maximiza este panadapter en un diseño de múltiples pan. Oculto en modo de un solo pan. |
| **× (cerrar)** | Cierra este panadapter. Oculto en modo de un solo pan. |
| **Spectrum / waterfall** | Haga clic para activar el panadapter; arrastre para sintonizar, desplácese para hacer zoom. |
| **Etiqueta de estadísticas CW** | Muestra el tono y la velocidad CW detectados en el formato `<hz> Hz  <wpm> WPM`. |
| **Sens** | Deslizador (0–100, predeterminado 30) que filtra decodificaciones de baja confianza; más alto = más estricto. Se asigna a un umbral de costo de 1.0–0.1. |
| **🔒P (Lock Pitch)** | Bloquea el tono del decodificador CW a la frecuencia sintonizada actual. |
| **🔒S (Lock Speed)** | Bloquea la velocidad del decodificador CW a los WPM actuales. |
| **Lo (pitch min)** | Deslizador (300–1200 Hz, predeterminado 500) para el tono mínimo que busca el decodificador CW; limitado a ≤ Hi. |
| **Hi (pitch max)** | Deslizador (300–1200 Hz, predeterminado 700) para el tono máximo que busca el decodificador CW; limitado a ≥ Lo. |
| **CPY ALL** | Copia todo el texto decodificado al portapapeles. |
| **CPY VIS** | Copia solo el texto visible actualmente en el área de desplazamiento. |
| **CLR** | Borra el búfer de decodificación CW. |
| **✕ (cerrar CW)** | Oculta el panel de decodificación CW. |
| **Texto de decodificación CW** | Pantalla rodante de solo lectura del CW decodificado con colores según la confianza. Colores: <0.15 verde, <0.35 amarillo, <0.60 naranja, ≥0.60 rojo. |

## Comportamiento del panadapter y modo canvas

El panadapter incluye varios comportamientos automáticos:

- La congelación/descongelación de la cascada está controlada por el estado de interbloqueo TRANSMITTING de la radio. Cuando cualquier cliente en la red (incluidos los clientes remotos) transmite, la cascada se congela; se descongela cuando termina la transmisión. Esto elimina el artefacto de estela de transmisión de 10 a 23 segundos después de soltar la tecla.
- Al reconectar la radio, la velocidad de fotogramas (FPS) deseada del panadapter y la duración de la línea de la cascada se vuelven a aplicar para evitar que se caigan silenciosamente al valor predeterminado de 10 Hz de la radio.
- Los panadapters secundarios (Slices B–H) tienen su rango de dBm preparado al reconectar para que el ajuste automático del piso de ruido comience desde la línea base correcta (en lugar del rango predeterminado que causaba un espectro plano al reconectar).
- Cuando el panadapter está alojado como un elemento en el canvas del espacio de trabajo (modo canvas), la barra de título transmite gestos de movimiento en vivo. Un umbral de arrastre de 6 px separa un clic (que activa el pan) de un arrastre. El botón de extracción permanece visible en modo canvas incluso si es el único panadapter.
- El decodificador CW también muestra una pista de que requiere enrutamiento de audio de PC para funcionar ("(requires PC Audio)").

## Consejos

- La vista FFT 3D incluye límites de historial con desplazamiento suave y sombras de elevación en caché para los marcadores de slice.
- El zoom de ancho de banda funciona normalmente — el piso se resincroniza automáticamente.
- Esta función es nueva en v26.7.x y es parte del SpectrumWidget.

## Relacionado

- [Leer el historial de señales como una superficie 3D en desplazamiento](read-signal-history-as-a-scrolling-3d-surface.md)
