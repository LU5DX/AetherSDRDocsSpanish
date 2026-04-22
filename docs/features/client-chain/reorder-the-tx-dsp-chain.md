# Reordenar la cadena DSP de TX

Arrastre los mosaicos de etapa en el applet PooDoo Audio Chain para cambiar el orden en que EQ, Compressor, Gate, De-Esser, Tube, PUDU y Reverb procesan el audio de transmisión. El nuevo orden se guarda en `ClientCompTxChainStages` y tiene efecto de inmediato.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado **PUDU** en la barra lateral derecha para mostrarlo.
- La cadena TX debe estar seleccionada. Confirme que el botón **TX** en la parte superior del applet esté activo (resaltado en ámbar). Si en cambio está seleccionado **RX**, haga clic en **TX**.

## Pasos

1. Localice la franja horizontal de mosaicos de etapa dentro del applet PooDoo Audio Chain. Los mosaicos están etiquetados como **Eq**, **Comp**, **Gate**, **DeEss**, **Tube**, **Enh** y **Reverb**.
2. Haga clic y mantenga presionado el mosaico que desea mover.
3. Arrástrelo hacia la izquierda o la derecha hasta la posición que desea en la cadena.
4. Suelte el botón del ratón. El mosaico se coloca en la nueva posición y el orden de la cadena se actualiza de inmediato.
5. Repita el procedimiento para cualquier otra etapa que desee reordenar.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave persistida |
|---|---|---|---|
| **TX** | Botón de alternancia | Cambia a la vista de cadena TX (la cadena interactiva y reordenable). Predeterminado: activado. | — |
| **RX** | Botón de alternancia | Cambia a la vista de marcador de posición RX. El reordenamiento no está disponible en este modo. Predeterminado: desactivado. | — |
| **BYPASS** | Botón de alternancia | Activado: deshabilita todas las etapas a la vez. Desactivado: restaura las etapas que estaban activas anteriormente. Predeterminado: desactivado. | — |
| Mosaico de etapa **Eq** | Controlador de arrastre | Un clic alterna el bypass del EQ; doble clic abre el editor de EQ; arrastrar reordena. | `ClientCompTxChainStages` |
| Mosaico de etapa **Comp** | Controlador de arrastre | Un clic alterna el bypass del compresor; doble clic abre el editor de compresor; arrastrar reordena. | `ClientCompTxChainStages` |
| Mosaico de etapa **Gate** | Controlador de arrastre | Un clic alterna el bypass del gate; doble clic abre el editor de gate; arrastrar reordena. | `ClientCompTxChainStages` |
| Mosaico de etapa **DeEss** | Controlador de arrastre | Un clic alterna el bypass del de-esser; doble clic abre el editor de de-ess; arrastrar reordena. | `ClientCompTxChainStages` |
| Mosaico de etapa **Tube** | Controlador de arrastre | Un clic alterna el bypass del saturador de tubo; doble clic abre el editor de tubo; arrastrar reordena. | `ClientCompTxChainStages` |
| Mosaico de etapa **Enh** | Controlador de arrastre | Un clic alterna el bypass del excitador PUDU; doble clic abre el editor de PUDU; arrastrar reordena. | `ClientCompTxChainStages` |
| Mosaico de etapa **Reverb** | Controlador de arrastre | Un clic alterna el bypass del reverb; doble clic abre el editor de reverb; arrastrar reordena. | `ClientCompTxChainStages` |

## Consejos

- Una indicación debajo de la franja de la cadena dice "Click to bypass · Double click to edit · Drag to reorder" — solo se muestra cuando el modo TX está activo.
- Un clic simple en un mosaico alterna el estado de bypass de esa etapa. Tenga cuidado de no hacer clic simple cuando su intención sea arrastrar; el estado de bypass cambia al soltar un clic simple.
- Para escuchar la cadena sin ningún procesamiento, haga clic en **BYPASS** en lugar de desactivar las etapas una por una. **BYPASS** guarda una instantánea de las etapas activas y las restaura cuando lo desactive.

## Solución de problemas

- **Los mosaicos de etapa no responden al arrastre** — confirme que el botón **TX** esté seleccionado (ámbar). La vista **RX** es un marcador de posición y no admite reordenamiento.
- **El botón de bandeja PUDU no es visible** — abra `View > Applet Panel` para asegurarse de que la barra lateral derecha esté visible y luego busque el botón de bandeja **PUDU**.

## Relacionados

- [Descripción general de PooDoo Audio Chain](overview.md)
- [Aplicar bypass a todas las etapas de TX a la vez](bypass-every-tx-stage-at-once.md)
- [Abrir el editor flotante de una etapa desde la cadena](open-a-stage-s-floating-editor-from-the-chain.md)
- [Reactivar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
