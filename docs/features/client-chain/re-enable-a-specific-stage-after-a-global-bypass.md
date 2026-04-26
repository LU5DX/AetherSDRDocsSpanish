# Reactivar una etapa específica después de un bypass global

Después de usar BYPASS para silenciar todas las etapas de TX DSP a la vez, es posible que desee volver a activar una sola etapa sin liberar el bypass global. Esta página muestra cómo hacerlo sin alterar la instantánea que BYPASS está manteniendo.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón PUDU de la bandeja en la barra lateral derecha para mostrarlo.
- TX debe ser el modo activo en el applet. Confirme que el botón de alternancia TX esté marcado (ámbar). BYPASS no tiene efecto en modo RX.
- BYPASS debe estar ya marcado. Si no lo está, este procedimiento no aplica — haga clic directamente en una etapa para alternarla.

## Pasos

1. Localice la tira de cadena en el contenedor PooDoo Audio. Las etapas se muestran de izquierda a derecha: Eq, Comp, Gate, DeEss, Tube, Enh / PUDU, Reverb.
2. Encuentre la etapa que desea reactivar. Las etapas en bypass aparecen visualmente inactivas.
3. Haga clic una vez en esa etapa. Un solo clic alterna el estado de bypass únicamente para esa etapa, volviéndola a activar mientras todas las demás etapas en bypass permanecen desactivadas.
4. Repita el proceso para cualquier otra etapa individual que desee restaurar.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| BYPASS | Marcado: toma una instantánea de las etapas actualmente habilitadas y las deshabilita todas. Desmarcado: restaura exactamente las etapas que estaban activas antes. | Desmarcado | — |
| Etapa de cadena (Eq) | Un clic alterna el bypass para la etapa de ecualización. | — | `ClientCompTxChainStages` |
| Etapa de cadena (Comp) | Un clic alterna el bypass para el compresor. | — | `ClientCompTxChainStages` |
| Etapa de cadena (Gate) | Un clic alterna el bypass para el gate. | — | `ClientCompTxChainStages` |
| Etapa de cadena (DeEss) | Un clic alterna el bypass para el de-esser. | — | `ClientCompTxChainStages` |
| Etapa de cadena (Tube) | Un clic alterna el bypass para el saturador de tubo. | — | `ClientCompTxChainStages` |
| Etapa de cadena (Enh / PUDU) | Un clic alterna el bypass para el excitador PUDU. | — | `ClientCompTxChainStages` |
| Etapa de cadena (Reverb) | Un clic alterna el bypass para el reverb. | — | `ClientCompTxChainStages` |

## Consejos

- Las etapas alternadas manualmente mientras BYPASS está marcado se registran fuera de la instantánea. Si posteriormente desmarca BYPASS, solo se restauran las etapas que estaban activas antes de marcar BYPASS por primera vez — las etapas que reactivó individualmente durante el bypass no forman parte de esa instantánea.
- Para restaurar todas las etapas previamente habilitadas a la vez, simplemente desmarque BYPASS. Esto es más rápido que hacer clic en cada etapa individualmente.
- La sugerencia que aparece debajo de la tira de cadena dice "Click to bypass · Double click to edit · Drag to reorder" y es visible siempre que el modo TX esté activo. Hacer doble clic en una etapa abre su editor en lugar de alternarla.

## Solución de problemas

- **Hacer clic en una etapa no produce ningún efecto visible** — Confirme que TX sea el modo activo. La vista de cadena RX es un marcador de posición y BYPASS no tiene efecto allí. Haga clic en TX para volver.
- **Desmarcar BYPASS no restaura la etapa que reactivó manualmente** — Esto es esperado. Las etapas que alterna individualmente mientras BYPASS está marcado quedan excluidas de la instantánea que BYPASS registra. Configure la etapa después de desmarcar BYPASS.

## Relacionado

- [Poner en bypass todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Abrir el editor flotante de una etapa desde la cadena](open-a-stage-s-floating-editor-from-the-chain.md)
- [Alternar entre la vista de cadena TX y el marcador de posición RX](switch-between-tx-chain-view-and-rx-placeholder.md)
