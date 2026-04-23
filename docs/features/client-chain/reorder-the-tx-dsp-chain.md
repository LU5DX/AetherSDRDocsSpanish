# Reordenar la cadena DSP de TX

Arrastre los mosaicos de etapa en la tira de la cadena de audio PooDoo para cambiar el orden en que el procesamiento DSP se aplica a su audio de TX. El nuevo orden se guarda automáticamente en `ClientCompTxChainStages`.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado **PUDU** en la barra lateral derecha para mostrarlo.
- El botón de modo **TX** debe estar seleccionado (está seleccionado por defecto). La vista RX no admite el reordenamiento.

## Pasos

1. Localice la tira de cadena en la parte superior del contenedor PooDoo Audio. Muestra las etapas en su orden actual: **Eq**, **Comp**, **Gate**, **DeEss**, **Tube**, **Enh / PUDU**, **Reverb**.
2. Haga clic y mantenga presionado el mosaico de etapa que desea mover.
3. Arrástrelo hacia la izquierda o la derecha hasta la posición de destino. Los demás mosaicos se desplazan para indicar el punto de inserción.
4. Suelte para colocar la etapa en la nueva posición. La cadena se actualiza inmediatamente y el nuevo orden se guarda en `ClientCompTxChainStages`.

## Qué hace cada control

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **TX** | Botón de alternancia | Activado | Muestra la cadena DSP de TX interactiva. Color ámbar cuando está seleccionado. |
| **RX** | Botón de alternancia | Desactivado | Cambia a la vista de marcador de posición de RX. El reordenamiento no está disponible en este modo. |
| **BYPASS** | Botón de alternancia | Desactivado | Cuando está activado, deshabilita todas las etapas a la vez. Cuando está desactivado, restaura las etapas que estaban activas anteriormente. |
| **Etapa de cadena (Eq)** | Control de arrastre | — | Un solo clic omite la etapa de ecualización; doble clic abre su editor; arrastrar reordena. |
| **Etapa de cadena (Comp)** | Control de arrastre | — | Un solo clic omite el compresor; doble clic abre su editor; arrastrar reordena. |
| **Etapa de cadena (Gate)** | Control de arrastre | — | Un solo clic omite el gate; doble clic abre su editor; arrastrar reordena. |
| **Etapa de cadena (DeEss)** | Control de arrastre | — | Un solo clic omite el de-esser; doble clic abre su editor; arrastrar reordena. |
| **Etapa de cadena (Tube)** | Control de arrastre | — | Un solo clic omite el saturador de tubo; doble clic abre su editor; arrastrar reordena. |
| **Etapa de cadena (Enh / PUDU)** | Control de arrastre | — | Un solo clic omite el excitador PUDU; doble clic abre su editor; arrastrar reordena. |
| **Etapa de cadena (Reverb)** | Control de arrastre | — | Un solo clic omite el reverb; doble clic abre su editor; arrastrar reordena. |

El ajuste persistente `Applet_TXDSP` controla si el contenedor PooDoo Audio se muestra en absoluto.

## Consejos

- La línea de ayuda debajo de la tira de cadena muestra "Click to bypass · Double click to edit · Drag to reorder" y solo es visible cuando **TX** está seleccionado.
- Un solo clic en un mosaico de etapa omite esa etapa, no solo la selecciona. Inicie el arrastre antes de soltar para evitar activar involuntariamente el bypass.
- Para silenciar todas las etapas temporalmente sin perder el orden actual, use **BYPASS** en lugar de omitir las etapas individualmente. Consulte [Omitir todas las etapas de TX a la vez](bypass-every-tx-stage-at-once.md).

## Solución de problemas

- **La tira de cadena no es visible** — Es posible que el contenedor esté oculto. Haga clic en el botón de bandeja **PUDU** en la barra lateral derecha para mostrarlo, o verifique que **TX** esté seleccionado en lugar de **RX**.
- **El arrastre no tiene efecto** — Confirme que **TX** esté seleccionado. El marcador de posición de RX no admite arrastrar para reordenar.
- **Las etapas vuelven a su posición después de arrastrar** — Si **BYPASS** está activado, la instantánea de bypass puede entrar en conflicto con el reordenamiento. Desactive **BYPASS** primero, reordene y luego vuelva a habilitar **BYPASS** si es necesario.

## Relacionado

- [Descripción general de la cadena de audio PooDoo](overview.md)
- [Omitir todas las etapas de TX a la vez](bypass-every-tx-stage-at-once.md)
- [Abrir el editor flotante de una etapa desde la cadena](open-a-stage-s-floating-editor-from-the-chain.md)
- [Reactivar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
