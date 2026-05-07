# Configurar el retardo de break-in en CW

El retardo de break-in en CW controla cuánto tiempo espera el radio después de la última pulsación de tecla antes de volver a recepción. Ajustar esto evita una conmutación QSK entrecortada, mientras permite un rápido retorno a RX entre palabras o caracteres.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Phone/CW muestra controles solo cuando hay una conexión activa con el radio.
- El slice activo debe estar en modo CW. El subpanel CW reemplaza automáticamente al subpanel Phone cuando se selecciona CW en el slice activo.

## Pasos

1. Localice el botón de bandeja **P/CW** en la barra lateral derecha y confirme que el applet esté visible. Si el applet no se ve, haga clic en el botón de bandeja **P/CW** para mostrarlo.
2. Confirme que se muestre el subpanel CW. Si en su lugar aparecen los controles Phone, cambie el slice activo a un modo CW usando el selector de modo en el área principal del VFO.
3. Localice el control deslizante **Delay (CW)** en el subpanel CW.
4. Arrastre el control deslizante **Delay (CW)** hacia la izquierda para reducir el retardo o hacia la derecha para aumentarlo. El valor se aplica al radio inmediatamente.
5. Alternativamente, haga clic en la visualización del valor junto al control deslizante y escriba un número directamente (0-2000 ms). Presione Enter para aplicar el valor.

## Qué hace cada control

| Control      | Descripción                                                                                                                                                                                                                                                                                                                     | Rango válido                                                                                                                |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| Delay (CW)   | Establece el retardo de break-in en CW; llama a TransmitModel::setCwDelay. El QLineEdit adyacente acepta valores escritos (0-2000) (v0.9.8, #2429). En v0.9.8, se corrigió setCwDelay para almacenar en caché el valor inmediatamente, de modo que la emisión del radio no devuelva el control deslizante a su posición anterior (#2428). El QLineEdit usa QIntValidator para restringir la entrada al rango válido. | 0-2000 ms (paso 10)                                                                                                        |
| Breakin      | Activa o desactiva el break-in completo (QSK). Con **Breakin** activado, los flancos de las teclas disparan TX y el retardo de break-in mantiene el relé antes de regresar a recepción. Con **Breakin** desactivado, los caracteres tecleados se ponen en cola y el operador activa PTT manualmente.                              | On / Off                                                                                                                   |

## Consejos

- Un retardo de 0 ms con **Breakin** activado proporciona operación QSK completa. Aumente el retardo para reducir el desgaste del relé durante el envío rápido.
- El control deslizante **Delay (CW)** avanza en incrementos de 10 ms. Para un ajuste fino, haga clic en la pista del control deslizante y use las teclas de flecha (si los atajos de teclado están habilitados en `View > Keyboard Shortcuts`).
- La visualización del valor es un QLineEdit editable. Haga clic en él para escribir un valor preciso, luego presione Enter. El control deslizante se moverá para coincidir.

## Notas para v0.9.8

- **Campos de valor editables:** Las cuatro etiquetas de valor CW (Delay, Speed, Sidetone Volume, Pitch) ahora son widgets QLineEdit con QIntValidator. Haga clic en cualquier valor y escriba un número directamente para una entrada precisa.
- **Corregido el almacenamiento en caché del valor de retardo:** La función setCwDelay ahora almacena en caché el valor inmediatamente, evitando que la emisión del radio devuelva el control deslizante a su valor anterior.

## Notas para v0.9.7

- **Comportamiento de Breakin corregido:** El interruptor **Breakin** ahora controla completamente si el teclado CW y las rutas de tecleo MIDI disparan TX automáticamente. Anteriormente, una envolvente interna de auto-PTT anulaba el estado **Breakin OFF** y suprimía el tiempo de persistencia QSK. Esa envolvente se ha eliminado. Con **Breakin** desactivado, las teclas ponen caracteres en cola y se debe activar PTT manualmente; con **Breakin** activado, los flancos de las teclas disparan TX inmediatamente y `break_in_delay` gobierna el tiempo de persistencia del relé.
- **Indicador de compresión limitado al estado de transmisión:** El indicador **Compression** en el subpanel Phone ahora muestra 0 dB durante recepción. Solo muestra un valor distinto de cero cuando el interbloqueo del radio informa TRANSMITTING y el procesador de voz está habilitado. Esto evita que aparezcan lecturas obsoletas de la cadena de TX mientras escucha.
- **Control deslizante de ganancia de micrófono en modo RADE:** Cuando el modo RADE está activo, el control deslizante **Mic gain** actúa como un control de ganancia RADE del lado del cliente y usa el ajuste `PcMicGain`, la misma clave utilizada para la fuente de micrófono de PC. El valor del control deslizante ya no se envía al radio como `mic_level` mientras RADE está activo, lo que de otro modo sobrescribiría silenciosamente el ajuste de micrófono del hardware. Cuando el modo RADE se desactiva, el control deslizante vuelve a reflejar el nivel de micrófono informado por el radio.
- **Indicador de nivel en modo RADE:** Cuando el modo RADE está activo, el indicador **Level** permanece activo durante recepción (no requiere que `met_in_rx` esté configurado), de manera consistente con el comportamiento existente de la fuente de micrófono de PC. Cuando el modo RADE se desactiva, el indicador se restablece a −150 dBFS.

## Notas para v0.9.3

- **Indicador de nivel (panel Phone):** Cuando la fuente de micrófono está configurada en **PC**, el indicador Level ahora aparece inmediatamente al conectar, sin esperar a que se establezca la bandera `met_in_rx` del radio. Esto se debe a que la medición del micrófono de PC se ejecuta del lado del cliente y es independiente de `met_in_rx`. Para todas las demás fuentes de micrófono, el comportamiento de supresión anterior no cambia: el indicador muestra −150 dBFS cuando `met_in_rx` está desactivado y el radio no está transmitiendo.
- **Actualización del panel VOX / Phone:** Los establecedores de VOX ahora emiten `phoneStateChanged`, por lo que el subpanel Phone se actualiza instantáneamente cuando se activa o desactiva VOX mediante un atajo de teclado. No es necesaria ninguna interacción manual con el panel para ver el estado actual de VOX.
- **Sidetone en Windows:** El flujo de sidetone CW (CwSidetoneGenerator de baja latencia) ahora comienza inmediatamente al conectar en Windows. Si anteriormente tenía que activar y desactivar **Sidetone** después de conectar para escuchar el sidetone local, esta solución alternativa ya no es necesaria.

## Relacionado

- [Habilitar el tecleo con paleta iambic](enable-iambic-paddle-keying.md)
- [Establecer la velocidad de tecleo CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Cambiar el tono CW / frecuencia de sidetone](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md)
