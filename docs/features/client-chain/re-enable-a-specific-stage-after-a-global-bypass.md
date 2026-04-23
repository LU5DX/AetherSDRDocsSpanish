# Reactivar una etapa específica tras un bypass global

Cuando BYPASS está activo, todas las etapas de TX DSP se deshabilitan simultáneamente. Esta página muestra cómo reactivar una sola etapa dejando el resto en bypass.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón PUDU de la bandeja en la barra lateral derecha para mostrarlo.
- TX debe estar seleccionado (no RX). El botón TX está marcado por defecto; si RX está seleccionado, haga clic en TX.
- BYPASS debe estar activado (borde ámbar, color saturado). Si no lo está, consulte [Bypass de todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md).

## Pasos

1. Localice la tira de cadena. Los bloques de etapa — Eq, Comp, Gate, DeEss, Tube, Enh / PUDU, Reverb — son visibles en la tira horizontal debajo de la fila de encabezado TX / RX / BYPASS.
2. Identifique la etapa que desea reactivar.
3. Haga clic una vez en ese bloque de etapa. Un solo clic conmuta el estado de bypass únicamente para esa etapa, reactivándola sin afectar ninguna otra.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|---|
| BYPASS | Botón de alternancia | Desactivado | Activado: guarda una instantánea de todas las etapas habilitadas y las deshabilita todas. Desactivado: restaura exactamente las etapas que estaban activas antes. | — |
| Etapa de cadena (Eq) | Controlador de arrastre | — | Un clic alterna el bypass de la etapa de EQ. Doble clic abre su editor. Arrastrar reordena. | `ClientCompTxChainStages` |
| Etapa de cadena (Comp) | Controlador de arrastre | — | Un clic alterna el bypass del compresor. Doble clic abre su editor. Arrastrar reordena. | `ClientCompTxChainStages` |
| Etapa de cadena (Gate) | Controlador de arrastre | — | Un clic alterna el bypass de la puerta de ruido. Doble clic abre su editor. Arrastrar reordena. | `ClientCompTxChainStages` |
| Etapa de cadena (DeEss) | Controlador de arrastre | — | Un clic alterna el bypass del de-esser. Doble clic abre su editor. Arrastrar reordena. | `ClientCompTxChainStages` |
| Etapa de cadena (Tube) | Controlador de arrastre | — | Un clic alterna el bypass del saturador de tubo. Doble clic abre su editor. Arrastrar reordena. | `ClientCompTxChainStages` |
| Etapa de cadena (Enh / PUDU) | Controlador de arrastre | — | Un clic alterna el bypass del excitador PUDU. Doble clic abre su editor. Arrastrar reordena. | `ClientCompTxChainStages` |
| Etapa de cadena (Reverb) | Controlador de arrastre | — | Un clic alterna el bypass de la reverberación. Doble clic abre su editor. Arrastrar reordena. | `ClientCompTxChainStages` |

## Consejos

- Al hacer clic en un bloque de etapa mientras BYPASS está activado, se reactiva esa etapa de forma independiente. La instantánea de BYPASS no absorbe este cambio: si posteriormente desactiva BYPASS, solo se restauran las etapas que estaban habilitadas antes de que BYPASS se activara por primera vez. Las etapas que se conmutaron manualmente mientras BYPASS estaba activo se conservan fuera de esa instantánea.
- La indicación debajo de la tira de cadena dice "Click to bypass · Double click to edit · Drag to reorder" y solo es visible en modo TX.

## Relacionados

- [Bypass de todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Abrir el editor flotante de una etapa desde la cadena](open-a-stage-s-floating-editor-from-the-chain.md)
- [Reordenar la cadena TX DSP](reorder-the-tx-dsp-chain.md)
- [Descripción general de la cadena PooDoo Audio](overview.md)
