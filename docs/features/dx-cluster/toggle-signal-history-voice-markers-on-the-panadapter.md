# Alternar marcadores de señal de voz histórica en el panadapter

Active marcadores dorados en el panadapter que muestran señales detectadas con ancho de voz, ayudándole a identificar visualmente transmisiones de voz activas.

## Antes de comenzar

- AetherSDR debe estar ejecutándose (no se requiere conexión de radio para esta configuración).

## Pasos

1. Abra **Settings > SpotHub...**.
2. Haga clic en la pestaña **Display**.
3. Haga clic en **Signals** (etiquetado como "Signal History") para cambiarlo al estado activado.

Los marcadores dorados aparecen ahora en el panadapter en las frecuencias donde AetherSDR ha detectado señales con ancho de voz. Haga clic en un marcador con el cursor para sintonizar su slice activo a esa frecuencia.

## Función de cada control

| Control | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| **Signals** (botón de alternancia, etiquetado "Signal History" en la pestaña Display) | Deshabilitado | Activado / Desactivado | `SHistoryMarkersEnabled` |

Esta alternancia tiene una doble vía: también puede activarse desde **View > Signal History Markers** en el menú principal.

## Consejos

- Los marcadores dorados aparecen solo mientras la señal está activa. Use el control deslizante **Marker Lifetime** en la misma pestaña Display para controlar cuánto tiempo permanece visible un marcador inactivo (60 segundos predeterminado).
- Para eliminar todos los marcadores (y todos los spots) del panadapter de una vez, haga clic en **Clear All** en la pestaña Display.
- En las pestañas **Cluster** y **RBN**, haga clic en **Startup Commands…** para abrir un cuadro de diálogo donde puede ingresar un comando por línea (por ejemplo, `SET/NAME`, `SET/QTH`, `ACCEPT/SPOT`) que se envía automáticamente al clúster después de cada inicio de sesión. Los comandos se guardan en la configuración de la aplicación (`DxClusterStartupCommands` y `RbnStartupCommands` respectivamente).

## Relacionado

- [Toggle QRM markers to see persistent carriers and interference](toggle-qrm-markers-to-see-persistent-carriers-and-interference.md)
- [Adjust S-History marker lifetime, QRM gate and edge threshold](adjust-s-history-marker-lifetime-qrm-gate-and-edge-threshold.md)
- [Pick custom colors for voice signal and QRM markers](pick-custom-colors-for-voice-signal-and-qrm-markers.md)
- [Enable Snap to Step for precise S-History tuning](enable-snap-to-step-for-precise-s-history-tuning.md)
- [SpotHub dialog overview](spothub-dialog-overview.md)
