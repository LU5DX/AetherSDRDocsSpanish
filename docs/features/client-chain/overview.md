# Descripción general de la cadena de audio Aetherial

El applet Aetherial Audio Chain le ofrece una vista visual e interactiva del procesamiento de señal DSP del lado del cliente en AetherSDR. Úselo para monitorear, omitir, reordenar y editar las etapas que dan forma al audio transmitido y recibido antes de que llegue al radio o a sus altavoces.

## Antes de comenzar

- El contenedor Aetherial Audio debe estar visible. Haga clic en el botón de bandeja etiquetado "PUDU" en la barra lateral derecha para alternarlo. El applet de la cadena aparece como la sección superior de ese contenedor.
- No se requiere conexión a un radio para ver o editar las cadenas.

## Cómo funciona

El applet presenta dos cadenas DSP independientes — TX y RX — como una tira horizontal de bloques de etapa. Solo se muestra una cadena a la vez. Use los botones TX y RX para alternar entre ellas.

**La cadena TX** procesa el audio en la ruta de transmisión a través de estas etapas en orden: EQ, COMP, GATE, DESS, TUBE, PUDU, VERB.

**La cadena RX** procesa el audio recibido a través de: EQ, GATE, COMP, TUBE, PUDU. La tira RX está delimitada por tres bloques de estado no interactivos — RADIO, DSP y SPEAK — que muestran de un vistazo si la ruta de recepción está activa de extremo a extremo.

Cada bloque de etapa admite tres interacciones:

- **Clic simple** — activa o desactiva la omisión (bypass) solo para esa etapa.
- **Doble clic** — abre el editor flotante sin marco de la etapa.
- **Arrastrar** — reordena la etapa dentro de su cadena. Una barra vertical de color cian indica dónde quedará la etapa antes de soltarla. Las cadenas TX y RX se ordenan de forma independiente; arrastrar en una cadena no tiene efecto en la otra.

Una indicación estática debajo de la cadena dice: *Click to bypass · Double click to edit · Drag to reorder*.

El orden de la cadena y los estados individuales de cada etapa se guardan de forma independiente para TX y RX mediante `ClientCompTxChainStages` y `ClientCompRxChainStages`. La pestaña activa al último uso (TX o RX) se guarda mediante `PooDooAudioActiveTab`. La visibilidad del contenedor se guarda mediante `Applet_TXDSP`.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|---|
| TX | Botón de alternancia | Activado | Muestra y activa la cadena TX para edición. Se muestra en ámbar cuando está seleccionado. | `PooDooAudioActiveTab` |
| RX | Botón de alternancia | Desactivado | Muestra y activa la cadena RX para edición. Se muestra en ámbar cuando está seleccionado. | `PooDooAudioActiveTab` |
| BYPASS | Botón de alternancia | Desactivado | Activado: toma una instantánea de las etapas habilitadas en el lado activo y las deshabilita todas. Desactivado: vuelve a habilitar solo las etapas que estaban activas antes. TX y RX mantienen instantáneas separadas. | — |
| Grabar (⏺) | Botón de alternancia | Desactivado | Captura hasta 30 s de audio TX posterior a PUDU. Haga clic de nuevo para detener; la reproducción comienza automáticamente. Parpadea en rojo durante la grabación. Solo visible en modo TX. Se habilita cuando la fuente MIC es PC, DAX está desactivado y no hay reproducción en curso. | — |
| Reproducir (▶) | Botón de alternancia | Desactivado | Reproduce el audio PUDU capturado. Haga clic de nuevo para cancelar. Parpadea en verde durante la reproducción. Solo visible en modo TX. Se habilita una vez que existe una grabación y no hay grabación activa. | — |
| Bloque de etapa de cadena TX | Controlador de arrastre | — | Un clic omite la etapa; doble clic abre su editor; arrastrar reordena la cadena TX. | — |
| Bloque de etapa de cadena RX | Controlador de arrastre | — | Un clic omite la etapa; doble clic abre su editor; arrastrar reordena la cadena RX. | — |
| Bloque de estado RADIO | Indicador | — | Se pone en verde cuando PC Audio está habilitado. Solo visible en modo RX. | — |
| Bloque de estado DSP | Indicador | — | Refleja el reductor de ruido del lado del cliente activo (p. ej., NR2, NR4, BNR). Muestra "DSP" de forma genérica cuando ninguno está activo. Solo visible en modo RX. | — |
| Bloque de estado SPEAK | Indicador | — | Se pone en verde cuando la salida de audio de AetherSDR está sin silencio. Solo visible en modo RX. | — |

## Consejos

- El botón BYPASS conserva una instantánea de qué etapas estaban habilitadas. Si activa o desactiva manualmente etapas individuales mientras BYPASS está activado, esos cambios manuales se conservan fuera de la instantánea y no se restaurarán automáticamente al desactivar BYPASS.
- El indicador de extremo TX parpadea en rojo mientras está transmitiendo (MOX activo), lo que confirma en tiempo real que la cadena TX está procesando audio.
- Cambiar de TX a RX y viceversa no afecta los estados de etapa ni la instantánea de BYPASS de ninguna de las cadenas. Cada lado es completamente independiente.
- La información de herramienta del botón Grabar dice: "Record up to 30 s of post-PooDoo™ TX audio (MIC must be set to PC and DAX off)." Si el botón aparece atenuado, verifique primero la configuración de la fuente MIC y el estado de DAX.

## Relacionados

- [Alternar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Omitir todas las etapas RX a la vez](bypass-every-rx-stage-at-once.md)
- [Volver a habilitar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Reordenar la cadena DSP TX](reorder-the-tx-dsp-chain.md)
- [Reordenar la cadena DSP RX (independientemente del orden TX)](reorder-the-rx-dsp-chain-independent-of-tx-order.md)
- [Abrir el editor flotante sin marco de una etapa desde la cadena](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
- [Grabar hasta 30 segundos de audio TX posterior a PUDU](record-up-to-30-seconds-of-post-pudu-tx-audio.md)
- [Reproducir el audio PUDU capturado](play-back-the-captured-pudu-audio.md)
- [Ver de un vistazo si PC Audio, el reductor de ruido y la salida de audio están activos (bloques de estado RX)](see-at-a-glance-whether-pc-audio-the-noise-reducer-and-audio-output-are-live-rx-status-tiles.md)
- [Confirmar visualmente cuando TX (MOX) está activo](visually-confirm-when-tx-mox-is-live.md)
