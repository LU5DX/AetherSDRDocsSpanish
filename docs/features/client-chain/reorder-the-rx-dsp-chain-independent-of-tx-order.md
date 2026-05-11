# Reordenar la cadena DSP de RX (independiente del orden de TX)

Esta página explica cómo arrastrar las etapas DSP de RX a un nuevo orden dentro del applet Aetherial Audio Chain. El orden de la cadena RX se almacena y aplica independientemente de la cadena TX.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja denominado "PUDU" en el panel del applet para mostrarlo.
- La tira de la cadena RX debe estar activa. Si la cadena TX está visible actualmente, cambie primero a RX (consulte [Switch between editing the TX and RX chains](switch-between-editing-the-tx-and-rx-chains.md)).

## Pasos

1. En la fila de encabezado de Aetherial Audio Chain, haga clic en "RX" para mostrar la tira de la cadena RX. El botón RX se vuelve ámbar cuando está seleccionado.
2. Localice la etapa que desea mover. La cadena RX contiene hasta seis etapas: EQ, AGC-G, AGC-C, DESS, TUBE y EVO, delimitadas por los mosaicos de estado no interactivos RADIO, ADSP y SPEAK.
3. Haga clic y mantenga presionado el mosaico de la etapa que desea reordenar.
4. Arrástrelo hacia la izquierda o derecha a lo largo de la tira de la cadena. Aparece una barra cian vertical entre los mosaicos para indicar dónde se colocará la etapa.
5. Suelte para soltar la etapa en la nueva posición. La cadena se reordena inmediatamente y el nuevo orden se guarda en `ClientCompRxChainStages`.

## Qué hace cada control

