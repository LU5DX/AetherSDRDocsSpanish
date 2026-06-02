# Descripción general de la Cadena de Audio Aetherial

El applet de la Cadena de Audio Aetherial le ofrece una vista visual e interactiva del procesamiento de señales DSP del lado del cliente de AetherSDR. Úselo para monitorear, omitir, reordenar y editar las etapas que dan forma al audio transmitido y recibido antes de que llegue a la radio o a sus altavoces.

## Antes de comenzar

- El contenedor de Audio Aetherial debe estar visible. Haga clic en el botón de la bandeja etiquetado como "PUDU" en la barra lateral derecha para alternar su visibilidad. El applet de la cadena aparece como la sección superior de ese contenedor.
- No se requiere conexión a la radio para ver o editar las cadenas.

## Cómo funciona

El applet presenta dos cadenas DSP independientes — TX y RX — como una tira horizontal de mosaicos de etapa. Solo se muestra una cadena a la vez. Use los botones TX y RX para cambiar entre ellas.

**Cadena TX** procesa el audio en la ruta de transmisión a través de estas etapas en orden: EQ, COMP, GATE, DESS, TUBE, PUDU, VERB.

**Cadena RX** procesa el audio recibido a través de: EQ, AGC-G, AGC-C, DESS, TUBE, EVO. La tira RX está flanqueada por tres mosaicos de estado no interactivos — RADIO, ADSP y SPEAK — que muestran de un vistazo si la ruta de recepción está activa de extremo a extremo. Las seis etapas de RX están completamente implementadas.

Cada mosaico de etapa admite tres interacciones:

- **Clic simple** — alterna la omisión de esa etapa solamente.
- **Doble clic** — abre el editor de la etapa (vea las diferencias de comportamiento entre TX y RX a continuación).
- **Arrastrar** — reordena la etapa dentro de su cadena. Una barra cian vertical muestra dónde se ubicará la etapa antes de soltarla. Las cadenas TX y RX se ordenan de forma independiente; arrastrar en una cadena no tiene efecto sobre la otra.

Una sugerencia estática debajo de la cadena dice: *Click para omitir · Doble click para editar · Arrastrar para reordenar*.

### Comportamiento del doble clic por cadena

**Cadena TX:** Al hacer doble clic en cualquier mosaico de etapa TX se abre el Canal de Audio Aetherial — la ventana DSP de TX unificada. Esta es la forma canónica de editar su audio TX desde la cadena. Los editores flotantes individuales por etapa siguen siendo accesibles desde el propio canal.

**Cadena RX:** Al hacer doble clic en un mosaico de etapa RX se abre directamente ese editor flotante sin marco de la etapa, como antes.

### BYPASS y el motor de audio

El botón BYPASS está sincronizado con el control BYPASS en el Canal de Audio Aetherial del lado TX, y con el motor de audio en ambos lados. Hacer clic en BYPASS en cualquier ubicación actualiza ambos. Cuando cambia el applet entre los lados TX y RX, el botón BYPASS refleja el estado de omisión actual del motor para ese lado.

El orden de la cadena y los estados de las etapas individuales se conservan por separado para TX y RX mediante `ClientCompTxChainStages` y `ClientCompRxChainStages`. La última pestaña activa (TX o RX) se conserva mediante `PooDooAudioActiveTab`. La visibilidad del contenedor se conserva mediante `Applet_TXDSP`.

### Intervalo de discriminación de clics

Los widgets de la cadena utilizan un intervalo de discriminación de clics configurable en lugar del intervalo de doble clic del sistema. Este intervalo se establece en la Configuración de Interacción y determina cuánto tiempo espera el widget después de soltar el mouse para decidir si la acción fue un clic simple (alternar omisión) o el inicio de un doble clic (abrir editor). Ajustar este intervalo en la Configuración de Interacción afecta la capacidad de respuesta de los mosaicos de la cadena.

## Qué hace cada control

