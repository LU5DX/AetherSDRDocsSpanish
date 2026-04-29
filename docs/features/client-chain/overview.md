# Descripción general del applet Aetherial Audio Chain

El applet Aetherial Audio Chain ofrece una vista visual e interactiva del procesamiento DSP de señal en el lado del cliente de AetherSDR. Úselo para supervisar, omitir, reordenar y editar las etapas que dan forma al audio transmitido y recibido antes de que llegue al radio o a sus altavoces.

## Antes de comenzar

- El contenedor Aetherial Audio debe estar visible. Haga clic en el botón de la bandeja etiquetado "PUDU" en la barra lateral derecha para alternarlo. El applet de cadena aparece como la sección superior de ese contenedor.
- No se requiere conexión con el radio para ver o editar las cadenas.

## Cómo funciona

El applet presenta dos cadenas DSP independientes — TX y RX — como una tira horizontal de fichas de etapa. Solo se muestra una cadena a la vez. Use los botones TX y RX para alternar entre ellas.

La **cadena TX** procesa el audio en la ruta de transmisión a través de estas etapas en orden: EQ, COMP, GATE, DESS, TUBE, PUDU, VERB.

La **cadena RX** procesa el audio recibido a través de: EQ, AGC-T, AGC-C, TUBE, PUDU. La tira RX está delimitada por tres fichas de estado no interactivas — RADIO, DSP y SPEAK — que muestran de un vistazo si la ruta de recepción está activa de extremo a extremo.

Cada ficha de etapa admite tres interacciones:

- **Clic simple** — alterna el bypass solo para esa etapa.
- **Doble clic** — abre el editor flotante sin marco de la etapa.
- **Arrastrar** — reordena la etapa dentro de su cadena. Una barra vertical cian indica dónde se colocará la etapa antes de soltar. Las cadenas TX y RX se ordenan de forma independiente; arrastrar en una cadena no tiene efecto en la otra.

Una indicación estática debajo de la cadena dice: *Click to bypass · Double click to edit · Drag to reorder*.

El orden de la cadena y los estados individuales de cada etapa se guardan por separado para TX y RX mediante `ClientCompTxChainStages` y `ClientCompRxChainStages`. La última pestaña activa (TX o RX) se guarda mediante `PooDooAudioActiveTab`. La visibilidad del contenedor se guarda mediante `Applet_TXDSP`.

## Qué hace cada control

| Control                                            | Tipo                                                                                                                                          | Valor predeterminado                                                                                                                                                                                                                                                                                                           |
|----------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TX                                                 | Botón de alternancia                                                                                                                          | Activado                                                                                                                                                                                                                                                                                                                       |
| RX                                                 | Botón de alternancia                                                                                                                          | Desactivado                                                                                                                                                                                                                                                                                                                    |
| BYPASS                                             | Botón de alternancia                                                                                                                          | Desactivado                                                                                                                                                                                                                                                                                                                    |
| Record (⏺)                                         | Botón de alternancia                                                                                                                          | Desactivado                                                                                                                                                                                                                                                                                                                    |
| Play (▶)                                           | Botón de alternancia                                                                                                                          | Desactivado                                                                                                                                                                                                                                                                                                                    |
| Ficha de etapa de cadena TX                        | Controlador de arrastre                                                                                                                       | —                                                                                                                                                                                                                                                                                                                              |
| Ficha de etapa de cadena RX                        | Controlador de arrastre                                                                                                                       | —                                                                                                                                                                                                                                                                                                                              |
| Ficha de estado RADIO                              | Indicador                                                                                                                                     | —                                                                                                                                                                                                                                                                                                                              |
| Ficha de estado DSP                                | Indicador                                                                                                                                     | —                                                                                                                                                                                                                                                                                                                              |
| Ficha de estado SPEAK                              | Indicador                                                                                                                                     | —                                                                                                                                                                                                                                                                                                                              |
| Etapa de cadena RX (EQ / AGC-T / AGC-C / TUBE / PUDU) | Un clic simple alterna el bypass de la etapa RX; el doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena RX. | Delegado a ClientRxChainWidget. Las cinco etapas RX (EQ, AGC-T/Gate, AGC-C/Comp, Tube, PUDU) están completamente implementadas. El orden es independiente de la cadena TX. El tipo MIME exclusivo `application/x-aethersdr-rx-chain-stage` evita soltadas accidentales entre las dos tiras. |

## Consejos

- El botón BYPASS guarda una instantánea de las etapas que estaban habilitadas. Si alterna etapas individuales manualmente mientras BYPASS está activado, esos cambios manuales se conservan fuera de la instantánea y no se restaurarán automáticamente al desactivar BYPASS.
- El indicador de extremo TX parpadea en rojo mientras está transmitiendo (MOX activo), lo que confirma en tiempo real que la cadena TX está procesando audio.
- Cambiar de TX a RX y viceversa no afecta los estados de etapa de ninguna cadena ni la instantánea de BYPASS. Cada lado es completamente independiente.
- El tooltip del botón Record dice: "Record up to 30 s of post-PooDoo™ TX audio (MIC must be set to PC and DAX off)." Si el botón aparece atenuado, verifique primero la configuración de su fuente MIC y el estado de DAX.

## Relacionados

- [Alternar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Omitir todas las etapas RX a la vez](bypass-every-rx-stage-at-once.md)
- [Reactivar una etapa específica tras un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Reordenar la cadena DSP TX](reorder-the-tx-dsp-chain.md)
- [Reordenar la cadena DSP RX (independiente del orden TX)](reorder-the-rx-dsp-chain-independent-of-tx-order.md)
- [Abrir el editor flotante sin marco de una etapa desde la cadena](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
- [Grabar hasta 30 segundos de audio TX posterior a PUDU](record-up-to-30-seconds-of-post-pudu-tx-audio.md)
- [Reproducir el audio PUDU capturado](play-back-the-captured-pudu-audio.md)
- [Ver de un vistazo si el audio de PC, el reductor de ruido y la salida de audio están activos (fichas de estado RX)](see-at-a-glance-whether-pc-audio-the-noise-reducer-and-audio-output-are-live-rx-status-tiles.md)
- [Confirmar visualmente cuando TX (MOX) está activo](visually-confirm-when-tx-mox-is-live.md)
