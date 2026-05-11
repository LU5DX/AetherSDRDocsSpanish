# Descripción general de Phone/CW

El applet Phone/CW es un panel de transmisión con detección de modo que proporciona controles de micrófono, procesador y monitor en modos de voz, y cambia automáticamente a controles de CW cuando el slice activo está en modo CW. Ábralo para ajustar el audio de transmisión o configurar los parámetros de tecleo.

## Cómo funciona

El applet está siempre presente en el Panel de Applets de la barra lateral derecha. Actívelo o desactívelo usando el botón **P/CW** de la bandeja. Contiene dos subpaneles gestionados por una disposición apilada:

- **Subpanel Phone** — visible cuando el slice activo está en un modo de voz (SSB, AM, FM y similares).
- **Subpanel CW** — visible cuando el slice activo está en un modo CW.

AetherSDR cambia entre subpaneles automáticamente al cambiar el modo del slice. No los cambia manualmente.

### Subpanel Phone

| Control          | Tipo          | Qué hace                                                                                                                                                                                                                                                                                                                                             |
|------------------|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Level            | Medidor       | Muestra el nivel máximo de entrada del micrófono en dBFS. Se suprime a -150 cuando met_in_rx está desactivado y no se está transmitiendo. Excepción: cuando la fuente del micrófono es PC, o cuando el modo RADE está activo, el indicador usa medición del lado cliente y no se suprime por met_in_rx. Cuando RADE está activo, el indicador Level continúa mostrando la señal durante RX ("Level Meter During Receive"). |
| Compression      | Medidor       | Muestra la cantidad de compresión de voz en dB. Se activa en función del estado TRANSMITIENDO del interlock de la radio y del habilitador del procesador de voz: muestra 0 dB durante RX para evitar lecturas obsoletas de la cadena de TX. Controlado a través de la ranura `updateCompression()`, independiente de la ruta del nivel de micrófono.      |
| Mic profile      | Cuadro combinado | Carga el perfil de procesamiento de micrófono nombrado de la lista de perfiles de la radio.                                                                                                                                                                                                                                                          |
| Mic source       | Cuadro combinado | Selecciona la fuente de entrada del micrófono.                                                                                                                                                                                                                                                                                                       |
| Mic gain         | Deslizador     | Ajusta el nivel de entrada del micrófono. Cuando la fuente es PC, o cuando el modo RADE está activo, el valor se mantiene del lado cliente (almacenado como `PcMicGain`) porque la radio siempre reporta nivel 0 para fuentes PC y no usa este valor para TX RADE. En modo RADE, mover el deslizador ajusta solo la ganancia RADE del lado cliente y no envía un comando de nivel de micrófono a la radio. |
| +ACC             | Botón de alternancia | Habilita la mezcla de entrada del micrófono accesorio.                                                                                                                                                                                                                                                                                               |
| PROC             | Botón de alternancia | Activa o desactiva el procesador de voz.                                                                                                                                                                                                                                                                                                             |
| NOR/DX/DX+       | Deslizador     | Establece el nivel del procesador de voz. Tres posiciones: NOR (0), DX (1), DX+ (2).                                                                                                                                                                                                                                                                |
| DAX              | Botón de alternancia | Habilita DAX como fuente de audio de TX.                                                                                                                                                                                                                                                                                                             |
| MON              | Botón de alternancia | Habilita el monitor de TX de banda lateral.                                                                                                                                                                                                                                                                                                          |
| Monitor volume   | Deslizador     | Establece el volumen del monitor de banda lateral.                                                                                                                                                                                                                                                                                                   |
| ALC              | Medidor        | Muestra la lectura de control automático de nivel de MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS, rango -20 a 0 dBFS, rojo por encima de -3). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Reconfigurado de HWALC (voltaje RCA) al medidor ALC de software en v26.5.1 (#2552). Reflejado por un indicador idéntico en el subpanel CW. |

### Subpanel CW

| Control          | Tipo           | Qué hace                                                                                                                                                                                                                                                                                                                       | Predeterminado | Rango / Opciones       | Clave de ajuste |
|------------------|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------|-----------------|
| ALC              | Medidor        | Muestra la lectura de control automático de nivel de MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS, rango -20 a 0 dBFS, rojo por encima de -3). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Refleja idénticamente el indicador ALC del subpanel Phone. Añadido en v26.5.1 (#2552) como parte de la división del medidor ALC de software. | —              | -20 a 0 dBFS           | —               |
| Delay            | Deslizador     | Establece el retardo de break-in de CW en milisegundos. El QLineEdit adyacente acepta valores escritos (0–2000). Cuando escribe un valor y presiona Enter, el deslizador se actualiza para coincidir. El deslizador no retrocede inesperadamente porque el valor se almacena en caché inmediatamente (v0.9.8, #2428).              | 500            | 0–2000 ms (paso 10)    | —               |
| Speed            | Deslizador     | Establece la velocidad de tecleo CW. El QLineEdit adyacente acepta valores escritos (5–100). Cuando escribe un valor y presiona Enter, el deslizador se actualiza para coincidir.                                                                                                                                               | 20             | 5–100 WPM              | —               |
| Breakin          | Botón de alternancia | Activa o desactiva el break-in completo (QSK). Con Breakin activado, los flancos de la llave activan TX y el retardo de break-in mantiene el relé. Con Breakin desactivado, las teclas se ponen en cola y el operador activa PTT manualmente. La envolvente de PTT automático anterior que enmascaraba Breakin desactivado e interfería con el tiempo de colgado QSK se eliminó en v0.9.7. | —              | On / Off               | —               |
| Iambic           | Botón de alternancia | Activa o desactiva el manipulador de paleta iámbica.                                                                                                                                                                                                                                                                           | —              | On / Off               | —               |
| Pitch < / >      | Campo de texto | QLineEdit con botones < / > (CwTriBtn). Escriba un valor (100–6000) o haga clic en los botones para aumentar o disminuir en pasos de 10 Hz. Ajusta el tono de la señal de prueba CW y la altura del decodificador.                                                                                                               | 600 Hz         | 100–6000 Hz (paso 10)  | —               |
| Sidetone         | Botón de alternancia | Activa o desactiva simultáneamente el monitor de señal de prueba CW de la radio (alimentado por DAX) y el generador de señal de prueba CW de baja latencia del lado cliente. En Windows, el flujo de señal de prueba ahora se inicia inmediatamente al conectar (#2105).                                                                | —              | On / Off               | —               |
| Sidetone volume  | Deslizador     | Establece simultáneamente el volumen del monitor CW de la radio (mon_gain_cw) y el volumen del generador de señal de prueba del lado cliente. El QLineEdit adyacente acepta valores escritos (0–100). Cuando escribe un valor y presiona Enter, el deslizador se actualiza para coincidir.                                          | 50             | 0–100                  | —               |
| L / R pan (CW)   | Deslizador     | Posición panorámica del monitor CW. Aplica panorámica de potencia constante tanto al monitor de la radio como al generador local de señal de prueba. Haga doble clic para volver a centrar.                                                                                                                                    | 50             | 0–100                  | —               |

### Edición de valor en línea (v0.9.8)

En v0.9.8, las cuatro etiquetas de valor CW (Delay, Speed, Sidetone Volume, Pitch) ahora son widgets QLineEdit con QIntValidator. Haga clic en cualquier valor y escriba un número directamente, luego presione Enter. El deslizador o control se actualiza para coincidir con el valor escrito. Esto proporciona paridad con SmartSDR para la entrada numérica directa. Los campos editables son:

- **Delay (CW)** — acepta 0–2000
- **Speed (CW)** — acepta 5–100
- **Sidetone volume** — acepta 0–100
- **Pitch < / >** — acepta 100–6000

Cuando está editando activamente un campo, el deslizador deja de actualizar el texto de ese campo hasta que termine de editar, evitando conflictos visuales.

### Comportamiento de la señal de prueba (v0.9.1+)

El botón de alternancia **Sidetone** y el deslizador **Sidetone volume** controlan simultáneamente el monitor alimentado por DAX de la radio y el generador de señal de prueba CW de baja latencia del lado cliente (CwSidetoneGenerator, aproximadamente 10 ms de latencia). No hay un botón de alternancia de señal de prueba local ni un deslizador de volumen separados. El tono y la panorámica siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio; no se requiere ni está disponible una anulación manual.

La señal de prueba local es adecuada para transmisiones con paleta, llave recta y generadas por CWX donde la latencia de ida y vuelta de la red haría que el monitor alimentado por DAX de la radio no fuera utilizable a velocidades más altas.

El bus de señal de prueba se comparte con los tonos Quindar. La señal de prueba y los tonos Quindar son mutuamente excluyentes a nivel de modo.

### Comportamiento de break-in (v0.9.7)

Las rutas de teclado CW y MIDI ahora respetan completamente el ajuste `break_in` de la radio. Con **Breakin** activado (QSK), los flancos de la llave activan TX y el retardo de break-in mantiene el relé abierto entre elementos. Con **Breakin** desactivado, los caracteres tecleados se ponen en cola y usted activa PTT manualmente antes de enviar. Se eliminó una envolvente de PTT automático presente en versiones anteriores que enmascaraba el estado Breakin desactivado y eliminaba el tiempo de colgado QSK.

### Interacción con el modo RADE (v0.9.7)

Cuando el modo RADE está activo, el deslizador **Mic gain** actúa como un control de ganancia RADE del lado cliente en lugar de enviar un comando de nivel de micrófono a la radio. El valor del deslizador se almacena bajo el ajuste `PcMicGain`, compartido con la ruta de fuente de micrófono PC. El ajuste de nivel de micrófono de la radio no se sobrescribe mientras RADE está activo.

El indicador **Level** continúa mostrando el nivel de señal durante RX cuando RADE está activo, independientemente del ajuste `met_in_rx`. Cuando RADE se desactiva, el indicador vuelve al comportamiento de supresión normal y se restablece a -150 dBFS inmediatamente.

### Comportamiento de VOX y atajos de teclado (v0.9.3)

Cuando se activa o desactiva VOX mediante un atajo de teclado, el panel Phone ahora se actualiza inmediatamente para reflejar el nuevo estado de VOX (#2084). En versiones anteriores, el panel no se actualizaba hasta que ocurría algún otro evento de la interfaz de usuario.

## Consejos

- El valor `PcMicGain` se almacena solo del lado cliente. Se utiliza tanto cuando la fuente del micrófono es PC como cuando el modo RADE está activo. Si cambia la fuente del micrófono de PC a otra y luego vuelve, AetherSDR restaura el valor guardado en lugar de leerlo de la radio.
- Cuando la fuente del micrófono es PC, o cuando el modo RADE está activo, el indicador Level usa medición del lado cliente y aparece inmediatamente al conectar, independientemente del ajuste `met_in_rx`.
- El indicador **Compression** muestra 0 dB durante RX. Esto es intencional: evita que se muestren lecturas obsoletas de la cadena de TX mientras se recibe.
- Debido a que el tono y la panorámica siempre siguen automáticamente los ajustes de la radio, ajuste el tono CW usando el campo de texto **Pitch < / >** y la panorámica usando el deslizador **L / R pan (CW)**; tanto el monitor de la radio como la señal de prueba local se actualizan juntos.
- Para escribir un valor CW directamente, haga clic en el número, escriba un valor y presione Enter. El deslizador se mueve para coincidir.
- El botón de alternancia **Sidetone** habilita o deshabilita la señal de prueba local al mismo tiempo que el monitor de la radio. No puede habilitar uno independientemente del otro.
- Con **Breakin** desactivado, las pulsaciones de teclas se ponen en cola pero TX no se activa automáticamente. Active PTT manualmente antes de comenzar a enviar.

## Relacionados

- [Pick a mic source (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Adjust mic gain and enable the accessory mix](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Select a mic profile for a specific microphone](select-a-mic-profile-for-a-specific-microphone.md)
- [Enable speech processor at NOR, DX, or DX+ level](enable-speech-processor-at-nor-dx-or-dx-level.md)
- [Listen to a TX sidetone monitor](listen-to-a-tx-sidetone-monitor.md)
- [Set CW keying speed in WPM](set-cw-keying-speed-in-wpm.md)
- [Set CW break-in delay](set-cw-break-in-delay.md)
- [Enable iambic paddle keying](enable-iambic-paddle-keying.md)
- [Change CW pitch / sidetone frequency](change-cw-pitch-sidetone-frequency.md)
