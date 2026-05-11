# Activar los Medidores de FPS

Active los medidores de FPS para mostrar las lecturas de tasa de cuadros del espectro y el waterfall en el pie de página. Esto le ayuda a supervisar el rendimiento y diagnosticar problemas de representación.

## Antes de comenzar

- AetherSDR debe estar ejecutándose y conectado a una radio.

## Pasos

1. Abra el menú **View**.
2. Haga clic en **FPS Meters** para marcarlo (activar) o desmarcarlo (desactivar).

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Clave de AppSettings |
|---|---|---|---|
| **FPS Meters** (menú View) | Activa o desactiva las lecturas de FPS del espectro/waterfall en el pie de página. | Desactivado (sin marcar) | `DisplayFpsMeters` |

## Consejos

- Use los medidores de FPS para verificar que la escala de la interfaz de usuario u otros ajustes visuales no estén causando caídas en la tasa de cuadros.
- La lectura aparece en el pie de página de la ventana principal, entre otros indicadores de estado.

## Relacionado

- [Configure UI Scale](configure-ui-scale.md)
