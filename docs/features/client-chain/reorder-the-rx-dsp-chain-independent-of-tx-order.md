# Reordenar la cadena de DSP de RX (independiente del orden de TX)

Esta página explica cómo arrastrar las etapas de DSP de RX a un nuevo orden dentro del applet Aetherial Audio Chain. El orden de la cadena de RX se almacena y aplica de forma independiente de la cadena de TX.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado "PUDU" en el panel del applet para mostrarlo.
- La tira de la cadena de RX debe estar activa. Si la cadena de TX está actualmente visible, cambie primero a RX (consulte [Cambiar entre la edición de las cadenas de TX y RX](switch-between-editing-the-tx-and-rx-chains.md)).

## Pasos

1. En la fila de encabezado de Aetherial Audio Chain, haga clic en "RX" para mostrar la tira de la cadena de RX. El botón RX se vuelve ámbar cuando está seleccionado.
2. Localice la etapa que desea mover. La cadena de RX contiene hasta seis etapas: EQ, AGC-G, AGC-C, DESS, TUBE y EVO, flanqueadas por los mosaicos de estado no interactivos RADIO, ADSP y SPEAK.
3. Haga clic y mantenga presionado el mosaico de la etapa que desea reordenar.
4. Arrástrelo hacia la izquierda o la derecha a lo largo de la tira de la cadena. Aparece una barra cian vertical entre los mosaicos para mostrar dónde se colocará la etapa.
5. Suelte para soltar la etapa en la nueva posición. La cadena se reordena inmediatamente y el nuevo orden se guarda en `ClientCompRxChainStages`.

## Función de cada control

