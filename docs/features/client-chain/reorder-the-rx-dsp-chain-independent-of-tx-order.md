# Reordenar la cadena DSP de RX (independientemente del orden de TX)

Esta página explica cómo arrastrar las etapas DSP de RX a un nuevo orden dentro del applet Aetherial Audio Chain. El orden de la cadena de RX se almacena y aplica de forma independiente de la cadena de TX.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado como "PUDU" en el panel del applet para mostrarlo.
- La tira de la cadena de RX debe estar activa. Si la cadena de TX está visible actualmente, cambie primero a RX (consulte [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)).

## Pasos

1. En la fila de encabezado de Aetherial Audio Chain, haga clic en "RX" para mostrar la tira de la cadena de RX. El botón RX se vuelve ámbar cuando está seleccionado.
2. Localice la etapa que desea mover. La cadena de RX contiene hasta seis etapas: EQ, AGC-G, AGC-C, DESS, TUBE y EVO, flanqueadas por los mosaicos de estado no interactivos RADIO, ADSP y SPEAK.
3. Haga clic y mantenga presionado el mosaico de la etapa que desea reordenar.
4. Arrástrelo hacia la izquierda o hacia la derecha a lo largo de la tira de la cadena. Aparece una barra cian vertical entre los mosaicos para mostrar dónde se colocará la etapa.
5. Suelte para soltar la etapa en la nueva posición. La cadena se reordena inmediatamente y el nuevo orden se guarda en `ClientCompRxChainStages`.

## Qué hace cada control

