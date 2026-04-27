# Reactivar una etapa específica tras un bypass global

Después de usar BYPASS para silenciar todas las etapas de la cadena TX o RX, puede reactivar etapas individuales una a una sin desactivar el bypass global ni restaurar todas las etapas a la vez.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón PUDU de la bandeja en la barra lateral derecha para mostrar el contenedor.
- BYPASS debe estar activo en este momento (el botón BYPASS aparecerá marcado, con borde y relleno ámbar) en el lado de la cadena que desea editar.
- Confirme que está viendo el lado correcto de la cadena — haga clic en TX o RX para cambiar si es necesario.

## Pasos

1. En la fila de encabezado de Aetherial Audio Chain, confirme que BYPASS está marcado. Mientras BYPASS está activo, todas las etapas aparecen deshabilitadas visualmente.
2. Haga clic en TX o RX para asegurarse de que se muestra el lado de la cadena que desea editar.
3. Localice el tile de etapa que desea reactivar en la franja horizontal (para TX: EQ, COMP, GATE, DESS, TUBE, PUDU, VERB; para RX: EQ, GATE, COMP, TUBE, PUDU).
4. Haga clic una vez en ese tile de etapa. Esto desactiva el bypass solo para esa etapa, reactivándola mientras las demás etapas permanecen en bypass.
5. Repita el paso 4 para cualquier etapa adicional que desee reactivar individualmente.

## Qué hace cada control

| Control | Tipo | Comportamiento | Valor predeterminado | Clave persistida |
|---|---|---|---|---|
| TX | Botón de alternancia | Cambia la vista de la cadena a la cadena DSP de TX. TX y RX mantienen estados de etapa y snapshots de BYPASS independientes. | Marcado | `PooDooAudioActiveTab` |
| RX | Botón de alternancia | Cambia la vista de la cadena a la cadena DSP de RX. | Sin marcar | `PooDooAudioActiveTab` |
| BYPASS | Botón de alternancia | Cuando está marcado, guarda un snapshot de las etapas habilitadas en ese momento y las deshabilita todas. Cuando se desmarca, restaura únicamente las etapas que estaban activas antes. Las etapas que se activen manualmente mientras BYPASS está activo se conservan fuera del snapshot. | Sin marcar | — |
| Etapa de cadena TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | Tile de etapa | Un clic alterna el bypass solo para esa etapa. Doble clic abre su editor flotante sin marco. Arrastrar reordena la cadena. | — | `ClientCompTxChainStages` |
| Etapa de cadena RX (EQ / GATE / COMP / TUBE / PUDU) | Tile de etapa | Un clic alterna el bypass solo para esa etapa. Doble clic abre su editor flotante sin marco. Arrastrar reordena la cadena RX. | — | `ClientCompRxChainStages` |

## Sugerencias

- Reactivar manualmente una etapa mientras BYPASS está marcado coloca esa etapa fuera del snapshot de bypass. Si posteriormente desmarca BYPASS para hacer una restauración completa, se aplicará el estado previo al bypass de esa etapa (no su estado actual). Reactive únicamente las etapas que desee tener activas deliberadamente durante el bypass.
- TX y RX mantienen snapshots de BYPASS separados. Habilitar etapas específicas en el lado TX no afecta el snapshot del lado RX, y viceversa.
- La indicación debajo de la franja de la cadena dice "Click to bypass · Double click to edit · Drag to reorder" y se aplica a ambos lados de la cadena.

## Relacionados

- [Aplicar bypass a todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Aplicar bypass a todas las etapas RX a la vez](bypass-every-rx-stage-at-once.md)
- [Alternar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Abrir el editor flotante sin marco de una etapa desde la cadena](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
