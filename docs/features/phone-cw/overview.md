# Resumen de Phone/CW

El applet Phone/CW es un panel de transmisión sensible al modo que proporciona controles de micrófono, procesador y monitor en modos de voz, y cambia automáticamente a controles de CW cuando el slice activo está en un modo CW. Ábralo para ajustar el audio de transmisión o configurar los parámetros de tecleo.

## Cómo funciona

El applet está siempre presente en el Panel de Applets de la barra lateral derecha. Actívelo o desactívelo usando el botón de la bandeja **P/CW**. Contiene dos subpaneles gestionados por un diseño apilado:

- **Phone sub-panel** — visible cuando el slice activo está en un modo de voz (SSB, AM, FM y similares).
- **CW sub-panel** — visible cuando el slice activo está en un modo CW.

AetherSDR cambia entre subpaneles automáticamente al cambiar el modo del slice. Usted no los cambia manualmente.

### Phone sub-panel

| Control       | Tipo         | Qué hace                                                                                                                                                                                                                                                                                                                                             |
|---------------|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Level         | Medidor      | Muestra el nivel pico de entrada del micrófono en dBFS. Se suprime a -150 cuando met_in_rx está desactivado y no se transmite. Excepción: cuando la fuente del micrófono es PC, o cuando el modo RADE está activo, el indicador usa medición del lado del cliente y no es suprimido por met_in_rx. Cuando RADE está activo, el indicador Level continúa mostrando la señal durante RX ("Level Meter During Receive"). |
| Compression   | Medidor      | Muestra la cantidad de compresión de voz en dB. Se activa con el estado TRANSMITTING del interlock de la radio y la habilitación del procesador de voz: lee 0 dB durante RX para evitar mostrar lecturas obsoletas de la cadena de TX. Se controla a través del slot `updateCompression()`, independiente de la ruta del nivel de micrófono.             |
| Mic profile   | Cuadro combo | Carga el perfil de procesamiento de micrófono nombrado de la lista de perfiles de la radio.                                                                                                                                                                                                                                                          |
| Mic source    | Cuadro combo | Selecciona la fuente de entrada del micrófono.                                                                                                                                                                                                                                                                                                       |
| Mic gain      | Deslizador   | Ajusta el nivel de entrada del micrófono. Cuando la fuente es PC, o cuando el modo RADE está activo, el valor se mantiene del lado del cliente (almacenado como `PcMicGain`) porque la radio siempre reporta el nivel 0 para fuentes PC y no usa este valor para TX en RADE. En modo RADE, mover el deslizador ajusta solo la ganancia RADE del lado del cliente y no envía un comando de nivel de micrófono a la radio. |
| +ACC          | Botón alternante | Habilita la mezcla de entrada del micrófono auxiliar.                                                                                                                                                                                                                                                                                            |
| PROC          | Botón alternante | Alterna el procesador de voz.                                                                                                                                                                                                                                                                                                              |
| NOR/DX/DX+    | Deslizador   | Establece el nivel del procesador de voz. Tres posiciones: NOR (0), DX (1), DX+ (2).                                                                                                                                                                                                                                                          |
| DAX           | Botón alternante | Habilita DAX como fuente de audio de TX.                                                                                                                                                                                                                                                                                                      |
| MON           | Botón alternante | Habilita el monitor de TX en banda lateral.                                                                                                                                                                                                                                                                                                  |
| Monitor volume | Deslizador   | Establece el volumen del monitor en banda lateral.                                                                                                                                                                                                                                                                                                   |

### CW sub-panel

