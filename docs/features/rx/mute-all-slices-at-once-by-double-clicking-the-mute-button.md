# Silenciar todos los segmentos de una vez haciendo doble clic en el botón de silencio

Silencie o reactive el audio de todos sus segmentos en una sola acción, sin tener que silenciar cada segmento individualmente.

## Antes de comenzar

- Debe tener más de un segmento activo (las pestañas A a H deben estar visibles en el applet RX Controls).
- El botón de silencio es el ícono del altavoz (🔊 / 🔇) en el applet RX Controls.

## Pasos

1. En el applet RX Controls, haga doble clic en el botón de silencio (🔊 cuando está activo, 🔇 cuando está silenciado).
2. Todos sus segmentos se silencian o reactivan al mismo tiempo, coincidiendo con el nuevo estado del botón.

## Función de cada control

| Control | Etiqueta | Predeterminado |
|---------|----------|----------------|
| Botón de silencio | 🔊 / 🔇 | 🔊 (activo) |

## Consejos

- La acción de un solo clic se retrasa debido al intervalo de discriminación de doble clic de la plataforma (~400 ms), por lo que un doble clic cancela el temporizador del clic simple y activa la acción sobre todos los segmentos.
- El estado de silencio no se guarda ni se restaura al reconectar: la radio es la fuente autorizada para el silencio de audio.

## Relacionados

- [Descripción general de RX Controls](overview.md)
- [Cambiar entre múltiples segmentos usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Entender por qué el estado de silencio no se restaura al reconectar (política de autoridad de la radio #2489)](../../getting-started/setup/understand-why-mute-state-is-not-restored-on-reconnect-radio-authoritative-policy-2489.md)
