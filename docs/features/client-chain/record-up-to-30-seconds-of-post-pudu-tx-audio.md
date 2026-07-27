# Cadena de Audio Aetherial

El applet de Cadena de Audio Aetherial muestra el flujo de señal DSP del lado del cliente como una tira horizontal de etapas, con cadenas TX y RX independientes. La cadena TX consta de EQ Paramétrico, Compresor (con Drive de pre-compresión integrado + reducción PAPR con rotador de fase), Puerta, De-esser (de banda dividida, con pendiente seleccionable de 12–48 dB/oct), Tubo (con conmutación de reducción de ruido RN2 en TX), excitador PUDU, Reverb. La cadena RX consta de EQ, AGC-G (puerta), AGC-C (compresor), DESS (de-esser), TUBE, EVO (pudu) — las seis etapas RX están completamente implementadas — flanqueadas por los mosaicos de estado RADIO / ADSP / SPEAK. El mosaico ADSP es un conmutador cliqueable que omite todo el clúster NR del lado del cliente (NR2 / NR4 / MNR / DFNR / RN2 / NVAFX); una instantánea en memoria restaura el estado NR anterior al desactivar la omisión.

## Grabe hasta 30 segundos de audio TX posterior a PUDU

Utilice el grabador de monitorización integrado para capturar y reproducir inmediatamente cómo suena su audio transmitido después de pasar por toda la cadena DSP de TX, incluyendo PUDU. Esto le ayuda a ajustar la configuración de su cadena sin necesidad de que otra estación le informe.

### Antes de empezar

- El applet de Cadena de Audio Aetherial debe estar abierto. Si no está visible, haga clic en el botón de bandeja etiquetado **PUDU** en la barra lateral derecha.
- Su entrada de micrófono debe estar configurada en **PC** (no en una fuente de micrófono del panel frontal del equipo).
- DAX debe estar desactivado. La información sobre herramientas del botón de grabación dice: "MIC must be set to PC and DAX off".
- La pestaña **TX** debe estar activa en el applet. Los controles de grabación están ocultos cuando está seleccionada **RX**.

### Pasos

