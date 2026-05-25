# Grabar hasta 30 segundos de audio de TX posterior a PUDU

Utilice el grabador de monitor integrado para capturar y reproducir inmediatamente cómo suena su audio transmitido después de pasar por toda la cadena DSP de TX, incluyendo PUDU. Esto le ayuda a ajustar la configuración de su cadena sin necesidad de una segunda estación que le informe.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar abierto. Si no está visible, haga clic en el botón de bandeja etiquetado **PUDU** en la barra lateral derecha.
- Su entrada de micrófono debe estar configurada en **PC** (no una fuente de micrófono del panel frontal de la radio).
- DAX debe estar desactivado. La información sobre herramientas del botón de grabación dice: "MIC must be set to PC and DAX off."
- La pestaña **TX** debe estar activa en el applet. Los controles de grabación están ocultos cuando está seleccionada **RX**.

## Pasos

1. Haga clic en el botón de la pestaña **TX** en la parte superior del applet Aetherial Audio Chain para asegurarse de que se muestra la cadena de TX. El botón se vuelve ámbar cuando está seleccionado.
2. Confirme que el botón de grabación (⏺) esté habilitado. Solo está habilitado cuando la entrada de micrófono está lista y la reproducción no se está ejecutando actualmente. Si aparece atenuado y no se puede hacer clic, verifique que su fuente de micrófono esté configurada en PC y que DAX esté desactivado.
3. Haga clic en **⏺** para iniciar la grabación. El botón parpadea en rojo para indicar que la captura está activa. La grabación se detiene automáticamente después de 30 segundos, o puede detenerla antes.
4. Para detener la grabación antes de que hayan transcurrido 30 segundos, haga clic en **⏺** nuevamente. La reproducción comienza automáticamente una vez que se detiene la grabación.
5. Para cancelar la reproducción antes de que termine, haga clic en **▶** mientras parpadea en verde.