| Control                      | Tipo                                                                                                                                | Valor predeterminado                                                                                                                              |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| TX                           | Muestra y edita la cadena DSP de TX (ClientChainWidget) — totalmente interactivo: clic-omitir, doble clic-editar, arrastrar-reordenar. | Parte de un par exclusivo con RX; color ámbar 'VUDU' cuando está seleccionado. La última pestaña activa se conserva mediante PooDooAudioActiveTab='TX' / 'RX'. |
| RX                           | Botón de alternancia                                                                                                                | Sin marcar                                                                                                                                        |
| BYPASS                       | Botón de alternancia                                                                                                                | Sin marcar                                                                                                                                        |
| Grabar (⏺)                   | Botón de alternancia                                                                                                                | Sin marcar                                                                                                                                        |
| Reproducir (▶)               | Botón de alternancia                                                                                                                | Sin marcar                                                                                                                                        |
| Mosaico de etapa de cadena TX | Manija de arrastre                                                                                                                  | —                                                                                                                                                 |
| Mosaico de etapa de cadena RX | Manija de arrastre                                                                                                                  | —                                                                                                                                                 |
| Mosaico de estado RADIO       | Indicador                                                                                                                           | —                                                                                                                                                 |
| Mosaico de estado/omisión ADSP | Botón de alternancia                                                                                                                | Sin marcar                                                                                                                                        |
| Mosaico de estado SPEAK       | Indicador                                                                                                                           | —                                                                                                                                                 |
### TX

Cambia el applet para mostrar y editar la cadena DSP de TX. El botón se muestra en color ámbar (color "PooDoo") cuando está seleccionado. La última pestaña activa se conserva mediante `PooDooAudioActiveTab`.

### RX

Cambia el applet para mostrar y editar la cadena DSP de RX. Cada lado mantiene el estado de la etapa, el orden de la cadena y la instantánea BYPASS de forma independiente. La última pestaña activa se conserva mediante `PooDooAudioActiveTab`.

### BYPASS

Marcado: captura una instantánea de las etapas actualmente habilitadas en el lado activo (TX o RX), incluido RN2, y las deshabilita todas. Sin marcar: vuelve a habilitar solo las etapas que estaban activas antes. TX y RX mantienen instantáneas separadas.

Tanto en el lado TX como en el RX, el estado BYPASS es propiedad del motor de audio y se mantiene sincronizado en el applet de la cadena y en cualquier otro control de la interfaz de usuario que administre la omisión (como el Canal de Audio Aetherial). El botón refleja el estado de omisión real del motor cada vez que está viendo cualquiera de las cadenas.

Las etapas activadas manualmente mientras BYPASS está activo se conservan fuera de la instantánea y no se restaurarán automáticamente cuando desmarque BYPASS.

Nota: El alcance de BYPASS es global (por motor de audio), no por perfil. El botón permanece presionado al cambiar de perfil en el Canal.

### Grabar (⏺)

Captura hasta 30 segundos de audio TX posterior a PUDU. Haga clic de nuevo para detener; la reproducción comienza automáticamente. Solo está habilitado cuando la fuente de entrada de micrófono está configurada en PC y DAX está desactivado. Parpadea en rojo mientras graba. Oculto en modo RX.

Información sobre herramientas: *Grabe hasta 30 s de audio TX posterior a PooDoo™ (MIC debe configurarse en PC y DAX apagado).*

### Reproducir (▶)

Reproduce el audio PUDU capturado. Haga clic de nuevo para cancelar. Solo está habilitado una vez que existe una grabación y la grabación no está activa actualmente. Parpadea en verde mientras reproduce. Oculto en modo RX.

### Mosaico de etapa de cadena TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB)

Un clic simple alterna la omisión de esa etapa. El doble clic abre el Canal de Audio Aetherial (la ventana DSP de TX unificada). Arrastrar reordena la cadena TX.

### Mosaico de etapa de cadena RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO)

Un clic simple alterna la omisión de esa etapa. El doble clic abre el editor flotante sin marco de la etapa. Arrastrar reordena la cadena RX. Las seis etapas de RX están completamente implementadas. El orden es independiente de la cadena TX. Un tipo MIME de arrastre distinto (`application/x-aethersdr-rx-chain-stage`) evita caídas accidentales entre las dos tiras.

