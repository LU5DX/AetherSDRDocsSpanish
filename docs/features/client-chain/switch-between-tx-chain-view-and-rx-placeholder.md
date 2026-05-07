# Cambiar entre la vista de la cadena de TX y el marcador de posición de RX

El applet de la Cadena de Audio PooDoo muestra las etapas de procesamiento DSP de TX o una vista de la cadena de RX. Utilice TX para trabajar con la cadena de señal en vivo; cambie a RX para ver el marcador de posición de la próxima función de procesamiento de RX.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de la bandeja PUDU en la barra lateral derecha para mostrarlo.

## Pasos

1. Localice la fila del encabezado en la parte superior del applet de la Cadena de Audio PooDoo. Contiene dos botones de modo: TX y RX.
2. Haga clic en TX para mostrar la cadena DSP de TX interactiva (etapas de EQ, Compresor, Puerta, De-Ésser, Tubo, PUDU, Reverberación). TX está seleccionado por defecto y se muestra en ámbar cuando está activo.
3. Haga clic en RX para cambiar a la vista de la cadena de RX. La tira de etapas de TX se oculta y se reemplaza con el texto "Client RX chain — coming in a future phase". El botón BYPASS no tiene efecto en este modo.
4. Vuelva a hacer clic en TX en cualquier momento para regresar a la cadena de TX editable.

AetherSDR guarda su última pestaña seleccionada automáticamente. La próxima vez que abra el applet, restaurará el modo que estaba activo cuando lo cerró.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|---|
| TX | Botón de alternancia | Marcado | Muestra y permite la edición de la cadena DSP de TX. Se muestra en ámbar cuando está seleccionado. | — |
| RX | Botón de alternancia | Sin marcar | Cambia a la vista de marcador de posición de la cadena de RX. BYPASS no tiene efecto en este modo. | — |
| BYPASS | Botón de alternancia | Sin marcar | Marcado: captura las etapas de TX actualmente habilitadas y las deshabilita todas. Sin marcar: restaura solo las etapas que estaban habilitadas antes. Sin efecto cuando RX está activo. | — |

El orden de las etapas de la cadena y el estado de habilitación de la cadena de TX se guardan bajo `ClientCompTxChainStages`. La visibilidad del contenedor se guarda bajo `Applet_TXDSP`.

## Consejos

- TX y RX son mutuamente excluyentes. Hacer clic en uno deselecciona automáticamente el otro; no hay forma de tener ninguno seleccionado.
- La sugerencia de interacción "Click to bypass · Double click to edit · Drag to reorder" solo se muestra cuando TX es el modo activo.

## Solución de problemas

- **El botón de la bandeja PUDU no está visible** — abra el panel de applets mediante `View > Applet Panel`, luego busque el botón de la bandeja PUDU en la barra lateral derecha.
- **Hacer clic en BYPASS en el modo RX no tiene efecto** — esto es esperado. BYPASS solo actúa sobre las etapas de la cadena de TX y no tiene efecto cuando RX está seleccionado.

## Relacionado

- [PooDoo Audio Chain overview](overview.md)
- [Bypass every TX stage at once](bypass-every-tx-stage-at-once.md)
- [Reorder the TX DSP chain](reorder-the-tx-dsp-chain.md)
- [Open a stage's floating editor from the chain](open-a-stage-s-floating-editor-from-the-chain.md)
