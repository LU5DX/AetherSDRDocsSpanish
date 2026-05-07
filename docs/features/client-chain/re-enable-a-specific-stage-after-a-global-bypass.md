# Reactivar una etapa específica después de un bypass global

Después de usar BYPASS para silenciar todas las etapas de la cadena de TX o RX, puede reactivar etapas individuales una por una sin levantar el bypass global ni restaurar todas las etapas a la vez.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de la bandeja PUDU en la barra lateral derecha para mostrar el contenedor.
- BYPASS debe estar activo en el lado de la cadena que desea editar (el botón BYPASS aparecerá marcado, con un borde y relleno de color ámbar).
- Confirme que está viendo el lado correcto de la cadena — haga clic en TX o RX para cambiar si es necesario.

## Pasos

1. En la fila de encabezado de Aetherial Audio Chain, confirme que BYPASS esté marcado. Mientras BYPASS esté activo, todas las etapas se mostrarán visualmente deshabilitadas.
2. Haga clic en TX o RX para asegurarse de que se muestre el lado de la cadena que desea editar.
3. Localice el mosaico de la etapa que desea reactivar en la tira horizontal (para TX: EQ, COMP, GATE, DESS, TUBE, PUDU, VERB; para RX: EQ, AGC-G, AGC-C, DESS, TUBE, EVO).
4. Haga un solo clic en ese mosaico de etapa. Esto desactiva el bypass solo para esa etapa, reactivándola mientras las demás permanecen en bypass.
5. Repita el paso 4 para cualquier otra etapa que desee reactivar individualmente.

## Qué hace cada control

| Control                                                        | Tipo          | Comportamiento                                                                                                                                                                                                                                                                                                                                                                                                                      |
|----------------------------------------------------------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TX                                                             | Botón de alternancia | Cambia la vista de la cadena a la cadena DSP de TX. TX y RX mantienen estados de etapa y capturas instantáneas de BYPASS independientes. Color 'PooDoo' ámbar cuando está seleccionado. La última pestaña activa persiste mediante la clave de configuración `PooDooAudioActiveTab`.                                                                                                                                                           |
| RX                                                             | Botón de alternancia | Cambia la vista de la cadena a la cadena DSP de RX. También es totalmente interactivo con bypass mediante clic, edición mediante doble clic y reordenación mediante arrastre; está delimitado por los mosaicos de estado RADIO / ADSP / SPEAK.                                                                                                                                                                                       |
| BYPASS                                                         | Botón de alternancia | Cuando está marcado, captura una instantánea de las etapas actualmente habilitadas en el lado activo (TX o RX) y las deshabilita todas. Cuando no está marcado, reactiva solo las etapas que estaban activas antes. Las etapas que se alternan manualmente mientras BYPASS está activo se conservan fuera de la instantánea. TX y RX mantienen instantáneas separadas: el estado visual marcado sigue el lado que se muestra actualmente. El estado de bypass es propiedad del motor de audio para ambos modos. |
| Grabar (glifo de círculo)                                      | Botón de alternancia | Captura hasta 30 s de audio TX posterior a PUDU; haga clic nuevamente para detener (la reproducción comienza automáticamente). Información sobre herramientas: 'Record up to 30 s of post-PooDoo™ TX audio (MIC must be set to PC and DAX off).' Oculto en modo RX (función solo de TX). Solo se habilita cuando la entrada del micrófono está lista y la reproducción no está activa. Parpadea en rojo mientras graba.                  |
| Reproducir (glifo de triángulo)                                | Botón de alternancia | Reproduce el audio PUDU capturado; haga clic nuevamente para cancelar. Oculto en modo RX. Solo se habilita si existe una grabación y la grabación no está activa. Parpadea en verde mientras se reproduce.                                                                                                                                                                                                                           |
| Etapa de cadena TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | Control de arrastre  | Un solo clic alterna el bypass de la etapa; doble clic abre su editor flotante sin marco; arrastrar reordena la cadena TX. El texto de sugerencia debajo dice 'Click to bypass · Double click to edit · Drag to reorder'.                                                                                                                                                                                                             |
| Etapa de cadena RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO)      | Control de arrastre  | Un solo clic alterna el bypass de la etapa RX; doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena RX. Las seis etapas RX (EQ, AGC-G/Gate, AGC-C/Comp, DESS/DeEss, TUBE, EVO/Pudu) están completamente implementadas. El orden es independiente de la cadena TX. El tipo MIME distintivo 'application/x-aethersdr-rx-chain-stage' evita caídas accidentales entre las dos tiras.                     |
| Mosaico de estado RADIO                                        | Indicador      | Delimitador del lado RX no interactivo. Se vuelve verde cuando PC Audio (la transmisión SSB estándar) está habilitado. Solo visible en modo RX.                                                                                                                                                                                                                                                                                     |
| Mosaico de estado/bypass ADSP                                  | Botón de alternancia | Mosaico interactivo del lado RX que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (p. ej., 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está activo. Un solo clic desvía todo el clúster NR con una instantánea en memoria; otro solo clic restaura el estado NR anterior. El doble clic abre el cuadro de diálogo AetherDSP Settings. Solo visible en modo RX. |
| Mosaico de estado SPEAK                                        | Indicador      | Delimitador del lado RX no interactivo. Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada. Solo visible en modo RX.                                                                                                                                                                                                                                                                                        |

## Consejos

- Reactivar manualmente una etapa mientras BYPASS está marcado coloca esa etapa fuera de la instantánea de bypass. Si luego desmarca BYPASS para restaurar completamente, se aplicará el estado anterior al bypass de esa etapa (no su estado actual). Reactive solo las etapas que desea que estén activas deliberadamente durante el bypass.
- TX y RX mantienen instantáneas de BYPASS separadas. Habilitar etapas específicas en el lado TX no afecta la instantánea del lado RX, y viceversa.
- En v0.9.8, el botón BYPASS refleja el estado controlado por el motor tanto para el modo TX como para el RX. Si alterna el bypass desde Aetherial Audio Channel Strip (TX) o desde el motor de audio mediante programación (RX), el botón BYPASS en el applet de la cadena se actualiza automáticamente para coincidir con el lado de la cadena actual.
- Hacer doble clic en cualquier mosaico de etapa TX abre un editor flotante sin marco para esa etapa específica. Aetherial Audio Channel Strip es la ventana DSP de TX universal, a la que se puede acceder por separado.
- La sugerencia debajo de la tira de la cadena dice "Click to bypass · Double click to edit · Drag to reorder" y se aplica a ambos lados de la cadena.

## Relacionados

- [Bypass every TX stage at once](bypass-every-tx-stage-at-once.md)
- [Bypass every RX stage at once](bypass-every-rx-stage-at-once.md)
- [Switch between editing the TX and RX chains](switch-between-editing-the-tx-and-rx-chains.md)
- [Open a stage's frameless floating editor from the chain](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
