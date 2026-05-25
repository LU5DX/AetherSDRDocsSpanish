# Reproducción del audio PUDU capturado

Esta página explica cómo reproducir el audio que ya ha grabado con el monitor de TX post-PUDU. Úsela para escuchar exactamente cómo suena su señal transmitida después de que la cadena completa de DSP de TX la haya procesado.

## Antes de comenzar

- Debe tener una grabación existente. El botón **Play (▶)** solo se habilita cuando existe una grabación.
- La grabación no debe estar activa en ese momento. El botón **Play (▶)** se deshabilita mientras el botón **Record (⏺)** está presionado.
- El contenedor Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado `PUDU` en la barra lateral derecha para mostrarlo.
- La cadena de TX debe ser la vista activa. El botón **Play (▶)** está oculto en modo RX.

## Pasos

1. En la fila de encabezado de Aetherial Audio Chain, confirme que el botón **TX** esté seleccionado. Si no es así, haga clic en **TX**.
2. Haga clic en el botón **Play (▶)**.
   - El botón parpadea en verde mientras la reproducción está en curso.
3. Para detener la reproducción antes de que termine, haga clic nuevamente en el botón **Play (▶)**.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---------|---------------|-------|
| **TX** | Muestra y edita la cadena DSP de TX (ClientChainWidget) — completamente interactiva: clic para bypass, doble clic para editar, arrastrar para reordenar. | Forma parte de un par exclusivo con RX; color ámbar 'VUDU' cuando está seleccionado. La última pestaña activa persiste mediante `PooDooAudioActiveTab='TX'` / `'RX'`. |
| **RX** | Muestra y edita la cadena DSP de RX (ClientRxChainWidget) — también completamente interactiva con clic para bypass, doble clic para editar, arrastrar para reordenar; flanqueada por los mosaicos de estado RADIO / DSP / SPEAK. | Cada lado mantiene el estado de etapa independiente, el orden de la cadena y la instantánea BYPASS. |
| **Play (▶)** | Inicia la reproducción del audio PUDU capturado; haga clic nuevamente para cancelar. | Oculto en modo RX. Habilitado solo cuando existe una grabación y la grabación no está activa. Parpadea en verde mientras se reproduce. |
| **Record (⏺)** | Deshabilitado durante la reproducción. | Se vuelve a habilitar automáticamente cuando termina la reproducción. |
| Etapa de la cadena TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | Un solo clic activa o desactiva el bypass de la etapa; doble clic abre el Aetherial Audio Channel Strip (la ventana unificada de DSP de TX); arrastrar reordena la cadena de TX. | Ahora, al hacer doble clic en cualquier mosaico de etapa de TX se abre el channel strip en lugar de un editor flotante por etapa. Los editores por etapa siguen siendo accesibles desde el propio channel strip. |
| **BYPASS** | Marcado: captura una instantánea de las etapas habilitadas en el lado activo y las deshabilita todas. Desmarcado: vuelve a habilitar las etapas que estaban activas antes. | Cuando el lado TX está activo, el estado del botón BYPASS se sincroniza con el bypass maestro de TX del motor. Cuando el lado RX está activo, el estado del botón BYPASS se sincroniza con el bypass de RX del motor. Alternar BYPASS en cualquier lado actualiza la instantánea propiedad del motor para ese lado. Cambiar de pestaña actualiza el visual de BYPASS automáticamente. |
| Etapa de la cadena RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO) | Un solo clic activa o desactiva el bypass de la etapa de RX; doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena de RX. | Delegado a ClientRxChainWidget. Las seis etapas de RX (EQ, AGC-G/Gate, AGC-C/Comp, DESS/DeEss, TUBE, EVO/Pudu) están completamente implementadas. El orden es independiente de la cadena de TX. El tipo MIME distinto `application/x-aethersdr-rx-chain-stage` evita caídas accidentales entre las dos tiras. |
| Mosaico de estado RADIO | Extremo no interactivo del lado RX. Se vuelve verde cuando el audio de PC (la transmisión SSB estándar) está habilitado. | Solo visible en modo RX. |
| Mosaico de estado/bypass ADSP | Mosaico interactivo del lado RX que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (p. ej., 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está activo. Un solo clic activa el bypass de todo el clúster NR con una instantánea en memoria; otro clic restaura el estado NR anterior. Doble clic abre el cuadro de diálogo AetherDSP Settings. | Solo visible en modo RX. Adopta el mismo estilo de anillo azul con punto LED verde que los mosaicos de etapa implementados. La restauración de la instantánea recurre a NR2 si no había módulos activos al momento del bypass. |
| Mosaico de estado SPEAK | Extremo no interactivo del lado RX. Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada. | Solo visible en modo RX. |

## Consejos

- El botón **Play (▶)** permanece habilitado mientras la reproducción está en curso para que pueda cancelarla en cualquier momento volviendo a hacer clic en él.
- Si desea una nueva grabación antes de escuchar, haga clic en **Record (⏺)** para capturar hasta 30 segundos de audio de TX post-PUDU. La reproducción comienza automáticamente cuando la grabación se detiene.
- El botón **Play (▶)** está oculto siempre que la pestaña **RX** esté activa. Cambie a **TX** para acceder a él.
- Al hacer doble clic en cualquier mosaico de etapa de la cadena TX se abre el Aetherial Audio Channel Strip, que proporciona acceso a todos los controles de DSP de TX en una sola ventana. Para editar una etapa específica de forma aislada, abra el channel strip y use sus propios controles.
- El botón BYPASS ahora utiliza instantáneas propiedad del motor tanto para TX como para RX. Cambiar entre las pestañas TX y RX actualiza automáticamente el estado de la marca BYPASS para que coincida con el lado activo.

## Solución de problemas

- **Play (▶) aparece atenuado** — Aún no existe una grabación, o hay una grabación en curso. Primero haga una grabación usando **Record (⏺)**, o espere a que finalice la grabación actual.
- **Play (▶) no es visible** — La pestaña **RX** está activa. Haga clic en **TX** para cambiar a la vista de la cadena TX.
- **El estado del botón BYPASS no coincide con lo que configuré en el channel strip** — El botón BYPASS en el applet de la cadena y el control BYPASS en el Aetherial Audio Channel Strip comparten el mismo estado de bypass de TX propiedad del motor. Cambiar al lado RX y volver restaurará el estado visual correcto. Para el bypass de RX, el estado visual ahora también está sincronizado con el motor.
- **El botón BYPASS muestra un estado incorrecto después de cambiar de pestaña** — En v0.9.8, el botón BYPASS lee correctamente el estado de bypass del motor para el lado activo. Cambiar de pestaña ahora activa la consulta correcta al motor: `isTxBypassed()` para modo TX y `isRxBypassed()` para modo RX.

## Relacionado

- [Grabar hasta 30 segundos de audio de TX post-PUDU](record-up-to-30-seconds-of-post-pudu-tx-audio.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Resumen de Aetherial Audio Chain](overview.md)
