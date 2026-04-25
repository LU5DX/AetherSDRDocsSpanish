# Abrir el editor flotante de una etapa desde la cadena

Al hacer doble clic en una etapa de la cadena de audio PooDoo, se abre el editor flotante de esa etapa, donde puede ajustar sus parámetros en detalle.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón PUDU de la bandeja en la barra lateral derecha para activarlo.
- La cadena debe estar en modo TX. El botón TX debe estar seleccionado (color ámbar) en el encabezado de la cadena.

## Pasos

1. Localice la tira de la cadena de audio PooDoo en la parte superior del contenedor TXDSP.
2. Encuentre la etapa que desea editar: Eq, Comp, Gate, DeEss, Tube, Enh / PUDU o Reverb.
3. Haga doble clic en el bloque de la etapa.

El editor flotante de la etapa se abre de inmediato.

## Qué hace cada control

| Bloque de etapa | Un solo clic | Doble clic | Arrastrar |
|---|---|---|---|
| Etapa de cadena (Eq) | Activa o desactiva el bypass de la etapa de EQ | Abre el editor de EQ | Reordena la cadena |
| Etapa de cadena (Comp) | Activa o desactiva el bypass del compresor | Abre el editor del compresor | Reordena la cadena |
| Etapa de cadena (Gate) | Activa o desactiva el bypass del gate | Abre el editor del gate | Reordena la cadena |
| Etapa de cadena (DeEss) | Activa o desactiva el bypass del de-esser | Abre el editor del de-esser | Reordena la cadena |
| Etapa de cadena (Tube) | Activa o desactiva el bypass del saturador de tubo | Abre el editor del tubo | Reordena la cadena |
| Etapa de cadena (Enh / PUDU) | Activa o desactiva el bypass del excitador PUDU | Abre el editor de PUDU | Reordena la cadena |
| Etapa de cadena (Reverb) | Activa o desactiva el bypass del reverb | Abre el editor del reverb | Reordena la cadena |

El orden de las etapas y sus estados de activación se guardan en `ClientCompTxChainStages`. El estado de visibilidad del contenedor se guarda en `Applet_TXDSP`.

## Consejos

- El texto de ayuda debajo de la tira de la cadena dice "Click to bypass · Double click to edit · Drag to reorder" y es visible siempre que el modo TX esté activo.
- Un solo clic pone la etapa en bypass en lugar de abrir el editor. Si el editor no se abrió, verifique si hizo un solo clic en lugar de doble clic.
- El bloque de etapa responde al doble clic independientemente de si la etapa está en bypass en ese momento.

## Solución de problemas

- **La tira de la cadena no es visible** — El contenedor TXDSP puede estar oculto. Haga clic en el botón PUDU de la bandeja en la barra lateral derecha para mostrarlo, o verifique que TX esté seleccionado en el encabezado de la cadena en lugar de RX.
- **El doble clic no tiene efecto** — La cadena debe estar en modo TX. Haga clic en TX en el encabezado de la cadena para cambiar a ese modo. En modo RX, la tira de la cadena es reemplazada por un marcador de posición y la interacción con las etapas no está disponible.

## Relacionados

- [Descripción general de la cadena de audio PooDoo](overview.md)
- [Reordenar la cadena TX DSP](reorder-the-tx-dsp-chain.md)
- [Poner en bypass todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Reactivar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Cambiar entre la vista de cadena TX y el marcador de posición RX](switch-between-tx-chain-view-and-rx-placeholder.md)
