# Silenciar todos los "slices" de una vez haciendo doble clic en el botón de silencio

Silencie o reactive el audio de todos los "slices" que posee en una sola acción, sin tener que silenciar cada "slice" individualmente.

## Antes de empezar

- Debe tener más de un "slice" activo (las pestañas A a la H deben estar visibles en el applet de controles de RX).
- El botón de silencio es el ícono del altavoz (🔊 / 🔇) en el applet de controles de RX.

## Pasos

1. En el applet de controles de RX, haga doble clic en el botón de silencio (🔊 cuando está activo, 🔇 cuando está silenciado).
2. Todos los "slices" que posee se silencian o reactivan juntos, coincidiendo con el nuevo estado del botón.

## Función de cada control

| Control | Etiqueta | Valor predeterminado | Comportamiento | Clave de configuración |
|---------|----------|----------------------|----------------|--------------------------|
| Botón de silencio | 🔊 / 🔇 | 🔊 (activo) | Un solo clic silencia/reactiva el "slice" actual. El doble clic silencia/reactiva todos los "slices" propios a través de la señal **muteAllToggled**. | Ninguna (el estado de silencio depende de la radio según la política n.º 2489) |

## Consejos

- La acción de un solo clic se retrasa por el intervalo de discriminación de doble clic de la plataforma (~400 ms), de modo que un doble clic cancela el temporizador de un solo clic y activa la acción sobre todos los "slice".
- El estado de silencio no se guarda ni se restablece al reconectar: la radio es la fuente de autoridad para el audio silenciado.

## Relacionado

- [Resumen de controles de RX](overview.md)
- [Cambiar entre varios "slices" usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Comprender por qué el estado de silencio no se restablece al reconectar (política n.º 2489 de autoridad de la radio)](../../getting-started/setup/understand-why-mute-state-is-not-restored-on-reconnect-radio-authoritative-policy-2489.md)
