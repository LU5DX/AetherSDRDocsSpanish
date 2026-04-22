# Cambiar entre la vista de cadena TX y el marcador de posición RX

El applet PooDoo Audio Chain muestra la cadena DSP TX interactiva o un panel de marcador de posición RX. Use los botones de alternancia TX y RX para cambiar entre ellos.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja PUDU en la barra lateral derecha para habilitarlo.

## Pasos

1. Localice la fila de encabezado en la parte superior del applet PooDoo Audio Chain. Contiene dos botones de modo: TX y RX.
2. Haga clic en TX para mostrar la cadena DSP TX — la tira interactiva completa de etapas (EQ, Compressor, Gate, De-Ess, Tube, PUDU, Reverb) con el texto de ayuda "Click to bypass · Double click to edit · Drag to reorder" debajo. TX está seleccionado de forma predeterminada.
3. Haga clic en RX para cambiar al marcador de posición RX. La tira de cadena y el texto de ayuda quedan ocultos y son reemplazados por el mensaje "Client RX chain — coming in a future phase".
4. Haga clic en TX nuevamente en cualquier momento para volver a la vista de cadena interactiva.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento |
|---|---|---|---|
| TX | Botón de alternancia | Activado | Muestra la cadena DSP TX interactiva. Se muestra en ámbar cuando está seleccionado. |
| RX | Botón de alternancia | Desactivado | Muestra el mensaje del marcador de posición RX. BYPASS no tiene efecto en este modo. |
| BYPASS | Botón de alternancia | Desactivado | Activado: toma una instantánea de las etapas habilitadas actualmente y las deshabilita todas. Desactivado: reactiva solo las etapas que estaban activas antes. No tiene efecto mientras RX está seleccionado. |

TX y RX son mutuamente excluyentes; al seleccionar uno se deselecciona el otro.

El orden de las etapas de la cadena y su estado habilitado se conservan en `ClientCompTxChainStages`. La visibilidad del contenedor se conserva en `Applet_TXDSP`.

## Consejos

- El botón BYPASS permanece visible en el modo RX pero no tiene efecto. Cualquier clic en modo RX no afecta al motor DSP.
- El texto de interacción "Click to bypass · Double click to edit · Drag to reorder" se oculta automáticamente cuando se selecciona RX, porque la cadena RX aún no es interactiva.

## Relacionado

- [Descripción general de PooDoo Audio Chain](overview.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Reordenar la cadena DSP TX](reorder-the-tx-dsp-chain.md)
- [Abrir el editor flotante de una etapa desde la cadena](open-a-stage-s-floating-editor-from-the-chain.md)