1. Haga clic en el botón de la pestaña **TX** en la parte superior del applet de Cadena de Audio Aetherial para asegurarse de que se muestra la cadena TX. El botón se vuelve ámbar cuando está seleccionado.
2. Confirme que el botón de grabación (⏺) está habilitado. Solo se habilita cuando la entrada del micrófono está lista y la reproducción no está activa. Si aparece atenuado y no se puede hacer clic, verifique que su fuente de micrófono esté configurada en PC y que DAX esté desactivado.
3. Haga clic en **⏺** para iniciar la grabación. El botón parpadea en rojo para indicar que la captura está activa. La grabación se detiene automáticamente después de 30 segundos, o puede detenerla antes.
4. Para detener la grabación antes de que hayan transcurrido 30 segundos, haga clic en **⏺** nuevamente. La reproducción comienza automáticamente una vez que se detiene la grabación.
5. Para cancelar la reproducción antes de que termine, haga clic en **▶** mientras parpadea en verde.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| Botones de alternancia **TX** / **RX** | TX está marcado | Par exclusivo; muestra y edita la cadena DSP correspondiente. La última pestaña activa persiste mediante `PooDooAudioActiveTab='TX'` / `'RX'`. |
| **BYPASS** | Sin marcar | Toma una instantánea de las etapas actualmente habilitadas en el lado activo (TX o RX) y las deshabilita todas (incluyendo RN2). Desmarque para volver a habilitar solo las etapas que estaban activas antes. TX y RX mantienen instantáneas separadas. El estado visual marcado sigue el lado que se muestra actualmente. El alcance es global (por motor de audio), no por perfil — el botón permanece presionado al cambiar entre perfiles de Canal. |
| **⏺** (grabar) | Sin marcar | Captura hasta 30 s de audio TX posterior a PUDU. Haga clic nuevamente para detener; la reproducción comienza automáticamente. Oculto en modo RX. Solo se habilita cuando la entrada del micrófono está lista y la reproducción no está activa. Parpadea en rojo mientras graba. |
| **▶** (reproducir) | Sin marcar | Reproduce el audio PUDU capturado. Haga clic nuevamente para cancelar. Oculto en modo RX. Solo se habilita una vez que existe una grabación y la grabación no está activa. Parpadea en verde mientras reproduce. |
| Etapa de la cadena TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | N/A | Un solo clic alterna la omisión de la etapa; doble clic abre su editor flotante sin marco (o el Canal en TX); arrastre reordena la cadena TX. Texto de ayuda: "Click to bypass · Double click to edit · Drag to reorder". |
| Etapa de la cadena RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO) | N/A | Un solo clic alterna la omisión de la etapa RX; doble clic abre su editor flotante sin marco en modo RX; arrastre reordena la cadena RX. Las seis etapas RX están completamente implementadas. El orden es independiente de la cadena TX. El tipo MIME distinto `application/x-aethersdr-rx-chain-stage` evita colocaciones accidentales entre las dos tiras. |
| Mosaico de estado **RADIO** | Siempre visible en modo RX | Se vuelve verde cuando el Audio de PC (flujo SSB estándar) está habilitado. No interactivo. |
| Mosaico de estado/omisión **ADSP** | Sin marcar | Mosaico interactivo del lado RX que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (ej. 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está activo. Un solo clic omite todo el clúster NR con una instantánea en memoria; otro clic restaura el estado NR anterior. El doble clic abre el diálogo de Configuración de AetherDSP. La omisión ahora maneja correctamente NVAFX en lugar del módulo BNR heredado. |
| Mosaico de estado **SPEAK** | Siempre visible en modo RX | Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada. No interactivo. |

## Configuración de interacción

El intervalo de discriminación de clic utilizado para distinguir un solo clic de un doble clic se configura a través del diálogo **Configuración de Interacción**. De forma predeterminada, AetherSDR utiliza el intervalo de doble clic del sistema, pero puede ajustarlo según su preferencia. Esta configuración afecta tanto a los widgets de la cadena TX como a los de la cadena RX.

Para ajustar el intervalo:

1. Abra **File > Settings**.
2. Seleccione **Interaction** en la barra lateral.
3. Ajuste el control deslizante **Click discrimination interval**.
4. Haga clic en **Apply**.

## Abrir el editor DSP de TX desde la cadena

Al hacer doble clic en cualquier mosaico de etapa de la cadena TX, se abre el Canal de Audio Aetherial, la ventana unificada de DSP de TX. El canal proporciona acceso a todos los editores de etapa individuales a través de sus propios controles. Este gesto de doble clic es la forma estándar de abrir la configuración de audio de TX desde el applet de la cadena.

## Sincronización de BYPASS de TX y RX

El botón **BYPASS** en el applet de Cadena de Audio Aetherial y el botón **BYPASS** en el Canal de Audio Aetherial comparten un único estado de omisión propiedad del motor para cada lado. Al presionar cualquiera de los botones, se actualizan ambos. Cuando cambia entre las pestañas **TX** y **RX**, el botón **BYPASS** refleja inmediatamente el estado actual del motor para el lado activo.

## Consejos

- El grabador captura el audio en el punto posterior a la etapa PUDU en la cadena TX. Para escuchar el efecto de una etapa específica, omita o desactive la omisión de esa etapa, haga una grabación y compare la reproducción.
- No necesita transmitir a un receptor; el monitor graba el audio directamente desde la salida DSP del lado del cliente.
- Si desea comparar configuraciones, detenga la grabación actual, ajuste una etapa, grabe nuevamente y reproduzca para comparar.
- Para ajustar la configuración de etapas TX individuales, haga doble clic en cualquier mosaico de etapa de la cadena TX. Se abre el Canal de Audio Aetherial; utilice sus controles para editar cada etapa.

## Solución de problemas

- **El botón ⏺ está atenuado y no se puede hacer clic** — La entrada del micrófono no está configurada en PC, DAX está activado o la reproducción está en curso. Desactive DAX, configure la fuente del micrófono en PC y espere a que finalice cualquier reproducción activa.
- **Los botones ⏺ y ▶ no son visibles** — La pestaña **RX** está activa. Haga clic en **TX** para cambiar a la cadena TX; ambos botones están ocultos en modo RX.
- **La reproducción no comienza después de que se detiene la grabación** — No se capturó audio. Confirme que su entrada de micrófono está enviando audio al PC durante la ventana de grabación.
- **Al hacer doble clic en un mosaico de etapa TX, no se abre un editor flotante** — Este es un comportamiento esperado. El doble clic abre el Canal de Audio Aetherial. Acceda a los editores de etapa individuales desde dentro del canal.
- **El estado del botón BYPASS no coincide con lo que configuré en el canal** — Si acaba de conectar el motor de audio, recargue el applet o cambie de la pestaña activa a otra y vuelva para que el botón pueda releer el estado actual del motor.
- **Las acciones de doble clic se sienten demasiado rápidas o demasiado lentas** — Ajuste el intervalo de discriminación de clic en **File > Settings > Interaction**.

## Relacionados

- [Aetherial Audio Chain overview](overview.md)
- [Play back the captured PUDU audio](play-back-the-captured-pudu-audio.md)
- [Switch between editing the TX and RX chains](switch-between-editing-the-tx-and-rx-chains.md)
- [Open a stage's frameless floating editor from the chain](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
