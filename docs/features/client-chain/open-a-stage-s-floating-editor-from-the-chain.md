# Abrir el editor flotante de una etapa desde la cadena

Al hacer doble clic en una etapa de la cadena de audio PooDoo, se abre el editor flotante de esa etapa, lo que permite ajustar sus parámetros sin salir de la vista de cadena.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón PUDU del área de bandeja en la barra lateral derecha para mostrarlo.
- La cadena debe estar en modo TX. Haga clic en TX en la fila de encabezado si actualmente está seleccionado RX.

## Pasos

1. Localice la tira de la cadena de audio PooDoo en la parte superior del contenedor TXDSP.
2. Encuentre la etapa que desea editar: Eq, Comp, Gate, DeEss, Tube, Enh / PUDU o Reverb.
3. Haga doble clic en el mosaico de esa etapa.

El editor flotante de la etapa se abre de inmediato. Un solo clic en el mismo mosaico alternaría su estado de omisión (bypass), así que asegúrese de hacer doble clic.

## Qué hace cada control

| Mosaico de etapa | Clic simple | Doble clic | Arrastrar |
|---|---|---|---|
| Etapa de cadena (Eq) | Activar/desactivar bypass del EQ | Abrir editor de EQ | Reordenar cadena |
| Etapa de cadena (Comp) | Activar/desactivar bypass del compresor | Abrir editor de compresor | Reordenar cadena |
| Etapa de cadena (Gate) | Activar/desactivar bypass del gate | Abrir editor de gate | Reordenar cadena |
| Etapa de cadena (DeEss) | Activar/desactivar bypass del de-esser | Abrir editor de de-esser | Reordenar cadena |
| Etapa de cadena (Tube) | Activar/desactivar bypass del saturador de tubo | Abrir editor de tubo | Reordenar cadena |
| Etapa de cadena (Enh / PUDU) | Activar/desactivar bypass del excitador PUDU | Abrir editor de PUDU | Reordenar cadena |
| Etapa de cadena (Reverb) | Activar/desactivar bypass del reverb | Abrir editor de reverb | Reordenar cadena |

El texto de ayuda debajo de la tira de cadena indica "Click to bypass · Double click to edit · Drag to reorder" y es visible siempre que el modo TX esté activo.

El orden de las etapas de la cadena y sus estados de habilitación se conservan en `ClientCompTxChainStages`. La visibilidad del contenedor se conserva en `Applet_TXDSP`.

## Consejos

- Si la etapa está en bypass, su editor se abre igualmente al hacer doble clic. Puede ajustar los parámetros antes de volver a habilitar la etapa.
- Un clic accidental activará o desactivará el bypass de la etapa. Si esto ocurre, haga clic simple en el mismo mosaico nuevamente para restaurar su estado anterior.

## Relacionado

- [Descripción general de la cadena de audio PooDoo](overview.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Volver a habilitar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Reordenar la cadena DSP de TX](reorder-the-tx-dsp-chain.md)
- [Cambiar entre la vista de cadena TX y el marcador de posición RX](switch-between-tx-chain-view-and-rx-placeholder.md)