## Función de cada control

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| Botones de alternancia **TX** / **RX** | TX está marcado | Par exclusivo; muestra y edita la cadena DSP correspondiente. La última pestaña activa persiste mediante `PooDooAudioActiveTab='TX'` / `'RX'`. |
| **BYPASS** | Sin marcar | Toma una instantánea de las etapas actualmente habilitadas en el lado activo y las deshabilita todas. Desmarque para volver a habilitar solo las etapas que estaban activas antes. TX y RX mantienen instantáneas separadas. |
| **⏺** (grabar) | Sin marcar | Captura hasta 30 s de audio de TX posterior a PUDU. Haga clic nuevamente para detener; la reproducción comienza automáticamente. Oculto en modo RX. Solo se habilita cuando la entrada de micrófono está lista y la reproducción no se está ejecutando. Parpadea en rojo mientras graba. |
| **▶** (reproducir) | Sin marcar | Reproduce el audio de PUDU capturado. Haga clic nuevamente para cancelar. Oculto en modo RX. Solo se habilita una vez que existe una grabación y la grabación no está activa. Parpadea en verde mientras reproduce. |
| Etapa de la cadena de TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | N/D | Un clic alterna el bypass de la etapa; doble clic abre su editor flotante sin marco (o el Channel Strip en TX); arrastrar reordena la cadena de TX. Texto de sugerencia: "Click to bypass · Double click to edit · Drag to reorder". |
| Etapa de la cadena de RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO) | N/D | Un clic alterna el bypass de la etapa de RX; doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena de RX. Las seis etapas de RX están completamente implementadas. El orden es independiente de la cadena de TX. |
| Mosaico de estado **RADIO** | Siempre visible en modo RX | Se vuelve verde cuando PC Audio (flujo SSB estándar) está habilitado. No interactivo. |
| Mosaico de estado / bypass de **ADSP** | Sin marcar | Mosaico interactivo del lado de RX que refleja el reductor de ruido del lado del cliente actualmente activo. La etiqueta cambia al nombre corto del módulo activo (p. ej., 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está activo. Un clic bypassa todo el grupo NR con una instantánea en memoria; otro clic restaura el estado NR anterior. Doble clic abre el diálogo AetherDSP Settings. |
| Mosaico de estado **SPEAK** | Siempre visible en modo RX | Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada. No interactivo. |

## Configuración de interacción

El intervalo de discriminación de clic utilizado para distinguir un solo clic de un doble clic se puede configurar a través del diálogo **Interaction Settings**. De forma predeterminada, AetherSDR utiliza el intervalo de doble clic del sistema, pero puede ajustarlo según su preferencia. Esta configuración afecta tanto a los widgets de la cadena de TX como a los de RX.

Para ajustar el intervalo:

1. Abra **File > Settings**.
2. Seleccione **Interaction** en la barra lateral.
3. Ajuste el deslizador **Click discrimination interval**.
4. Haga clic en **Apply**.

## Abrir el editor DSP de TX desde la cadena

Al hacer doble clic en cualquier mosaico de etapa de la cadena de TX se abre el Aetherial Audio Channel Strip, la ventana unificada de DSP de TX. El Channel Strip proporciona acceso a todos los editores de etapas individuales a través de sus propios controles. Este gesto de doble clic es la forma estándar de abrir la configuración de audio de TX desde el applet de la cadena.

## Sincronización de BYPASS de TX y RX

El botón **BYPASS** en el applet Aetherial Audio Chain y el botón **BYPASS** en el Aetherial Audio Channel Strip comparten un estado de bypass de propiedad del motor para cada lado. Presionar cualquiera de los botones actualiza ambos. Cuando cambia entre las pestañas **TX** y **RX**, el botón **BYPASS** refleja inmediatamente el estado actual del motor para el lado activo.

## Consejos

- El grabador captura el audio en el punto posterior a la etapa PUDU en la cadena de TX. Para escuchar el efecto de una etapa específica, active o desactive el bypass de esa etapa, haga una grabación y compare la reproducción.
- No necesita transmitir a un receptor: el monitor graba el audio directamente desde la salida DSP del lado del cliente.
- Si desea comparar configuraciones, detenga la grabación actual, ajuste una etapa, grabe nuevamente y reproduzca para comparar.
- Para ajustar la configuración de etapas individuales de TX, haga doble clic en cualquier mosaico de etapa en la cadena de TX. Se abre el Aetherial Audio Channel Strip; use sus controles para editar cada etapa.

## Solución de problemas

- **El botón ⏺ está atenuado y no se puede hacer clic** — La entrada de micrófono no está configurada en PC, DAX está activado o la reproducción se está ejecutando actualmente. Desactive DAX, configure la fuente del micrófono en PC y espere a que finalice cualquier reproducción activa.
- **Los botones ⏺ y ▶ no son visibles** — La pestaña **RX** está activa. Haga clic en **TX** para cambiar a la cadena de TX; ambos botones están ocultos en modo RX.
- **La reproducción no comienza después de que se detiene la grabación** — No se capturó audio. Confirme que su entrada de micrófono esté entregando audio a la PC durante la ventana de grabación.
- **Al hacer doble clic en un mosaico de etapa de TX no se abre un editor flotante** — Este es un comportamiento esperado. El doble clic abre el Aetherial Audio Channel Strip. Acceda a los editores de etapas individuales desde el Channel Strip.
- **El estado del botón BYPASS no coincide con lo que configuré en el Channel Strip** — Si acaba de conectar el motor de audio, recargue el applet o cambie a otra pestaña y luego regrese a la pestaña activa para que el botón pueda volver a leer el estado actual del motor.
- **Las acciones de doble clic se sienten demasiado rápidas o demasiado lentas** — Ajuste el intervalo de discriminación de clic en **File > Settings > Interaction**.

## Relacionado

- [Aetherial Audio Chain overview](overview.md)
- [Play back the captured PUDU audio](play-back-the-captured-pudu-audio.md)
- [Switch between editing the TX and RX chains](switch-between-editing-the-tx-and-rx-chains.md)
- [Open a stage's frameless floating editor from the chain](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
