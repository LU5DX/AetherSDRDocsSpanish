# Reordenar la cadena DSP de RX (independiente del orden de TX)

Esta página explica cómo arrastrar las etapas DSP de RX a un orden diferente en la cadena Aetherial Audio. El orden de la cadena de RX se almacena y se aplica de forma completamente independiente al orden de la cadena de TX.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado "PUDU" en la barra lateral derecha para mostrarlo.
- Debe estar en la pestaña RX del applet. La cadena de RX no es visible mientras TX está seleccionado.

## Pasos

1. En el applet Aetherial Audio Chain, haga clic en **RX**. La tira de la cadena de RX reemplaza a la de TX. Las etapas mostradas son: EQ, GATE, COMP, TUBE y PUDU, delimitadas por los indicadores de estado RADIO, DSP y SPEAK.
2. Localice la etapa que desea mover. El texto de ayuda debajo de la tira indica "Click to bypass · Double click to edit · Drag to reorder", lo que confirma que la función de arrastrar para reordenar está activa.
3. Haga clic y mantenga presionado el mosaico de la etapa, luego arrástrelo hacia la izquierda o la derecha. Una barra vertical de color cian aparece entre los mosaicos para previsualizar dónde quedará la etapa.
4. Suelte para soltar la etapa en la posición indicada. La cadena se actualiza de inmediato y el nuevo orden se persiste en `ClientCompRxChainStages`.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|---|
| **RX** | Botón de alternancia | Sin marcar | Cambia la tira de la cadena para mostrar las etapas DSP de RX. La última pestaña activa (TX o RX) se restaura en el siguiente inicio. | `PooDooAudioActiveTab` |
| **TX** | Botón de alternancia | Marcado | Cambia la tira de la cadena para mostrar las etapas DSP de TX. El orden de TX es independiente del orden de RX. | `PooDooAudioActiveTab` |
| **Etapa de la cadena de RX (EQ / GATE / COMP / TUBE / PUDU)** | Controlador de arrastre | Orden predeterminado de fábrica | Un solo clic activa o desactiva el bypass de esa etapa. Doble clic abre su editor flotante sin marco. Arrastre hacia la izquierda o la derecha para reordenar. | `ClientCompRxChainStages` |
| **BYPASS** | Botón de alternancia | Sin marcar | Marcado: toma una instantánea de todas las etapas de RX actualmente habilitadas y las deshabilita. Sin marcar: reactiva solo las etapas que estaban activas antes. TX y RX mantienen instantáneas separadas. | — |

## Consejos

- La cadena de RX utiliza un tipo de arrastre interno distinto (`application/x-aethersdr-rx-chain-stage`), por lo que las etapas no pueden soltarse accidentalmente en la tira de la cadena de TX ni viceversa.
- Cambiar a la pestaña TX y volver no altera el orden de RX que haya establecido. Cada cadena almacena su estado de forma independiente.
- Los mosaicos RADIO, DSP y SPEAK en cada extremo de la tira de RX son únicamente indicadores de estado: no pueden moverse ni desactivarse.

## Solución de problemas

- **Arrastrar una etapa no tiene efecto**: confirme que está en la pestaña RX (el botón **RX** debe mostrar texto y borde de color ámbar). Arrastrar en la tira de TX solo afecta a `ClientCompTxChainStages`, no al orden de RX.
- **La cadena de RX no es visible**: el contenedor TXDSP puede estar oculto. Haga clic en el botón de bandeja etiquetado "PUDU" para activarlo.
- **El orden de la cadena se revierte después de reiniciar**: `ClientCompRxChainStages` es la clave persistida. Si la configuración no puede escribirse (por ejemplo, un perfil de solo lectura o un problema de permisos), el orden no sobrevivirá al reinicio.

## Relacionado

- [Reordenar la cadena DSP de TX](reorder-the-tx-dsp-chain.md)
- [Alternar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Desactivar todas las etapas de RX a la vez](bypass-every-rx-stage-at-once.md)
- [Abrir el editor flotante sin marco de una etapa desde la cadena](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
- [Ver de un vistazo si el audio de PC, el reductor de ruido y la salida de audio están activos (indicadores de estado de RX)](see-at-a-glance-whether-pc-audio-the-noise-reducer-and-audio-output-are-live-rx-status-tiles.md)
- [Descripción general de Aetherial Audio Chain](overview.md)
