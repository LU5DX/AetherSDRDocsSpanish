# Reordenar la cadena DSP de TX

Arrastre las etapas DSP de TX a un orden diferente para cambiar la secuencia en que se procesa el audio antes de la transmisión. El nuevo orden se guarda automáticamente y persiste tras los reinicios.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja **PUDU** en la barra lateral derecha para mostrarlo.
- La cadena TX debe ser el lado activo. Si el botón **RX** está seleccionado actualmente, haga clic en **TX** primero.

## Pasos

1. Abra el contenedor Aetherial Audio haciendo clic en el botón de bandeja **PUDU** si aún no está visible.
2. Haga clic en **TX** en la fila de encabezado para asegurarse de que se muestra la cadena TX.
3. Localice la etapa que desea mover. La cadena TX contiene las siguientes etapas: **EQ**, **COMP**, **GATE**, **DESS**, **TUBE**, **PUDU**, **VERB**.
4. Haga clic y mantenga presionado sobre el mosaico de la etapa que desea mover, luego arrástrelo hacia la izquierda o la derecha a lo largo de la tira de la cadena.
5. Aparece una barra vertical cian entre los mosaicos mientras arrastra, indicando dónde se ubicará la etapa.
6. Suelte el botón del ratón para soltar la etapa en la nueva posición.
7. Repita el proceso para cualquier otra etapa que desee reordenar.

El nuevo orden de la cadena se guarda automáticamente en `ClientCompTxChainStages`.

## Qué hace cada control

| Control | Tipo | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|---|
| **TX** | Botón de alternancia | Muestra y habilita la edición de la cadena DSP de TX. Debe estar seleccionado para arrastrar etapas TX. | Activado | `PooDooAudioActiveTab` |
| **RX** | Botón de alternancia | Cambia la tira a la cadena RX. Las operaciones de arrastre en la tira RX no afectan el orden de TX. | Desactivado | `PooDooAudioActiveTab` |
| Etapa de la cadena TX (**EQ / COMP / GATE / DESS / TUBE / PUDU / VERB**) | Controlador de arrastre | Un solo clic activa o desactiva el bypass de esa etapa. Doble clic abre su editor flotante sin marco. Arrastre hacia la izquierda o la derecha para reordenar. | — | — |
| **BYPASS** | Botón de alternancia | Deshabilita todas las etapas del lado de la cadena que se muestra actualmente a la vez. No afecta el orden de las etapas. | Desactivado | — |

## Consejos

- El texto de ayuda debajo de la cadena indica "Click to bypass · Double click to edit · Drag to reorder" como recordatorio rápido de las tres interacciones.
- Los órdenes de las cadenas TX y RX son completamente independientes. Reordenar la cadena TX no tiene ningún efecto sobre `ClientCompRxChainStages`.
- Un solo clic en el mosaico de una etapa alterna su estado de bypass, no la reordena. Asegúrese de estar arrastrando, no haciendo clic, cuando desee mover una etapa.
- Si **BYPASS** está activado al reordenar, las posiciones de las etapas se actualizan de todas formas. La instantánea de bypass se basa en qué etapas estaban habilitadas, no en su posición.

## Solución de problemas

- **El arrastre no hace nada o el soltado es rechazado** — Confirme que **TX** es el botón de modo seleccionado (resaltado en ámbar). El arrastre solo está activo en la tira de la cadena que se muestra actualmente; si **RX** está seleccionado, no se aceptan soltados en la tira TX.
- **El nuevo orden se pierde después de reiniciar** — Esto no debería ocurrir si el soltado se completó correctamente (el indicador de soltado cian apareció y soltó sobre la tira). Si se repite, verifique que AetherSDR tenga acceso de escritura a su almacenamiento de configuración.

## Relacionado

- [Descripción general de la cadena Aetherial Audio](overview.md)
- [Reordenar la cadena DSP de RX (independiente del orden de TX)](reorder-the-rx-dsp-chain-independent-of-tx-order.md)
- [Desactivar todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Abrir el editor flotante sin marco de una etapa desde la cadena](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