### Mosaico de estado RADIO

No interactivo. Solo visible en modo RX. Se vuelve verde cuando el Audio de PC (la transmisión SSB estándar) está habilitado.

### Mosaico de estado/omisión ADSP

Interactivo. Solo visible en modo RX. Refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta rota al nombre corto del módulo activo (por ejemplo, `NR2`, `NR4`, `BNR`). Vuelve a `ADSP` cuando no hay ningún reductor de ruido activo. Un clic simple omite todo el clúster NR con una instantánea en memoria; otro clic simple restaura el estado NR anterior. El doble clic abre el diálogo de Configuración de AetherDSP. Adopta el mismo estilo de anillo azul + punto LED verde que los mosaicos de etapa implementados. La restauración de la instantánea vuelve a NR2 si no había módulos activos en el momento de la omisión.

### Mosaico de estado SPEAK

No interactivo. Solo visible en modo RX. Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada.

## Consejos

- El botón BYPASS tanto en el lado TX como en el RX está sincronizado con el motor de audio. Hacer clic en BYPASS en cualquier ubicación que lo ofrezca tiene el mismo efecto para la cadena actualmente activa.
- Si alterna manualmente etapas individuales mientras BYPASS está marcado, esos cambios se conservan fuera de la instantánea y no se restaurarán automáticamente cuando desmarque BYPASS.
- El indicador de punto final TX parpadea en rojo mientras está transmitiendo (MOX activo), lo que proporciona una confirmación en vivo de que la cadena TX está procesando audio.
- Cambiar de TX a RX y viceversa no afecta los estados de etapa de ninguna cadena ni la instantánea BYPASS. Cada lado es completamente independiente.
- La información sobre herramientas del botón Grabar dice: "Grabe hasta 30 s de audio TX posterior a PooDoo™ (MIC debe configurarse en PC y DAX apagado)." Si el botón está atenuado, verifique primero la configuración de su fuente MIC y el estado de DAX.
- Al hacer doble clic en un mosaico de etapa TX ahora se abre el Canal de Audio Aetherial completo en lugar de un editor por etapa. Acceda a los editores de etapa individuales desde el canal.
- La etiqueta del mosaico ADSP se actualiza dinámicamente para mostrar qué módulo reductor de ruido está activo actualmente, o vuelve a "ADSP" cuando no hay ningún módulo activado.
- El intervalo de discriminación de clics utilizado por los mosaicos de la cadena se configura en la Configuración de Interacción. Ajústelo si los mosaicos se sienten demasiado sensibles o no lo suficientemente receptivos al distinguir clics simples de dobles clics.
- El alcance de BYPASS es global (por motor de audio), no por perfil. Cambiar de perfil en el Canal no restablecerá el estado BYPASS.
- BYPASS también deshabilita el módulo RN2 en el lado TX, y la restauración vuelve a habilitar RN2 si estaba activo cuando se activó la omisión.

## Relacionados

- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Omitir todas las etapas RX a la vez](bypass-every-rx-stage-at-once.md)
- [Reactivar una etapa específica después de una omisión global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Reordenar la cadena DSP de TX](reorder-the-tx-dsp-chain.md)
- [Reordenar la cadena DSP de RX (independiente del orden TX)](reorder-the-rx-dsp-chain-independent-of-tx-order.md)
- [Abrir el editor flotante sin marco de una etapa desde la cadena](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
- [Grabar hasta 30 segundos de audio TX posterior a PUDU](record-up-to-30-seconds-of-post-pudu-tx-audio.md)
- [Reproducir el audio PUDU capturado](play-back-the-captured-pudu-audio.md)
- [Ver de un vistazo si el Audio de PC, el reductor de ruido y la salida de audio están activos (mosaicos de estado RX)](see-at-a-glance-whether-pc-audio-the-noise-reducer-and-audio-output-are-live-rx-status-tiles.md)
- [Confirmar visualmente cuando TX (MOX) está activo](visually-confirm-when-tx-mox-is-live.md)
