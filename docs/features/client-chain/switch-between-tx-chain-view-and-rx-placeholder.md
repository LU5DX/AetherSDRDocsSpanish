# Cambiar entre la vista de la cadena TX y el marcador de posición RX

El applet PooDoo Audio Chain muestra la cadena DSP TX activa o una vista de marcador de posición RX. Use los botones TX y RX para alternar entre ellas. La vista TX es el modo completamente interactivo; la vista RX muestra actualmente un mensaje de marcador de posición.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón PUDU de la bandeja en la barra lateral derecha para habilitarlo.

## Pasos

1. Localice la fila de encabezado en la parte superior del applet PooDoo Audio Chain. Contiene los botones TX, RX y BYPASS.
2. Haga clic en TX para mostrar la cadena DSP TX. El botón se vuelve ámbar y la tira de cadena con sus controles de etapa se hace visible. La indicación de interacción "Click to bypass · Double click to edit · Drag to reorder" aparece debajo de la cadena.
3. Haga clic en RX para cambiar a la vista RX. La tira de cadena y la indicación se ocultan y son reemplazadas por el texto de marcador de posición "Client RX chain — coming in a future phase".
4. Haga clic en TX para volver a la cadena TX interactiva en cualquier momento.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento |
|---|---|---|---|
| TX | Botón de alternancia | Activado | Muestra la cadena DSP TX. Se vuelve ámbar cuando está seleccionado. Exclusivo con RX. |
| RX | Botón de alternancia | Desactivado | Muestra el marcador de posición RX "Client RX chain — coming in a future phase". Exclusivo con TX. BYPASS no tiene efecto en este modo. |
| BYPASS | Botón de alternancia | Desactivado | En modo TX: toma una instantánea y deshabilita todas las etapas activas; haga clic de nuevo para restaurarlas. En modo RX: sin efecto. |

El orden de las etapas en la cadena TX se conserva en `ClientCompTxChainStages`. La visibilidad del contenedor TXDSP se conserva en `Applet_TXDSP`.

## Consejos

- TX está seleccionado de forma predeterminada cada vez que se muestra el applet. No es necesario configurarlo manualmente después de abrir el contenedor.
- El texto de indicación "Click to bypass · Double click to edit · Drag to reorder" solo es visible en el modo TX. Desaparece automáticamente al cambiar a RX.
- BYPASS no tiene efecto en la vista RX. Si BYPASS está activado cuando cambia a RX, permanece activado pero no hace nada hasta que regrese al modo TX.

## Relacionados

- [Descripción general de PooDoo Audio Chain](overview.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Reordenar la cadena DSP TX](reorder-the-tx-dsp-chain.md)
- [Abrir el editor flotante de una etapa desde la cadena](open-a-stage-s-floating-editor-from-the-chain.md)