| Control                                                       | Tipo                                                                                                                      | Comportamiento                                                                                                                                                                                                                                                                                                                                                                                         |
|---------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TX                                                            | Muestra y edita la cadena DSP de TX (ClientChainWidget) — completamente interactiva: clic para omitir, doble clic para editar, arrastrar para reordenar. | Forma parte de un par exclusivo con RX; color ámbar 'VUDU' cuando está seleccionado. La última pestaña activa persiste mediante PooDooAudioActiveTab='TX' / 'RX'.                                                                                                                                                                                                                                      |
| RX                                                            | Botón de alternancia                                                                                                      | Muestra y edita la cadena DSP de RX (ClientRxChainWidget) — también completamente interactiva con clic para omitir, doble clic para editar, arrastrar para reordenar; delimitada por mosaicos de estado RADIO / ADSP / SPEAK. Cada lado mantiene el estado de etapa, el orden de la cadena y la instantánea BYPASS independientes. Por defecto: desmarcado.                                              |
| BYPASS                                                        | Botón de alternancia                                                                                                      | Marcado: toma una instantánea de las etapas actualmente habilitadas en el lado activo (TX o RX) y las deshabilita todas. Desmarcado: vuelve a habilitar solo las etapas que estaban encendidas antes. Las etapas alternadas manualmente mientras BYPASS estaba activo se conservan fuera de la instantánea. TX y RX mantienen instantáneas separadas.                                                   |
| Record (glifo de círculo)                                     | Botón de alternancia                                                                                                      | Captura hasta 30 segundos de audio TX posterior a PUDU; haga clic nuevamente para detener (la reproducción comienza automáticamente). Información sobre herramientas: 'Record up to 30 s of post-PooDoo™ TX audio (MIC must be set to PC and DAX off).' Oculto en modo RX (función solo TX). Solo está habilitado cuando la entrada de micrófono está lista y la reproducción no está en ejecución. Parpadea en rojo mientras graba. |
| Play (glifo de triángulo)                                     | Botón de alternancia                                                                                                      | Reproduce el audio PUDU capturado; haga clic nuevamente para cancelar. Oculto en modo RX. Solo está habilitado una vez que existe una grabación y la grabación no está activa. Parpadea en verde mientras reproduce.                                                                                                                                                                                    |
| Etapa de cadena TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | Controlador de arrastre                                                                                                   | Un solo clic alterna la omisión de la etapa; doble clic abre Aetherial Audio Channel Strip (v0.9.7+); arrastrar reordena la cadena TX. El texto de sugerencia debajo dice 'Click to bypass · Double click to edit · Drag to reorder'.                                                                                                                                                                  |
| Etapa de cadena RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO)       | Controlador de arrastre                                                                                                   | Un solo clic alterna la omisión de la etapa RX; doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena RX. Las seis etapas RX (EQ, AGC-G/Gate, AGC-C/Comp, DESS/DeEss, TUBE, EVO/Pudu) están completamente implementadas. El orden es independiente de la cadena TX. Un tipo MIME distinto evita caídas accidentales.                                                   |
| Mosaico de estado RADIO                                        | Indicador                                                                                                                 | Delimitador RX no interactivo. Se vuelve verde cuando PC Audio (el flujo SSB estándar) está habilitado. Solo visible en modo RX.                                                                                                                                                                                                                                                                       |
| Mosaico de estado/omisión ADSP                                 | Botón de alternancia                                                                                                      | Mosaico RX interactivo que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (p. ej., 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está encendido. Un solo clic omite todo el clúster NR con una instantánea en memoria; otro solo clic restaura el estado NR anterior. Doble clic abre el diálogo AetherDSP Settings. Solo visible en modo RX. |
| Mosaico de estado SPEAK                                        | Indicador                                                                                                                 | Delimitador RX no interactivo. Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada. Solo visible en modo RX.                                                                                                                                                                                                                                                                     |
## Comportamiento de doble clic en la cadena TX (v0.9.7)

En la versión v0.9.7, hacer doble clic en cualquier mosaico de etapa de la cadena TX ya no abre directamente el editor flotante sin marco de esa etapa individual. En su lugar, abre el **Aetherial Audio Channel Strip** unificado — la ventana DSP de TX única. Los editores flotantes por etapa aún son accesibles desde dentro del Channel Strip. Este cambio afecta solo a la cadena TX; hacer doble clic en una etapa RX aún abre el editor flotante sin marco de esa etapa como antes.

## Sincronización de BYPASS (v0.9.8)

El botón BYPASS ahora refleja el estado de omisión propiedad del motor tanto para TX como para RX de forma independiente. Esto significa:

- El estado del botón BYPASS se actualiza automáticamente al cambiar entre los modos TX y RX.
- Activar BYPASS desde dentro de Aetherial Audio Channel Strip actualiza el botón BYPASS del applet de cadena, y viceversa tanto para TX como para RX.
- El estado visual marcado del botón BYPASS siempre refleja el estado del motor para el lado mostrado actualmente (TX o RX).

## Consejos

- El texto de sugerencia debajo de la cadena dice "Click to bypass · Double click to edit · Drag to reorder" y se aplica tanto a los modos TX como RX.
- La cadena RX utiliza un tipo de arrastrar y soltar distinto internamente, por lo que las etapas no se pueden soltar accidentalmente en la tira de la cadena TX y viceversa.
- Cambiar a TX con "TX" y reordenar allí no afecta el orden RX guardado. Las dos cadenas mantienen secuencias de etapas independientes.
- En el lado TX, hacer doble clic en cualquier etapa es el gesto canónico para abrir el editor de audio TX. Use los controles propios del Channel Strip para navegar a la configuración de etapas individuales.

## Solución de problemas

- **Arrastrar una etapa no tiene efecto** — Confirme que el botón "RX" está marcado (ámbar). Si la tira de la cadena TX está visible, los arrastres son ignorados por la cadena RX.
- **Los mosaicos RADIO, ADSP o SPEAK se mueven inesperadamente** — Estos mosaicos son indicadores de estado y no se pueden arrastrar. Solo se pueden reordenar los seis mosaicos de etapa con nombre (EQ, AGC-G, AGC-C, DESS, TUBE, EVO).
- **La cadena reordenada se revierte después de reiniciar** — Esto no debería ocurrir si `ClientCompRxChainStages` se está escribiendo. Verifique que AetherSDR tenga acceso de escritura a su ubicación de almacenamiento de configuración.
- **El estado del botón BYPASS no coincide entre TX y RX** — Asegúrese de que el motor de audio se haya inicializado antes de abrir el applet de cadena. Cada lado mantiene su propio estado de omisión propiedad del motor, y cambiar de modo actualiza el botón automáticamente.

## Relacionado

- [Switch between editing the TX and RX chains](switch-between-editing-the-tx-and-rx-chains.md)
- [Reorder the TX DSP chain](reorder-the-tx-dsp-chain.md)
- [Bypass every RX stage at once](bypass-every-rx-stage-at-once.md)
- [Open a stage's frameless floating editor from the chain](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
- [See at a glance whether PC Audio, the noise reducer, and audio output are live (RX status tiles)](see-at-a-glance-whether-pc-audio-the-noise-reducer-and-audio-output-are-live-rx-status-tiles.md)
