# Resumen de la cadena de audio Aetherial

El applet de la Cadena de Audio Aetherial le ofrece una vista visual e interactiva del procesamiento de señales DSP del lado cliente de AetherSDR. Úselo para monitorear, omitir, reordenar y editar las etapas que dan forma a su audio transmitido y recibido antes de que llegue a la radio o a sus altavoces.

## Antes de empezar

- El contenedor de Audio Aetherial debe estar visible. Haga clic en el botón de la bandeja etiquetado "PUDU" en la barra lateral derecha para alternar su visibilidad. El applet de la cadena aparece como la sección superior de ese contenedor.
- No se requiere conexión a la radio para ver o editar las cadenas.

## Cómo funciona

El applet presenta dos cadenas DSP independientes — TX y RX — como una tira horizontal de mosaicos de etapa. Solo se muestra una cadena a la vez. Use los botones TX y RX para cambiar entre ellas.

**Cadena TX** procesa el audio en la ruta de transmisión a través de estas etapas en orden: EQ, COMP, GATE, DESS, TUBE, PUDU, VERB.

**Cadena RX** procesa el audio recibido a través de: EQ, AGC-G, AGC-C, DESS, TUBE, EVO. La tira RX está flanqueada por tres mosaicos de estado no interactivos — RADIO, ADSP y SPEAK — que muestran de un vistazo si la ruta de recepción está activa de extremo a extremo. Las seis etapas RX están completamente implementadas.

Cada mosaico de etapa admite tres interacciones:

- **Clic simple** — alterna la omisión solo para esa etapa.
- **Doble clic** — abre el editor de la etapa (vea las diferencias de comportamiento entre TX y RX a continuación).
- **Arrastrar** — reordena la etapa dentro de su cadena. Una barra cian vertical muestra dónde se colocará la etapa antes de soltarla. Las cadenas TX y RX se ordenan independientemente; arrastrar en una cadena no tiene efecto en la otra.

Una sugerencia estática debajo de la cadena dice: *Click to bypass · Double click to edit · Drag to reorder*.

### Comportamiento del doble clic por cadena

**Cadena TX:** Hacer doble clic en cualquier mosaico de etapa TX abre la tira de canal de audio Aetherial — la ventana DSP TX unificada. Esta es la forma canónica de editar su audio TX desde la cadena. Los editores flotantes individuales por etapa siguen siendo accesibles desde dentro de la propia tira de canal.

**Cadena RX:** Hacer doble clic en un mosaico de etapa RX abre directamente el editor flotante sin marco de esa etapa, como antes.

### BYPASS y el motor de audio

El botón BYPASS está sincronizado con el control BYPASS en la tira de canal de audio Aetherial en el lado TX, y con el motor de audio en ambos lados. Hacer clic en BYPASS en cualquier ubicación actualiza ambos. Cuando cambia el applet entre los lados TX y RX, el botón BYPASS refleja el estado de omisión actual del motor para ese lado.

El orden de la cadena y los estados individuales de las etapas se conservan por separado para TX y RX a través de `ClientCompTxChainStages` y `ClientCompRxChainStages`. La última pestaña activa (TX o RX) se conserva a través de `PooDooAudioActiveTab`. La visibilidad del contenedor se conserva a través de `Applet_TXDSP`.

### Intervalo de discriminación de clics

Los widgets de la cadena utilizan un intervalo de discriminación de clics configurable en lugar del intervalo de doble clic del sistema. Este intervalo se establece en la Configuración de Interacción y determina cuánto tiempo espera el widget después de soltar el ratón para decidir si la acción fue un clic simple (alternar omisión) o el inicio de un doble clic (abrir editor). Ajustar este intervalo en la Configuración de Interacción afecta la capacidad de respuesta de los mosaicos de la cadena.

## Qué hace cada control

| Control                   | Tipo                                                                                                                      | Valor predeterminado                                                                                                                |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| TX                        | Muestra y edita la cadena DSP TX (ClientChainWidget) — totalmente interactivo: clic-omitir, doble clic-editar, arrastre-reordenar. | Parte de un par exclusivo con RX; color ámbar 'VUDU' cuando está seleccionado. La última pestaña activa se conserva mediante PooDooAudioActiveTab='TX' / 'RX'. |
| RX                        | Botón de alternancia                                                                                                      | Sin marcar                                                                                                                          |
| BYPASS                    | Botón de alternancia                                                                                                      | Sin marcar                                                                                                                          |
| Record (⏺)                | Botón de alternancia                                                                                                      | Sin marcar                                                                                                                          |
| Play (▶)                  | Botón de alternancia                                                                                                      | Sin marcar                                                                                                                          |
| Mosaico de etapa cadena TX | Mango de arrastre                                                                                                         | —                                                                                                                                   |
| Mosaico de etapa cadena RX | Mango de arrastre                                                                                                         | —                                                                                                                                   |
| Mosaico de estado RADIO   | Indicador                                                                                                                 | —                                                                                                                                   |
| Mosaico de estado/omisión ADSP | Botón de alternancia                                                                                                      | Sin marcar                                                                                                                          |
| Mosaico de estado SPEAK   | Indicador                                                                                                                 | —                                                                                                                                   |
### TX

Cambia el applet para mostrar y editar la cadena DSP TX. El botón está estilizado en ámbar (color "PooDoo") cuando está seleccionado. La última pestaña activa se conserva mediante `PooDooAudioActiveTab`.

### RX

Cambia el applet para mostrar y editar la cadena DSP RX. Cada lado mantiene estados de etapa, orden de cadena e instantánea BYPASS independientes. La última pestaña activa se conserva mediante `PooDooAudioActiveTab`.

