# Abrir el Editor Flotante de una Etapa desde la Cadena

Cada etapa en la cadena DSP de TX dispone de un editor flotante dedicado donde puede ajustar sus parámetros en detalle. Al hacer doble clic en el mosaico de una etapa, se abre ese editor sin afectar el estado de bypass de la etapa.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de la bandeja PUDU en la barra lateral derecha para mostrarlo.
- La cadena debe estar en modo TX. Confirme que TX está seleccionado (no RX) en la parte superior de la tira de la cadena.

## Pasos

1. Localice la tira de la cadena en la parte superior del contenedor PooDoo Audio. La línea de sugerencia debajo de la tira indica "Click to bypass · Double click to edit · Drag to reorder".
2. Identifique la etapa que desea editar: Eq, Comp, Gate, DeEss, Tube, Enh / PUDU o Reverb.
3. Haga doble clic en el mosaico de la etapa. El editor de esa etapa se abre como una ventana flotante.
4. Ajuste los parámetros en el editor según sea necesario. Cierre el editor cuando haya terminado.

## Función de cada control

| Mosaico de etapa | Abre el editor para | Acción de un solo clic |
|---|---|---|
| Etapa de cadena (Eq) | EQ | Activa/desactiva el bypass para la etapa EQ |
| Etapa de cadena (Comp) | Compresor | Activa/desactiva el bypass para el compresor |
| Etapa de cadena (Gate) | Puerta | Activa/desactiva el bypass para la puerta |
| Etapa de cadena (DeEss) | De-esser | Activa/desactiva el bypass para el de-esser |
| Etapa de cadena (Tube) | Saturdor de válvula | Activa/desactiva el bypass para el saturador de válvula |
| Etapa de cadena (Enh / PUDU) | Excitador PUDU | Activa/desactiva el bypass para el excitador PUDU |
| Etapa de cadena (Reverb) | Reverberación | Activa/desactiva el bypass para la reverberación |

El orden de la tira de la cadena y los estados de bypass por etapa se guardan bajo `ClientCompTxChainStages`. La visibilidad del contenedor TXDSP se guarda bajo `Applet_TXDSP`.

## Consejos

- Un solo clic en un mosaico de etapa activa o desactiva su bypass, no abre el editor. Asegúrese de hacer doble clic para acceder al editor.
- Abrir un editor no desvía ni cambia el estado activo de la etapa.

## Relacionado

- [Reordenar la cadena DSP de TX](reorder-the-tx-dsp-chain.md)
- [Pasar por alto todas las etapas de TX a la vez](bypass-every-tx-stage-at-once.md)
- [Reactivar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Cambiar entre la vista de la cadena TX y el marcador de posición RX](switch-between-tx-chain-view-and-rx-placeholder.md)
