# Reordenar la cadena DSP de TX

Arrastre las etapas DSP de TX a un orden diferente para cambiar la secuencia en que se procesa el audio antes de la transmisión. El nuevo orden se guarda automáticamente y persiste entre reinicios.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja con la etiqueta **PUDU** en la barra lateral derecha para mostrarlo.
- La cadena TX debe ser el lado activo. Si el botón **RX** está seleccionado actualmente, haga clic primero en **TX**.

## Pasos

1. Abra el contenedor Aetherial Audio haciendo clic en el botón de bandeja **PUDU** si aún no está visible.
2. Haga clic en **TX** en la fila de encabezado para asegurarse de que se muestre la cadena TX.
3. Localice la etapa que desea mover. La cadena TX contiene estas etapas: **EQ**, **COMP**, **GATE**, **DESS**, **TUBE**, **PUDU**, **VERB**.
4. Haga clic y mantenga presionado sobre el mosaico de la etapa que desea mover, luego arrástrelo hacia la izquierda o la derecha a lo largo de la tira de la cadena.
5. Una barra vertical de color cian aparece entre los mosaicos mientras arrastra, indicando dónde se colocará la etapa.
6. Suelte el botón del ratón para soltar la etapa en la nueva posición.
7. Repita el proceso para cualquier otra etapa que desee reordenar.

El nuevo orden de la cadena se guarda automáticamente en `ClientCompTxChainStages`.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **TX** | Botón de alternancia | Muestra y habilita la edición de la cadena DSP de TX. Debe estar seleccionado para arrastrar etapas TX. |
| **RX** | Botón de alternancia | Cambia la tira a la cadena RX. Las operaciones de arrastre en la tira RX no afectan el orden TX. |
| Etapa de la cadena TX (**EQ / COMP / GATE / DESS / TUBE / PUDU / VERB**) | Controlador de arrastre | Un clic alterna el bypass de esa etapa. Doble clic abre su editor flotante sin marco. Arrastre hacia la izquierda o la derecha para reordenar. |
| **BYPASS** | Botón de alternancia | Deshabilita todas las etapas del lado de la cadena que se muestra actualmente a la vez. No afecta el orden de las etapas. |
| Etapa de la cadena RX (**EQ / AGC-T / AGC-C / TUBE / PUDU**) | Controlador de arrastre | Un clic alterna el bypass de la etapa RX. Doble clic abre su editor flotante sin marco en modo RX. Arrastre hacia la izquierda o la derecha para reordenar la cadena RX. El orden es independiente de la cadena TX. |

## Consejos

- El texto de ayuda debajo de la cadena indica "Click to bypass · Double click to edit · Drag to reorder" como recordatorio rápido de las tres interacciones.
- Los órdenes de las cadenas TX y RX son completamente independientes. Reordenar la cadena TX no tiene ningún efecto en `ClientCompRxChainStages`.
- Las etiquetas de las etapas de la cadena RX son **AGC-T** (gate) y **AGC-C** (compresor). Estas corresponden a las funciones de puerta y compresor, respectivamente.
- Un solo clic sobre un mosaico de etapa alterna su estado de bypass, no produce un reordenamiento. Asegúrese de estar arrastrando, no haciendo clic, cuando desee mover una etapa.
- Si **BYPASS** está activado cuando reordena, las posiciones de las etapas se actualizan de todos modos. La instantánea de bypass se basa en qué etapas estaban habilitadas, no en su posición.

## Solución de problemas

- **El arrastre no hace nada o se rechaza la colocación** — Confirme que **TX** es el botón de modo seleccionado (resaltado en ámbar). El arrastre solo está activo en la tira de cadena que se muestra actualmente; si **RX** está seleccionado, no se aceptan colocaciones en la tira TX.
- **El nuevo orden se pierde después de reiniciar** — Esto no debería ocurrir si la colocación se completó correctamente (apareció el indicador de colocación cian y soltó sobre la tira). Si vuelve a ocurrir, verifique que AetherSDR tenga acceso de escritura al almacenamiento de configuración.

## Relacionados

- [Descripción general de la cadena Aetherial Audio](overview.md)
- [Reordenar la cadena DSP de RX (independiente del orden TX)](reorder-the-rx-dsp-chain-independent-of-tx-order.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Abrir el editor flotante sin marco de una etapa desde la cadena](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
