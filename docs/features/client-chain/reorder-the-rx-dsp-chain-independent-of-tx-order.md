# Reordenar la cadena DSP de RX (independiente del orden de TX)

Esta página explica cómo arrastrar las etapas DSP de RX a un nuevo orden dentro del applet Aetherial Audio Chain. El orden de la cadena de RX se almacena y aplica independientemente de la cadena de TX.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado como "PUDU" en el panel del applet para mostrarlo.
- La tira de la cadena de RX debe estar activa. Si la cadena de TX está visible actualmente, cambie primero a RX (consulte [Switch between editing the TX and RX chains](switch-between-editing-the-tx-and-rx-chains.md)).

## Pasos

1. En la fila de encabezado de Aetherial Audio Chain, haga clic en "RX" para mostrar la tira de la cadena de RX. El botón RX se vuelve ámbar cuando está seleccionado.
2. Localice la etapa que desea mover. La cadena de RX contiene hasta seis etapas: EQ, AGC-G, AGC-C, DESS, TUBE y EVO, enmarcadas por los mosaicos de estado no interactivos RADIO, ADSP y SPEAK.
3. Haga clic y mantenga presionado el mosaico de la etapa que desea reordenar.
4. Arrástrelo hacia la izquierda o la derecha a lo largo de la tira de la cadena. Aparece una barra cian vertical entre los mosaicos para mostrar dónde se colocará la etapa.
5. Suelte para soltar la etapa en la nueva posición. La cadena se reordena inmediatamente y el nuevo orden se guarda en `ClientCompRxChainStages`.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---------|------|----------|
| TX | Botón de alternancia | Muestra y edita la cadena DSP de TX (ClientChainWidget) — completamente interactivo: clic para bypass, doble clic para editar, arrastrar para reordenar. Forma parte de un par exclusivo con RX; color ámbar 'VUDU' cuando está seleccionado. La última pestaña activa persiste mediante `PooDooAudioActiveTab='TX'` / `'RX'`. |
| RX | Botón de alternancia | Muestra y edita la cadena DSP de RX (ClientRxChainWidget) — también completamente interactivo con clic para bypass, doble clic para editar, arrastrar para reordenar; enmarcado por los mosaicos de estado RADIO / ADSP / SPEAK. Cada lado mantiene el estado de etapa, el orden de la cadena y la instantánea de BYPASS independientes. Predeterminado: sin marcar. |
| BYPASS | Botón de alternancia | Deshabilita cada etapa en la cadena seleccionada (incluyendo módulos NR). Haga clic de nuevo para restaurar las etapas que estaban activas antes. El ámbito es global (por motor de audio), no por perfil — el botón permanece presionado al cambiar de perfil en Channel Strip. TX y RX mantienen instantáneas separadas. |
| Record (glifo de círculo) | Botón de alternancia | Captura hasta 30 s de audio de TX posterior a PUDU; haga clic de nuevo para detener (la reproducción comienza automáticamente). Información sobre herramienta: 'Record up to 30 s of post-PooDoo™ TX audio (MIC must be set to PC and DAX off).' Oculto en modo RX (función solo de TX). Solo se habilita cuando la entrada de micrófono está lista y la reproducción no está en ejecución. Parpadea en rojo durante la grabación. |
| Play (glifo de triángulo) | Botón de alternancia | Reproduce el audio PUDU capturado; haga clic de nuevo para cancelar. Oculto en modo RX. Solo se habilita una vez que existe una grabación y la grabación no está activa. Parpadea en verde mientras se reproduce. |
| Etapa de cadena de TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | Mango de arrastre | Un solo clic alterna el bypass de la etapa; doble clic abre el Aetherial Audio Channel Strip; arrastrar reordena la cadena de TX. El texto de sugerencia debajo dice 'Click to bypass · Double click to edit · Drag to reorder'. |
| Etapa de cadena de RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO) | Mango de arrastre | Un solo clic alterna el bypass de la etapa de RX; doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena de RX. Las seis etapas de RX están completamente implementadas. El orden es independiente de la cadena de TX. El tipo mime distinto `'application/x-aethersdr-rx-chain-stage'` evita caídas accidentales entre las dos tiras. |
| Mosaico de estado RADIO | Indicador | Soporte de extremo de RX no interactivo. Se vuelve verde cuando PC Audio (el flujo SSB estándar) está habilitado. Solo visible en modo RX. |
| Mosaico de estado/bypass ADSP | Botón de alternancia | Mosaico de RX interactivo que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (p. ej., 'NR2', 'NR4', 'BNR', 'NVA'); vuelve a 'ADSP' cuando ninguno está activo. Un solo clic bypassa todo el clúster NR con una instantánea en memoria; un solo clic de nuevo restaura el estado NR anterior. La restauración de la instantánea utiliza el último módulo activo conocido (o vuelve a NR2 si no había ninguno activo). El mosaico ADSP ahora reconoce el módulo NVA (NVidia Affects) como parte del clúster NR — al pasar por alto o restaurar el clúster se alterna NVA además de NR2, NR4, MNR, DFNR y RN2. El doble clic abre el cuadro de diálogo AetherDSP Settings. Solo visible en modo RX. |
| Mosaico de estado SPEAK | Indicador | Soporte de extremo de RX no interactivo. Se vuelve verde cuando la salida de audio de AetherSDR está activada. Solo visible en modo RX. |

## Comportamiento de doble clic en la cadena de TX (v0.9.7)

