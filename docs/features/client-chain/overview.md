# Descripción general del applet PooDoo Audio Chain

El applet PooDoo Audio Chain muestra la ruta de señal DSP de TX como una tira horizontal de etapas y permite omitir, reordenar o editar cada una. Úselo para moldear el audio transmitido antes de que llegue al radio.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de la bandeja etiquetado **PUDU** en la barra lateral derecha para activarlo.
- No se requiere una conexión de radio para configurar la cadena, pero las etapas no tienen efecto sobre el audio hasta que un radio esté conectado y una fuente de micrófono esté activa.

## Cómo funciona

El applet aparece como la sección superior del contenedor TXDSP. Presenta una fila de encabezado con controles sobre una tira horizontal de etapas de procesamiento. El audio fluye de izquierda a derecha a través de las etapas que no están omitidas.

La cadena tiene actualmente dos modos, seleccionados mediante los botones de alternancia **TX** y **RX** en el encabezado:

- **Modo TX** (predeterminado) — muestra la cadena DSP interactiva. Todos los controles de etapa y el texto de ayuda "Click to bypass · Double click to edit · Drag to reorder" están activos.
- **Modo RX** — muestra el mensaje de marcador de posición "Client RX chain — coming in a future phase". No hay controles de etapa disponibles y **BYPASS** no tiene efecto.

Cuando transmite en su propio slice (canal de recepción), el indicador del extremo TX pulsa en rojo para confirmar que la cadena está activa.

El orden de la cadena y el estado por etapa se guardan en `ClientCompTxChainStages`. Si el contenedor TXDSP se muestra o no se guarda en `Applet_TXDSP`.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento |
|---|---|---|---|
| **TX** | Botón de alternancia | Activado | Selecciona la vista de la cadena TX. Se muestra en ámbar cuando está activo. |
| **RX** | Botón de alternancia | Desactivado | Selecciona la vista de marcador de posición RX. BYPASS no tiene efecto en este modo. |
| **BYPASS** | Botón de alternancia | Desactivado | Activado: guarda una instantánea de las etapas habilitadas y las deshabilita todas. Desactivado: restaura únicamente las etapas que estaban habilitadas antes de la instantánea. Las etapas activadas o desactivadas manualmente mientras BYPASS estaba activo no se ven afectadas por la restauración. |
| **Record (⏺)** | Botón de alternancia | Desactivado | Captura hasta 30 segundos de audio de TX posterior a PUDU. Haga clic nuevamente para detener; la reproducción inicia automáticamente. Se habilita solo cuando MIC está configurado en PC, DAX está desactivado y la reproducción no está en curso. Pulsa en rojo durante la grabación. |
| **Play (▶)** | Botón de alternancia | Desactivado | Reproduce el audio capturado. Haga clic nuevamente para cancelar. Se habilita únicamente cuando existe una grabación y no hay grabación activa. Pulsa en verde durante la reproducción. |
| **Etapa de cadena (Eq)** | Controlador de arrastre | — | Un solo clic activa o desactiva el bypass de la etapa de ecualización. Doble clic abre el editor de EQ. Arrastre para reordenar. |
| **Etapa de cadena (Comp)** | Controlador de arrastre | — | Un solo clic activa o desactiva el bypass del compresor. Doble clic abre el editor del compresor. Arrastre para reordenar. |
| **Etapa de cadena (Gate)** | Controlador de arrastre | — | Un solo clic activa o desactiva el bypass de la puerta de ruido. Doble clic abre el editor de la puerta. Arrastre para reordenar. |
| **Etapa de cadena (DeEss)** | Controlador de arrastre | — | Un solo clic activa o desactiva el bypass del desibilador. Doble clic abre el editor del desibilador. Arrastre para reordenar. |
| **Etapa de cadena (Tube)** | Controlador de arrastre | — | Un solo clic activa o desactiva el bypass del saturador de tubo. Doble clic abre el editor de tubo. Arrastre para reordenar. |
| **Etapa de cadena (Enh / PUDU)** | Controlador de arrastre | — | Un solo clic activa o desactiva el bypass del excitador PUDU. Doble clic abre el editor PUDU. Arrastre para reordenar. |
| **Etapa de cadena (Reverb)** | Controlador de arrastre | — | Un solo clic activa o desactiva el bypass de la reverberación. Doble clic abre el editor de reverberación. Arrastre para reordenar. |

## Consejos

- Las etapas activadas o desactivadas individualmente mientras **BYPASS** está activado quedan excluidas de la restauración automática al desactivar **BYPASS**. Use clics individuales en las etapas cuando desee que una etapa específica permanezca desactivada después de levantar el bypass global.
- El botón **Record (⏺)** permanece habilitado durante la grabación para que pueda hacer clic y detenerla antes de tiempo. Del mismo modo, **Play (▶)** permanece habilitado durante la reproducción para que pueda cancelarla en cualquier momento.
- El texto de ayuda "Click to bypass · Double click to edit · Drag to reorder" se muestra solo en el modo TX y no aparece cuando **RX** está seleccionado.

## Relacionado

- [Omitir todas las etapas de TX a la vez](bypass-every-tx-stage-at-once.md)
- [Rehabilitar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Reordenar la cadena DSP de TX](reorder-the-tx-dsp-chain.md)
- [Abrir el editor flotante de una etapa desde la cadena](open-a-stage-s-floating-editor-from-the-chain.md)
- [Grabar hasta 30 segundos de audio de TX posterior a PUDU](record-up-to-30-seconds-of-post-pudu-tx-audio.md)
- [Reproducir el audio PUDU capturado](play-back-the-captured-pudu-audio.md)
- [Alternar entre la vista de cadena TX y el marcador de posición RX](switch-between-tx-chain-view-and-rx-placeholder.md)
- [Confirmar visualmente cuando TX (MOX) está activo](visually-confirm-when-tx-mox-is-live.md)
