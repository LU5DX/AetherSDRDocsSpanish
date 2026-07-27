# Omitir todo el clúster NR desde el mosaico ADSP de la cadena RX

Omita todos los reductores de ruido del lado del cliente (NR2, NR4, MNR, DFNR, RN2, NV-AFX) a la vez usando el mosaico ADSP en la cadena RX. El mosaico recuerda qué reductor de ruido estaba activo antes de la omisión, por lo que al hacer clic nuevamente se restaura ese módulo.

## Antes de comenzar

- El contenedor Aetherial Audio Chain debe estar visible. Haga clic en el botón **PUDU** de la bandeja en la barra lateral derecha para activarlo.
- Haga clic en **RX** en la fila del encabezado para mostrar la cadena DSP de RX.

## Pasos

1. Localice el mosaico **ADSP** en la tira de la cadena RX. Se encuentra entre **RADIO** (izquierda) y **SPEAK** (derecha).
   - Cuando un reductor de ruido está activo, el mosaico muestra su nombre abreviado (p. ej., `NR2`, `NR4`, `NV-AFX`).
   - Cuando no hay ningún reductor de ruido activo, el mosaico muestra `ADSP`.

2. **Haga clic una vez** en el mosaico **ADSP**.

   - Todos los reductores de ruido del lado del cliente se omiten. La etiqueta del mosaico muestra `ADSP`.
   - AetherSDR toma una instantánea en memoria de qué reductor de ruido estaba activo.

3. Para restaurar el reductor de ruido anterior, **haga clic una vez** en el mosaico **ADSP** nuevamente.

   - El módulo previamente activo se rehabilita y su nombre abreviado vuelve a aparecer en el mosaico. Si no había ningún módulo activo al momento de la omisión, se habilita NR2 como valor predeterminado.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| **Mosaico ADSP** | Haga clic para omitir todo el clúster NR. La etiqueta rota para mostrar el nombre abreviado del módulo activo (`NR2`, `NR4`, `NV-AFX`) o `ADSP` cuando ninguno está activo. El doble clic abre el diálogo de configuración de AetherDSP. | Solo visible en modo RX. Adopta el estilo de anillo azul con punto LED verde. |
| **Botón BYPASS** | Deshabilita todas las etapas de la cadena seleccionada (incluyendo NV-AFX). Haga clic nuevamente para restaurar las etapas que estaban activas antes. El alcance es global (por motor de audio), no por perfil: el botón permanece presionado al cambiar entre perfiles de Channel Strip. | TX y RX mantienen instantáneas independientes. |
| **Pestaña TX** | Muestra y edita la cadena DSP de TX (EQ paramétrico, Compresor con Drive previo al compresor y reducción de PAPR con rotador de fase, Puerta, De-Ess con pendiente seleccionable de 12–48 dB/oct, Tube con conmutación de reducción de ruido RN2, excitador PUDU, Reverberación). Color ámbar 'VUDU' cuando está seleccionada. La última pestaña activa persiste mediante `PooDooAudioActiveTab`. | Forma un par exclusivo con RX. |
| **Pestaña RX** | Muestra y edita la cadena DSP de RX (EQ, AGC-G/Puerta, AGC-C/Compresor, DESS/DeEss, TUBE, EVO/Pudu). Las seis etapas están completamente implementadas. Enmarcada por los mosaicos de estado RADIO / ADSP / SPEAK. Interactiva: clic para omitir, doble clic para editar, arrastrar para reordenar. El color indica el lado activo. La última pestaña activa persiste mediante `PooDooAudioActiveTab`. | Cada lado mantiene estado de etapa independiente, orden de cadena e instantánea de BYPASS. |
| **Grabar** (glifo de círculo) | Captura hasta 30 segundos de audio TX posterior a PUDU. Haga clic nuevamente para detener (la reproducción comienza automáticamente). Información sobre herramientas: "Record up to 30 s of post-PooDoo™ TX audio (MIC must be set to PC and DAX off)". Oculto en modo RX. Solo se habilita cuando la entrada de micrófono está lista y la reproducción no está en curso. Parpadea en rojo durante la grabación. | |
| **Reproducir** (glifo de triángulo) | Reproduce el audio PUDU capturado. Haga clic nuevamente para cancelar. Oculto en modo RX. Solo se habilita cuando existe una grabación y la grabación no está activa. Parpadea en verde durante la reproducción. | |
| **Etapa de cadena TX** (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | Un solo clic activa o desactiva la omisión de la etapa. El doble clic abre su editor flotante sin marco. Arrastrar reordena la cadena TX. | Delegado a ClientChainWidget. Texto de ayuda: "Click to bypass · Double click to edit · Drag to reorder". |
| **Etapa de cadena RX** (EQ / AGC-G / AGC-C / DESS / TUBE / EVO) | Un solo clic activa o desactiva la omisión de la etapa. El doble clic abre su editor flotante sin marco. Arrastrar reordena la cadena RX. | Delegado a ClientRxChainWidget. El tipo MIME distinto `application/x-aethersdr-rx-chain-stage` evita colocaciones accidentales entre las tiras de TX y RX. |
| **Mosaico de estado RADIO** | No interactivo. Se vuelve verde cuando PC Audio (la transmisión SSB estándar) está habilitado. Solo visible en modo RX. | |
| **Mosaico de estado/omisión ADSP** | Interactivo. Refleja qué reductor de ruido está activo actualmente. La etiqueta rota al nombre abreviado del módulo activo (p. ej., `NR2`, `NR4`, `NV-AFX`). Vuelve a `ADSP` cuando ninguno está activo. Un solo clic omite todo el clúster NR con una instantánea en memoria; un solo clic nuevamente restaura el estado NR anterior. El doble clic abre el diálogo de configuración de AetherDSP. | Solo visible en modo RX. Estilo de anillo azul con punto LED verde. |
| **Mosaico de estado SPEAK** | No interactivo. Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada. Solo visible en modo RX. | |

## Consejos

- La omisión de ADSP es independiente del botón **BYPASS**. Omitir todas las etapas de RX con **BYPASS** no afecta el estado del mosaico ADSP, y viceversa.
- Haga doble clic en el mosaico **ADSP** para abrir la configuración de AetherDSP y ajustar los parámetros individuales del reductor de ruido.
- El intervalo de discriminación de clics para distinguir un clic simple de un doble clic sigue la elección en Click Discrimination Interval, no el intervalo de doble clic del sistema.
- El botón **BYPASS** opera globalmente (por motor de audio), no por perfil. Permanece presionado incluso al cambiar entre perfiles de Channel Strip.

## Relacionado

- [Bypass every RX stage at once](bypass-every-rx-stage-at-once.md)
- [Open a stage's frameless floating editor from the chain](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
- [See at a glance whether PC Audio, the noise reducer, and audio output are live (RX status tiles)](see-at-a-glance-whether-pc-audio-the-noise-reducer-and-audio-output-are-live-rx-status-tiles.md)
- Click Discrimination Interval
