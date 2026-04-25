# Reordenar la cadena DSP de TX

Arrastre las fichas de etapa en la tira PooDoo Audio Chain para cambiar el orden en que las etapas DSP procesan el audio de TX. El nuevo orden se guarda en `ClientCompTxChainStages`.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado `PUDU` en la barra lateral derecha para mostrarlo.
- TX debe estar seleccionado en el applet. El botón TX está marcado de forma predeterminada; si RX está seleccionado, haga clic en TX para volver a la vista de cadena interactiva.

## Pasos

1. Localice la tira de cadena en la parte superior del contenedor PooDoo Audio. La tira muestra las etapas en su orden de procesamiento actual: Eq, Comp, Gate, DeEss, Tube, Enh, Reverb.
2. Haga clic y mantenga presionada cualquier ficha de etapa (por ejemplo, Chain stage (Comp)).
3. Arrastre la ficha hacia la izquierda o la derecha hasta la posición que desee en la cadena. Un indicador visual muestra dónde se colocará la etapa.
4. Suelte el botón del mouse. La etapa se fija en su nueva posición y el orden se guarda en `ClientCompTxChainStages`.

## Qué hace cada control

| Control | Tipo | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|---|
| TX | Botón de alternancia | Muestra la cadena DSP de TX interactiva. Color ámbar cuando está seleccionado. | Marcado | — |
| RX | Botón de alternancia | Cambia a la vista de marcador de posición de RX. El arrastre no está disponible en este modo. | Sin marcar | — |
| BYPASS | Botón de alternancia | Marcado: deshabilita todas las etapas a la vez. Sin marcar: restaura solo las etapas que estaban habilitadas antes. | Sin marcar | — |
| Chain stage (Eq) | Controlador de arrastre | Un clic omite el ecualizador; doble clic abre el editor; arrastrar reordena. | — | — |
| Chain stage (Comp) | Controlador de arrastre | Un clic omite el compresor; doble clic abre el editor; arrastrar reordena. | — | — |
| Chain stage (Gate) | Controlador de arrastre | Un clic omite la puerta de ruido; doble clic abre el editor; arrastrar reordena. | — | — |
| Chain stage (DeEss) | Controlador de arrastre | Un clic omite el de-esser; doble clic abre el editor; arrastrar reordena. | — | — |
| Chain stage (Tube) | Controlador de arrastre | Un clic omite el saturador de válvulas; doble clic abre el editor; arrastrar reordena. | — | — |
| Chain stage (Enh / PUDU) | Controlador de arrastre | Un clic omite el excitador PUDU; doble clic abre el editor; arrastrar reordena. | — | — |
| Chain stage (Reverb) | Controlador de arrastre | Un clic omite el reverb; doble clic abre el editor; arrastrar reordena. | — | — |

## Consejos

- El texto de ayuda debajo de la tira de cadena indica "Click to bypass · Double click to edit · Drag to reorder" y es visible siempre que el modo TX esté activo. Está oculto en el modo RX.
- Un solo clic en una ficha de etapa omite esa etapa, no toda la cadena. Tenga cuidado de no hacer clic cuando su intención sea arrastrar.
- BYPASS no restablece el orden de las etapas. El reordenamiento realizado mientras BYPASS está activo se conserva al desmarcar BYPASS.

## Solución de problemas

- **La tira de cadena no es visible** — Es posible que el botón RX esté seleccionado. Haga clic en TX para cambiar a la vista de cadena interactiva.
- **El arrastre no tiene efecto** — Confirme que el contenedor PooDoo Audio muestra la cadena de TX. La interacción de arrastrar para reordenar no está disponible en la vista de marcador de posición de RX.

## Relacionado

- [Descripción general de PooDoo Audio Chain](overview.md)
- [Omitir todas las etapas de TX a la vez](bypass-every-tx-stage-at-once.md)
- [Abrir el editor flotante de una etapa desde la cadena](open-a-stage-s-floating-editor-from-the-chain.md)
- [Volver a habilitar una etapa específica tras un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Cambiar entre la vista de cadena TX y el marcador de posición RX](switch-between-tx-chain-view-and-rx-placeholder.md)
