# Rehabilitar una etapa específica tras un bypass global

Después de usar BYPASS para silenciar todas las etapas de DSP de TX a la vez, puede rehabilitar etapas individuales sin desactivar primero el bypass global. Esto resulta útil cuando desea auditar una sola etapa de forma aislada mientras el resto de la cadena permanece en silencio.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón PUDU de la bandeja en la barra lateral derecha para mostrarlo.
- TX debe estar seleccionado en el encabezado del applet de cadena (no RX).
- BYPASS debe estar ya activo (el interruptor BYPASS está marcado).

## Pasos

1. Localice el interruptor BYPASS en la fila de encabezado de la PooDoo Audio Chain. Confirme que está marcado (borde y relleno de color ámbar).
2. Encuentre la etapa que desea rehabilitar en la tira de cadena — por ejemplo, Chain stage (Comp) o Chain stage (Eq).
3. Haga clic una sola vez en el mosaico de esa etapa. La etapa cambia de estado de bypass a activa. Su estado visual se actualiza de inmediato.
4. Repita el paso 3 para cualquier otra etapa individual que desee rehabilitar.

Las etapas que rehabilite manualmente mientras BYPASS está marcado se preservan fuera del snapshot de bypass. Si posteriormente desmarca BYPASS, solo se restauran las etapas que estaban activas antes de que BYPASS se activara por primera vez; las etapas que activó manualmente durante el bypass conservan su estado actual.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| BYPASS | Marcado: guarda un snapshot de las etapas habilitadas actualmente y las desactiva todas. Desmarcado: vuelve a habilitar solo las etapas que estaban activas antes de que se activara BYPASS. | Desmarcado | — |
| Chain stage (Eq) | Un clic alterna el bypass de la etapa de EQ. | — | `ClientCompTxChainStages` |
| Chain stage (Comp) | Un clic alterna el bypass del compresor. | — | `ClientCompTxChainStages` |
| Chain stage (Gate) | Un clic alterna el bypass de la puerta de ruido. | — | `ClientCompTxChainStages` |
| Chain stage (DeEss) | Un clic alterna el bypass del de-esser. | — | `ClientCompTxChainStages` |
| Chain stage (Tube) | Un clic alterna el bypass del saturador de tubo. | — | `ClientCompTxChainStages` |
| Chain stage (Enh / PUDU) | Un clic alterna el bypass del excitador PUDU. | — | `ClientCompTxChainStages` |
| Chain stage (Reverb) | Un clic alterna el bypass del reverb. | — | `ClientCompTxChainStages` |

## Consejos

- Para devolver toda la cadena a su estado anterior al bypass en una sola acción, desmarque BYPASS. Solo se restauran las etapas que estaban habilitadas antes del snapshot de bypass; las etapas que activó individualmente mientras BYPASS estaba activo no se ven afectadas por esta restauración.
- La indicación de interacción que aparece debajo de la tira de cadena dice "Click to bypass · Double click to edit · Drag to reorder" — el clic simple siempre actúa como interruptor de bypass independientemente del estado de BYPASS.
- BYPASS no tiene efecto en modo RX. Cambie a TX antes de intentar rehabilitar etapas.

## Relacionados

- [Aplicar bypass a todas las etapas de TX a la vez](bypass-every-tx-stage-at-once.md)
- [Descripción general de PooDoo Audio Chain](overview.md)
- [Abrir el editor flotante de una etapa desde la cadena](open-a-stage-s-floating-editor-from-the-chain.md)
