# Silenciar todos los segmentos a la vez haciendo doble clic en el botón de silencio

Silencie o reactive el audio de todos sus segmentos con una sola acción, sin tener que silenciar cada segmento individualmente.

## Antes de comenzar

- Debe tener más de un segmento activo (las pestañas A a la H deben estar visibles en el applet de controles de RX).
- El botón de silencio es el ícono del altavoz (🔊 / 🔇) en el applet de controles de RX.

## Pasos

1. En el applet de controles de RX, haga doble clic en el botón de silencio (🔊 cuando no está silenciado, 🔇 cuando está silenciado).
2. Todos sus segmentos se silencian o reactivan al mismo tiempo, adoptando el nuevo estado del botón.

## Función de cada control

| Control                | Etiqueta | Valor predeterminado |
|------------------------|----------|----------------------|
| Botón de silencio      | 🔊 / 🔇  | 🔊 (sin silencio)    |

## Consejos

- La acción de un solo clic se aplaza según el intervalo de discriminación de doble clic de la plataforma (~400 ms), por lo que un doble clic cancela el temporizador del clic único y activa la acción sobre todos los segmentos.
- El estado de silencio no se guarda ni se restaura al reconectar; la radio es la fuente de referencia para el silencio de audio.

## Relacionados

- [Descripción general de controles de RX](overview.md)
- [Cambiar entre varios segmentos usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Comprender por qué el estado de silencio no se restaura al reconectar (política autoritativa de la radio #2489)](../../getting-started/setup/understand-why-mute-state-is-not-restored-on-reconnect-radio-authoritative-policy-2489.md)
