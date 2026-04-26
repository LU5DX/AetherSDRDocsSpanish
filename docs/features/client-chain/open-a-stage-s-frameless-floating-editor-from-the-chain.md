# Abrir el editor flotante sin marco de una etapa desde la cadena

Hacer doble clic en una ficha de etapa en el Aetherial Audio Chain abre el editor flotante sin marco de esa etapa, lo que permite acceder directamente a sus parámetros sin salir de la vista de la cadena.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón `PUDU` de la bandeja en la barra lateral derecha para activarlo.
- Decida si desea editar una etapa TX o una etapa RX, y asegúrese de que se muestre la cadena correcta.

## Pasos

1. Si la cadena muestra el lado incorrecto, haga clic en `TX` o `RX` en la parte superior del Aetherial Audio Chain para cambiar a la cadena que contiene la etapa que desea editar.
2. Localice la ficha de etapa que desea editar. Las fichas de la cadena TX están etiquetadas como `EQ`, `COMP`, `GATE`, `DESS`, `TUBE`, `PUDU` y `VERB`. Las fichas de la cadena RX están etiquetadas como `EQ`, `GATE`, `COMP`, `TUBE` y `PUDU`.
3. Haga doble clic en la ficha de etapa. El editor flotante sin marco de esa etapa se abre.

El texto de ayuda debajo de la cadena indica "Click to bypass · Double click to edit · Drag to reorder" como recordatorio rápido de las interacciones disponibles.

## Qué hace cada control

| Control | Tipo | Comportamiento | Ajuste persistido |
|---|---|---|---|
| `TX` | Botón de alternancia | Muestra la cadena DSP de TX. Color ámbar cuando está seleccionado. | `PooDooAudioActiveTab` |
| `RX` | Botón de alternancia | Muestra la cadena DSP de RX. Color ámbar cuando está seleccionado. | `PooDooAudioActiveTab` |
| Etapa de cadena TX (`EQ` / `COMP` / `GATE` / `DESS` / `TUBE` / `PUDU` / `VERB`) | Controlador de arrastre | Un solo clic activa o desactiva el bypass; doble clic abre el editor flotante sin marco; arrastrar reordena. | `ClientCompTxChainStages` |
| Etapa de cadena RX (`EQ` / `GATE` / `COMP` / `TUBE` / `PUDU`) | Controlador de arrastre | Un solo clic activa o desactiva el bypass; doble clic abre el editor flotante sin marco en modo RX; arrastrar reordena. | `ClientCompRxChainStages` |

## Consejos

- Un solo clic en una ficha de etapa activa o desactiva su estado de bypass, no abre su editor. Asegúrese de hacer doble clic para abrir el editor.
- Las cadenas TX y RX son independientes. Editar una etapa en un lado no afecta la etapa correspondiente en el otro lado.
- La última pestaña activa (`TX` o `RX`) se restaura automáticamente al volver a abrir el contenedor, mediante el ajuste persistido `PooDooAudioActiveTab`.

## Relacionados

- [Descripción general del Aetherial Audio Chain](overview.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Reordenar la cadena DSP de TX](reorder-the-tx-dsp-chain.md)
- [Reordenar la cadena DSP de RX (independiente del orden de TX)](reorder-the-rx-dsp-chain-independent-of-tx-order.md)
