# Abrir el editor flotante sin marco de una etapa desde la cadena

Al hacer doble clic en un mosaico de etapa en la cadena Aetherial Audio, se abre el editor flotante sin marco de esa etapa, lo que permite acceder directamente a sus parámetros sin abandonar el diseño de la ventana principal.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja **PUDU** en la barra lateral derecha para mostrarlo.
- Decida si desea editar una etapa TX o una etapa RX, y asegúrese de que la cadena correcta esté activa.

## Pasos

1. Si la cadena no muestra el lado que desea, haga clic en **TX** o **RX** en la fila de encabezado de la cadena Aetherial Audio para cambiar a esa cadena.
2. Localice el mosaico de etapa que desea editar. Los mosaicos de la cadena TX están etiquetados como **EQ**, **COMP**, **GATE**, **DESS**, **TUBE**, **PUDU** y **VERB**. Los mosaicos de la cadena RX están etiquetados como **EQ**, **GATE**, **COMP**, **TUBE** y **PUDU**.
3. Haga doble clic en el mosaico de etapa. Se abre el editor flotante sin marco correspondiente a esa etapa.

Un solo clic omite la etapa en lugar de abrir el editor. Asegúrese de hacer doble clic.

## Qué hace cada control

| Control | Tipo | Comportamiento | Ajuste persistido |
|---|---|---|---|
| **TX** | Botón de alternancia | Muestra la cadena DSP TX. Color ámbar cuando está seleccionado. | `PooDooAudioActiveTab` (`TX`) |
| **RX** | Botón de alternancia | Muestra la cadena DSP RX. Color ámbar cuando está seleccionado. | `PooDooAudioActiveTab` (`RX`) |
| Etapa de la cadena TX (**EQ** / **COMP** / **GATE** / **DESS** / **TUBE** / **PUDU** / **VERB**) | Mosaico de etapa | Un solo clic activa o desactiva el bypass. Doble clic abre el editor flotante sin marco. Arrastrar reordena la cadena. | `ClientCompTxChainStages` |
| Etapa de la cadena RX (**EQ** / **GATE** / **COMP** / **TUBE** / **PUDU**) | Mosaico de etapa | Un solo clic activa o desactiva el bypass. Doble clic abre el editor flotante sin marco en modo RX. Arrastrar reordena la cadena. | `ClientCompRxChainStages` |

## Consejos

- La línea de ayuda debajo de la cadena muestra "Click to bypass · Double click to edit · Drag to reorder" y sirve como recordatorio rápido de estas interacciones.
- Las cadenas TX y RX son independientes. Abrir un editor en el lado TX no afecta la cadena RX, y viceversa.
- La última pestaña activa (**TX** o **RX**) se restaura al volver a abrir el applet, por lo que regresará a la misma cadena que estaba editando anteriormente.

## Solución de problemas

- **Un solo clic realizó la acción incorrecta (se activó el bypass en lugar de abrir el editor)** — Hizo clic una sola vez en lugar de dos. Haga clic en el mosaico de etapa una segunda vez, o haga un solo clic nuevamente para restaurar el estado de bypass y luego haga doble clic para abrir el editor.
- **El contenedor TXDSP no es visible y no se puede acceder a la cadena** — Haga clic en el botón de bandeja **PUDU** en la barra lateral derecha para activar el contenedor Aetherial Audio.

## Relacionados

- [Descripción general de la cadena Aetherial Audio](overview.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Omitir todas las etapas RX a la vez](bypass-every-rx-stage-at-once.md)
- [Reordenar la cadena DSP TX](reorder-the-tx-dsp-chain.md)
- [Reordenar la cadena DSP RX (independiente del orden TX)](reorder-the-rx-dsp-chain-independent-of-tx-order.md)
