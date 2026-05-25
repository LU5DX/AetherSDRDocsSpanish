# Omitir todo el clúster NR desde el mosaico ADSP de la cadena RX

Omita todos los reductores de ruido del lado del cliente (NR2, NR4, MNR, DFNR, RN2, BNR) a la vez usando el mosaico ADSP en la cadena RX. El mosaico recuerda qué reductor de ruido estaba activo antes de la omisión, por lo que al hacer clic nuevamente se restaura ese módulo.

## Antes de comenzar

- El contenedor de la cadena de audio Aetherial debe estar visible. Haga clic en el botón de la bandeja **PUDU** en la barra lateral derecha para alternar su visibilidad.
- Haga clic en **RX** en la fila del encabezado para mostrar la cadena DSP de RX.

## Pasos

1. Localice el mosaico **ADSP** en la tira de la cadena RX. Se encuentra entre **RADIO** (izquierda) y **SPEAK** (derecha).
   - Cuando un reductor de ruido está activo, el mosaico muestra su nombre abreviado (p. ej., `NR2`, `NR4`, `BNR`).
   - Cuando ningún reductor de ruido está activo, el mosaico muestra `ADSP`.

2. **Haga clic una vez** en el mosaico **ADSP**.

   - Todos los reductores de ruido del lado del cliente se omiten. La etiqueta del mosaico muestra `ADSP`.
   - AetherSDR toma una instantánea en memoria de qué reductor de ruido estaba activo.

3. Para restaurar el reductor de ruido anterior, **haga clic una vez** en el mosaico **ADSP** nuevamente.

   - El módulo previamente activo se reactiva y su nombre abreviado reaparece en el mosaico. Si ningún módulo estaba activo al momento de la omisión, se habilita NR2 como valor predeterminado.

## Qué hace cada control

| Control                | Comportamiento                                                                                                                                                                                                                                                                                     | Notas |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------|
| **Mosaico ADSP**       | Haga clic para omitir todo el clúster NR. La etiqueta cambia para mostrar el nombre abreviado del módulo activo (`NR2`, `NR4`, `BNR`) o `ADSP` cuando ninguno está encendido. Haga doble clic para abrir el cuadro de diálogo de configuración de AetherDSP.                                         |       |
| **Botón BYPASS**       | Deshabilita todas las etapas de la cadena actual (TX o RX). No afecta la omisión de ADSP; funcionan de forma independiente.                                                                                                                                                                          |       |
| **Pestaña TX**         | Muestra y edita la cadena DSP de TX (Ecualización paramétrica, Compresor con previo de Drive y reducción de PAPR con rotador de fase, Puerta, De-Ess con pendiente seleccionable de 12–48 dB/oct, Tube con conmutación de reducción de ruido RN2, excitador PUDU, Reverberación). Color ámbar 'VUDU' cuando está seleccionada. La última pestaña activa se conserva mediante `PooDooAudioActiveTab`. | Forma parte de un par exclusivo con RX. |
| **Pestaña RX**         | Muestra y edita la cadena DSP de RX (EQ, AGC-G/Puerta, AGC-C/Compresor, DESS/DeEss, TUBE, EVO/Pudu). Las seis etapas están completamente implementadas. Limitada por los mosaicos de estado RADIO / ADSP / SPEAK. Interactiva: clic para omitir, doble clic para editar, arrastrar para reordenar. El color indica el lado activo. La última pestaña activa se conserva mediante `PooDooAudioActiveTab`. | Cada lado mantiene estado de etapa independiente, orden de cadena e instantánea BYPASS. |
| **Grabar** (glifo circular) | Captura hasta 30 segundos de audio TX posterior a PUDU. Haga clic nuevamente para detener (la reproducción comienza automáticamente). Información sobre herramientas: "Record up to 30 s of post-PooDoo™ TX audio (MIC must be set to PC and DAX off)." Oculto en modo RX. Solo habilitado cuando la entrada de micrófono está lista y la reproducción no está en curso. Parpadea en rojo mientras graba. | |
| **Reproducir** (glifo triangular) | Reproduce el audio PUDU capturado. Haga clic nuevamente para cancelar. Oculto en modo RX. Solo habilitado si existe una grabación y la grabación no está activa. Parpadea en verde mientras reproduce. | |
| **Etapa de cadena TX** (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | Un clic alterna la omisión de la etapa. Doble clic abre su editor flotante sin marco. Arrastre para reordenar la cadena TX. | Delegado a ClientChainWidget. Texto de sugerencia: "Click to bypass · Double click to edit · Drag to reorder". |
| **Etapa de cadena RX** (EQ / AGC-G / AGC-C / DESS / TUBE / EVO) | Un clic alterna la omisión de la etapa. Doble clic abre su editor flotante sin marco. Arrastre para reordenar la cadena RX. | Delegado a ClientRxChainWidget. Tipo MIME distinto para evitar solturas accidentales entre tiras TX y RX. |
| **Mosaico de estado RADIO** | No interactivo. Se vuelve verde cuando el audio de PC (la transmisión SSB estándar) está habilitado. Solo visible en modo RX. | |
| **Mosaico de estado/omisión ADSP** | Interactivo. Refleja qué reductor de ruido está activo actualmente. La etiqueta cambia al nombre abreviado del módulo activo (p. ej., `NR2`, `NR4`, `BNR`). Vuelve a `ADSP` cuando ninguno está encendido. Un clic omite todo el clúster NR con una instantánea en memoria; otro clic restaura el estado NR anterior. Doble clic abre el cuadro de diálogo de configuración de AetherDSP. | Solo visible en modo RX. Estilo de anillo azul con punto LED verde. |
| **Mosaico de estado SPEAK** | No interactivo. Se vuelve verde cuando la salida de audio de AetherSDR está activada. Solo visible en modo RX. | |

## Consejos

- La omisión de ADSP es independiente del botón **BYPASS**. Omitir todas las etapas de RX con **BYPASS** no afecta el estado del mosaico ADSP y viceversa.
- Haga doble clic en el mosaico **ADSP** para abrir la configuración de AetherDSP y ajustar parámetros individuales del reductor de ruido.
- El intervalo de discriminación de clics para distinguir un clic de un doble clic sigue la configuración en Intervalo de discriminación de clics, no el intervalo de doble clic del sistema.

## Relacionados

- [Omitir todas las etapas de RX a la vez](bypass-every-rx-stage-at-once.md)
- [Abrir el editor flotante sin marco de una etapa desde la cadena](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
- [Ver de un vistazo si el audio de PC, el reductor de ruido y la salida de audio están activos (mosaicos de estado RX)](see-at-a-glance-whether-pc-audio-the-noise-reducer-and-audio-output-are-live-rx-status-tiles.md)
- Intervalo de discriminación de clics
