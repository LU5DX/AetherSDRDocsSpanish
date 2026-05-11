# Activar marcadores de historial de señales de voz en el panadapter

Active marcadores dorados en el panadapter que muestran las señales de ancho de voz detectadas, ayudándole a identificar visualmente transmisiones de voz activas.

## Antes de comenzar

- AetherSDR debe estar en ejecución (no se requiere conexión de radio para esta configuración).

## Pasos

1. Abra **Settings > SpotHub...**.
2. Haga clic en la pestaña **Display**.
3. Haga clic en **Signals** (etiquetado como "Signal History") para activarlo al estado marcado/encendido.

Los marcadores dorados aparecen ahora en el panadapter en las frecuencias donde AetherSDR ha detectado señales de ancho de voz. Haga clic en un marcador con el cursor para sintonizar su slice activo a esa frecuencia.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| **Signals** (botón de activación, etiquetado como "Signal History" en la pestaña Display) | Desactivado | Activado / Desactivado | `SHistoryMarkersEnabled` |

Este interruptor tiene una ruta dual; también se puede activar desde **View > Signal History Markers** en el menú principal.

## Consejos

- Los marcadores dorados aparecen solo mientras la señal está activa. Utilice el control deslizante **Marker Lifetime** en la misma pestaña Display para controlar cuánto tiempo permanece visible un marcador inactivo (60 segundos por defecto).
- Para eliminar todos los marcadores (y todas las spots) del panadapter de una sola vez, haga clic en **Clear All** en la pestaña Display.

## Relacionados

- [Toggle QRM markers to see persistent carriers and interference](toggle-qrm-markers-to-see-persistent-carriers-and-interference.md)
- [Adjust S-History marker lifetime, QRM gate and edge threshold](adjust-s-history-marker-lifetime-qrm-gate-and-edge-threshold.md)
- [Pick custom colors for voice signal and QRM markers](pick-custom-colors-for-voice-signal-and-qrm-markers.md)
- [Enable Snap to Step for precise S-History tuning](enable-snap-to-step-for-precise-s-history-tuning.md)
