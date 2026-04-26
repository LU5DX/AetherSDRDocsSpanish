# Abrir el editor flotante de una etapa desde la cadena

Cada etapa de la cadena TX DSP tiene un editor flotante dedicado donde puede ajustar sus parámetros en detalle. Al hacer doble clic en el mosaico de una etapa se abre ese editor sin afectar el estado de bypass de la etapa.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón PUDU de la bandeja en la barra lateral derecha para mostrarlo.
- La cadena debe estar en modo TX. Confirme que TX esté seleccionado (no RX) en la parte superior de la tira de cadena.

## Pasos

1. Localice la tira de cadena en la parte superior del contenedor PooDoo Audio. La línea de ayuda debajo de la tira indica "Click to bypass · Double click to edit · Drag to reorder".
2. Identifique la etapa que desea editar: Eq, Comp, Gate, DeEss, Tube, Enh / PUDU o Reverb.
3. Haga doble clic en el mosaico de la etapa. El editor de esa etapa se abre como ventana flotante.
4. Ajuste los parámetros en el editor según sea necesario. Cierre el editor cuando termine.

## Qué hace cada control

| Mosaico de etapa | Abre el editor de | Acción con un solo clic |
|---|---|---|
| Etapa de cadena (Eq) | EQ | Activa o desactiva el bypass de la etapa EQ |
| Etapa de cadena (Comp) | Compresor | Activa o desactiva el bypass del compresor |
| Etapa de cadena (Gate) | Gate | Activa o desactiva el bypass del gate |
| Etapa de cadena (DeEss) | De-esser | Activa o desactiva el bypass del de-esser |
| Etapa de cadena (Tube) | Saturador de tubo | Activa o desactiva el bypass del saturador de tubo |
| Etapa de cadena (Enh / PUDU) | Excitador PUDU | Activa o desactiva el bypass del excitador PUDU |
| Etapa de cadena (Reverb) | Reverb | Activa o desactiva el bypass del reverb |

El orden de la tira de cadena y los estados de bypass por etapa se guardan en `ClientCompTxChainStages`. La visibilidad del contenedor TXDSP se guarda en `Applet_TXDSP`.

## Consejos

- Un solo clic en el mosaico de una etapa activa o desactiva su bypass en lugar de abrir el editor. Asegúrese de hacer doble clic para acceder al editor.
- Abrir un editor no aplica bypass ni modifica de ninguna otra forma el estado activo de la etapa.

## Temas relacionados

- [Reordenar la cadena TX DSP](reorder-the-tx-dsp-chain.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Reactivar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Cambiar entre la vista de cadena TX y el marcador de posición RX](switch-between-tx-chain-view-and-rx-placeholder.md)
