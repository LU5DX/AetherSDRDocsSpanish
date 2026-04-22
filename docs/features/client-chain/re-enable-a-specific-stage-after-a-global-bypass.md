# Reactivar una etapa específica después de un bypass global

Después de usar BYPASS para silenciar todas las etapas de DSP de TX a la vez, es posible que desee restaurar una sola etapa — por ejemplo, el compresor — sin restaurar todas las demás. Al hacer clic directamente en esa etapa se anula la instantánea que mantiene BYPASS, de modo que la etapa se activa de forma independiente del estado global.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón PUDU de la bandeja en la barra lateral derecha para mostrarlo.
- TX debe estar seleccionado (no RX). Haga clic en TX en la fila de encabezado si es necesario.
- BYPASS debe estar marcado (activo). Si no lo está, consulte [Bypass de todas las etapas de TX a la vez](bypass-every-tx-stage-at-once.md).

## Pasos

1. Localice la tira de cadena que muestra los mosaicos de etapas: Eq, Comp, Gate, DeEss, Tube, Enh / PUDU, Reverb.
2. Haga clic en el mosaico de la etapa que desea reactivar — por ejemplo, haga clic una vez en el mosaico Comp.
3. La etapa se activa de forma independiente. Ahora está activa aunque BYPASS continúe marcado.
4. Repita el paso 2 para cualquier otra etapa individual que desee restaurar.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|---|
| BYPASS | Botón de alternancia | Desmarcado | Marcado: toma una instantánea de las etapas habilitadas actualmente y las deshabilita todas. Desmarcado: restaura exactamente las etapas que estaban activas antes. | — |
| Etapa de cadena (Eq) | Controlador de arrastre / alternancia | — | Un clic alterna el bypass de la etapa de EQ. | `ClientCompTxChainStages` |
| Etapa de cadena (Comp) | Controlador de arrastre / alternancia | — | Un clic alterna el bypass del compresor. | `ClientCompTxChainStages` |
| Etapa de cadena (Gate) | Controlador de arrastre / alternancia | — | Un clic alterna el bypass de la puerta de ruido. | `ClientCompTxChainStages` |
| Etapa de cadena (DeEss) | Controlador de arrastre / alternancia | — | Un clic alterna el bypass del de-esser. | `ClientCompTxChainStages` |
| Etapa de cadena (Tube) | Controlador de arrastre / alternancia | — | Un clic alterna el bypass del saturador de tubo. | `ClientCompTxChainStages` |
| Etapa de cadena (Enh / PUDU) | Controlador de arrastre / alternancia | — | Un clic alterna el bypass del excitador PUDU. | `ClientCompTxChainStages` |
| Etapa de cadena (Reverb) | Controlador de arrastre / alternancia | — | Un clic alterna el bypass de la reverberación. | `ClientCompTxChainStages` |

## Consejos

- Las etapas activadas o desactivadas manualmente mientras BYPASS está activo se conservan fuera de la instantánea. Cuando posteriormente desmarque BYPASS, la instantánea restaura únicamente las etapas que estaban habilitadas antes de activar BYPASS; no deshace los clics individuales realizados durante el bypass.
- Para restaurar todas las etapas a la vez, desmarque BYPASS en lugar de hacer clic en las etapas una por una.

## Relacionado

- [Bypass de todas las etapas de TX a la vez](bypass-every-tx-stage-at-once.md)
- [Descripción general de la cadena PooDoo Audio](overview.md)
- [Abrir el editor flotante de una etapa desde la cadena](open-a-stage-s-floating-editor-from-the-chain.md)
