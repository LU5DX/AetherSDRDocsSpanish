# Comprenda por qué el estado de silencio no se restaura al reconectar (política radio-autoritaria #2489)

Cuando silencia un "slice" usando el botón de silencio en el applet RX Controls, el estado de silencio no se guarda ni se restaura después de una desconexión y reconexión del radio. Esto es por diseño: AetherSDR trata al radio como la fuente autoritaria para el estado de silencio de audio.

## Pasos

1. Haga clic en el botón de silencio (🔊 / 🔇) en el applet RX Controls para silenciar o reactivar el audio del "slice".
2. Desconéctese y reconéctese al radio — el botón de silencio regresa a su estado predeterminado sin silencio (🔊).

## Qué hace cada control

| Control | Etiqueta | Predeterminado | Comportamiento |
|---|---|---|---|
| Alternar silencio | 🔊 / 🔇 | 🔊 (sin silencio) | Silencia la salida de audio del "slice". El estado NO se guarda ni se restaura entre reconexiones según la Política de Configuración Radio-Autoritaria (#2489). |

## Consejos

- El botón de silencio solo controla el audio del "slice" seleccionado actualmente. Cada "slice" tiene su propio alternador de silencio.
- Si necesita que el audio comience silenciado regularmente después de una reconexión, silencie el "slice" manualmente después de conectarse, o use el silencio por hardware del radio si está disponible.

## Relacionado

- [Visión general de RX Controls](../../features/rx/overview.md)
- [Sintonice el radio a una frecuencia (escriba MHz en el indicador)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
