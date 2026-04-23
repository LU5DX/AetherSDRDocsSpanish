# Descripción general de la cadena de audio PooDoo

El applet PooDoo Audio Chain muestra el flujo de señal DSP de TX como una tira interactiva de etapas de procesamiento. Úselo para omitir, reordenar y editar etapas individuales, o para capturar y revisar una muestra corta de su audio TX procesado.

## Antes de comenzar

- Abra el contenedor PooDoo Audio haciendo clic en el botón PUDU de la bandeja en la barra lateral derecha. El applet de cadena siempre es visible en la parte superior de ese contenedor cuando el tile está habilitado.
- No se requiere una conexión de radio para ver o reorganizar la cadena, pero el procesamiento de audio requiere un motor de audio activo.

## Cómo funciona

El encabezado del applet contiene tres controles — TX, RX y BYPASS — seguidos de los botones de grabación y reproducción de monitor. Debajo del encabezado se encuentra la tira de cadena, que muestra cada etapa de procesamiento como un tile arrastrable. Una línea de ayuda estática debajo de la tira indica "Click to bypass · Double click to edit · Drag to reorder".

El botón TX está seleccionado de forma predeterminada. En el modo TX, la tira de cadena completa es interactiva. Al hacer clic en RX se cambia a un marcador de posición que indica "Client RX chain — coming in a future phase"; en ese modo no hay edición de etapas ni bypass disponible.

La cadena procesa el audio a través de hasta siete etapas en el orden mostrado en la tira: Eq, Comp, Gate, DeEss, Tube, Enh (PUDU) y Reverb. Cada etapa puede omitirse individualmente, abrirse para edición o arrastrarse a una nueva posición. El orden de las etapas y los estados habilitados se guardan en `ClientCompTxChainStages`. El estado de visibilidad del contenedor en sí se guarda en `Applet_TXDSP`.

Cuando está transmitiendo, el indicador de punto final TX pulsa en rojo en la tira de cadena, impulsado por el estado MOX de su slice.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento |
|---|---|---|---|
| TX | Botón de alternancia | Activado | Cambia a la vista de cadena DSP de TX. Color ámbar cuando está seleccionado. |
| RX | Botón de alternancia | Desactivado | Cambia al marcador de posición de la cadena RX. BYPASS no tiene efecto en este modo. |
| BYPASS | Botón de alternancia | Desactivado | Activado: toma una instantánea de todas las etapas habilitadas actualmente y las deshabilita todas. Desactivado: vuelve a habilitar exactamente las etapas que estaban activas antes de la instantánea. Las etapas alternadas manualmente mientras BYPASS estaba activo se conservan fuera de la instantánea. |
| Grabar (⏺) | Botón de alternancia | Desactivado | Captura hasta 30 s de audio TX posterior a PUDU. Haga clic de nuevo para detener; la reproducción comienza automáticamente. Pulsa en rojo durante la grabación. Solo se habilita cuando la fuente MIC está configurada como PC, DAX está desactivado y la reproducción no está en curso. |
| Reproducir (▶) | Botón de alternancia | Desactivado | Reproduce el audio capturado. Haga clic de nuevo para cancelar. Pulsa en verde durante la reproducción. Solo se habilita una vez que existe una grabación y la grabación no está activa. |
| Etapa de cadena (Eq) | Controlador de arrastre | — | Un solo clic alterna el bypass de la etapa de EQ. Doble clic abre el editor de EQ. Arrastre para reordenar. |
| Etapa de cadena (Comp) | Controlador de arrastre | — | Un solo clic alterna el bypass del compresor. Doble clic abre el editor de compresor. Arrastre para reordenar. |
| Etapa de cadena (Gate) | Controlador de arrastre | — | Un solo clic alterna el bypass de la puerta de ruido. Doble clic abre el editor de puerta. Arrastre para reordenar. |
| Etapa de cadena (DeEss) | Controlador de arrastre | — | Un solo clic alterna el bypass del de-esser. Doble clic abre el editor de de-ess. Arrastre para reordenar. |
| Etapa de cadena (Tube) | Controlador de arrastre | — | Un solo clic alterna el bypass del saturador de tubo. Doble clic abre el editor de tubo. Arrastre para reordenar. |
| Etapa de cadena (Enh / PUDU) | Controlador de arrastre | — | Un solo clic alterna el bypass del excitador PUDU. Doble clic abre el editor PUDU. Arrastre para reordenar. |
| Etapa de cadena (Reverb) | Controlador de arrastre | — | Un solo clic alterna el bypass de la reverberación. Doble clic abre el editor de reverberación. Arrastre para reordenar. |

## Consejos

- Mientras BYPASS está activo, aún puede alternar etapas individuales. Esos cambios por etapa no se incluyen en la instantánea de bypass y persistirán después de desactivar BYPASS.
- El botón Grabar permanece habilitado durante la grabación para que pueda hacer clic por segunda vez y detenerla antes de tiempo.
- La línea de ayuda "Click to bypass · Double click to edit · Drag to reorder" solo se muestra en el modo TX.

## Relacionado

- [Omitir todas las etapas de TX a la vez](bypass-every-tx-stage-at-once.md)
- [Volver a habilitar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Reordenar la cadena DSP de TX](reorder-the-tx-dsp-chain.md)
- [Abrir el editor flotante de una etapa desde la cadena](open-a-stage-s-floating-editor-from-the-chain.md)
- [Grabar hasta 30 segundos de audio TX posterior a PUDU](record-up-to-30-seconds-of-post-pudu-tx-audio.md)
- [Reproducir el audio PUDU capturado](play-back-the-captured-pudu-audio.md)
- [Cambiar entre la vista de cadena TX y el marcador de posición RX](switch-between-tx-chain-view-and-rx-placeholder.md)
- [Confirmar visualmente cuándo TX (MOX) está activo](visually-confirm-when-tx-mox-is-live.md)
