# Omitir todo el clúster NR desde el mosaico ADSP de la cadena RX

Omite todos los reductores de ruido del lado del cliente (NR2, NR4, MNR, DFNR, RN2, BNR) a la vez utilizando el mosaico ADSP en la cadena RX. El mosaico recuerda qué reductor de ruido estaba activo antes de la omisión, por lo que al hacer clic nuevamente se restaura ese módulo.

## Antes de comenzar

- El contenedor de la Cadena de Audio Aetherial debe estar visible. Haga clic en el botón **PUDU** de la bandeja en la barra lateral derecha para alternar su visibilidad.
- Haga clic en **RX** en la fila del encabezado para mostrar la cadena DSP de RX.

## Pasos

1. Localice el mosaico **ADSP** en la tira de la cadena RX. Se encuentra entre **RADIO** (izquierda) y **SPEAK** (derecha).
   - Cuando un reductor de ruido está activo, el mosaico muestra su nombre abreviado (por ejemplo, `NR2`, `NR4`, `BNR`).
   - Cuando no hay ningún reductor de ruido activo, el mosaico muestra `ADSP`.

2. **Haga clic una vez** en el mosaico **ADSP**.

   - Se omiten todos los reductores de ruido del lado del cliente. La etiqueta del mosaico muestra `ADSP`.
   - AetherSDR toma una instantánea en memoria de qué reductor de ruido estaba activo.

3. Para restaurar el reductor de ruido anterior, **haga clic una vez** nuevamente en el mosaico **ADSP**.

   - El módulo previamente activo se rehabilita y su nombre abreviado vuelve a aparecer en el mosaico. Si no había ningún módulo activo al momento de la omisión, se habilita NR2 como opción predeterminada.

## Función de cada control

| Control | Comportamiento | Notas |
|---|---|---|
| **Mosaico ADSP** | Haga clic para omitir todo el clúster NR. La etiqueta rota para mostrar el nombre abreviado del módulo activo (`NR2`, `NR4`, `BNR`) o `ADSP` cuando no hay ninguno activo. Haga doble clic para abrir el cuadro de diálogo de Configuración de AetherDSP. | Solo visible en modo RX. Adopta el estilo de anillo azul con punto LED verde. |
| **Botón BYPASS** | Desactiva todas las etapas en la cadena seleccionada (incluido RN2). Haga clic nuevamente para restaurar las etapas que estaban activas antes. El alcance es global (por motor de audio), no por perfil: el botón permanece presionado al cambiar entre perfiles de la tira del canal. | TX y RX mantienen instantáneas independientes. |
| **Pestaña TX** | Muestra y edita la cadena DSP de TX (Ecualizador paramétrico, Compresor con Drive previo a la compresión y reducción de PAPR con rotador de fase, Puerta, De-Ess con pendiente seleccionable de 12–48 dB/oct, Tube con conmutación de reducción de ruido RN2, excitador PUDU, Reverberación). Color ámbar 'VUDU' cuando está seleccionada. La última pestaña activa persiste mediante `PooDooAudioActiveTab`. | Forma parte de un par exclusivo con RX. |
| **Pestaña RX** | Muestra y edita la cadena DSP de RX (EQ, AGC-G/Puerta, AGC-C/Compresor, DESS/DeEss, TUBE, EVO/Pudu). Las seis etapas están completamente implementadas. Enmarcada por los mosaicos de estado RADIO / ADSP / SPEAK. Interactiva: haga clic para omitir, doble clic para editar, arrastre para reordenar. El color indica el lado activo. La última pestaña activa persiste mediante `PooDooAudioActiveTab`. | Cada lado mantiene estado de etapa independiente, orden de cadena e instantánea de BYPASS. |
| **Grabar** (glifo de círculo) | Captura hasta 30 segundos de audio TX posterior a PUDU. Haga clic nuevamente para detener (la reproducción comienza automáticamente). Información sobre herramientas: "Grabe hasta 30 s de audio TX posterior a PooDoo™ (el MIC debe estar configurado en PC y DAX apagado)". Oculto en modo RX. Solo se habilita cuando la entrada de micrófono está lista y la reproducción no está en curso. Parpadea en rojo durante la grabación. | |
| **Reproducir** (glifo de triángulo) | Reproduce el audio PUDU capturado. Haga clic nuevamente para cancelar. Oculto en modo RX. Solo se habilita una vez que existe una grabación y la grabación no está activa. Parpadea en verde durante la reproducción. | |
| **Etapa de cadena TX** (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | Un solo clic alterna la omisión de la etapa. Doble clic abre su editor flotante sin marco. Arrastre para reordenar la cadena TX. | Delegado a ClientChainWidget. Texto de sugerencia: "Haga clic para omitir · Haga doble clic para editar · Arrastre para reordenar". |
| **Etapa de cadena RX** (EQ / AGC-G / AGC-C / DESS / TUBE / EVO) | Un solo clic alterna la omisión de la etapa. Doble clic abre su editor flotante sin marco. Arrastre para reordenar la cadena RX. | Delegado a ClientRxChainWidget. Tipo mime distinto `application/x-aethersdr-rx-chain-stage` evita caídas accidentales entre las tiras TX y RX. |
| **Mosaico de estado RADIO** | No interactivo. Se vuelve verde cuando Audio de PC (la transmisión SSB estándar) está habilitado. Solo visible en modo RX. | |
| **Mosaico de estado/omisión ADSP** | Interactivo. Refleja qué reductor de ruido está actualmente activo. La etiqueta rota al nombre abreviado del módulo activo (por ejemplo, `NR2`, `NR4`, `BNR`). Vuelve a `ADSP` cuando no hay ninguno activo. Un solo clic omite todo el clúster NR con una instantánea en memoria; un solo clic nuevamente restaura el estado NR anterior. Doble clic abre el cuadro de diálogo de Configuración de AetherDSP. | Solo visible en modo RX. Estilo de anillo azul con punto LED verde. |
| **Mosaico de estado SPEAK** | No interactivo. Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada. Solo visible en modo RX. | |

## Consejos

- La omisión ADSP es independiente del botón **BYPASS**. Omitir todas las etapas RX con **BYPASS** no afecta el estado del mosaico ADSP, y viceversa.
- Haga doble clic en el mosaico **ADSP** para abrir la Configuración de AetherDSP y ajustar los parámetros individuales del reductor de ruido.
- El intervalo de discriminación de clic para distinguir un solo clic de un doble clic sigue la selección en Intervalo de Discriminación de Clic, no el intervalo de doble clic del sistema.
- El botón **BYPASS** opera de forma global (por motor de audio), no por perfil. Permanece presionado incluso al cambiar entre perfiles de la tira del canal.

## Relacionado

- [Omitir todas las etapas RX a la vez](bypass-every-rx-stage-at-once.md)
- [Abrir el editor flotante sin marco de una etapa desde la cadena](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
- [Ver de un vistazo si Audio de PC, el reductor de ruido y la salida de audio están activos (mosaicos de estado RX)](see-at-a-glance-whether-pc-audio-the-noise-reducer-and-audio-output-are-live-rx-status-tiles.md)
- Intervalo de Discriminación de Clic
