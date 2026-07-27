# Reproducir el audio PUDU capturado

Esta página explica cómo reproducir el audio que ya ha grabado con el monitor TX posterior a PUDU. Úselo para escuchar exactamente cómo suena su señal transmitida después de que la cadena DSP de TX completa la haya procesado.

## Antes de comenzar

- Debe tener una grabación existente. El botón **Play (▶)** solo está habilitado cuando existe una grabación.
- La grabación no debe estar activa en ese momento. El botón **Play (▶)** se deshabilita mientras el botón **Record (⏺)** está presionado.
- El contenedor Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado `PUDU` en la barra lateral derecha para mostrarlo.
- La cadena TX debe ser la vista activa. El botón **Play (▶)** está oculto en el modo RX.

## Pasos

1. En la fila de encabezado de Aetherial Audio Chain, confirme que el botón **TX** esté seleccionado. Si no es así, haga clic en **TX**.
2. Haga clic en el botón **Play (▶)**.
   - El botón parpadea en verde mientras la reproducción está en curso.
3. Para detener la reproducción antes de que termine, haga clic en el botón **Play (▶)** nuevamente.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---------|---------------|-------|
| **TX** | Muestra y edita la cadena DSP de TX (ClientChainWidget) — totalmente interactiva: clic para omitir, doble clic para editar, arrastrar para reordenar. | Forma parte de un par exclusivo con RX; color ámbar 'VUDU' cuando está seleccionado. La última pestaña activa se conserva mediante `PooDooAudioActiveTab='TX'` / `'RX'`. |
| **RX** | Muestra y edita la cadena DSP de RX (ClientRxChainWidget) — también totalmente interactiva con clic para omitir, doble clic para editar, arrastrar para reordenar; flanqueada por mosaicos de estado RADIO / DSP / SPEAK. | Cada lado mantiene el estado de etapa independiente, el orden de la cadena y la instantánea BYPASS. |
| **Play (▶)** | Inicia la reproducción del audio PUDU capturado; haga clic nuevamente para cancelar. | Oculto en el modo RX. Habilitado solo cuando existe una grabación y la grabación no está activa. Parpadea en verde mientras se reproduce. |
| **Record (⏺)** | Deshabilitado durante la reproducción. | Se vuelve a habilitar automáticamente cuando termina la reproducción. |
| Etapa de la cadena TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | Un solo clic activa o desactiva la omisión de la etapa; el doble clic abre Aetherial Audio Channel Strip (la ventana unificada DSP de TX); arrastrar reordena la cadena TX. | Al hacer doble clic en cualquier mosaico de etapa TX ahora se abre el channel strip en lugar de un editor flotante por etapa. Los editores por etapa siguen siendo accesibles desde el propio channel strip. |
| **BYPASS** | Marcado: captura una instantánea de las etapas habilitadas actualmente en el lado activo (incluido RN2) y las deshabilita todas. Sin marcar: vuelve a habilitar las etapas que estaban activas antes. | El alcance es global (por motor de audio), no por perfil. El botón permanece presionado al cambiar de perfil de Channel Strip. Cuando el lado TX está activo, el estado del botón BYPASS se sincroniza con la omisión maestra de TX del motor. Cuando el lado RX está activo, el estado del botón BYPASS se sincroniza con la omisión de RX del motor. Alternar BYPASS en cualquier lado actualiza la instantánea propiedad del motor para ese lado. Cambiar de pestaña actualiza el estado visual de BYPASS automáticamente. |
| Etapa de la cadena RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO) | Un solo clic activa o desactiva la omisión de la etapa RX; el doble clic abre su editor flotante sin marco en el modo RX; arrastrar reordena la cadena RX. | Delegado a ClientRxChainWidget. Las seis etapas RX (EQ, AGC-G/Gate, AGC-C/Comp, DESS/DeEss, TUBE, EVO/Pudu) están completamente implementadas. El orden es independiente de la cadena TX. El tipo mime distinto `application/x-aethersdr-rx-chain-stage` evita caídas accidentales entre las dos tiras. |
| Mosaico de estado RADIO | Flanqueo del lado RX no interactivo. Se ilumina en verde cuando PC Audio (el flujo SSB estándar) está habilitado. | Solo visible en el modo RX. |
| Mosaico de estado/omisión ADSP | Mosaico interactivo del lado RX que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (p. ej., 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está activo. Un solo clic omite todo el clúster NR con una instantánea en memoria; otro solo clic restaura el estado NR anterior. El doble clic abre el cuadro de diálogo AetherDSP Settings. | Solo visible en el modo RX. Adopta el mismo estilo de anillo azul con punto LED verde que los mosaicos de etapa implementados. La restauración de la instantánea vuelve a NR2 si no había módulos activos en el momento de la omisión. Usa NvAfx en lugar de BNR para la restauración de la instantánea en v26.7.4. |
| Mosaico de estado SPEAK | Flanqueo del lado RX no interactivo. Se ilumina en verde cuando la salida de audio de AetherSDR no está silenciada. | Solo visible en el modo RX. |

## Consejos

- El botón **Play (▶)** permanece habilitado mientras la reproducción está en curso para que pueda cancelarla en cualquier momento volviendo a hacer clic en él.
- Si desea hacer una nueva grabación antes de escuchar, haga clic en **Record (⏺)** para capturar hasta 30 segundos de audio TX posterior a PUDU. La reproducción comienza automáticamente cuando la grabación se detiene.
- El botón **Play (▶)** está oculto siempre que la pestaña **RX** está activa. Vuelva a **TX** para acceder a él.
- Al hacer doble clic en cualquier mosaico de etapa de la cadena TX se abre Aetherial Audio Channel Strip, que brinda acceso a todos los controles DSP de TX en una sola ventana. Para editar una etapa específica de forma aislada, abra el channel strip y use sus propios controles.
- El botón BYPASS usa instantáneas propiedad del motor tanto para TX como para RX. Cambiar entre las pestañas TX y RX actualiza automáticamente el estado marcado de BYPASS para que coincida con el lado activo. El estado de BYPASS es global por motor de audio y persiste al cambiar de perfil de Channel Strip: presionar BYPASS en un perfil lo mantendrá presionado al cambiar a otro perfil.

## Solución de problemas

- **Play (▶) aparece atenuado** — Aún no existe una grabación, o la grabación está en curso. Primero haga una grabación usando **Record (⏺)** , o espere a que termine la grabación actual.
- **Play (▶) no está visible** — La pestaña **RX** está activa. Haga clic en **TX** para cambiar a la vista de la cadena TX.
- **El estado del botón BYPASS no coincide con lo que configuré en el channel strip** — El botón BYPASS en el applet de la cadena y el control BYPASS en Aetherial Audio Channel Strip comparten el mismo estado de omisión TX propiedad del motor. Cambiar al lado RX y volver restaurará el estado visual correcto. Para la omisión RX, el estado visual ahora también está sincronizado con el motor.
- **El botón BYPASS muestra un estado incorrecto después de cambiar de pestaña** — En v26.6.1, el botón BYPASS lee correctamente el estado de omisión del motor para el lado activo. Cambiar de pestaña ahora activa la consulta correcta al motor: `isTxBypassed()` para el modo TX y `isRxBypassed()` para el modo RX.
- **El botón BYPASS parece reiniciarse al cambiar de perfil de Channel Strip** — Este es un comportamiento esperado. El estado de BYPASS es global por motor de audio, no se almacena por perfil. El botón permanece presionado independientemente del perfil que esté cargado.
- **El mosaico ADSP restaura DNR/NR2 en lugar de BNR** — En v26.7.4, la restauración de la instantánea al desactivar la omisión del mosaico ADSP usa NvAfx (anteriormente BNR). Si el estado anterior del reductor de ruido incluía BNR, se restaurará como NvAfx.

## Relacionado

- [Record up to 30 seconds of post-PUDU TX audio](record-up-to-30-seconds-of-post-pudu-tx-audio.md)
- [Switch between editing the TX and RX chains](switch-between-editing-the-tx-and-rx-chains.md)
- [Aetherial Audio Chain overview](overview.md)
