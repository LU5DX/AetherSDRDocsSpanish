# Comprenda por qué el estado de silencio no se restaura al reconectar (política autoritativa del radio #2489)

Cuando silencia un segmento (slice) mediante el botón de silencio en el applet de Controles RX, el estado de silencio no se guarda ni se restaura después de una desconexión y reconexión del radio. Esto es intencional: AetherSDR trata al radio como la fuente autoritativa para el estado de silencio de audio.

## Pasos

1. Haga clic en el botón de silencio (🔊 / 🔇) en el applet de Controles RX para silenciar o activar el sonido del segmento.
2. Desconéctese y reconéctese al radio: el botón de silencio vuelve a su estado predeterminado sin silencio (🔊).

## Qué hace cada control

| Control           | Etiqueta | Predeterminado |
|--------------------|----------|----------------|
| Alternar silencio  | 🔊 / 🔇   | 🔊 (sin silencio) |

## Detalles de comportamiento

- Un solo clic en el botón de silencio alterna el silencio para este segmento. El icono (🔊 o 🔇) se actualiza solo cuando el radio confirma el cambio de estado mediante `SliceModel::audioMuteChanged`.
- Un doble clic en el botón de silencio alterna el silencio para todos los segmentos propios simultáneamente.
- La acción de un solo clic se retrasa por el intervalo de doble clic de la plataforma (aproximadamente 400 ms). Este retraso permite que un doble clic anule el clic simple y alterne todos los segmentos.
- No se necesita ninguna bandera de supresión para la señal `clicked()` posterior de una secuencia de doble clic. El `eventFilter` devuelve `true` en `MouseButtonDblClick`, por lo que `QAbstractButton::mouseDoubleClickEvent` nunca se llama. El botón nunca ingresa al estado presionado en el segundo clic, y la segunda liberación no emite `clicked()`.

## Consejos

- El botón de silencio solo controla el audio del segmento actualmente seleccionado. Cada segmento tiene su propio alternador de silencio.
- Si habitualmente necesita que el audio comience silenciado después de una reconexión, silencie manualmente el segmento después de conectar, o use el silencio por hardware del radio si está disponible.

## Relacionado

- [Resumen de Controles RX](../../features/rx/overview.md)
- [Sintonice el radio a una frecuencia (escriba MHz en el visor)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
