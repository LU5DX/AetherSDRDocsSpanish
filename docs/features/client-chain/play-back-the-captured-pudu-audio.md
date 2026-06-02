# Reproducir el audio PUDU capturado

Esta página explica cómo reproducir el audio que ya ha grabado con el monitor TX post-PUDU. Úsela para escuchar exactamente cómo suena su señal transmitida después de que la cadena DSP de TX completa la haya procesado.

## Antes de comenzar

- Debe tener una grabación existente. El botón **Play (▶)** solo se habilita cuando existe una grabación.
- La grabación no debe estar activa en ese momento. El botón **Play (▶)** se deshabilita mientras el botón **Record (⏺)** está presionado.
- El contenedor Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado `PUDU` en la barra lateral derecha para mostrarlo.
- La cadena TX debe ser la vista activa. El botón **Play (▶)** está oculto en modo RX.

## Pasos

1. En la fila de encabezado de Aetherial Audio Chain, confirme que el botón **TX** esté seleccionado. Si no es así, haga clic en **TX**.
2. Haga clic en el botón **Play (▶)**.
   - El botón parpadea en verde mientras la reproducción está en curso.
3. Para detener la reproducción antes de que termine, vuelva a hacer clic en el botón **Play (▶)**.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---------|---------------|-------|
| **TX** | Muestra y edita la cadena DSP de TX (ClientChainWidget) — completamente interactiva: clic para desviar, doble clic para editar, arrastrar para reordenar. | Forma parte de un par exclusivo con RX; color ámbar 'VUDU' cuando está seleccionado. La última pestaña activa persiste mediante `PooDooAudioActiveTab='TX'` / `'RX'`. |
| **RX** | Muestra y edita la cadena DSP de RX (ClientRxChainWidget) — también completamente interactiva con clic para desviar, doble clic para editar, arrastrar para reordenar; flanqueada por los mosaicos de estado RADIO / DSP / SPEAK. | Cada lado mantiene el estado de etapa independiente, el orden de la cadena y la instantánea BYPASS. |
| **Play (▶)** | Inicia la reproducción del audio PUDU capturado; vuelva a hacer clic para cancelar. | Oculto en modo RX. Solo se habilita cuando existe una grabación y la grabación no está activa. Parpadea en verde mientras se reproduce. |
| **Record (⏺)** | Deshabilitado durante la reproducción. | Se rehabilita automáticamente cuando termina la reproducción. |
| Etapa de la cadena TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | Un solo clic alterna el desvío de la etapa; doble clic abre el Aetherial Audio Channel Strip (la ventana unificada de DSP de TX); arrastrar reordena la cadena TX. | Ahora, al hacer doble clic en cualquier mosaico de etapa TX se abre el channel strip en lugar de un editor flotante por etapa. Los editores por etapa permanecen accesibles desde el propio channel strip. |
| **BYPASS** | Marcado: captura una instantánea de las etapas habilitadas actualmente en el lado activo (incluyendo RN2) y las deshabilita todas. Desmarcado: vuelve a habilitar las etapas que estaban antes. | El alcance es global (por motor de audio), no por perfil. El botón permanece presionado al cambiar de perfil en el Channel Strip. Cuando el lado TX está activo, el estado del botón BYPASS se sincroniza con el desvío maestro TX del motor. Cuando el lado RX está activo, el estado del botón BYPASS se sincroniza con el desvío RX del motor. Alternar BYPASS en cualquier lado actualiza la instantánea propiedad del motor para ese lado. Al cambiar de pestaña, el estado visual de BYPASS se actualiza automáticamente. |
| Etapa de la cadena RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO) | Un solo clic alterna el desvío de la etapa RX; doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena RX. | Delegado a ClientRxChainWidget. Las seis etapas RX (EQ, AGC-G/Gate, AGC-C/Comp, DESS/DeEss, TUBE, EVO/Pudu) están completamente implementadas. El orden es independiente de la cadena TX. El tipo MIME distinto `application/x-aethersdr-rx-chain-stage` evita caídas accidentales entre las dos tiras. |
| Mosaico de estado RADIO | Flanqueo RX no interactivo. Se ilumina en verde cuando PC Audio (el flujo SSB estándar) está habilitado. | Solo visible en modo RX. |
| Mosaico de estado/desvío ADSP | Mosaico RX interactivo que refleja el reductor de ruido del lado del cliente actualmente activo. La etiqueta cambia al nombre corto del módulo activo (p. ej., 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está activo. Un solo clic desvía todo el clúster NR con una instantánea en memoria; otro solo clic restaura el estado NR anterior. El doble clic abre el cuadro de diálogo AetherDSP Settings. | Solo visible en modo RX. Adopta el mismo estilo de anillo azul con punto LED verde que los mosaicos de etapa implementados. La restauración de la instantánea vuelve a NR2 si no había módulos activos en el momento del desvío. |
| Mosaico de estado SPEAK | Flanqueo RX no interactivo. Se ilumina en verde cuando la salida de audio de AetherSDR no está silenciada. | Solo visible en modo RX. |

## Consejos

- El botón **Play (▶)** permanece habilitado mientras la reproducción está en curso para que pueda cancelarla en cualquier momento volviendo a hacer clic en él.
- Si desea realizar una nueva grabación antes de escuchar, haga clic en **Record (⏺)** para capturar hasta 30 segundos de audio TX post-PUDU. La reproducción comienza automáticamente cuando la grabación se detiene.
- El botón **Play (▶)** está oculto siempre que la pestaña **RX** esté activa. Vuelva a **TX** para acceder a él.
- Al hacer doble clic en cualquier mosaico de la cadena TX se abre el Aetherial Audio Channel Strip, que da acceso a todos los controles DSP de TX en una sola ventana. Para editar una etapa específica de forma aislada, abra el channel strip y use sus propios controles.
- El botón **BYPASS** utiliza instantáneas propiedad del motor tanto para TX como para RX. Al cambiar entre las pestañas TX y RX, el estado marcado de BYPASS se actualiza automáticamente para coincidir con el lado activo. El estado de BYPASS es global por motor de audio y persiste al cambiar de perfil en el Channel Strip: presionar BYPASS en un perfil lo mantendrá presionado al cambiar a otro perfil.

## Solución de problemas

- **Play (▶) aparece atenuado** — Aún no existe una grabación, o la grabación está en curso. Primero haga una grabación usando **Record (⏺)**, o espere a que termine la grabación actual.
- **Play (▶) no está visible** — La pestaña **RX** está activa. Haga clic en **TX** para cambiar a la vista de la cadena TX.
- **El estado del botón BYPASS no coincide con lo que configuré en el channel strip** — El botón BYPASS en el applet de la cadena y el control BYPASS en el Aetherial Audio Channel Strip comparten el mismo estado de desvío TX propiedad del motor. Cambiar al lado RX y volver restaurará el estado visual correcto. Para el desvío RX, el estado visual ahora también está sincronizado con el motor.
- **El botón BYPASS muestra un estado incorrecto después de cambiar de pestaña** — En la v26.6.1, el botón BYPASS lee correctamente el estado de desvío del motor para el lado activo. Cambiar de pestaña ahora activa la consulta correcta al motor: `isTxBypassed()` para modo TX e `isRxBypassed()` para modo RX.
- **El botón BYPASS parece reiniciarse al cambiar los perfiles del Channel Strip** — Este comportamiento es esperado. El estado de BYPASS es global por motor de audio, no se almacena por perfil. El botón permanece presionado independientemente del perfil que esté cargado.

## Relacionados

- [Grabar hasta 30 segundos de audio TX post-PUDU](record-up-to-30-seconds-of-post-pudu-tx-audio.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Resumen de Aetherial Audio Chain](overview.md)
