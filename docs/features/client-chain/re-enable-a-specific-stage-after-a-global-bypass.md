# Reactivar una etapa específica tras un bypass global

Después de usar BYPASS para silenciar toda la cadena TX o RX, es posible recuperar una o más etapas individuales sin desactivar el bypass global ni restaurar todas las etapas a la vez. Basta con hacer clic una vez en el bloque de la etapa.

## Antes de comenzar

- El Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón PUDU de la bandeja en la barra lateral derecha para mostrarlo.
- BYPASS debe estar activo en este momento (ámbar, activo) en la cadena — TX o RX — donde desea reactivar una etapa.
- Asegúrese de estar visualizando el lado correcto de la cadena. Haga clic en TX o RX en el encabezado del applet para confirmarlo.

## Pasos

1. Observe la fila de encabezado del Aetherial Audio Chain. Confirme que BYPASS está marcado (borde y relleno ámbar).
2. Si necesita trabajar en la cadena TX, haga clic en TX. Si necesita trabajar en la cadena RX, haga clic en RX.
3. Localice el bloque de la etapa que desea reactivar — por ejemplo, COMP en la cadena TX o GATE en la cadena RX.
4. Haga clic una vez en el bloque de la etapa. La etapa cambia de estado de bypass a activo.
5. Repita el paso 4 para cualquier otra etapa individual que desee restaurar.

El botón BYPASS permanece marcado. Solo las etapas en las que hizo clic están ahora activas; el resto permanece en bypass. Las etapas reactivadas de esta manera se preservan fuera del instantánea de bypass, por lo que al desactivar BYPASS más adelante solo se restauran las etapas que estaban activas *antes* de que BYPASS se activara por primera vez.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|---|
| TX | Botón de alternancia | Marcado | Cambia el applet para mostrar e interactuar con la cadena DSP TX (EQ, COMP, GATE, DESS, TUBE, PUDU, VERB). | `PooDooAudioActiveTab` |
| RX | Botón de alternancia | Sin marcar | Cambia el applet para mostrar e interactuar con la cadena DSP RX (EQ, GATE, COMP, TUBE, PUDU). | `PooDooAudioActiveTab` |
| BYPASS | Botón de alternancia | Sin marcar | Marcado: toma una instantánea de las etapas activas en ese momento y las desactiva todas. Sin marcar: restaura solo las etapas que estaban activas antes. TX y RX mantienen instantáneas independientes. | — |
| Etapa de la cadena TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | Bloque de etapa | — | Un clic alterna el bypass de esa etapa. Doble clic abre su editor sin marco. Arrastrar reordena la cadena. | `ClientCompTxChainStages` |
| Etapa de la cadena RX (EQ / GATE / COMP / TUBE / PUDU) | Bloque de etapa | — | Un clic alterna el bypass de esa etapa. Doble clic abre su editor sin marco. Arrastrar reordena la cadena. | `ClientCompRxChainStages` |

## Consejos

- Las etapas alternadas manualmente mientras BYPASS está activo no se registran en la instantánea de bypass. Si reactiva una etapa mientras BYPASS está marcado y luego lo desmarca, esa etapa permanece activa — la restauración de la instantánea no la desactivará.
- TX y RX mantienen instantáneas de bypass independientes. Hacer clic en BYPASS en un lado no afecta al otro.
- La línea de ayuda debajo de la cadena muestra "Click to bypass · Double click to edit · Drag to reorder" como recordatorio de que un solo clic es siempre una alternancia.

## Solución de problemas

- **Hacer clic en un bloque de etapa no produce ningún efecto** — Confirme que el contenedor del Aetherial Audio Chain está completamente expandido y que está haciendo clic en el bloque de la etapa en sí, no en el espacio entre bloques.
- **Desmarcar BYPASS restaura una etapa que quería mantener en bypass** — Cualquier etapa que estuviera activa antes de que BYPASS se marcara por primera vez se restaurará al desmarcar BYPASS. Para mantener una etapa en bypass tras desactivar BYPASS, haga clic en ella una vez después de desmarcar BYPASS para volver a desactivarla.

## Relacionados

- [Activar bypass en todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Activar bypass en todas las etapas RX a la vez](bypass-every-rx-stage-at-once.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Descripción general del Aetherial Audio Chain](overview.md)
