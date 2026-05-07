# Resumen de la cadena de audio Aetherial

El applet de la cadena de audio Aetherial le ofrece una vista visual e interactiva del procesamiento DSP del lado cliente de AetherSDR. Úselo para monitorear, omitir, reordenar y editar las etapas que dan forma al audio transmitido y recibido antes de que llegue a la radio o a sus altavoces.

## Antes de empezar

- El contenedor de audio Aetherial debe estar visible. Haga clic en el botón de la bandeja etiquetado como "PUDU" en la barra lateral derecha para activarlo. El applet de la cadena aparece como la sección superior de ese contenedor.
- No se requiere conexión a la radio para ver o editar las cadenas.

## Cómo funciona

El applet presenta dos cadenas DSP independientes — TX y RX — como una tira horizontal de mosaicos de etapa. Solo se muestra una cadena a la vez. Use los botones TX y RX para cambiar entre ellas.

**Cadena TX** procesa el audio en la ruta de transmisión a través de estas etapas en orden: EQ, COMP, GATE, DESS, TUBE, PUDU, VERB.

**Cadena RX** procesa el audio recibido a través de: EQ, AGC-G, AGC-C, DESS, TUBE, EVO. La tira RX está rematada por tres mosaicos de estado no interactivos — RADIO, ADSP y SPEAK — que muestran de un vistazo si la ruta de recepción está activa de extremo a extremo. Las seis etapas RX están completamente implementadas.

Cada mosaico de etapa admite tres interacciones:

- **Un clic** — activa o desactiva la omisión solo para esa etapa.
- **Doble clic** — abre el editor de la etapa (vea las diferencias de comportamiento entre TX y RX a continuación).
- **Arrastrar** — reordena la etapa dentro de su cadena. Una barra cian vertical muestra dónde se colocará la etapa antes de soltarla. Las cadenas TX y RX se ordenan de forma independiente; arrastrar en una cadena no afecta a la otra.

Una pista estática debajo de la cadena dice: *Click to bypass · Double click to edit · Drag to reorder*.

### Comportamiento del doble clic por cadena

**Cadena TX:** Al hacer doble clic en cualquier mosaico de etapa TX se abre el Aetherial Audio Channel Strip, la ventana unificada de DSP de TX. Esta es la forma canónica de editar su audio TX desde la cadena. Los editores flotantes individuales por etapa siguen siendo accesibles desde el propio channel strip.

**Cadena RX:** Al hacer doble clic en un mosaico de etapa RX se abre directamente el editor flotante sin marco de esa etapa, como antes.

### BYPASS y el motor de audio

El botón BYPASS está sincronizado con el control BYPASS en el Aetherial Audio Channel Strip en el lado TX, y con el motor de audio en ambos lados. Al hacer clic en BYPASS en cualquier ubicación, se actualizan ambos. Cuando cambia el applet entre los lados TX y RX, el botón BYPASS refleja el estado de omisión actual del motor para ese lado.

El orden de la cadena y los estados de las etapas individuales se conservan por separado para TX y RX a través de `ClientCompTxChainStages` y `ClientCompRxChainStages`. La última pestaña activa (TX o RX) se conserva a través de `PooDooAudioActiveTab`. La visibilidad del contenedor se conserva a través de `Applet_TXDSP`.

## Qué hace cada control

| Control                                                 | Tipo                                                                                                                                                                                                                                                                                                                                                                                   | Valor predeterminado                                                                                                                                                                                                                                                                |
|---------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TX                                                      | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                   | Activado                                                                                                                                                                                                                                                                           |
| RX                                                      | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                   | Desactivado                                                                                                                                                                                                                                                                        |
| BYPASS                                                  | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                   | Desactivado                                                                                                                                                                                                                                                                        |
| Grabar (⏺)                                              | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                   | Desactivado                                                                                                                                                                                                                                                                        |
| Reproducir (▶)                                           | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                   | Desactivado                                                                                                                                                                                                                                                                        |
| Mosaico de etapa de la cadena TX                        | Controlador de arrastre                                                                                                                                                                                                                                                                                                                                                                | —                                                                                                                                                                                                                                                                                  |
| Mosaico de etapa de la cadena RX                        | Controlador de arrastre                                                                                                                                                                                                                                                                                                                                                                | —                                                                                                                                                                                                                                                                                  |
| Mosaico de estado RADIO                                 | Indicador                                                                                                                                                                                                                                                                                                                                                                              | —                                                                                                                                                                                                                                                                                  |
| Mosaico de estado/omisión ADSP                          | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                   | Desactivado                                                                                                                                                                                                                                                                        |
| Mosaico de estado SPEAK                                 | Indicador                                                                                                                                                                                                                                                                                                                                                                              | —                                                                                                                                                                                                                                                                                  |

### TX

Cambia el applet para mostrar y editar la cadena DSP de TX. El botón se muestra en color ámbar (color "PooDoo") cuando está seleccionado. La última pestaña activa se conserva a través de `PooDooAudioActiveTab`.

### RX

Cambia el applet para mostrar y editar la cadena DSP de RX. Cada lado mantiene un estado de etapa, orden de cadena e instantánea de BYPASS independientes. La última pestaña activa se conserva a través de `PooDooAudioActiveTab`.

### BYPASS

Activado: toma una instantánea de las etapas actualmente habilitadas en el lado activo (TX o RX) y las deshabilita todas. Desactivado: reactiva solo las etapas que estaban activas antes. TX y RX mantienen instantáneas separadas.

