# Reactivar una etapa específica después de un bypass global

Después de usar BYPASS para silenciar todas las etapas de la cadena TX o RX, puede reactivar etapas individuales una a la vez sin desactivar el bypass global ni restaurar todas las etapas a la vez.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón PUDU de la bandeja en la barra lateral derecha para mostrar el contenedor.
- BYPASS debe estar activo en este momento (el botón BYPASS aparecerá marcado, con borde y relleno ámbar) en el lado de la cadena que desea editar.
- Confirme que está viendo el lado de la cadena correcto — haga clic en TX o RX para cambiar si es necesario.

## Pasos

1. En la fila de encabezado del Aetherial Audio Chain, confirme que BYPASS está marcado. Mientras BYPASS está activo, todas las etapas aparecen visualmente deshabilitadas.
2. Haga clic en TX o RX para asegurarse de que se muestra el lado de la cadena que desea editar.
3. Localice el tile de la etapa que desea reactivar en la tira horizontal (para TX: EQ, COMP, GATE, DESS, TUBE, PUDU, VERB; para RX: EQ, AGC-T, AGC-C, TUBE, PUDU).
4. Haga un solo clic en ese tile de etapa. Esto desactiva el bypass únicamente para esa etapa, reactivándola mientras todas las demás etapas permanecen en bypass.
5. Repita el paso 4 para cualquier etapa adicional que desee reactivar individualmente.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| TX | Botón de alternancia | Cambia la vista de la cadena a la cadena DSP de TX. TX y RX mantienen estados de etapa y capturas de BYPASS independientes. |
| RX | Botón de alternancia | Cambia la vista de la cadena a la cadena DSP de RX. |
| BYPASS | Botón de alternancia | Cuando está marcado, captura las etapas actualmente habilitadas y las deshabilita todas. Cuando se desmarca, restaura únicamente las etapas que estaban activas antes. Las etapas activadas o desactivadas manualmente mientras BYPASS está activo se conservan fuera de la captura. |
| Etapa de la cadena TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | Tile de etapa | Un solo clic activa o desactiva el bypass solo para esa etapa. Doble clic abre su editor flotante sin marco. Arrastrar reordena la cadena. |
| Etapa de la cadena RX (EQ / AGC-T / AGC-C / TUBE / PUDU) | Tile de etapa | Un solo clic activa o desactiva el bypass solo para esa etapa. Doble clic abre su editor flotante sin marco en modo RX. Arrastrar reordena la cadena RX. Las cinco etapas RX están completamente implementadas. El orden es independiente de la cadena TX. |

## Consejos

- Reactivar manualmente una etapa mientras BYPASS está marcado coloca esa etapa fuera de la captura de bypass. Si posteriormente desmarca BYPASS para hacer una restauración completa, se aplica el estado previo al bypass de esa etapa (no su estado actual). Reactive únicamente las etapas que deliberadamente desea tener activas durante el bypass.
- TX y RX mantienen capturas de BYPASS separadas. Habilitar etapas específicas en el lado TX no afecta la captura del lado RX, y viceversa.
- La sugerencia debajo de la tira de la cadena indica "Click to bypass · Double click to edit · Drag to reorder" y se aplica a ambos lados de la cadena.

## Relacionados

- [Poner en bypass todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Poner en bypass todas las etapas RX a la vez](bypass-every-rx-stage-at-once.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Abrir el editor flotante sin marco de una etapa desde la cadena](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
