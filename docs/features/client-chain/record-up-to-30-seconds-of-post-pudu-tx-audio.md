# Grabar hasta 30 segundos de audio TX posterior a PUDU

Use el grabador de monitor incorporado para capturar y reproducir inmediatamente cómo suena su audio transmitido después de pasar por toda la cadena DSP de TX, incluido PUDU. Esto le ayuda a ajustar la configuración de su cadena sin necesidad de una segunda estación que le informe.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar abierto. Si no está visible, haga clic en el botón de bandeja etiquetado **PUDU** en la barra lateral derecha.
- La entrada de su micrófono debe estar configurada en **PC** (no en una fuente de micrófono del panel frontal del radio).
- DAX debe estar desactivado. La información sobre herramientas del botón de grabación dice: "MIC must be set to PC and DAX off."
- La pestaña **TX** debe estar activa en el applet. Los controles de grabación están ocultos cuando **RX** está seleccionado.

## Pasos

1. Haga clic en el botón de la pestaña **TX** en la parte superior del applet Aetherial Audio Chain para asegurarse de que se muestre la cadena TX. El botón se vuelve ámbar cuando está seleccionado.
2. Confirme que el botón de grabación (⏺) esté habilitado. Solo está habilitado cuando la entrada del micrófono está lista y la reproducción no está en curso. Si aparece atenuado y no se puede hacer clic, verifique que la fuente de su micrófono esté configurada en PC y que DAX esté desactivado.
3. Haga clic en **⏺** para iniciar la grabación. El botón parpadea en rojo para indicar que la captura está activa. La grabación se detiene automáticamente después de 30 segundos, o puede detenerla antes.
4. Para detener la grabación antes de que hayan transcurrido 30 segundos, haga clic en **⏺** nuevamente. La reproducción comienza automáticamente una vez que la grabación se detiene.
5. Para cancelar la reproducción antes de que termine, haga clic en **▶** mientras parpadea en verde.

## Qué hace cada control

| Control                                                     | Valor predeterminado | Comportamiento                                                                                                                                                                                                                                                                                                                                                                         |
|-------------------------------------------------------------|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Botones de alternancia **TX** / **RX**                      | TX está marcado      | Par exclusivo; muestra y edita la cadena DSP correspondiente. La última pestaña activa se conserva mediante `PooDooAudioActiveTab`.                                                                                                                                                                                                                                                          |
| **BYPASS**                                                  | Sin marcar           | Toma una instantánea de las etapas actualmente habilitadas en el lado activo y las deshabilita todas. Desmarque para volver a habilitar solo las etapas que estaban activas antes. TX y RX mantienen instantáneas separadas propiedad del motor.                                                                                                                                              |
| **⏺** (grabar)                                              | Sin marcar           | Captura hasta 30 s de audio TX posterior a PUDU. Haga clic de nuevo para detener; la reproducción comienza automáticamente. Oculto en modo RX.                                                                                                                                                                                                                                       |
| **▶** (reproducir)                                           | Sin marcar           | Reproduce el audio capturado. Haga clic de nuevo para cancelar. Oculto en modo RX.                                                                                                                                                                                                                                                                                                   |
| Etapa de la cadena TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | Un clic alterna el bypass de la etapa; un doble clic abre Aetherial Audio Channel Strip; arrastrar reordena la cadena TX. | Delegado a ClientChainWidget. Texto de sugerencia: "Click to bypass · Double click to edit · Drag to reorder".                                                                                                                                                                                                                                      |
| Etapa de la cadena RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO) | Un clic alterna el bypass de la etapa RX; un doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena RX. | Delegado a ClientRxChainWidget. Las seis etapas RX están completamente implementadas. El orden es independiente de la cadena TX.                                                                                                                                                                                                                                      |
| Panel de estado **RADIO**                                   | Siempre visible en modo RX | Se pone verde cuando PC Audio (flujo SSB estándar) está habilitado. No interactivo.                                                                                                                                                                                                                                                                                           |
| Panel de estado / bypass **ADSP**                           | Sin marcar           | Refleja qué reductor de ruido del lado del cliente está activo actualmente. Un solo clic bypass de todo el clúster NR con una instantánea en memoria; haga clic de nuevo para restaurar el estado NR anterior. Un doble clic abre el cuadro de diálogo AetherDSP Settings.                                                                                                             |
| Panel de estado **SPEAK**                                   | Siempre visible en modo RX | Se pone verde cuando la salida de audio de AetherSDR está activada. No interactivo.                                                                                                                                                                                                                                                                                                  |

## Abrir el editor DSP de TX desde la cadena

Al hacer doble clic en cualquier panel de etapa de la cadena TX se abre Aetherial Audio Channel Strip, la ventana DSP de TX unificada. La tira de canal proporciona acceso a todos los editores de etapa individuales a través de sus propios controles. Este gesto de doble clic es la forma estándar de abrir la configuración de audio TX desde el applet de la cadena.

## Sincronización de BYPASS de TX y RX

El botón **BYPASS** en el applet Aetherial Audio Chain y el botón **BYPASS** en Aetherial Audio Channel Strip comparten un único estado de bypass propiedad del motor para cada lado. Al presionar cualquiera de los botones se actualizan ambos. Cuando cambia entre las pestañas **TX** y **RX**, el botón **BYPASS** refleja inmediatamente el estado actual del motor para el lado activo.

## Consejos

- El grabador captura el audio en el punto posterior a la etapa PUDU en la cadena TX. Para escuchar el efecto de una etapa específica, active o desactive el bypass de esa etapa, haga una grabación y compare la reproducción.
- No necesita transmitir a un receptor: el monitor graba el audio directamente desde la salida DSP del lado del cliente.
- Si desea comparar configuraciones, detenga la grabación actual, ajuste una etapa, grabe nuevamente y reproduzca para comparar.
- Para ajustar la configuración de una etapa TX individual, haga doble clic en cualquier panel de etapa en la cadena TX. Se abre Aetherial Audio Channel Strip; use sus controles para editar cada etapa.

## Solución de problemas

- **El botón ⏺ está atenuado y no se puede hacer clic** — La entrada del micrófono no está configurada en PC, DAX está activado o la reproducción está en curso. Desactive DAX, configure la fuente del micrófono en PC y espere a que finalice cualquier reproducción activa.
- **Los botones ⏺ y ▶ no son visibles** — La pestaña **RX** está activa. Haga clic en **TX** para cambiar a la cadena TX; ambos botones están ocultos en modo RX.
- **La reproducción no comienza después de que se detiene la grabación** — No se capturó audio. Confirme que su entrada de micrófono está entregando audio a la PC durante la ventana de grabación.
- **Al hacer doble clic en un panel de etapa TX no se abre un editor flotante** — Este es el comportamiento esperado. El doble clic abre Aetherial Audio Channel Strip en su lugar. Acceda a los editores de etapa individuales desde dentro de la tira de canal.
- **El estado del botón BYPASS no coincide con lo que configuré en la tira de canal** — Si acaba de conectar el motor de audio, recargue el applet o cambie a la pestaña activa y luego vuelva a ella para que el botón pueda releer el estado actual del motor.

## Relacionados

- [Aetherial Audio Chain overview](overview.md)
- [Play back the captured PUDU audio](play-back-the-captured-pudu-audio.md)
- [Switch between editing the TX and RX chains](switch-between-editing-the-tx-and-rx-chains.md)
- [Open a stage's frameless floating editor from the chain](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
