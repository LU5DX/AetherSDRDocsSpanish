# Cambiar entre la vista de cadena TX y el marcador de posición RX

El applet PooDoo Audio Chain muestra las etapas de procesamiento DSP de TX o la vista de cadena RX. Use TX para trabajar con la cadena de señal activa; cambie a RX para ver el marcador de posición de la próxima función de procesamiento RX.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja PUDU en la barra lateral derecha para mostrarlo.

## Pasos

1. Localice la fila de encabezado en la parte superior del applet PooDoo Audio Chain. Contiene dos botones de modo: TX y RX.
2. Haga clic en TX para mostrar la cadena DSP de TX interactiva (etapas EQ, Compressor, Gate, De-Ess, Tube, PUDU, Reverb). TX está seleccionado de forma predeterminada y se muestra en color ámbar cuando está activo.
3. Haga clic en RX para cambiar a la vista de cadena RX. La tira de etapas TX se oculta y se reemplaza con el texto "Client RX chain — coming in a future phase". El botón BYPASS no tiene efecto en este modo.
4. Haga clic en TX nuevamente en cualquier momento para volver a la cadena TX editable.

AetherSDR guarda automáticamente la última pestaña seleccionada. La próxima vez que abra el applet, restaurará el modo que estaba activo cuando lo cerró.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|---|
| TX | Botón de alternancia | Activado | Muestra y permite editar la cadena DSP de TX. Se muestra en color ámbar cuando está seleccionado. | — |
| RX | Botón de alternancia | Desactivado | Cambia a la vista de marcador de posición de la cadena RX. BYPASS no tiene efecto en este modo. | — |
| BYPASS | Botón de alternancia | Desactivado | Activado: toma una instantánea de las etapas TX habilitadas actualmente y las deshabilita todas. Desactivado: restaura solo las etapas que estaban habilitadas antes. No tiene efecto cuando RX está activo. | — |

El orden de las etapas y el estado habilitado de la cadena TX se guardan bajo `ClientCompTxChainStages`. La visibilidad del contenedor se guarda bajo `Applet_TXDSP`.

## Consejos

- TX y RX son mutuamente excluyentes. Al hacer clic en uno se deselecciona automáticamente el otro; no es posible que ninguno esté seleccionado.
- La indicación de interacción "Click to bypass · Double click to edit · Drag to reorder" solo se muestra cuando TX es el modo activo.

## Solución de problemas

- **El botón de bandeja PUDU no está visible** — abra el panel de applets mediante `View > Applet Panel` y busque el botón de bandeja PUDU en la barra lateral derecha.
- **Hacer clic en BYPASS en el modo RX no tiene efecto** — esto es el comportamiento esperado. BYPASS solo actúa sobre las etapas de la cadena TX y no tiene efecto cuando RX está seleccionado.

## Relacionados

- [Descripción general de PooDoo Audio Chain](overview.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Reordenar la cadena DSP de TX](reorder-the-tx-dsp-chain.md)
- [Abrir el editor flotante de una etapa desde la cadena](open-a-stage-s-floating-editor-from-the-chain.md)
