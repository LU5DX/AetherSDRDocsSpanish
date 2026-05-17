# Alternar los marcadores de señal de voz en el panadaptador

Active marcadores dorados en el panadaptador que muestran las señales detectadas con ancho de voz, ayudándole a identificar visualmente transmisiones de voz activas.

## Antes de comenzar

- AetherSDR debe estar en ejecución (no se requiere conexión de radio para este ajuste).

## Pasos

1. Abra **Settings > SpotHub...**.
2. Haga clic en la pestaña **Display**.
3. Haga clic en **Signals** (etiquetado "Signal History") para activarlo al estado marcado/encendido.

Los marcadores dorados aparecen ahora en el panadaptador en las frecuencias donde AetherSDR ha detectado señales de ancho de voz. Haga clic en un marcador con el cursor para sintonizar su rebanada activa a esa frecuencia.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|
| **Signals** (botón de alternancia, etiquetado "Signal History" en la pestaña Display) | Desactivado | Activado / Desactivado | `SHistoryMarkersEnabled` |

Esta alternancia tiene una ruta dual — también se puede activar desde **View > Signal History Markers** en el menú principal.

## Consejos

- Los marcadores dorados aparecen solo mientras la señal está activa. Use el deslizador **Marker Lifetime** en la misma pestaña Display para controlar cuánto tiempo permanece visible un marcador inactivo (valor predeterminado 60 segundos).
- Para eliminar todos los marcadores (y todas las marcas) del panadaptador de una vez, haga clic en **Clear All** en la pestaña Display.
- En las pestañas **Cluster** y **RBN**, haga clic en **Startup Commands…** para abrir un cuadro de diálogo donde puede ingresar un comando por línea (por ejemplo, `SET/NAME`, `SET/QTH`, `ACCEPT/SPOT`) que se envía automáticamente al cluster después de cada inicio de sesión. Los comandos se guardan en la configuración de la aplicación (`DxClusterStartupCommands` y `RbnStartupCommands` respectivamente).

## Relacionado

- [Toggle QRM markers to see persistent carriers and interference](toggle-qrm-markers-to-see-persistent-carriers-and-interference.md)
- [Adjust S-History marker lifetime, QRM gate and edge threshold](adjust-s-history-marker-lifetime-qrm-gate-and-edge-threshold.md)
- [Pick custom colors for voice signal and QRM markers](pick-custom-colors-for-voice-signal-and-qrm-markers.md)
- [Enable Snap to Step for precise S-History tuning](enable-snap-to-step-for-precise-s-history-tuning.md)