En v0.9.7, el doble clic en cualquier mosaico de etapa de la cadena de TX ya no abre directamente el editor flotante sin marco individual de esa etapa. En su lugar, abre el **Aetherial Audio Channel Strip** unificado — la única ventana DSP de TX. Los editores flotantes por etapa siguen siendo accesibles desde dentro del channel strip. Este cambio afecta solo a la cadena de TX; el doble clic en una etapa de RX todavía abre el editor flotante sin marco de esa etapa como antes.

## Sincronización de BYPASS (v0.9.8)

El botón BYPASS ahora refleja el estado de bypass propiedad del motor tanto para TX como para RX de forma independiente. Esto significa:

- El estado del botón BYPASS se actualiza automáticamente al cambiar entre los modos TX y RX.
- Activar BYPASS desde dentro del Aetherial Audio Channel Strip actualiza el botón BYPASS del applet de cadena, y viceversa tanto para TX como para RX.
- El estado visual marcado del botón BYPASS siempre refleja el estado del motor para el lado mostrado actualmente (TX o RX).

## Intervalo de discriminación de clics

La ventana de tiempo utilizada para distinguir un solo clic de un doble clic ahora está controlada por el cuadro de diálogo **Interaction Settings** en lugar del intervalo de doble clic del sistema. Esto le permite ajustar la capacidad de respuesta de las acciones de un solo clic (bypass) frente a las de doble clic (editar) independientemente de la configuración de su sistema operativo. Tanto los widgets de cadena de TX como los de RX utilizan este intervalo personalizado.

## Soporte de temas (v26.6.1)

A partir de v26.6.1, el applet de cadena y todos los mosaicos de etapa utilizan colores conscientes del tema en lugar de valores hexadecimales codificados. El contenedor ahora tiene el selector de tema `applet/chain` aplicado, y todos los colores de los mosaicos de etapa se derivan del tema activo actual. Esto significa:

- Los fondos, bordes, líneas de conexión y colores de texto de los mosaicos de etapa se actualizan automáticamente al cambiar de tema.
- El indicador de micrófono listo y los estados activos de TX utilizan los mismos colores de acento que otros applets (verde de éxito para listo, rojo de peligro para TX activo).
- El indicador de caída cian y los bordes de acento azul utilizan el color de acento del tema.

## Consejos

- El texto de sugerencia debajo de la cadena dice "Click to bypass · Double click to edit · Drag to reorder" y se aplica tanto al modo TX como al RX.
- La cadena de RX utiliza un tipo de arrastrar y soltar distinto internamente, por lo que las etapas no se pueden soltar accidentalmente en la tira de la cadena de TX y viceversa.
- Cambiar a TX con "TX" y reordenar allí no afecta el orden de RX guardado. Las dos cadenas mantienen secuencias de etapas independientes.
- En el lado de TX, el doble clic en cualquier etapa es el gesto canónico para abrir el editor de audio de TX. Utilice los propios controles del channel strip para navegar a la configuración de etapas individuales.
- El botón BYPASS es global (por motor de audio), no por perfil. Si cambia de perfil en el Channel Strip mientras BYPASS está activo, el botón permanece marcado y la cadena de TX permanece en bypass.
- La instantánea de bypass de ADSP ahora incluye el módulo NVA (NVidia Affects). Si estaba usando NVA antes de pasar por alto el clúster NR, se volverá a habilitar cuando anule el bypass.

## Solución de problemas

- **Arrastrar una etapa no tiene efecto** — Confirme que el botón "RX" está marcado (ámbar). Si la tira de la cadena de TX está visible, la cadena de RX ignora las caídas.
- **Los mosaicos RADIO, ADSP o SPEAK se mueven inesperadamente** — Estos mosaicos son indicadores de estado y no se pueden arrastrar. Solo los seis mosaicos de etapa nombrados (EQ, AGC-G, AGC-C, DESS, TUBE, EVO) se pueden reordenar.
- **La cadena reordenada se revierte después de reiniciar** — Esto no debería suceder si `ClientCompRxChainStages` se está escribiendo. Verifique que AetherSDR tenga acceso de escritura a su ubicación de almacenamiento de configuración.
- **El estado del botón BYPASS no coincide entre TX y RX** — Asegúrese de que el motor de audio se haya inicializado antes de abrir el applet de cadena. Cada lado mantiene su propio estado de bypass propiedad del motor, y al cambiar de modo se actualiza el botón automáticamente.
- **El clic/doble clic se siente demasiado rápido o demasiado lento** — Ajuste el intervalo de discriminación de clics en **Settings > Interaction Settings** para que coincida con su preferencia.
- **Los colores de las etapas se ven incorrectos después de un cambio de tema** — Esto es esperable si el tema se cambió mientras el applet de cadena estaba abierto. Cierre y vuelva a abrir el applet de cadena para recargar todos los colores del tema.
- **El estado de NVA no se restaura correctamente después de anular el bypass** — El mosaico ADSP ahora incluye NVA en su instantánea de bypass. Asegúrese de haber actualizado a la v26.7.4 o posterior para un manejo correcto de NVA.

## Relacionados

- [Switch between editing the TX and RX chains](switch-between-editing-the-tx-and-rx-chains.md)
- [Reorder the TX DSP chain](reorder-the-tx-dsp-chain.md)
- [Bypass every RX stage at once](bypass-every-rx-stage-at-once.md)
- [Open a stage's frameless floating editor from the chain](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
- [See at a glance whether PC Audio, the noise reducer, and audio output are live (RX status tiles)](see-at-a-glance-whether-pc-audio-the-noise-reducer-and-audio-output-are-live-rx-status-tiles.md)