| Control                                                       | Tipo                                                                                                                      | Comportamiento                                                                                                                                                                                                                                                                                                                                                                                                  |
|---------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TX                                                            | Muestra y edita la cadena DSP de TX (ClientChainWidget) — completamente interactiva: clic para bypass, doble clic para editar, arrastrar para reordenar. | Forma parte de un par exclusivo con RX; color ámbar 'VUDU' cuando está seleccionado. La última pestaña activa persiste mediante PooDooAudioActiveTab='TX' / 'RX'.                                                                                                                                                                                                                                                |
| RX                                                            | Botón de alternancia                                                                                                      | Muestra y edita la cadena DSP de RX (ClientRxChainWidget) — también completamente interactiva con clic para bypass, doble clic para editar, arrastrar para reordenar; flanqueada por los mosaicos de estado RADIO / ADSP / SPEAK. Cada lado mantiene el estado de etapa independiente, el orden de la cadena y la instantánea de BYPASS. Valor predeterminado: no marcado.                                        |
| BYPASS                                                        | Botón de alternancia                                                                                                      | Marcado: toma una instantánea de las etapas actualmente habilitadas en el lado activo (TX o RX) y las deshabilita todas. No marcado: reactiva solo las etapas que estaban activas antes. Las etapas activadas/desactivadas manualmente mientras BYPASS estaba activo se conservan fuera de la instantánea. TX y RX mantienen instantáneas separadas.                                                              |
| Record (glifo de círculo)                                     | Botón de alternancia                                                                                                      | Captura hasta 30 s de audio de TX posterior a PUDU; haga clic nuevamente para detener (la reproducción comienza automáticamente). Información sobre herramientas: 'Record up to 30 s of post-PooDoo™ TX audio (MIC must be set to PC and DAX off)'. Oculto en modo RX (función solo de TX). Solo habilitado cuando la entrada de micrófono está lista y la reproducción no está en ejecución. Parpadea en rojo mientras graba. |
| Play (glifo de triángulo)                                     | Botón de alternancia                                                                                                      | Reproduce el audio PUDU capturado; haga clic nuevamente para cancelar. Oculto en modo RX. Solo habilitado una vez que existe una grabación y la grabación no está activa. Parpadea en verde mientras reproduce.                                                                                                                                                                                                  |
| Etapa de cadena TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | Mango de arrastre                                                                                                         | Un solo clic alterna el bypass de la etapa; doble clic abre el Aetherial Audio Channel Strip (v0.9.7+); arrastre reordena la cadena TX. El texto de sugerencia debajo dice 'Click to bypass · Double click to edit · Drag to reorder'.                                                                                                                                                                         |
| Etapa de cadena RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO)       | Mango de arrastre                                                                                                         | Un solo clic alterna el bypass de la etapa RX; doble clic abre su editor flotante sin marco en modo RX; arrastre reordena la cadena RX. Las seis etapas RX (EQ, AGC-G/Gate, AGC-C/Comp, DESS/DeEss, TUBE, EVO/Pudu) están completamente implementadas. El orden es independiente de la cadena TX. Un tipo MIME distinto evita soltarlos accidentalmente.                                                         |
| Mosaico de estado RADIO                                       | Indicador                                                                                                                 | Flanqueo del lado RX no interactivo. Se vuelve verde cuando PC Audio (el flujo SSB estándar) está habilitado. Solo visible en modo RX.                                                                                                                                                                                                                                                                          |
| Mosaico de estado/bypass ADSP                                 | Botón de alternancia                                                                                                      | Mosaico interactivo del lado RX que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (p. ej., 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está activo. Un solo clic desvía todo el grupo NR con una instantánea en memoria; otro clic restaura el estado NR anterior. Doble clic abre el cuadro de diálogo AetherDSP Settings. Solo visible en modo RX. |
| Mosaico de estado SPEAK                                       | Indicador                                                                                                                 | Flanqueo del lado RX no interactivo. Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada. Solo visible en modo RX.                                                                                                                                                                                                                                                                        |
## Comportamiento de doble clic en la cadena TX (v0.9.7)

En la v0.9.7, hacer doble clic en cualquier mosaico de etapa de la cadena TX ya no abre directamente el editor flotante sin marco de esa etapa individual. En su lugar, abre el **Aetherial Audio Channel Strip** unificado — la ventana DSP única de TX. Los editores flotantes por etapa siguen siendo accesibles desde dentro del channel strip. Este cambio afecta solo a la cadena TX; hacer doble clic en una etapa RX aún abre el editor flotante sin marco de esa etapa como antes.

## Sincronización de BYPASS (v0.9.8)

El botón BYPASS ahora refleja el estado de bypass propiedad del motor tanto para TX como para RX de forma independiente. Esto significa:

- El estado del botón BYPASS se actualiza automáticamente al cambiar entre los modos TX y RX.
- Activar BYPASS desde dentro del Aetherial Audio Channel Strip actualiza el botón BYPASS del applet de la cadena, y viceversa tanto para TX como para RX.
- El estado visual marcado del botón BYPASS siempre refleja el estado del motor para el lado mostrado actualmente (TX o RX).

## Intervalo de discriminación de clic

La ventana de tiempo utilizada para distinguir un solo clic de un doble clic ahora está controlada por el cuadro de diálogo **Interaction Settings** en lugar del intervalo de doble clic del sistema. Esto permite ajustar la capacidad de respuesta de las acciones de un solo clic (bypass) frente a doble clic (editar) independientemente de la configuración de su sistema operativo. Tanto los widgets de la cadena TX como RX utilizan este intervalo personalizado.

## Consejos

- El texto de sugerencia debajo de la cadena dice "Click to bypass · Double click to edit · Drag to reorder" y se aplica tanto a los modos TX como RX.
- La cadena RX utiliza un tipo de arrastrar y soltar distinto internamente, por lo que las etapas no se pueden soltar accidentalmente en la tira de la cadena TX y viceversa.
- Cambiar a TX con "TX" y reordenar allí no afecta el orden de RX guardado. Las dos cadenas mantienen secuencias de etapa independientes.
- En el lado TX, hacer doble clic en cualquier etapa es el gesto canónico para abrir el editor de audio TX. Utilice los propios controles del channel strip para navegar a la configuración de etapa individual.

## Solución de problemas

- **Arrastrar una etapa no tiene efecto** — Confirme que el botón "RX" está marcado (ámbar). Si la tira de la cadena TX está visible, la cadena RX ignora los soltados.
- **Los mosaicos RADIO, ADSP o SPEAK se mueven inesperadamente** — Estos mosaicos son indicadores de estado y no se pueden arrastrar. Solo se pueden reordenar los seis mosaicos de etapa con nombre (EQ, AGC-G, AGC-C, DESS, TUBE, EVO).
- **La cadena reordenada se revierte después de reiniciar** — Esto no debería ocurrir si se está escribiendo `ClientCompRxChainStages`. Verifique que AetherSDR tenga acceso de escritura a su ubicación de almacenamiento de configuración.
- **El estado del botón BYPASS no coincide entre TX y RX** — Asegúrese de que el motor de audio se haya inicializado antes de abrir el applet de la cadena. Cada lado mantiene su propio estado de bypass propiedad del motor, y cambiar de modo actualiza el botón automáticamente.
- **El clic/doble clic se siente demasiado rápido o demasiado lento** — Ajuste el intervalo de discriminación de clic en **Settings > Interaction Settings** según su preferencia.

## Relacionados

- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Reordenar la cadena DSP de TX](reorder-the-tx-dsp-chain.md)
- [Desviar todas las etapas de RX a la vez](bypass-every-rx-stage-at-once.md)
- [Abrir el editor flotante sin marco de una etapa desde la cadena](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
- [Ver de un vistazo si PC Audio, el reductor de ruido y la salida de audio están activos (mosaicos de estado RX)](see-at-a-glance-whether-pc-audio-the-noise-reducer-and-audio-output-are-live-rx-status-tiles.md)
