# Alternar entre la vista de cadena TX y el marcador de posición RX

El applet PooDoo Audio Chain muestra ya sea la tira de etapas DSP TX interactiva o un panel de marcador de posición RX. Use los botones de alternancia TX y RX para cambiar entre ellos.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja PUDU en la barra lateral derecha para habilitarlo.

## Pasos

1. Localice la fila de encabezado en la parte superior del applet PooDoo Audio Chain. Contiene los botones TX y RX en el lado izquierdo.
2. Haga clic en TX para mostrar la tira de cadena DSP TX interactiva. TX está seleccionado de forma predeterminada y se muestra en color ámbar cuando está activo.
3. Haga clic en RX para cambiar al panel de marcador de posición RX. El panel muestra el texto "Client RX chain — coming in a future phase". La tira de etapas, la sugerencia de interacción y BYPASS quedan inactivos en este modo.
4. Haga clic en TX para volver a la cadena editable en cualquier momento.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento |
|---------|---------|----------|
| TX | Activado | Muestra la tira de cadena DSP TX con todas las etapas interactivas. Se resalta en ámbar cuando está seleccionado. |
| RX | Desactivado | Reemplaza la tira de cadena con un marcador de posición. BYPASS no tiene efecto en este modo. La sugerencia de interacción está oculta. |
| BYPASS | Desactivado | Deshabilita todas las etapas TX habilitadas a la vez; haga clic nuevamente para restaurarlas. No tiene efecto mientras RX está seleccionado. |

TX y RX son mutuamente excluyentes; solo uno puede estar seleccionado a la vez. El orden de las etapas y su estado de habilitación se guardan en `ClientCompTxChainStages`. La visibilidad del contenedor se guarda en `Applet_TXDSP`.

## Consejos

- La sugerencia de interacción "Click to bypass · Double click to edit · Drag to reorder" aparece únicamente cuando TX está seleccionado, porque la cadena RX aún no es interactiva.
- Cambiar a RX no afecta el estado de la cadena TX. Las etapas permanecen en el estado habilitado o en bypass en que las dejó.

## Solución de problemas

- **El botón de bandeja PUDU no está visible** — Abra `View > Applet Panel` para asegurarse de que el panel de applets esté visible y, a continuación, localice el botón de bandeja PUDU en la barra lateral derecha.
- **BYPASS parece no hacer nada después de hacer clic en RX** — Esto es esperado. BYPASS no tiene efecto en el modo RX y no funcionará hasta que la cadena RX sea implementada en una versión futura.

## Relacionados

- [Descripción general de PooDoo Audio Chain](overview.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Reactivar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Reordenar la cadena DSP TX](reorder-the-tx-dsp-chain.md)
