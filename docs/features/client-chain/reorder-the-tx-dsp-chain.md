# Reordenar la cadena DSP de TX

Arrastre los mosaicos de etapa en el PooDoo Audio Chain para cambiar el orden en que el procesamiento DSP se aplica al audio transmitido. El nuevo orden se guarda automáticamente en `ClientCompTxChainStages`.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja `PUDU` en la barra lateral derecha para mostrarlo.
- La cadena de TX debe estar activa. Confirme que TX está seleccionado (resaltado ámbar) en la fila de encabezado. Si en su lugar está seleccionado RX, haga clic en TX.

## Pasos

1. Localice la tira de cadena que muestra los mosaicos de etapa: Eq, Comp, Gate, DeEss, Tube, Enh / PUDU y Reverb.
2. Haga clic y mantenga presionado el mosaico de etapa que desea mover.
3. Arrastre el mosaico hacia la izquierda o la derecha hasta su nueva posición en la cadena.
4. Suelte para soltar el mosaico. La cadena se actualiza de inmediato y el nuevo orden se guarda en `ClientCompTxChainStages`.
5. Repita el procedimiento para cualquier otra etapa que desee reordenar.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| TX | Botón de alternancia | Selecciona la vista de la cadena de TX. Valor predeterminado: activado (ámbar). El reordenamiento solo está disponible en este modo. |
| RX | Botón de alternancia | Selecciona la vista de la cadena de RX. Valor predeterminado: desactivado. El arrastre para reordenar no está disponible en este modo. |
| BYPASS | Botón de alternancia | Valor predeterminado: desactivado. Cuando está activado, deshabilita todas las etapas a la vez. Desactívelo para restaurar las etapas que estaban activas anteriormente. No afecta el orden de las etapas. |
| Etapa de cadena (Eq) | Controlador de arrastre | Un clic activa o desactiva el bypass del ecualizador. Doble clic abre el editor de EQ. Arrastre para reordenar. |
| Etapa de cadena (Comp) | Controlador de arrastre | Un clic activa o desactiva el bypass del compresor. Doble clic abre el editor del compresor. Arrastre para reordenar. |
| Etapa de cadena (Gate) | Controlador de arrastre | Un clic activa o desactiva el bypass del gate. Doble clic abre el editor del gate. Arrastre para reordenar. |
| Etapa de cadena (DeEss) | Controlador de arrastre | Un clic activa o desactiva el bypass del de-esser. Doble clic abre el editor del de-esser. Arrastre para reordenar. |
| Etapa de cadena (Tube) | Controlador de arrastre | Un clic activa o desactiva el bypass del saturador de tubo. Doble clic abre el editor de tubo. Arrastre para reordenar. |
| Etapa de cadena (Enh / PUDU) | Controlador de arrastre | Un clic activa o desactiva el bypass del excitador PUDU. Doble clic abre el editor PUDU. Arrastre para reordenar. |
| Etapa de cadena (Reverb) | Controlador de arrastre | Un clic activa o desactiva el bypass del reverb. Doble clic abre el editor de reverb. Arrastre para reordenar. |

## Consejos

- El texto de ayuda debajo de la cadena indica "Click to bypass · Double click to edit · Drag to reorder" y solo se muestra en el modo TX.
- Un solo clic en un mosaico de etapa aplica el bypass a esa etapa, no a toda la cadena. Use BYPASS para deshabilitar todo a la vez.

## Solución de problemas

- **Arrastrar un mosaico no tiene efecto** — Confirme que TX está seleccionado. La vista de RX no admite el reordenamiento en la versión actual.
- **El botón de bandeja PUDU no está visible** — Abra el panel de applets mediante `View > Applet Panel` y luego localice el botón de bandeja PUDU en la barra lateral derecha.

## Relacionado

- [Descripción general del PooDoo Audio Chain](overview.md)
- [Aplicar bypass a todas las etapas de TX a la vez](bypass-every-tx-stage-at-once.md)
- [Abrir el editor flotante de una etapa desde la cadena](open-a-stage-s-floating-editor-from-the-chain.md)
- [Reactivar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
