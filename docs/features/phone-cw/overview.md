# Descripción general de Phone/CW

El applet Phone/CW es un panel de transmisión sensible al modo que proporciona controles de micrófono, procesador y monitor en los modos de voz, y cambia automáticamente a controles de CW cuando el slice activo está en un modo CW. Ábralo para ajustar el audio de transmisión o establecer los parámetros de tecleo.

## Cómo funciona

El applet está siempre presente en el Panel de Applets de la barra lateral derecha. Actívelo o desactívelo con el botón de la bandeja **P/CW**. Contiene dos sub-paneles gestionados mediante un diseño apilado:

- **Sub-panel Phone** — visible cuando el slice activo está en un modo de voz (SSB, AM, FM y similares).
- **Sub-panel CW** — visible cuando el slice activo está en un modo CW.

AetherSDR cambia automáticamente entre los sub-paneles a medida que usted cambia el modo del slice. No los cambia manualmente.

### Sub-panel Phone

| Control           | Tipo         | Qué hace                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Level             | Medidor      | Muestra el nivel máximo de entrada del micrófono en dBFS. Se suprime a -150 cuando met_in_rx está desactivado y no hay transmisión. Pase el ratón sobre el indicador para ver el nivel máximo exacto en dB con un decimal (#3936).                                                                                                                                                                                        |
| Compression       | Medidor      | Muestra la cantidad de compresión de voz en dB. Se activa con el estado TRANSMITTIENDO del interlock de la radio y con el procesador de voz habilitado: lee 0 dB durante RX para evitar lecturas obsoletas y confusas de la cadena de TX. En v26.5.3, el rango del medidor está invertido: 0 = sin compresión, -25 = compresión completa. Pase el ratón sobre el indicador para ver la cantidad exacta de compresión en dB (#3936). |
| Mic profile       | Cuadro combinado | Carga el perfil de procesamiento de micrófono nombrado de la lista de perfiles de la radio.                                                                                                                                                                                                                                                                                                                                                                                 |
| Mic source        | Cuadro combinado | Selecciona la fuente de entrada del micrófono. Cuando la radio es modulada por AetherSDR (modulación del host activa), este cuadro combinado está deshabilitado y muestra solo "PC" como fuente disponible, con una información sobre herramientas que explica la limitación. En v26.8.4, en radios cuya audio de transmisión proviene de la computadora, el cuadro combinado se reconstruye para contener solo "PC" — las otras entradas se eliminan, no solo se atenúan, y se informa al modelo que la fuente PC está en efecto. |
| Mic gain          | Control deslizante | Ajusta el nivel de entrada del micrófono. Cuando la fuente es PC, el valor se mantiene en el lado del cliente (almacenado como `PcMicGain`). En v26.8.4, la lógica de propiedad de ganancia del cliente fue refactorizada: la radio nunca se actualiza en modo PC (la radio siempre reporta mic_level=0 para PC), y la señal `micLevelChanged` se emite para la ganancia propiedad del cliente solo cuando corresponde — para el modo RADE o para una radio seleccionable cuya fuente actual es PC. |
| +ACC              | Botón de alternancia| Habilita la mezcla de entrada de micrófono accesoria.                                                                                                                                                                                                                                                                                                                                                                                                                        |
| PROC              | Botón de alternancia| Activa o desactiva el procesador de voz.                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| NOR/DX/DX+        | Control deslizante | Establece el nivel del procesador de voz. Tres posiciones: NOR (0), DX (1), DX+ (2).                                                                                                                                                                                                                                                                                                                                                                                         |
| DAX               | Botón de alternancia| Habilita DAX como fuente de audio TX. En v26.8.4, el botón DAX se oculta por completo en radios que toman audio de transmisión directamente de la computadora (modulación del host), y se fuerza a desmarcarse cuando está oculto. |
| MON               | Botón de alternancia| Habilita el monitor de TX de banda lateral.                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Monitor volume    | Control deslizante | Establece el volumen del monitor de banda lateral.                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ALC (Panel Phone) | Medidor      | Muestra la lectura de control automático de nivel de MeterModel::swAlcChanged (pico SSB post-ALC de software en dBFS, rango -20 a 0 dBFS, rojo por encima de -3). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Pase el ratón sobre el indicador para ver el nivel exacto en dBFS con un decimal (#3936). Reconectado de HWALC (voltaje RCA) al medidor ALC de software en v26.5.1 (#2552). En v26.5.3, el indicador se inicializa a -20 dBFS en su construcción. Reflejado por un indicador idéntico en el sub-panel CW. |

### Sub-panel CW

| Control           | Tipo          | Qué hace                                                                                                                                                                                                                                                                                                                                                                                          | Predeterminado | Rango / Opciones        | Clave de ajuste |
|-------------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|-------------------------|-----------------|
| ALC (Panel CW)    | Medidor       | Muestra la lectura de control automático de nivel de MeterModel::swAlcChanged (pico SSB post-ALC de software en dBFS, rango -20 a 0 dBFS, rojo por encima de -3). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Pase el ratón sobre el indicador para ver el nivel exacto en dBFS con un decimal (#3936). En v26.5.3, el indicador se inicializa a -20 dBFS en su construcción. Refleja el indicador ALC del panel Phone de manera idéntica. | —              | -20 a 0 dBFS            | —             |
| Delay             | Control deslizante | Establece el retardo de break-in en milisegundos. El QLineEdit adyacente acepta valores escritos (0–2000). Cuando escribe un valor y presiona Enter, el control deslizante se actualiza para coincidir. El control deslizante no retrocede inesperadamente porque el valor se almacena en caché de inmediato (v0.9.8, #2428).                                                                  | 500            | 0–2000 ms (paso 10)     | —             |
| Speed             | Control deslizante | Establece la velocidad de tecleo CW. El QLineEdit adyacente acepta valores escritos (5–100). Cuando escribe un valor y presiona Enter, el control deslizante se actualiza para coincidir.                                                                                                                                         | 20             | 5–100 WPM               | —             |
| Breakin           | Botón de alternancia | Activa o desactiva el break-in completo (QSK). Con Breakin ACTIVADO, los flancos de tecla activan TX y el retardo de break-in mantiene el relé. Con Breakin DESACTIVADO, las teclas se ponen en cola y el operador activa PTT manualmente. La envolvente de auto-PTT anterior que enmascaraba Breakin DESACTIVADO e interfería con el tiempo de retención de QSK se ha eliminado en v0.9.7. | —              | Activado / Desactivado  | —             |
| Iambic            | Botón de alternancia | Activa o desactiva el manipulado iambic con paddle.                                                                                                                                                                                                                                                                                | —              | Activado / Desactivado  | —             |
| Pitch < / >       | Campo de texto | QLineEdit con botones < / > (CwTriBtn). Escriba un valor (100–6000) o haga clic en los botones para avanzar en pasos de 10 Hz. Cambia el tono lateral y el tono de decodificación CW.                                                                                                                                             | 600 Hz         | 100–6000 Hz (paso 10)   | —             |
| Sidetone          | Botón de alternancia | Activa o desactiva tanto el monitor de tono lateral de la radio (alimentado por DAX) como el generador de tono lateral CW de baja latencia del lado del cliente, en sincronía. En v26.5.3, el tono lateral se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). En Windows, la transmisión de tono lateral comienza inmediatamente al conectar (#2105). | —              | Activado / Desactivado  | —             |
| Sidetone volume   | Control deslizante | Establece tanto el volumen del monitor CW de la radio (mon_gain_cw) como el volumen del generador de tono lateral del lado del cliente, en sincronía. El QLineEdit adyacente acepta valores escritos (0–100). Cuando escribe un valor y presiona Enter, el control deslizante se actualiza para coincidir.                                                                                        | 50             | 0–100                   | —             |
| L / R pan (CW)    | Control deslizante | Posición de paneo del monitor CW. Aplica paneo de potencia constante tanto al monitor de la radio como al generador de tono lateral local. Haga doble clic para volver a centrar.                                                                                                                                                  | 50             | 0–100                   | —             |

### Edición de valores en línea (v0.9.8)

En v0.9.8, las cuatro etiquetas de valores CW (Delay, Speed, Sidetone Volume y Pitch) son ahora widgets QLineEdit con QIntValidator. Haga clic en cualquier valor y escriba un número directamente, luego presione Enter. El control deslizante o el control se actualizan para coincidir con el valor escrito. Esto proporciona paridad con SmartSDR para la entrada numérica directa. Los campos editables son:

- **Delay (CW)** — acepta 0–2000
- **Speed (CW)** — acepta 5–100
- **Sidetone volume** — acepta 0–100
- **Pitch < / >** — acepta 100–6000

Cuando está editando activamente un campo, el control deslizante deja de actualizar el texto de ese campo hasta que termine de editar, evitando conflictos visuales.

### Comportamiento del tono lateral (v0.9.1+)

El botón de alternancia **Sidetone** y el control deslizante **Sidetone volume** controlan tanto el monitor alimentado por DAX de la radio como el generador de tono lateral CW de baja latencia del lado del cliente (CwSidetoneGenerator, aproximadamente 10 ms de latencia) en sincronía. En v26.5.3, el tono lateral local se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). No hay un botón de alternancia ni un control deslizante de volumen separados para el tono lateral local. El tono y el paneo siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio — no se requiere ni está disponible una anulación manual.

El tono lateral local es adecuado para transmisiones con paddle, manipulador de mano y CWX donde la latencia de ida y vuelta de la red haría que el monitor alimentado por DAX de la radio fuera inutilizable a velocidades más altas.

El bus de tono lateral se comparte con los tonos Quindar. El tono lateral y los tonos Quindar son mutuamente excluyentes a nivel de modo.

### Comportamiento de break-in (v0.9.7)

Las rutas del teclado CW y MIDI ahora respetan completamente el ajuste `break_in` de la radio. Con **Breakin** ACTIVADO (QSK), los flancos de tecla activan TX y el retardo de break-in mantiene el relé abierto entre elementos. Con **Breakin** DESACTIVADO, los caracteres tecleados se ponen en cola y usted activa PTT manualmente antes de enviar. Una envolvente de auto-PTT presente en versiones anteriores que enmascaraba el estado Breakin DESACTIVADO y eliminaba el tiempo de retención de QSK se ha eliminado.

### Compuerta de recepción del medidor de nivel (v26.5.3)

En v26.5.3, la lógica de supresión del medidor Level durante la recepción fue refactorizada en el método dedicado `applyLevelMeterReceiveGate()`. Cuando `met_in_rx` está desactivado y la radio no está transmitiendo, el medidor Level se suprime a -150 dBFS independientemente de la fuente del micrófono. Este método se llama cada vez que cambia el estado de transmisión o el estado MOX, y también cuando el modo RADE se activa o desactiva.

### Inicialización del medidor ALC (v26.5.3)

En v26.5.3, tanto los medidores ALC del panel Phone como del panel CW ahora se inicializan a -20 dBFS en su construcción usando `setValueImmediate()`. Esto asegura que los medidores comiencen vacíos cuando el applet aparece por primera vez, en lugar de mostrar un estado indefinido hasta que llegue la primera actualización del medidor desde la radio.

### Actualización del medidor de compresión (v26.5.3)

En v26.5.3, se corrigió la interpretación del medidor Compression. MeterModel expone COMPPEAK como una cantidad de compresión positiva de 0..25 dB. La cara del medidor P/CW está invertida: 0 = sin compresión, -25 = compresión completa. El medidor muestra el negativo del valor de compresión, por lo que la aguja o barra se mueve hacia abajo a medida que aumenta la compresión.

### Interacción con el modo RADE (v0.9.7)

Cuando el modo RADE está activo, el control deslizante **Mic gain** actúa como un control de ganancia RADE del lado del cliente en lugar de enviar un comando de nivel de micrófono a la radio. El valor del control deslizante se almacena bajo el ajuste `PcMicGain`, compartido con la ruta de fuente de PC. El ajuste de nivel de micrófono de la radio no se sobrescribe mientras RADE está activo.

El medidor **Level** continúa mostrando el nivel de señal durante RX cuando RADE está activo, independientemente del ajuste `met_in_rx`. Cuando RADE se desactiva, el medidor vuelve al comportamiento de supresión normal y se restablece a -150 dBFS inmediatamente.

### Comportamiento de VOX y atajos de teclado (v0.9.3)

Cuando VOX se activa o desactiva mediante un atajo de teclado, el panel Phone ahora se actualiza inmediatamente para reflejar el nuevo estado de VOX (#2084). En versiones anteriores, el panel no se actualizaba hasta que ocurriera algún otro evento de interfaz.

### Panel CWX (v0.9.7)

El panel CWX integrado limita sus atajos F1-F12 a la visibilidad del panel (#2464, #2469) para que las asignaciones de teclas F del panel DVK y los atajos de CWX ya no se activen simultáneamente. Las macros CWX también liberan TX automáticamente cuando la cola se vacía (#2450, #2507).

### Modo de modulación del host (v26.7.4, refinado en v26.8.4)

Cuando la radio está siendo modulada directamente por AetherSDR (modulación del host activa), el comportamiento del cuadro combinado **Mic source** cambió en v26.8.4 para ser más explícito:

- Anteriormente (v26.7.4), el cuadro combinado estaba deshabilitado y mostraba solo "PC" como entrada disponible, con una información sobre herramientas que explicaba la limitación.
- En v26.8.4, el cuadro combinado se **reconstruye** para contener solo "PC" cuando la radio no puede aceptar una entrada seleccionable. Las otras entradas (MIC, BAL, LINE, ACC) se eliminan por completo en lugar de atenuarse, porque una entrada atenuada todavía sugiere "esta radio tiene una entrada de micrófono que podríamos usar". El cuadro combinado se deshabilita entonces, y una información sobre herramientas indica: "Esta radio toma audio de transmisión de esta computadora. Su propia selección de entrada se realiza en la radio."
- También se informa explícitamente al modelo que la fuente PC está ahora en efecto, de modo que el estado de captura de audio de transmisión se informe de manera consistente.
- En una radio con una única posible
