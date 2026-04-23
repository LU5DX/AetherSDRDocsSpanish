# Abrir el editor flotante de una etapa desde la cadena

Hacer doble clic en una etapa de la cadena de audio PooDoo abre el editor flotante de esa etapa, donde puede ajustar sus parámetros en detalle sin abandonar la vista de la cadena.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón PUDU de la bandeja en la barra lateral derecha para habilitarlo.
- La cadena debe estar en modo TX. El botón de alternancia TX debe estar activo (ámbar). En modo RX, la cadena es un marcador de posición y las etapas no se pueden editar.

## Pasos

1. Localice la tira de la cadena de audio PooDoo en la parte superior del contenedor TXDSP.
2. Encuentre la etapa que desea editar: Eq, Comp, Gate, DeEss, Tube, Enh / PUDU o Reverb.
3. Haga doble clic en el mosaico de esa etapa.

El editor flotante de la etapa se abre de inmediato. Un solo clic en el mismo mosaico alternaría el estado de bypass en su lugar, por lo que debe usar un doble clic deliberado.

## Qué hace cada control

El texto de ayuda debajo de la tira de la cadena indica: "Click to bypass · Double click to edit · Drag to reorder". Esto describe las tres interacciones disponibles en cada mosaico de etapa.

| Etiqueta del mosaico de etapa | Resultado del doble clic |
|---|---|
| Etapa de cadena (Eq) | Abre el editor de ecualización |
| Etapa de cadena (Comp) | Abre el editor del compresor |
| Etapa de cadena (Gate) | Abre el editor del gate |
| Etapa de cadena (DeEss) | Abre el editor del de-esser |
| Etapa de cadena (Tube) | Abre el editor del tubo |
| Etapa de cadena (Enh / PUDU) | Abre el editor PUDU |
| Etapa de cadena (Reverb) | Abre el editor de reverberación |

El orden de las etapas y su estado de habilitación se guardan en `ClientCompTxChainStages`. La visibilidad del contenedor se guarda en `Applet_TXDSP`.

## Consejos

- Un solo clic en una etapa alterna su estado de bypass. Si accidentalmente pone en bypass una etapa con un solo clic, haga clic una vez más para volver a habilitarla antes de hacer doble clic para editarla.
- Puede abrir un editor para una etapa en bypass. Poner una etapa en bypass no impide editarla.

## Solución de problemas

- **El doble clic en una etapa no hace nada** — Confirme que el botón TX esté activo (ámbar). En modo RX, los mosaicos de etapa no se muestran y no se puede abrir ningún editor.
- **La tira de la cadena no es visible** — Es posible que el contenedor TXDSP esté oculto. Haga clic en el botón PUDU de la bandeja en la barra lateral derecha para mostrarlo.

## Relacionados

- [Descripción general de la cadena de audio PooDoo](overview.md)
- [Poner en bypass todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Volver a habilitar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Reordenar la cadena DSP de TX](reorder-the-tx-dsp-chain.md)
- [Cambiar entre la vista de cadena TX y el marcador de posición RX](switch-between-tx-chain-view-and-rx-placeholder.md)
