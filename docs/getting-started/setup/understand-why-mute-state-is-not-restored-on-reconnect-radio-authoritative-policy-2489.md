# Comprender por qué el estado de silencio no se restaura al reconectar (política de autoridad del radio #2489)

Cuando silencia un slice usando el botón de silencio en el applet de RX Controls, el estado de silencio no se guarda ni se restaura después de una desconexión y reconexión del radio. Esto es intencional: AetherSDR trata al radio como la fuente autoritaria para el estado de silencio de audio.

## Pasos

1. Haga clic en el botón de silencio (🔊 / 🔇) en el applet de RX Controls para silenciar o reactivar el audio del slice.
2. Desconecte y reconecte el radio — el botón de silencio vuelve a su estado predeterminado sin silencio (🔊).

## Qué hace cada control

| Control       | Etiqueta | Predeterminado |
|---------------|----------|----------------|
| Alternar silencio | 🔊 / 🔇 | 🔊 (sin silencio) |

## Detalles de comportamiento

- Un solo clic en el botón de silencio alterna el silencio para este slice. El ícono (🔊 o 🔇) se actualiza solo cuando el radio confirma el cambio de estado mediante `SliceModel::audioMuteChanged`.
- Un doble clic en el botón de silencio alterna el silencio para todos los slices propietarios simultáneamente.
- La acción de un solo clic se aplaza por el intervalo de doble clic de la plataforma (aproximadamente 400 ms). Este retraso permite que un doble clic anule el clic único y alterne todos los slices en su lugar.
- No se necesita ninguna bandera de supresión para la señal `clicked()` posterior de una secuencia de doble clic. El `eventFilter` devuelve `true` en `MouseButtonDblClick`, por lo que `QAbstractButton::mouseDoubleClickEvent` nunca se llama. El botón nunca entra en estado presionado en el segundo clic, y la segunda liberación no emite `clicked()`.

## Consejos

- El botón de silencio solo controla el audio del slice seleccionado actualmente. Cada slice tiene su propio alternador de silencio.
- Si necesita regularmente que el audio comience silenciado después de una reconexión, silencie el slice manualmente después de conectar, o use el silencio por hardware del radio si está disponible.

## Relacionado

- [Resumen de RX Controls](../../features/rx/overview.md)
- [Sintonice el radio a una frecuencia (escriba MHz en el indicador)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
