# Descripción general del applet PooDoo Audio Chain

El applet PooDoo Audio Chain muestra el flujo de señal DSP de TX como una tira ordenada de etapas de procesamiento. Permite omitir (bypass), reordenar y editar cada etapa sin salir de la ventana principal, y ofrece un grabador de monitoreo integrado para auditar el audio procesado antes de transmitir.

## Antes de comenzar

- Abra el contenedor PooDoo Audio haciendo clic en el botón PUDU de la bandeja en la barra lateral derecha. El applet de la cadena siempre es visible en la parte superior de ese contenedor cuando este está habilitado.
- No se requiere conexión a la radio para configurar la cadena.

## Cómo funciona

El applet de la cadena muestra hasta siete etapas de procesamiento en una tira horizontal: Eq, Comp, Gate, DeEss, Tube, Enh (PUDU) y Reverb. El audio fluye de izquierda a derecha a través de las etapas que estén activas en ese momento. El orden de las etapas puede modificarse arrastrándolas.

Encima de la tira hay una fila de encabezado que contiene el selector de modo TX/RX, los botones del grabador de monitoreo post-PUDU y el botón BYPASS. Debajo de la tira aparece una línea de ayuda fija que indica: "Click to bypass · Double click to edit · Drag to reorder".

El orden activo de las etapas y el estado habilitado/omitido de cada una se guardan en `ClientCompTxChainStages`. Si el contenedor PooDoo Audio está visible o no se guarda en `Applet_TXDSP`.

**El modo TX** es la ruta completamente implementada. Al hacer clic en TX, la tira de la cadena se vuelve interactiva y se muestra la línea de ayuda.

**El modo RX** actualmente muestra un marcador de posición ("Client RX chain — coming in a future phase"). BYPASS no tiene efecto en el modo RX.

## Qué hace cada control

| Etiqueta | Tipo | Valor predeterminado | Comportamiento |
|---|---|---|---|
| TX | Botón de alternar | Activado | Cambia a la vista de la cadena DSP de TX. Se muestra en color ámbar cuando está seleccionado. |
| RX | Botón de alternar | Desactivado | Cambia a la vista de la cadena RX. Actualmente es solo un marcador de posición. |
| BYPASS | Botón de alternar | Desactivado | Activado: toma una instantánea de todas las etapas habilitadas y las deshabilita. Desactivado: vuelve a habilitar exactamente las etapas que estaban activas antes de la instantánea. Las etapas que se alternan individualmente mientras BYPASS está activo se conservan fuera de la instantánea. |
| Grabar (⏺) | Botón de alternar | Desactivado | Captura hasta 30 s de audio TX post-PUDU. Haga clic de nuevo para detener; la reproducción comienza automáticamente. Solo está habilitado cuando la entrada de micrófono está configurada como PC y DAX está desactivado, y la reproducción no está en curso. Parpadea en rojo durante la grabación. |
| Reproducir (▶) | Botón de alternar | Desactivado | Reproduce la grabación más reciente. Haga clic de nuevo para cancelar. Solo está habilitado cuando existe una grabación y no hay grabación activa. Parpadea en verde durante la reproducción. |
| Etapa de cadena (Eq) | Controlador de arrastre | — | Un clic alterna el bypass de la etapa de ecualización. Doble clic abre el editor de EQ. Arrastre para reordenar. |
| Etapa de cadena (Comp) | Controlador de arrastre | — | Un clic alterna el bypass del compresor. Doble clic abre el editor del compresor. Arrastre para reordenar. |
| Etapa de cadena (Gate) | Controlador de arrastre | — | Un clic alterna el bypass del gate. Doble clic abre el editor del gate. Arrastre para reordenar. |
| Etapa de cadena (DeEss) | Controlador de arrastre | — | Un clic alterna el bypass del de-esser. Doble clic abre el editor del de-esser. Arrastre para reordenar. |
| Etapa de cadena (Tube) | Controlador de arrastre | — | Un clic alterna el bypass del saturador de tubo. Doble clic abre el editor de tubo. Arrastre para reordenar. |
| Etapa de cadena (Enh / PUDU) | Controlador de arrastre | — | Un clic alterna el bypass del excitador PUDU. Doble clic abre el editor de PUDU. Arrastre para reordenar. |
| Etapa de cadena (Reverb) | Controlador de arrastre | — | Un clic alterna el bypass del reverb. Doble clic abre el editor del reverb. Arrastre para reordenar. |

## Consejos

- El indicador del extremo TX parpadea en rojo mientras transmite en su propio slice, lo que confirma de forma visual que MOX está activo sin necesidad de salir de la vista de la cadena de audio.
- El botón Grabar está deshabilitado cuando DAX está activo o la fuente de micrófono no está configurada como PC. Verifique ambas condiciones si el botón permanece atenuado.
- Las etapas que se alternan individualmente mientras BYPASS está activado se rastrean por separado. Al desactivar BYPASS, solo se restauran las etapas que estaban habilitadas antes de activarlo.

## Temas relacionados

- [Omitir todas las etapas de TX a la vez](bypass-every-tx-stage-at-once.md)
- [Volver a habilitar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Reordenar la cadena DSP de TX](reorder-the-tx-dsp-chain.md)
- [Abrir el editor flotante de una etapa desde la cadena](open-a-stage-s-floating-editor-from-the-chain.md)
- [Grabar hasta 30 segundos de audio TX post-PUDU](record-up-to-30-seconds-of-post-pudu-tx-audio.md)
- [Reproducir el audio PUDU capturado](play-back-the-captured-pudu-audio.md)
- [Alternar entre la vista de la cadena TX y el marcador de posición RX](switch-between-tx-chain-view-and-rx-placeholder.md)
- [Confirmar visualmente cuándo TX (MOX) está activo](visually-confirm-when-tx-mox-is-live.md)
