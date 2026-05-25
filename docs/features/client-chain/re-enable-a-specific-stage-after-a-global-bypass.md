# Reincorporar una etapa específica tras un bypass global

Después de usar BYPASS para silenciar todas las etapas de la cadena TX o RX, puede reactivar etapas individuales de una en una sin levantar el bypass global ni restaurar todas las etapas a la vez.

## Antes de empezar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de la bandeja PUDU en la barra lateral derecha para mostrar el contenedor.
- BYPASS debe estar activo actualmente (el botón BYPASS aparecerá marcado, con borde y relleno ámbar) en el lado de la cadena que desea editar.
- Confirme que está viendo el lado correcto de la cadena: haga clic en TX o RX para cambiar si es necesario.

## Pasos

1. En la fila de encabezado de Aetherial Audio Chain, confirme que BYPASS esté marcado. Mientras BYPASS está activo, todas las etapas aparecen deshabilitadas visualmente.
2. Haga clic en TX o RX para asegurarse de que se muestre el lado de la cadena que desea editar.
3. Localice el mosaico de la etapa que desea reactivar en la tira horizontal (para TX: EQ, COMP, GATE, DESS, TUBE, PUDU, VERB; para RX: EQ, AGC-G, AGC-C, DESS, TUBE, EVO).
4. Haga un solo clic en ese mosaico de etapa. Esto desactiva el bypass solo para esa etapa, reincorporándola mientras el resto de etapas permanecen en bypass.
5. Repita el paso 4 para cualquier otra etapa que desee reactivar individualmente.

## Función de cada control

| Control | Tipo | Comportamiento |
|---------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TX | Muestra y edita la cadena DSP de TX (ClientChainWidget) — completamente interactivo: clic para bypass, doble clic para editar, arrastrar para reordenar. | Forma parte de un par exclusivo con RX; color ámbar 'VUDU' cuando está seleccionado. La última pestaña activa persiste mediante PooDooAudioActiveTab='TX' / 'RX'. |
| RX | Botón de alternancia | Cambia la vista de la cadena a la cadena DSP de RX. También completamente interactivo con clic para bypass, doble clic para editar, arrastrar para reordenar; flanqueado por los mosaicos de estado RADIO / ADSP / SPEAK. |
| BYPASS | Botón de alternancia | Cuando está marcado, captura una instantánea de las etapas actualmente habilitadas en el lado activo (TX o RX) y las deshabilita todas. Cuando está desmarcado, reactiva solo las etapas que estaban activas antes. Las etapas activadas manualmente mientras BYPASS está activo se conservan fuera de la instantánea. TX y RX mantienen instantáneas independientes: el estado visual marcado sigue el lado que se muestra actualmente. El estado de bypass es gestionado por el motor de audio para ambos modos. |
| Record (glifo de círculo) | Botón de alternancia | Captura hasta 30 s de audio TX posterior a PUDU; haga clic de nuevo para detener (la reproducción comienza automáticamente). Información sobre herramienta: 'Record up to 30 s of post-PooDoo™ TX audio (MIC must be set to PC and DAX off).' Oculto en modo RX (función exclusiva de TX). Solo se habilita cuando la entrada de micrófono está lista y la reproducción no está activa. Parpadea en rojo durante la grabación. |
| Play (glifo de triángulo) | Botón de alternancia | Reproduce el audio PUDU capturado; haga clic de nuevo para cancelar. Oculto en modo RX. Solo se habilita cuando existe una grabación y la grabación no está activa. Parpadea en verde durante la reproducción. |
| Etapa de cadena TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | Manija de arrastre | Un solo clic alterna el bypass de la etapa; doble clic abre su editor flotante sin marco; arrastrar reordena la cadena TX. El texto de ayuda debajo dice 'Click to bypass · Double click to edit · Drag to reorder'. |
| Etapa de cadena RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO) | Manija de arrastre | Un solo clic alterna el bypass de la etapa RX; doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena RX. Las seis etapas RX (EQ, AGC-G/Gate, AGC-C/Comp, DESS/DeEss, TUBE, EVO/Pudu) están completamente implementadas. El orden es independiente de la cadena TX. El tipo MIME distintivo 'application/x-aethersdr-rx-chain-stage' evita caídas accidentales entre las dos tiras. |
| Mosaico de estado RADIO | Indicador | Flanqueo no interactivo del lado RX. Se vuelve verde cuando PC Audio (el flujo SSB estándar) está habilitado. Solo visible en modo RX. |
| Mosaico de estado/bypass ADSP | Botón de alternancia | Mosaico interactivo del lado RX que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (p. ej., 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está activo. Un solo clic pone en bypass todo el grupo NR con una instantánea en memoria; otro solo clic restaura el estado NR anterior. El doble clic abre el diálogo de configuración de AetherDSP Settings. Solo visible en modo RX. |
| Mosaico de estado SPEAK | Indicador | Flanqueo no interactivo del lado RX. Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada. Solo visible en modo RX. |

## Consejos

- Reactivar manualmente una etapa mientras BYPASS está marcado coloca esa etapa fuera de la instantánea de bypass. Si luego desmarca BYPASS para hacer una restauración completa, se aplicará el estado anterior al bypass de esa etapa (no su estado actual). Active solo las etapas que desee deliberadamente activas durante el bypass.
- TX y RX mantienen instantáneas BYPASS independientes. Activar etapas específicas en el lado TX no afecta la instantánea del lado RX, y viceversa.
- En v0.9.8, el botón BYPASS refleja el estado gestionado por el motor tanto para modo TX como RX. Si alterna el bypass desde Aetherial Audio Channel Strip (TX) o desde el motor de audio mediante programación (RX), el botón BYPASS en el applet de la cadena se actualiza automáticamente para coincidir con el lado de cadena actual.
- Hacer doble clic en cualquier mosaico de etapa TX abre un editor flotante sin marco para esa etapa específica. Aetherial Audio Channel Strip es la ventana DSP universal de TX, accesible por separado.
- La pista debajo de la tira de la cadena dice "Click to bypass · Double click to edit · Drag to reorder" y se aplica a ambos lados de la cadena.
- En v26.5.3, el intervalo de discriminación de clics es configurable mediante el diálogo Interaction Settings. Esto afecta la rapidez con que un doble clic debe seguir a un solo clic para ser reconocido como doble clic en lugar de dos clics simples. Ajuste este intervalo en `Settings > Interaction` si considera que el tiempo predeterminado es demasiado corto o demasiado largo.

## Relacionado

- [Bypass every TX stage at once](bypass-every-tx-stage-at-once.md)
- [Bypass every RX stage at once](bypass-every-rx-stage-at-once.md)
- [Switch between editing the TX and RX chains](switch-between-editing-the-tx-and-rx-chains.md)
- [Open a stage's frameless floating editor from the chain](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