| Control           | Tipo          | Qué hace                                                                                                                                                                                                                                                                                                                                           | Predeterminado | Rango / Opciones     | Clave de configuración |
|-------------------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|----------------------|------------------------|
| ALC               | Medidor       | Muestra la lectura del control automático de nivel. Rojo por encima de 80.                                                                                                                                                                                                                                                                         | —              | 0–100                | —                      |
| Delay             | Deslizador    | Establece el retardo de break-in en CW en milisegundos. El QLineEdit adyacente acepta valores escritos (0–2000). Cuando escribe un valor y presiona Enter, el deslizador se actualiza para coincidir. El deslizador no retrocede inesperadamente porque el valor se almacena en caché inmediatamente (v0.9.8, #2428).                    | 500            | 0–2000 ms (paso 10)  | —                      |
| Speed             | Deslizador    | Establece la velocidad de tecleo CW. El QLineEdit adyacente acepta valores escritos (5–100). Cuando escribe un valor y presiona Enter, el deslizador se actualiza para coincidir.                                                                                                                                                                 | 20             | 5–100 WPM            | —                      |
| Breakin           | Botón alternante | Alterna el break-in completo (QSK). Con Breakin ACTIVADO, los flancos de tecla activan TX y el retardo de break-in mantiene el relé. Con Breakin DESACTIVADO, las teclas se ponen en cola y el operador activa PTT manualmente. La envolvente de PTT automática anterior que enmascaraba Breakin DESACTIVADO e interfería con el tiempo de espera QSK se ha eliminado en v0.9.7. | —              | On / Off             | —                      |
| Iambic            | Botón alternante | Alterna el manipulador de paleta iámbico.                                                                                                                                                                                                                                                                                                      | —              | On / Off             | —                      |
| Pitch < / >       | Campo de texto | QLineEdit con botones < / > (CwTriBtn). Escriba un valor (100–6000) o haga clic en los botones para avanzar en pasos de 10 Hz. Ajusta el tono de la señal lateral y la frecuencia de decodificación CW.                                                                                                                        | 600 Hz         | 100–6000 Hz (paso 10)| —                      |
| Sidetone          | Botón alternante | Alterna tanto el monitor de tono lateral CW de la radio (alimentado por DAX) como el generador de tono lateral CW de baja latencia del lado del cliente al unísono. En Windows, el flujo de tono lateral ahora comienza inmediatamente al conectar (#2105).                                                                         | —              | On / Off             | —                      |
| Sidetone volume   | Deslizador    | Establece tanto el volumen del monitor CW de la radio (mon_gain_cw) como el volumen del generador de tono lateral del lado del cliente al unísono. El QLineEdit adyacente acepta valores escritos (0–100). Cuando escribe un valor y presiona Enter, el deslizador se actualiza para coincidir.                                                 | 50             | 0–100                | —                      |
| L / R pan (CW)    | Deslizador    | Posición panorámica del monitor CW. Aplica panorámica de potencia constante tanto al monitor de la radio como al generador de tono lateral local. Haga doble clic para recentrar.                                                                                                                                                          | 50             | 0–100                | —                      |

### Edición de valores en línea (v0.9.8)

En v0.9.8, las cuatro etiquetas de valor CW (Delay, Speed, Sidetone Volume, Pitch) ahora son widgets QLineEdit con QIntValidator. Haga clic en cualquier valor y escriba un número directamente, luego presione Enter. El deslizador o control se actualiza para coincidir con el valor escrito. Esto proporciona paridad con SmartSDR para la entrada numérica directa. Los campos editables son:

- **Delay (CW)** — acepta 0–2000
- **Speed (CW)** — acepta 5–100
- **Sidetone volume** — acepta 0–100
- **Pitch < / >** — acepta 100–6000

Cuando está editando un campo activamente, el deslizador deja de actualizar el texto de ese campo hasta que termine de editar, evitando conflictos visuales.

### Comportamiento del tono lateral (v0.9.1+)

El botón alternante **Sidetone** y el deslizador **Sidetone volume** controlan tanto el monitor alimentado por DAX de la radio como el generador de tono lateral CW de baja latencia del lado del cliente (CwSidetoneGenerator, aproximadamente 10 ms de latencia) al unísono. No hay un botón alternante o deslizador de volumen de tono lateral local independiente. El tono (Pitch) y la panorámica (pan) siempre siguen automáticamente las configuraciones `cw_pitch` y `mon_pan_cw` de la radio; no se requiere ni está disponible una anulación manual.

El tono lateral local es adecuado para transmisiones generadas por paleta, manipulador recto y CWX donde la latencia de ida y vuelta de la red haría que el monitor alimentado por DAX de la radio no fuera utilizable a velocidades más altas.

El bus de tono lateral se comparte con los tonos Quindar. El tono lateral y los tonos Quindar son mutuamente excluyentes a nivel de modo.

### Comportamiento de break-in (v0.9.7)

Las rutas de teclado y MIDI de CW ahora respetan completamente la configuración `break_in` de la radio. Con **Breakin** ACTIVADO (QSK), los flancos de tecla activan TX y el retardo de break-in mantiene el relé abierto entre elementos. Con **Breakin** DESACTIVADO, los caracteres tecleados se ponen en cola y usted activa PTT manualmente antes de enviar. Se ha eliminado una envolvente de PTT automática presente en versiones anteriores que enmascaraba el estado Breakin DESACTIVADO y eliminaba el tiempo de espera QSK.

### Interacción con el modo RADE (v0.9.7)

Cuando el modo RADE está activo, el deslizador **Mic gain** actúa como un control de ganancia RADE del lado del cliente en lugar de enviar un comando de nivel de micrófono a la radio. El valor del deslizador se almacena bajo la configuración `PcMicGain`, compartida con la ruta de la fuente de micrófono PC. La configuración del nivel de micrófono de la radio no se sobrescribe mientras RADE está activo.

El indicador **Level** continúa mostrando el nivel de la señal durante RX cuando RADE está activo, independientemente de la configuración `met_in_rx`. Cuando RADE se desactiva, el indicador vuelve al comportamiento de supresión normal y se restablece inmediatamente a -150 dBFS.

### Comportamiento de VOX y atajos de teclado (v0.9.3)

Cuando VOX se activa mediante un atajo de teclado, el panel Phone ahora se actualiza inmediatamente para reflejar el nuevo estado de VOX (#2084). En versiones anteriores, el panel no se actualizaba hasta que ocurría algún otro evento de la interfaz de usuario.

## Consejos

- El valor `PcMicGain` se almacena solo del lado del cliente. Se usa tanto cuando la fuente del micrófono es PC como cuando el modo RADE está activo. Si cambia la fuente del micrófono de PC a otra y luego vuelve, AetherSDR restaura el valor guardado en lugar de leerlo de la radio.
- Cuando la fuente del micrófono es PC, o cuando el modo RADE está activo, el indicador Level usa medición del lado del cliente y aparece inmediatamente al conectar, independientemente de la configuración `met_in_rx`.
- El indicador **Compression** lee 0 dB durante RX. Esto es intencional: evita que se muestren lecturas obsoletas de la cadena de TX mientras se recibe.
- Dado que el tono y la panorámica siempre siguen automáticamente las configuraciones de la radio, ajuste el tono CW usando el campo de texto **Pitch < / >** y la panorámica usando el deslizador **L / R pan (CW)** — tanto el monitor de la radio como el tono lateral local se actualizan juntos.
- Para escribir un valor CW directamente, haga clic en el número, escriba un valor y presione Enter. El deslizador se mueve para coincidir.
- El botón alternante **Sidetone** habilita o deshabilita el tono lateral local al mismo tiempo que el monitor de la radio. No puede habilitar uno independientemente del otro.
- Con **Breakin** DESACTIVADO, las pulsaciones de tecla se ponen en cola pero TX no se activa automáticamente. Active PTT manualmente antes de comenzar a enviar.

## Relacionado

- [Pick a mic source (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Adjust mic gain and enable the accessory mix](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Select a mic profile for a specific microphone](select-a-mic-profile-for-a-specific-microphone.md)
- [Enable speech processor at NOR, DX, or DX+ level](enable-speech-processor-at-nor-dx-or-dx-level.md)
- [Listen to a TX sidetone monitor](listen-to-a-tx-sidetone-monitor.md)
- [Set CW keying speed in WPM](set-cw-keying-speed-in-wpm.md)
- [Set CW break-in delay](set-cw-break-in-delay.md)
- [Enable iambic paddle keying](enable-iambic-paddle-keying.md)
- [Change CW pitch / sidetone frequency](change-cw-pitch-sidetone-frequency.md)
