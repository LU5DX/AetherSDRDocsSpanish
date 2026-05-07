# Configurar la velocidad de manipulación CW en PPM

Use el control deslizante de Velocidad en el applet Phone/CW para ajustar la velocidad a la que la radio manipula CW, medida en palabras por minuto. Esto controla el manipulador interno de la radio y afecta las transmisiones con manípulo, manipulador recto y CWX.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El slice activo debe estar en modo CW. El applet Phone/CW muestra el subpanel de CW solo cuando el slice activo está en modo CW; de lo contrario, se muestra el panel Phone.
- Abra el applet Phone/CW haciendo clic en el botón P/CW en la barra lateral derecha, o confirme que ya está visible.

## Pasos

1. Verifique que el slice activo esté en modo CW. El applet cambia automáticamente al subpanel CW cuando el modo CW está activo.
2. Localice el control deslizante **Speed (CW)** en el subpanel CW.
3. Arrastre el control deslizante **Speed (CW)** hacia la izquierda para disminuir las PPM o hacia la derecha para aumentarlas. El rango válido es de 5 a 100 PPM.
4. Alternativamente, haga clic en el valor numérico adyacente al control deslizante y escriba un valor directamente (5–100) usando su teclado. El control deslizante se actualiza para coincidir con el valor escrito.

## Función de cada control

| Control      | Descripción                                                                                                                | Predeterminado |
|--------------|----------------------------------------------------------------------------------------------------------------------------|----------------|
| Speed (CW)   | Establece la velocidad de manipulación CW; llama a TransmitModel::setCwSpeed. El QLineEdit adyacente acepta valores escritos (5–100) (v0.9.8, #2429). | 20 PPM         |

## Consejos

- El control deslizante **Speed (CW)** opera la velocidad del manipulador de la radio. Los cambios surten efecto de inmediato y se aplican al manípulo, manipulador recto y cualquier transmisión de texto CWX.
- Las cuatro etiquetas de valor de CW (Delay, Speed, Sidetone Volume, Pitch) ahora son widgets QLineEdit con QIntValidator. Haga clic en cualquier valor y escriba un número directamente para la paridad con SmartSDR (v0.9.8).
- El interruptor **Sidetone** y el control deslizante **Sidetone volume** controlan tanto el monitor alimentado por DAX de la radio como el tono lateral de baja latencia del lado del cliente de forma sincronizada. Ajustar la velocidad no afecta el tono del tono lateral; el tono siempre sigue automáticamente la configuración `cw_pitch` de la radio.
- El indicador **Level** aparece inmediatamente al conectar cuando la fuente del micrófono está configurada en PC, o cuando el modo RADE está activo. En ambos casos, el indicador usa la medición del lado del cliente y no es suprimido por la configuración `met_in_rx`, incluso cuando no se está transmitiendo. Cuando el modo RADE está activo, el indicador continúa mostrando el nivel durante RX.
- El indicador **Compression** lee 0 dB durante RX. Solo muestra un valor distinto de cero mientras el interlock de la radio reporta un estado TRANSMITTING y el procesador de voz está habilitado, evitando que lecturas obsoletas de la cadena de TX aparezcan durante la recepción (v0.9.7).
- El control deslizante **Mic gain** se comporta de manera diferente cuando el modo RADE está activo: actúa como ganancia RADE del lado del cliente y almacena su valor bajo `PcMicGain` en lugar de enviar un comando de nivel de micrófono a la radio. Esto evita sobrescribir silenciosamente la configuración de hardware del micrófono. La misma configuración `PcMicGain` se comparte entre el modo de fuente PC y el modo RADE.
- El interruptor **Breakin** controla completamente si los bordes de las teclas de CW del teclado y MIDI activan TX. Con Breakin activado (QSK), los bordes de las teclas activan TX y el retardo de break-in mantiene el relé. Con Breakin desactivado, las teclas se ponen en cola y usted activa PTT manualmente. Ningún sobre de PTT automático anula este comportamiento (v0.9.7).
- El valor del control deslizante **Delay (CW)** se almacena en caché inmediatamente cuando se cambia, evitando que la emisión de la radio reubique el control deslizante (v0.9.8, #2428).
- El bus de tono lateral se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).

## Relacionados

- [Configurar el retardo de break-in CW](set-cw-break-in-delay.md)
- [Habilitar la manipulación con manípulo iámbico](enable-iambic-paddle-keying.md)
- [Cambiar el tono CW / frecuencia del tono lateral](change-cw-pitch-sidetone-frequency.md)
- [Configurar el volumen del tono lateral](set-sidetone-volume.md)
- [Activar/desactivar el tono lateral CW](toggle-cw-sidetone.md)
