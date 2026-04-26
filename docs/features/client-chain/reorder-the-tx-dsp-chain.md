# Reordenar la cadena DSP de TX

Arrastre las etapas en la cadena DSP de TX para cambiar el orden en que se procesa el audio antes de la transmisión. El nuevo orden se guarda automáticamente y persiste entre sesiones.

## Antes de comenzar

- El contenedor Aetherial Audio debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado **PUDU** en el panel de applets para mostrarlo.
- La cadena TX debe ser la vista activa. Si el botón **RX** está actualmente seleccionado, haga clic en **TX** para cambiar.

## Pasos

1. Abra el contenedor Aetherial Audio haciendo clic en el botón de bandeja **PUDU** en el panel de applets, si no está ya visible.
2. En la fila de encabezado, haga clic en **TX** si no está ya seleccionado. La tira de la cadena TX se activa.
3. Localice la etapa que desea mover. La cadena TX contiene hasta siete etapas: EQ, COMP, GATE, DESS, TUBE, PUDU y VERB.
4. Haga clic y mantenga presionado sobre el mosaico de la etapa que desea reordenar.
5. Arrastre el mosaico hacia la izquierda o la derecha a lo largo de la tira de la cadena. Aparece una barra vertical de color cian entre los mosaicos para indicar dónde se colocará la etapa cuando suelte.
6. Suelte el botón del ratón para soltar la etapa en la nueva posición.
7. Repita el procedimiento para cualquier otra etapa que desee reordenar.

El orden actualizado se guarda inmediatamente en `ClientCompTxChainStages`.

## Qué hace cada control

| Control | Tipo | Predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|---|
| **TX** | Botón de alternancia | Activado | Muestra y habilita la edición de la cadena DSP de TX. Forma parte de un par exclusivo con **RX**. | `PooDooAudioActiveTab` |
| **RX** | Botón de alternancia | Desactivado | Cambia la vista a la cadena RX. El reordenamiento de la cadena TX no está disponible mientras RX está activo. | `PooDooAudioActiveTab` |
| Etapa de la cadena TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | Controlador de arrastre | — | Un solo clic activa o desactiva el bypass de la etapa. Doble clic abre su editor flotante sin marco. Arrastrar reordena la cadena TX. | — |
| **BYPASS** | Botón de alternancia | Desactivado | Activado: guarda una instantánea de las etapas habilitadas actualmente y las desactiva todas. Desactivado: reactiva únicamente las etapas que estaban activas antes. No afecta el orden de las etapas. | — |

## Consejos

- Una indicación estática debajo de la tira de la cadena muestra "Click to bypass · Double click to edit · Drag to reorder" como recordatorio rápido de las tres interacciones disponibles.
- El indicador de colocación cian muestra la posición de destino antes de soltar, lo que permite ajustar el punto de destino sin confirmar la acción.
- Las cadenas TX y RX tienen órdenes independientes. Reordenar la cadena TX no afecta la cadena RX, y viceversa.
- Si desea comparar su audio con y sin el orden de cadena actual, use **BYPASS** para deshabilitar todas las etapas temporalmente sin perder el orden establecido.

## Relacionados

- [Descripción general de la cadena Aetherial Audio](overview.md)
- [Reordenar la cadena DSP de RX (independiente del orden de TX)](reorder-the-rx-dsp-chain-independent-of-tx-order.md)
- [Aplicar bypass a todas las etapas de TX a la vez](bypass-every-tx-stage-at-once.md)
- [Abrir el editor flotante sin marco de una etapa desde la cadena](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
