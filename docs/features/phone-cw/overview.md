# Resumen de Phone/CW

El applet Phone/CW es un panel de transmisión consciente del modo que proporciona controles de micrófono, procesador y monitor en modos de voz, y cambia automáticamente a controles CW cuando el slice activo está en un modo CW. Ábralo para ajustar el audio de transmisión o configurar los parámetros de manipulación.

## Cómo funciona

El applet está siempre presente en el Panel de Applets en la barra lateral derecha. Actívelo usando el botón de la bandeja **P/CW**. Contiene dos subpaneles gestionados por un diseño apilado:

- **Subpanel Phone** — visible cuando el slice activo está en un modo de voz (SSB, AM, FM y similares).
- **Subpanel CW** — visible cuando el slice activo está en un modo CW.

AetherSDR cambia entre subpaneles automáticamente al cambiar el modo del slice. No los cambia manualmente.

### Subpanel Phone

| Control           | Tipo         | Qué hace                                                                                                                                                                                                                                                                                                                                             |
|-------------------|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Level             | Medidor      | Muestra el nivel pico de entrada del micrófono en dBFS. Suprimido a -150 cuando met_in_rx está desactivado y no está transmitiendo.                                                                                                                                                                                                                  |
| Compression       | Medidor      | Muestra la cantidad de compresión de voz en dB. Está limitado por el estado TRANSMITIENDO del interlock del radio y la habilitación del procesador de voz: lee 0 dB durante RX para evitar lecturas obsoletas y confusas de la cadena de TX. En v26.5.3, el rango del medidor está invertido: 0 = sin compresión, -25 = compresión completa.        |
| Mic profile       | Cuadro combo | Carga el perfil de procesamiento de micrófono nombrado de la lista de perfiles del radio.                                                                                                                                                                                                                                                            |
| Mic source        | Cuadro combo | Selecciona la fuente de entrada del micrófono.                                                                                                                                                                                                                                                                                                       |
| Mic gain          | Deslizador   | Ajusta el nivel de entrada del micrófono. Cuando la fuente es PC, el valor se mantiene del lado del cliente (almacenado como `PcMicGain`).                                                                                                                                                                                                            |
| +ACC              | Botón de alternancia | Habilita la mezcla de entrada del micrófono auxiliar.                                                                                                                                                                                                                                                                                       |
| PROC              | Botón de alternancia | Activa o desactiva el procesador de voz.                                                                                                                                                                                                                                                                                                      |
| NOR/DX/DX+        | Deslizador   | Establece el nivel del procesador de voz. Tres posiciones: NOR (0), DX (1), DX+ (2).                                                                                                                                                                                                                                                                |
| DAX               | Botón de alternancia | Habilita DAX como fuente de audio de TX.                                                                                                                                                                                                                                                                                                      |
| MON               | Botón de alternancia | Habilita el monitor de TX de banda lateral.                                                                                                                                                                                                                                                                                                   |
| Monitor volume    | Deslizador   | Establece el volumen del monitor de banda lateral.                                                                                                                                                                                                                                                                                                   |
| ALC (Panel Phone) | Medidor      | Muestra la lectura del control automático de nivel de MeterModel::swAlcChanged (pico SSB post-ALC de software en dBFS, rango -20 a 0 dBFS, rojo por encima de -3). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Reconectado de HWALC (voltaje RCA) al medidor SW ALC en v26.5.1 (#2552). En v26.5.3, el indicador se inicializa a -20 dBFS al construirse. Reflejado por un indicador idéntico en el subpanel CW. |

### Subpanel CW

| Control           | Tipo          | Qué hace                                                                                                                                                                                                                                                                                                                              | Predeterminado | Rango / Opciones       | Clave de configuración |
|-------------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------|-------------|
| ALC (Panel CW)    | Medidor       | Muestra la lectura del control automático de nivel de MeterModel::swAlcChanged (pico SSB post-ALC de software en dBFS, rango -20 a 0 dBFS, rojo por encima de -3). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. En v26.5.3, el indicador se inicializa a -20 dBFS al construirse. Refleja idénticamente el indicador ALC del panel Phone. | —              | -20 a 0 dBFS           | —           |
| Delay             | Deslizador   | Establece el retardo de inserción CW en milisegundos. El QLineEdit adyacente acepta valores escritos (0–2000). Cuando escribe un valor y presiona Enter, el deslizador se actualiza para coincidir. El deslizador no retrocede inesperadamente porque el valor se almacena en caché inmediatamente (v0.9.8, #2428).                     | 500            | 0–2000 ms (paso 10)    | —           |
| Speed             | Deslizador   | Establece la velocidad de manipulación CW. El QLineEdit adyacente acepta valores escritos (5–100). Cuando escribe un valor y presiona Enter, el deslizador se actualiza para coincidir.                                                                                                                                             | 20             | 5–100 WPM              | —           |
| Breakin           | Botón de alternancia | Activa o desactiva la inserción completa (QSK). Con Breakin ACTIVADO, los bordes de la manipulación activan TX y el retardo de inserción mantiene el relé. Con Breakin DESACTIVADO, las teclas se ponen en cola y el operador activa PTT manualmente. La envolvente PTT automática anterior que enmascaraba Breakin DESACTIVADO e interfería con el tiempo de retención QSK se ha eliminado en v0.9.7. | —              | Activado / Desactivado | —           |
| Iambic            | Botón de alternancia | Activa o desactiva el manipulador de paleta iámbica.                                                                                                                                                                                                                                                                                  | —              | Activado / Desactivado | —           |
| Pitch < / >       | Campo de texto| QLineEdit con botones < / > (CwTriBtn). Escriba un valor (100–6000) o haga clic en los botones para avanzar en pasos de 10 Hz. Cambia el tono del sidetone CW y la altura de decodificación.                                                                                                                                    | 600 Hz         | 100–6000 Hz (paso 10)  | —           |
| Sidetone          | Botón de alternancia | Activa o desactiva tanto el monitor sidetone CW del radio (alimentado por DAX) como el generador de sidetone CW de baja latencia del lado del cliente, al unísono. En v26.5.3, el sidetone se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). En Windows, el flujo de sidetone se inicia inmediatamente al conectar (#2105). | —              | Activado / Desactivado | —           |
| Sidetone volume   | Deslizador   | Establece tanto el volumen del monitor CW del radio (mon_gain_cw) como el volumen del generador de sidetone del lado del cliente, al unísono. El QLineEdit adyacente acepta valores escritos (0–100). Cuando escribe un valor y presiona Enter, el deslizador se actualiza para coincidir.                                                | 50             | 0–100                  | —           |
| L / R pan (CW)    | Deslizador   | Posición panorámica del monitor CW. Aplica panorámica de potencia constante tanto al monitor del radio como al generador de sidetone local. Haga doble clic para recentrar.                                                                                                                                                           | 50             | 0–100                  | —           |

### Edición de valor en línea (v0.9.8)

En v0.9.8, las cuatro etiquetas de valor CW (Delay, Speed, Sidetone Volume, Pitch) ahora son widgets QLineEdit con QIntValidator. Haga clic en cualquier valor y escriba un número directamente, luego presione Enter. El deslizador o control se actualiza para coincidir con el valor escrito. Esto proporciona paridad con SmartSDR para la entrada numérica directa. Los campos editables son:

- **Delay (CW)** — acepta 0–2000
- **Speed (CW)** — acepta 5–100
- **Sidetone volume** — acepta 0–100
- **Pitch < / >** — acepta 100–6000

Cuando está editando activamente un campo, el deslizador deja de actualizar el texto de ese campo hasta que termine de editar, evitando conflictos visuales.

### Comportamiento del sidetone (v0.9.1+)

El botón de alternancia **Sidetone** y el deslizador **Sidetone volume** controlan tanto el monitor alimentado por DAX del radio como el generador de sidetone CW de baja latencia del lado del cliente (CwSidetoneGenerator, aproximadamente 10 ms de latencia) al unísono. En v26.5.3, el sidetone local se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). No hay un botón de alternancia ni un deslizador de volumen de sidetone local separados. El tono y la panorámica siempre siguen automáticamente la configuración de `cw_pitch` y `mon_pan_cw` del radio — no se requiere ni está disponible ninguna anulación manual.

El sidetone local es adecuado para transmisiones generadas por paleta, manipulador rectilíneo y CWX donde la latencia de ida y vuelta de la red haría que el monitor alimentado por DAX del radio no fuera utilizable a velocidades más altas.

El bus de sidetone se comparte con los tonos Quindar. El sidetone y los tonos Quindar son mutuamente excluyentes a nivel de modo.

### Comportamiento de inserción (v0.9.7)

Las rutas de teclado CW y MIDI ahora respetan completamente la configuración `break_in` del radio. Con **Breakin** ACTIVADO (QSK), los bordes de la manipulación activan TX y el retardo de inserción mantiene el relé abierto entre elementos. Con **Breakin** DESACTIVADO, los caracteres tecleados se ponen en cola y usted activa PTT manualmente antes de enviar. Se ha eliminado una envolvente PTT automática presente en versiones anteriores que enmascaraba el estado Breakin DESACTIVADO y eliminaba el tiempo de retención QSK.

### Puerta de recepción del medidor de nivel (v26.5.3)

En v26.5.3, la lógica de supresión del medidor Level durante la recepción se refactorizó en el método dedicado `applyLevelMeterReceiveGate()`. Cuando `met_in_rx` está desactivado y el radio no está transmitiendo, el medidor Level se suprime a -150 dBFS independientemente de la fuente del micrófono. Este método se llama cada vez que cambia el estado de transmisión o el estado MOX, y también cuando el modo RADE se activa o desactiva.

### Inicialización del indicador ALC (v26.5.3)

En v26.5.3, tanto los indicadores ALC del panel Phone como del panel CW ahora se inicializan a -20 dBFS al construirse usando `setValueImmediate()`. Esto asegura que los indicadores comiencen vacíos cuando el applet aparece por primera vez, en lugar de mostrar un estado indefinido hasta que llegue la primera actualización del medidor desde el radio.

### Actualización del medidor de compresión (v26.5.3)

En v26.5.3, se corrigió la interpretación del medidor Compression. El MeterModel expone COMPPEAK como una cantidad de compresión positiva de 0..25 dB. La cara del indicador P/CW está invertida: 0 = sin compresión, -25 = compresión completa. El indicador muestra el negativo del valor de compresión, por lo que la aguja o barra se mueve hacia abajo a medida que aumenta la compresión.

### Interacción con el modo RADE (v0.9.7)

Cuando el modo RADE está activo, el deslizador **Mic gain** actúa como un control de ganancia RADE del lado del cliente en lugar de enviar un comando de nivel de micrófono al radio. El valor del deslizador se almacena bajo la configuración `PcMicGain`, compartida con la ruta de fuente de micrófono PC. El nivel de micrófono del radio no se sobrescribe mientras RADE esté activo.

El medidor **Level** continúa mostrando el nivel de señal durante RX cuando RADE está activo, independientemente de la configuración `met_in_rx`. Cuando RADE se desactiva, el medidor vuelve al comportamiento de supresión normal y se restablece a -150 dBFS inmediatamente.

### Comportamiento de VOX y atajos de teclado (v0.9.3)

Cuando VOX se activa o desactiva mediante un atajo de teclado, el panel Phone ahora se actualiza inmediatamente para reflejar el nuevo estado de VOX (#2084). En versiones anteriores, el panel no se actualizaba hasta que ocurría algún otro evento de la interfaz de usuario.

### Panel CWX (v0.9.7)

El panel CWX integrado limita sus atajos F1-F12 a la visibilidad del panel (#2464, #2469), por lo que las vinculaciones de teclas F del panel DVK y las teclas rápidas CWX ya no se activan simultáneamente. Las macros CWX también liberan TX automáticamente cuando la cola se vacía (#2450, #2507).

## Consejos

- El valor `PcMicGain` se almacena solo del lado del cliente. Se usa tanto cuando la fuente del micrófono es PC como cuando el modo RADE está activo. Si cambia la fuente del micrófono de PC a otra y luego vuelve, AetherSDR restaura el valor guardado en lugar de leerlo del radio.
- Cuando la fuente del micrófono es PC, o cuando el modo RADE está activo, el medidor Level usa medición del lado del cliente y aparece inmediatamente al conectar, independientemente de la configuración `met_in_rx`.
- El medidor **Compression** lee 0 dB durante RX. Esto es intencional: evita que se muestren lecturas obsoletas de la cadena de TX mientras se recibe.
- Debido a que el tono y la panorámica siempre siguen automáticamente la configuración del radio, ajuste el tono CW usando el campo de texto **Pitch < / >** y la panorámica usando el deslizador **L / R pan (CW)** — tanto el monitor del radio como el sidetone local se actualizan juntos.
- Para escribir un valor CW directamente, haga clic en el número, escriba un valor y presione Enter. El deslizador se mueve para coincidir.
- El botón de alternancia **Sidetone** habilita o deshabilita el sidetone local al mismo tiempo que el monitor del radio. No puede habilitar uno independientemente del otro.
- Con **Breakin** DESACTIVADO, las pulsaciones de teclas se ponen en cola pero TX no se activa automáticamente. Active PTT manualmente antes de comenzar a enviar.
- Los indicadores ALC comienzan vacíos (-20 dBFS) cuando el applet aparece por primera vez, así que no se preocupe si no muestran ninguna lectura hasta el primer evento de transmisión.

## Relacionados

- [Pick a mic source (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Adjust mic gain and enable the accessory mix](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Select a mic profile for a specific microphone](select-a-mic-profile-for-a-specific-microphone.md)
- [Enable speech processor at NOR, DX, or DX+ level](enable-speech-processor-at-nor-dx-or-dx-level.md)
- [Listen to a TX sidetone monitor](listen-to-a-tx-sidetone-monitor.md)
- [Set CW keying speed in WPM](set-cw-keying-speed-in-wpm.md)
- [Set CW break-in delay](set-cw-break-in-delay.md)
- Enable iambic paddle key