### BYPASS

Marcado: toma una instantánea de las etapas actualmente habilitadas en el lado activo (TX o RX), incluyendo RN2, y las deshabilita todas. Sin marcar: reactiva solo las etapas que estaban activas antes. TX y RX mantienen instantáneas separadas.

Tanto en el lado TX como en el RX, el estado de BYPASS es propiedad del motor de audio y se mantiene sincronizado entre el applet de la cadena y cualquier otro control de la interfaz de usuario que administre la omisión (como la tira de canal de audio Aetherial). El botón refleja el estado de omisión real del motor cuando está viendo cualquiera de las cadenas.

Las etapas alternadas manualmente mientras BYPASS está activo se conservan fuera de la instantánea y no se restaurarán automáticamente cuando desmarque BYPASS.

Nota: El ámbito de BYPASS es global (por motor de audio), no por perfil. El botón permanece presionado al cambiar de perfil en la tira de canal.

### Record (⏺)

Captura hasta 30 segundos de audio TX posterior a PUDU. Vuelva a hacer clic para detener; la reproducción comienza automáticamente. Solo está habilitado cuando la fuente de entrada del micrófono está configurada en PC y DAX está desactivado. Parpadea en rojo mientras graba. Oculto en modo RX.

Información sobre herramientas: *Record up to 30 s of post-PooDoo™ TX audio (MIC must be set to PC and DAX off).*

### Play (▶)

Reproduce el audio PUDU capturado. Vuelva a hacer clic para cancelar. Solo está habilitado si existe una grabación y la grabación no está activa actualmente. Parpadea en verde mientras reproduce. Oculto en modo RX.

### Mosaico de etapa de cadena TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB)

Un clic simple alterna la omisión para esa etapa. El doble clic abre la tira de canal de audio Aetherial (la ventana DSP TX unificada). Arrastrar reordena la cadena TX.

### Mosaico de etapa de cadena RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO)

Un clic simple alterna la omisión para esa etapa. El doble clic abre el editor flotante sin marco de la etapa. Arrastrar reordena la cadena RX. Las seis etapas RX están completamente implementadas. El orden es independiente de la cadena TX. Un tipo MIME de arrastre distinto (`application/x-aethersdr-rx-chain-stage`) evita caídas accidentales entre las dos tiras.

### Mosaico de estado RADIO

No interactivo. Solo visible en modo RX. Se vuelve verde cuando el Audio de PC (la transmisión SSB estándar) está habilitado.

### Mosaico de estado/omisión ADSP

Interactivo. Solo visible en modo RX. Refleja qué reductor de ruido del lado cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (por ejemplo, `NR2`, `NR4`, `BNR` o `NVAFX`). Vuelve a `ADSP` cuando ningún reductor de ruido está encendido. Un clic simple omite todo el clúster NR con una instantánea en memoria; otro clic simple restaura el estado NR anterior. El doble clic abre el cuadro de diálogo de Configuración de AetherDSP. Adopta el mismo estilo de anillo azul + punto LED verde que los mosaicos de etapa implementados. La restauración de la instantánea recurre a NR2 si no había módulos activos en el momento de la omisión.

Nota: El módulo `NVAFX` se trata como el equivalente del módulo `BNR` heredado para fines de instantánea y restauración. Al omitir, si NVAFX está activo, se deshabilitará junto con todos los demás módulos NR. Al restaurar, si la instantánea guardada indica que BNR estaba activo, se habilitará NVAFX en su lugar.

### Mosaico de estado SPEAK

No interactivo. Solo visible en modo RX. Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada.

## Consejos

- El botón BYPASS tanto en el lado TX como en el RX está sincronizado con el motor de audio. Hacer clic en BYPASS en cualquier ubicación que lo ofrezca tiene el mismo efecto para la cadena actualmente activa.
- Si alterna manualmente etapas individuales mientras BYPASS está marcado, esos cambios se conservan fuera de la instantánea y no se restaurarán automáticamente cuando desmarque BYPASS.
- El indicador de punto final TX parpadea en rojo mientras está transmitiendo (MOX activo), dando una confirmación en vivo de que la cadena TX está procesando audio.
- Cambiar de TX a RX y viceversa no afecta los estados de etapa de ninguna cadena ni la instantánea de BYPASS. Cada lado es completamente independiente.
- La información sobre herramientas del botón Record dice: "Record up to 30 s of post-PooDoo™ TX audio (MIC must be set to PC and DAX off)". Si el botón está atenuado, verifique primero la configuración de su fuente de MIC y el estado de DAX.
- Hacer doble clic en un mosaico de etapa TX ahora abre la tira de canal de audio Aetherial completa en lugar de un editor por etapa. Acceda a los editores de etapas individuales desde dentro de la tira.
- La etiqueta del mosaico ADSP se actualiza dinámicamente para mostrar qué módulo reductor de ruido está activo actualmente, o vuelve a "ADSP" cuando ningún módulo está activado. El módulo NVAFX se etiqueta como "NVAFX" cuando está activo.
- El intervalo de discriminación de clics utilizado por los mosaicos de la cadena se configura en la Configuración de Interacción. Ajústelo si los mosaicos se sienten demasiado sensibles o no responden lo suficiente al distinguir entre clics simples y dobles clics.
- El ámbito de BYPASS es global (por motor de audio), no por perfil. Cambiar de perfil en la tira de canal no restablecerá el estado de BYPASS.
- BYPASS también deshabilita el módulo RN2 en el lado TX, y la restauración vuelve a habilitar RN2 si estaba activo cuando se activó la omisión.

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
