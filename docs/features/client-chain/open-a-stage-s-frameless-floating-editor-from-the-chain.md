# Abrir el editor flotante sin marco de una etapa desde la cadena

Hacer doble clic en un mosaico de etapa dentro de la Aetherial Audio Chain abre el editor flotante sin marco de esa etapa, lo que le permite acceder directamente a sus parámetros sin abandonar el diseño de la ventana principal.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja **PUDU** en la barra lateral derecha para mostrarlo.
- Decida si desea editar una etapa TX o una etapa RX, y asegúrese de que la cadena correcta esté activa.

## Pasos

1. Si la cadena no muestra el lado que desea, haga clic en **TX** o **RX** en la fila de encabezado de la Aetherial Audio Chain para cambiar a esa cadena.
2. Localice el mosaico de etapa que desea editar. Los mosaicos de la cadena TX están etiquetados como **EQ**, **COMP**, **GATE**, **DESS**, **TUBE**, **PUDU** y **VERB**. Los mosaicos de la cadena RX están etiquetados como **EQ**, **AGC-T**, **AGC-C**, **TUBE** y **PUDU**.
3. Haga doble clic en el mosaico de etapa. El editor flotante sin marco para esa etapa se abre.

Un solo clic pone la etapa en bypass en lugar de abrir el editor. Asegúrese de hacer doble clic.

## Qué hace cada control

| Control                                                                                    | Tipo          | Comportamiento                                                                                                                        |
|--------------------------------------------------------------------------------------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **TX**                                                                                     | Botón de alternancia | Muestra la cadena DSP de TX. Color ámbar cuando está seleccionado.                                                              |
| **RX**                                                                                     | Botón de alternancia | Muestra la cadena DSP de RX. Color ámbar cuando está seleccionado.                                                              |
| Etapa de cadena TX (**EQ** / **COMP** / **GATE** / **DESS** / **TUBE** / **PUDU** / **VERB**) | Mosaico de etapa | Un clic activa o desactiva el bypass. Doble clic abre el editor flotante sin marco. Arrastrar reordena la cadena.               |
| Etapa de cadena RX (**EQ** / **AGC-T** / **AGC-C** / **TUBE** / **PUDU**)                 | Mosaico de etapa | Un clic activa o desactiva el bypass. Doble clic abre el editor flotante sin marco en modo RX. Arrastrar reordena la cadena RX de forma independiente a la cadena TX. |

## Consejos

- La línea de ayuda debajo de la cadena indica "Click to bypass · Double click to edit · Drag to reorder" y sirve como recordatorio rápido de estas interacciones.
- Las cadenas TX y RX son independientes. Abrir un editor en el lado TX no afecta la cadena RX, y viceversa.
- La última pestaña activa (**TX** o **RX**) se restaura al volver a abrir el applet, por lo que regresará a la misma cadena que estaba editando anteriormente.

## Solución de problemas

- **Un solo clic realizó la acción incorrecta (se activó el bypass en lugar de abrir el editor)** — Hizo clic una vez en lugar de dos. Haga clic en el mosaico de etapa una segunda vez, o haga clic una vez más para restaurar el estado de bypass, y luego haga doble clic para abrir el editor.
- **El contenedor TXDSP no está visible y no se puede acceder a la cadena** — Haga clic en el botón de bandeja **PUDU** en la barra lateral derecha para activar el contenedor Aetherial Audio.

## Relacionados

- [Descripción general de la Aetherial Audio Chain](overview.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Poner en bypass todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Poner en bypass todas las etapas RX a la vez](bypass-every-rx-stage-at-once.md)
- [Reordenar la cadena DSP de TX](reorder-the-tx-dsp-chain.md)
- [Reordenar la cadena DSP de RX (independientemente del orden de TX)](reorder-the-rx-dsp-chain-independent-of-tx-order.md)