En ambos lados, TX y RX, el estado de BYPASS es propiedad del motor de audio y se mantiene sincronizado entre el applet de la cadena y cualquier otro control de la interfaz de usuario que gestione la omisión (como el Aetherial Audio Channel Strip). El botón refleja el estado real de omisión del motor cada vez que usted está viendo una de las cadenas.

Las etapas activadas o desactivadas manualmente mientras BYPASS está activo se conservan fuera de la instantánea y no se restaurarán automáticamente al desactivar BYPASS.

### Grabar (⏺)

Captura hasta 30 segundos de audio TX posterior a PUDU. Haga clic de nuevo para detener; la reproducción comienza automáticamente. Solo está habilitado cuando la fuente de entrada del micrófono está configurada en PC y DAX está desactivado. Parpadea en rojo durante la grabación. Oculto en modo RX.

Información sobre herramientas: *Record up to 30 s of post-PooDoo™ TX audio (MIC must be set to PC and DAX off).*

### Reproducir (▶)

Reproduce el audio PUDU capturado. Haga clic de nuevo para cancelar. Solo está habilitado si existe una grabación y la grabación no está actualmente activa. Parpadea en verde durante la reproducción. Oculto en modo RX.

### Mosaico de etapa de la cadena TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB)

Un clic activa o desactiva la omisión para esa etapa. El doble clic abre el Aetherial Audio Channel Strip (la ventana unificada de DSP de TX). Arrastrar reordena la cadena TX.

### Mosaico de etapa de la cadena RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO)

Un clic activa o desactiva la omisión para esa etapa. El doble clic abre el editor flotante sin marco de la etapa. Arrastrar reordena la cadena RX. Las seis etapas RX están completamente implementadas. El orden es independiente de la cadena TX. Un tipo MIME de arrastre distinto (`application/x-aethersdr-rx-chain-stage`) evita caídas accidentales entre las dos tiras.

### Mosaico de estado RADIO

No interactivo. Solo visible en modo RX. Se vuelve verde cuando PC Audio (el flujo SSB estándar) está habilitado.

### Mosaico de estado/omisión ADSP

Interactivo. Solo visible en modo RX. Refleja qué reductor de ruido del lado cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (por ejemplo, `NR2`, `NR4`, `BNR`). Vuelve a `ADSP` cuando ningún reductor de ruido está activo. Un clic omite todo el grupo NR con una instantánea en memoria; otro clic restaura el estado NR anterior. El doble clic abre el cuadro de diálogo de configuración de AetherDSP. Adopta el mismo estilo de anillo azul + punto LED verde que los mosaicos de etapa implementados. La restauración de la instantánea vuelve a NR2 si no había módulos activos en el momento de la omisión.

### Mosaico de estado SPEAK

No interactivo. Solo visible en modo RX. Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada.

## Consejos

- El botón BYPASS en los lados TX y RX está sincronizado con el motor de audio. Al hacer clic en BYPASS en cualquier ubicación que lo ofrezca, se obtiene el mismo efecto para la cadena actualmente activa.
- Si activa o desactiva etapas individuales manualmente mientras BYPASS está marcado, esos cambios se conservan fuera de la instantánea y no se restaurarán automáticamente al desmarcar BYPASS.
- El indicador de punto final TX parpadea en rojo mientras está transmitiendo (MOX activo), proporcionando una confirmación en vivo de que la cadena TX está procesando audio.
- Cambiar de TX a RX y viceversa no afecta los estados de etapa de ninguna cadena ni la instantánea de BYPASS. Cada lado es completamente independiente.
- La información sobre herramientas del botón Grabar dice: "Record up to 30 s of post-PooDoo™ TX audio (MIC must be set to PC and DAX off)." Si el botón aparece atenuado, verifique primero su configuración de fuente MIC y el estado de DAX.
- Al hacer doble clic en un mosaico de etapa TX, ahora se abre el Aetherial Audio Channel Strip completo en lugar de un editor por etapa. Acceda a los editores de etapa individuales desde el propio strip.
- La etiqueta del mosaico ADSP se actualiza dinámicamente para mostrar qué módulo reductor de ruido está activo actualmente, o vuelve a "ADSP" cuando no hay ningún módulo activado.

## Relacionados

- [Switch between editing the TX and RX chains](switch-between-editing-the-tx-and-rx-chains.md)
- [Bypass every TX stage at once](bypass-every-tx-stage-at-once.md)
- [Bypass every RX stage at once](bypass-every-rx-stage-at-once.md)
- [Re-enable a specific stage after a global bypass](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Reorder the TX DSP chain](reorder-the-tx-dsp-chain.md)
- [Reorder the RX DSP chain (independent of TX order)](reorder-the-rx-dsp-chain-independent-of-tx-order.md)
- [Open a stage's frameless floating editor from the chain](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
- [Record up to 30 seconds of post-PUDU TX audio](record-up-to-30-seconds-of-post-pudu-tx-audio.md)
- [Play back the captured PUDU audio](play-back-the-captured-pudu-audio.md)
- [See at a glance whether PC Audio, the noise reducer, and audio output are live (RX status tiles)](see-at-a-glance-whether-pc-audio-the-noise-reducer-and-audio-output-are-live-rx-status-tiles.md)
- [Visually confirm when TX (MOX) is live](visually-confirm-when-tx-mox-is-live.md)
