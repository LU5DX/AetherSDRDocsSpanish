# Establecer la velocidad de tecleo CW en WPM

Use el control deslizante de Velocidad en el applet Phone/CW para establecer la velocidad a la que la radio teclea CW, medida en palabras por minuto. Esto controla el keyer interno de la radio y afecta las transmisiones con paleta, manipulador recto y CWX.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- La slice activa debe estar en modo CW. El applet Phone/CW muestra el subpanel de CW solo cuando la slice activa está en modo CW; de lo contrario, se muestra el panel de Phone.
- Abra el applet Phone/CW haciendo clic en el botón P/CW en la barra lateral derecha, o confirme que ya está visible.

## Pasos

1. Verifique que la slice activa esté en modo CW. El applet cambia automáticamente al subpanel de CW cuando el modo CW está activo.
2. Localice el control deslizante **Speed (CW)** en el subpanel de CW.
3. Arrastre el control deslizante **Speed (CW)** hacia la izquierda para disminuir las WPM o hacia la derecha para aumentarlas. El rango válido es de 5 a 100 WPM.
4. Alternativamente, haga clic en el valor numérico junto al control deslizante y escriba un valor directamente (5 a 100 WPM) usando su teclado. El control deslizante se actualiza para coincidir con el valor escrito.

## Qué hace cada control

| Control           | Descripción                                                                                                                                                       | Valor predeterminado                                                                                                      |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| Speed (CW)        | Establece la velocidad de tecleo CW; llama a TransmitModel::setCwSpeed. El QLineEdit adyacente acepta valores escritos (5 a 100 WPM) (v0.9.8, #2429).              | 20 WPM                                                                                                                   |
| ALC (Panel Phone) | Muestra la lectura del control automático de nivel desde MeterModel::swAlcChanged (pico SSB post-ALC por software en dBFS). Se llena de derecha a izquierda: vacío en -20 dBFS, lleno en 0 dBFS. | Reconfigurado desde HWALC (voltaje RCA) al medidor SW ALC en v26.5.1 (#2552). Reflejado por un indicador idéntico en el subpanel de CW. |
| ALC (Panel CW)    | Refleja el indicador ALC del panel Phone; ambos leen de MeterModel::swAlcChanged para lecturas consistentes en voz y CW.                                          | Agregado en v26.5.1 (#2552) como parte de la división del medidor SW ALC. Usa el modo HGauge::setFillFromRight.           |

## Consejos

- El control deslizante Speed (CW) opera la velocidad del keyer de la radio. Los cambios surten efecto de inmediato y se aplican a la paleta, el manipulador recto y cualquier transmisión de texto CWX.
- Las cuatro etiquetas de valor de CW (Delay, Speed, Sidetone Volume, Pitch) ahora son widgets QLineEdit con QIntValidator. Haga clic en cualquier valor y escriba un número directamente para la paridad con SmartSDR (v0.9.8).
- La alternancia **Sidetone** y el control deslizante **Sidetone volume** controlan tanto el monitor alimentado por DAX de la radio como el sintonizador local de baja latencia del lado del cliente al unísono. Ajustar la velocidad no afecta el tono del sintonizador; el tono siempre sigue automáticamente el ajuste `cw_pitch` de la radio.
- El indicador **Level** aparece inmediatamente al conectar cuando la fuente de micrófono está configurada en PC, o cuando el modo RADE está activo. En ambos casos, el indicador usa medición del lado del cliente y no es suprimido por el ajuste `met_in_rx`, incluso cuando no se está transmitiendo. Cuando el modo RADE está activo, el indicador continúa mostrando el nivel durante RX.
- El indicador **Compression** lee 0 dB durante RX. Solo muestra un valor distinto de cero mientras el interbloqueo de la radio reporta un estado TRANSMITTING y el procesador de voz está habilitado, evitando que lecturas obsoletas de la cadena de TX aparezcan durante la recepción (v0.9.7).
- El control deslizante **Mic gain** se comporta de manera diferente cuando el modo RADE está activo: actúa como ganancia RADE del lado del cliente y almacena su valor bajo `PcMicGain` en lugar de enviar un comando de nivel de micrófono a la radio. Esto evita sobrescribir silenciosamente el ajuste de micrófono del hardware. El mismo ajuste `PcMicGain` se comparte entre el modo de fuente PC y el modo RADE.
- La alternancia **Breakin** controla completamente si los bordes de las teclas del teclado CW y MIDI activan TX. Con Breakin activado (QSK), los bordes de las teclas activan TX y el retardo de break-in mantiene el relé. Con Breakin desactivado, las teclas se ponen en cola y usted activa PTT manualmente. Ningún sobre automático de PTT anula este comportamiento (v0.9.7).
- El valor del control deslizante **Delay (CW)** se almacena en caché inmediatamente cuando se cambia, evitando que la emisión de la radio devuelva el control deslizante a su posición anterior (v0.9.8, #2428).
- El bus de sintonizador se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).
- El indicador ALC aparece tanto en el subpanel de Phone como en el de CW. Ambos indicadores leen de la misma fuente MeterModel::swAlcChanged, por lo que los operadores de SSB que observan la ganancia del micrófono ven el mismo indicador que los operadores de CW usan para verificar la forma limpia del sobre de tecleo (v26.5.1, #2552). El medidor HWALC anterior (ruta de voltaje RCA) ha sido eliminado.

## Relacionado

- [Establecer el retardo de break-in CW](set-cw-break-in-delay.md)
- [Habilitar el tecleo con paleta iámbica](enable-iambic-paddle-keying.md)
- [Cambiar el tono CW / frecuencia del sintonizador](change-cw-pitch-sidetone-frequency.md)
- [Establecer el volumen del sintonizador](set-sidetone-volume.md)
- [Alternar el sintonizador CW](toggle-cw-sidetone.md)