| Control | Tipo | Comportamiento |
|---------|------|----------|
| TX | Botón de alternancia | Muestra y edita la cadena de DSP de TX (ClientChainWidget) — totalmente interactiva: clic para bypass, doble clic para editar, arrastrar para reordenar. Forma parte de un par exclusivo con RX; color ámbar 'VUDU' cuando está seleccionado. La última pestaña activa persiste mediante `PooDooAudioActiveTab='TX'` / `'RX'`. |
| RX | Botón de alternancia | Muestra y edita la cadena de DSP de RX (ClientRxChainWidget) — también totalmente interactiva con clic para bypass, doble clic para editar, arrastrar para reordenar; flanqueada por los mosaicos de estado RADIO / ADSP / SPEAK. Cada lado mantiene un estado de etapa, orden de cadena y captura de BYPASS independientes. Valor predeterminado: desmarcado. |
| BYPASS | Botón de alternancia | Deshabilita todas las etapas de la cadena seleccionada (incluido RN2). Vuelva a hacer clic para restaurar las etapas que estaban activas antes. El alcance es global (por motor de audio), no por perfil: el botón permanece presionado al cambiar de perfil en Channel Strip. TX y RX mantienen capturas separadas. |
| Record (glifo de círculo) | Botón de alternancia | Captura hasta 30 s de audio de TX posterior a PUDU; vuelva a hacer clic para detener (la reproducción comienza automáticamente). Información sobre herramientas: 'Graba hasta 30 s de audio de TX posterior a PooDoo™ (el MIC debe estar configurado en PC y DAX desactivado)'. Oculto en modo RX (función solo de TX). Solo se habilita cuando la entrada de micrófono está lista y la reproducción no está en ejecución. Parpadea en rojo mientras graba. |
| Play (glifo de triángulo) | Botón de alternancia | Reproduce el audio PUDU capturado; vuelva a hacer clic para cancelar. Oculto en modo RX. Solo se habilita si existe una grabación y la grabación no está activa. Parpadea en verde mientras reproduce. |
| Etapa de cadena TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | Asa de arrastre | Un clic alterna el bypass de la etapa; doble clic abre Aetherial Audio Channel Strip; arrastrar reordena la cadena TX. El texto de sugerencia debajo indica 'Clic para bypass · Doble clic para editar · Arrastrar para reordenar'. |
| Etapa de cadena RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO) | Asa de arrastre | Un clic alterna el bypass de la etapa RX; doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena RX. Las seis etapas de RX están completamente implementadas. El orden es independiente de la cadena TX. El tipo mime `'application/x-aethersdr-rx-chain-stage'` evita que las caídas accidentales se mezclen entre las dos tiras. |
| Mosaico de estado RADIO | Indicador | Flanqueo no interactivo del lado RX. Se vuelve verde cuando PC Audio (el flujo SSB estándar) está habilitado. Solo visible en modo RX. |
| Mosaico de estado/bypass ADSP | Botón de alternancia | Mosaico interactivo del lado RX que refleja qué reductor de ruido del lado del cliente está actualmente activo. La etiqueta cambia al nombre corto del módulo activo (p. ej., 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está activo. Un clic bypassa todo el clúster NR con una captura en memoria; otro clic restaura el estado NR anterior. Doble clic abre el diálogo AetherDSP Settings. Solo visible en modo RX. La restauración de la captura vuelve a NR2 si no había módulos activos en el momento del bypass. |
| Mosaico de estado SPEAK | Indicador | Flanqueo no interactivo del lado RX. Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada. Solo visible en modo RX. |

## Comportamiento de doble clic en la cadena TX (v0.9.7)

En v0.9.7, hacer doble clic en cualquier mosaico de etapa de la cadena TX ya no abre el editor flotante sin marco de esa etapa individual directamente. En su lugar, abre el **Aetherial Audio Channel Strip** unificado — la ventana única de DSP de TX. Los editores flotantes por etapa permanecen accesibles desde dentro de Channel Strip. Este cambio afecta solo a la cadena TX; hacer doble clic en una etapa de RX aún abre su editor flotante sin marco como antes.

## Sincronización de BYPASS (v0.9.8)

El botón BYPASS ahora refleja el estado de bypass propiedad del motor tanto para TX como para RX de forma independiente. Esto significa:

- El estado del botón BYPASS se actualiza automáticamente al cambiar entre modos TX y RX.
- Activar BYPASS desde dentro de Aetherial Audio Channel Strip actualiza el botón BYPASS del applet de cadena, y viceversa tanto para TX como para RX.
- El estado visual marcado del botón BYPASS siempre refleja el estado del motor para el lado actualmente mostrado (TX o RX).

## Intervalo de discriminación de clic

La ventana de tiempo utilizada para distinguir un clic simple de un doble clic ahora está controlada por el diálogo **Interaction Settings** en lugar del intervalo de doble clic del sistema. Esto permite ajustar la capacidad de respuesta de las acciones de clic simple (bypass) frente a doble clic (editar) independientemente de la configuración de su sistema operativo. Tanto los widgets de cadena TX como RX utilizan este intervalo personalizado.

## Soporte de temas (v26.6.1)

A partir de v26.6.1, el applet de cadena y todos los mosaicos de etapa utilizan colores conscientes del tema en lugar de valores hexadecimales fijos. El contenedor ahora tiene aplicado el selector de tema `applet/chain`, y todos los colores de los mosaicos de etapa se derivan del tema activo actual. Esto significa:

- Los fondos, bordes, líneas de conexión y colores de texto de los mosaicos de etapa se actualizan automáticamente al cambiar de tema.
- El indicador de MIC listo y los estados activos de TX utilizan los mismos colores de acento que otros applets (verde de éxito para listo, rojo de peligro para TX activo).
- El indicador de caída cian y los bordes de acento azul utilizan el color de acento del tema.

## Consejos

- El texto de sugerencia debajo de la cadena dice "Clic para bypass · Doble clic para editar · Arrastrar para reordenar" y se aplica tanto a los modos TX como RX.
- La cadena de RX utiliza un tipo de arrastrar y soltar distinto internamente, por lo que las etapas no se pueden soltar accidentalmente en la tira de la cadena TX y viceversa.
- Cambiar a TX con "TX" y reordenar allí no afecta el orden de RX guardado. Las dos cadenas mantienen secuencias de etapa independientes.
- En el lado TX, hacer doble clic en cualquier etapa es el gesto canónico para abrir el editor de audio de TX. Use los controles propios de Channel Strip para navegar a la configuración de etapa individual.
- El botón BYPASS es global (por motor de audio), no por perfil. Si cambia de perfil en Channel Strip mientras BYPASS está activo, el botón permanece marcado y la cadena TX permanece en bypass.

## Solución de problemas

- **Arrastrar una etapa no tiene efecto** — Confirme que el botón "RX" esté marcado (ámbar). Si la tira de la cadena TX está visible, la cadena RX ignora las caídas.
- **Los mosaicos RADIO, ADSP o SPEAK se mueven inesperadamente** — Estos mosaicos son indicadores de estado y no se pueden arrastrar. Solo los seis mosaicos de etapa con nombre (EQ, AGC-G, AGC-C, DESS, TUBE, EVO) se pueden reordenar.
- **La cadena reordenada se revierte después de reiniciar** — Esto no debería ocurrir si `ClientCompRxChainStages` se está escribiendo. Verifique que AetherSDR tenga acceso de escritura a su ubicación de almacenamiento de configuración.
- **El estado del botón BYPASS no coincide entre TX y RX** — Asegúrese de que el motor de audio se haya inicializado antes de abrir el applet de cadena. Cada lado mantiene su propio estado de bypass propiedad del motor, y cambiar de modo actualiza el botón automáticamente.
- **El clic/doble clic se siente demasiado rápido o demasiado lento** — Ajuste el intervalo de discriminación de clic en **Settings > Interaction Settings** para que coincida con su preferencia.
- **Los colores de las etapas se ven incorrectos después de un cambio de tema** — Esto es esperable si el tema se cambió mientras el applet de cadena estaba abierto. Cierre y vuelva a abrir el applet de cadena para recargar todos los colores del tema.

## Relacionados

- [Cambiar entre la edición de las cadenas de TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Reordenar la cadena de DSP de TX](reorder-the-tx-dsp-chain.md)
- [Bypass de todas las etapas de RX a la vez](bypass-every-rx-stage-at-once.md)
- [Abrir el editor flotante sin marco de una etapa desde la cadena](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
- [Ver de un vistazo si PC Audio, el reductor de ruido y la salida de audio están activos (mosaicos de estado de RX)](see-at-a-glance-whether-pc-audio-the-noise-reducer-and-audio-output-are-live-rx-status-tiles.md)
