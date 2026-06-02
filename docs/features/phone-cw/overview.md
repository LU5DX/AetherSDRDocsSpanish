# Resumen de Phone/CW

El applet Phone/CW es un panel de transmisión que se adapta al modo activo, proporcionando controles de micrófono, procesador y monitor en modos de voz, y cambiando automáticamente a controles CW cuando el slice activo está en un modo CW. Ábralo para ajustar el audio de transmisión o configurar los parámetros de tecleo.

## Cómo funciona

El applet siempre está presente en el Panel de Applets de la barra lateral derecha. Actívelo o desactívelo usando el botón **P/CW** de la bandeja. Contiene dos subpaneles gestionados por una disposición apilada:

- **Phone sub-panel** — visible cuando el slice activo está en un modo de voz (SSB, AM, FM y similares).
- **CW sub-panel** — visible cuando el slice activo está en un modo CW.

AetherSDR cambia entre subpaneles automáticamente al cambiar el modo del slice. No los cambia manualmente.

### Phone sub-panel

| Control             | Tipo           | Qué hace                                                                                                                                                                                                                                                                                                                                     |
|---------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Level               | Medidor        | Muestra el nivel máximo de entrada del micrófono en dBFS. Se suprime a -150 cuando met_in_rx está desactivado y no se está transmitiendo.                                                                                                                                                                                                   |
| Compression         | Medidor        | Muestra la cantidad de compresión de voz en dB. Se activa con el estado TRANSMITTING del interlock de la radio y la activación del procesador de voz: lee 0 dB durante RX para evitar lecturas obsoletas de la cadena de TX. En v26.5.3, el rango del medidor está invertido: 0 = sin compresión, -25 = compresión máxima. |
| Mic profile         | Cuadro combinado | Carga el perfil de procesamiento de micrófono nombrado de la lista de perfiles de la radio.                                                                                                                                                                                                                                                  |
| Mic source          | Cuadro combinado | Selecciona la fuente de entrada del micrófono.                                                                                                                                                                                                                                                                                               |
| Mic gain            | Deslizador      | Ajusta el nivel de entrada del micrófono. Cuando la fuente es PC, el valor se mantiene del lado del cliente (almacenado como `PcMicGain`).                                                                                                                                                                                                   |
| +ACC                | Botón de alternancia | Activa la mezcla de entrada del micrófono accesorio.                                                                                                                                                                                                                                                                                     |
| PROC                | Botón de alternancia | Activa o desactiva el procesador de voz.                                                                                                                                                                                                                                                                                                   |
| NOR/DX/DX+          | Deslizador      | Establece el nivel del procesador de voz. Tres posiciones: NOR (0), DX (1), DX+ (2).                                                                                                                                                                                                                                                         |
| DAX                 | Botón de alternancia | Activa DAX como fuente de audio TX.                                                                                                                                                                                                                                                                                                        |
| MON                 | Botón de alternancia | Activa el monitor TX de banda lateral.                                                                                                                                                                                                                                                                                                     |
| Monitor volume      | Deslizador      | Establece el volumen del monitor de banda lateral.                                                                                                                                                                                                                                                                                           |
| ALC (Phone panel)   | Medidor        | Muestra la lectura del control automático de nivel procedente de MeterModel::swAlcChanged (pico SSB post-ALC de software en dBFS, rango -20 a 0 dBFS, rojo por encima de -3). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Reconectado desde HWALC (voltaje RCA) al medidor SW ALC en v26.5.1 (#2552). En v26.5.3, el indicador se inicializa a -20 dBFS en la construcción. Es reflejado por un indicador idéntico en el CW sub-panel. |

### CW sub-panel

| Control               | Tipo           | Qué hace                                                                                                                                                                                                                                                                                                                                 | Valor predeterminado | Rango / Opciones    | Clave de configuración |
|-----------------------|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|---------------------|------------------------|
| ALC (CW panel)        | Medidor        | Muestra la lectura del control automático de nivel procedente de MeterModel::swAlcChanged (pico SSB post-ALC de software en dBFS, rango -20 a 0 dBFS, rojo por encima de -3). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. En v26.5.3, el indicador se inicializa a -20 dBFS en la construcción. Refleja el indicador ALC del Phone panel de manera idéntica. | —                    | -20 a 0 dBFS        | —                    |
| Delay                 | Deslizador      | Establece el retardo de break-in CW en milisegundos. El QLineEdit adyacente acepta valores escritos (0–2000). Al escribir un valor y pulsar Enter, el deslizador se actualiza para coincidir. El deslizador no retrocede inesperadamente porque el valor se almacena en caché inmediatamente (v0.9.8, #2428).                                     | 500                  | 0–2000 ms (paso 10) | —                    |
| Speed                 | Deslizador      | Establece la velocidad de tecleo CW. El QLineEdit adyacente acepta valores escritos (5–100). Al escribir un valor y pulsar Enter, el deslizador se actualiza para coincidir.                                                                                                                                                             | 20                   | 5–100 WPM           | —                    |
| Breakin               | Botón de alternancia | Activa o desactiva el break-in completo (QSK). Con Breakin activado, los flancos de las teclas activan TX y el retardo de break-in mantiene el relé. Con Breakin desactivado, las teclas se ponen en cola y el operador activa el PTT manualmente. La envolvente de auto-PTT anterior que enmascaraba el estado Breakin OFF e interfería con el tiempo de retención QSK se ha eliminado en v0.9.7. | —                    | Activado / Desactivado | —                    |
| Iambic               | Botón de alternancia | Activa o desactiva el manipulador de paleta iámbica.                                                                                                                                                                                                                                                                                      | —                    | Activado / Desactivado | —                    |
| Pitch < / >          | Campo de texto  | QLineEdit con botones < / > (CwTriBtn). Escriba un valor (100–6000) o haga clic en los botones para avanzar en pasos de 10 Hz. Ajusta el tono del sidetone CW y el tono de decodificación.                                                                                                                                                 | 600 Hz               | 100–6000 Hz (paso 10) | —                    |
| Sidetone             | Botón de alternancia | Activa o desactiva al mismo tiempo el monitor CW de la radio (alimentado por DAX) y el generador de sidetone CW de baja latencia del lado del cliente. En v26.5.3, el sidetone local se enruta a la salida de audio seleccionada por el usuario en lugar de a la salida predeterminada (#2899). En Windows, el flujo de sidetone se inicia inmediatamente al conectar (#2105). | —                    | Activado / Desactivado | —                    |
| Sidetone volume      | Deslizador      | Establece al mismo tiempo el volumen del monitor CW de la radio (mon_gain_cw) y el volumen del generador de sidetone del lado del cliente. El QLineEdit adyacente acepta valores escritos (0–100). Al escribir un valor y pulsar Enter, el deslizador se actualiza para coincidir.                                                         | 50                   | 0–100                | —                    |
| L / R pan (CW)       | Deslizador      | Posición panorámica del monitor CW. Aplica paneo de potencia constante tanto al monitor de la radio como al generador de sidetone local. Haga doble clic para recentrar.                                                                                                                                                                  | 50                   | 0–100                | —                    |

### Edición de valor en línea (v0.9.8)

En v0.9.8, las cuatro etiquetas de valor CW (Delay, Speed, Sidetone Volume, Pitch) ahora son widgets QLineEdit con QIntValidator. Haga clic en cualquier valor y escriba un número directamente, luego pulse Enter. El deslizador o control se actualiza para coincidir con el valor escrito. Esto proporciona paridad con SmartSDR para la entrada numérica directa. Los campos editables son:

- **Delay (CW)** — acepta 0–2000
- **Speed (CW)** — acepta 5–100
- **Sidetone volume** — acepta 0–100
- **Pitch < / >** — acepta 100–6000

Cuando está editando activamente un campo, el deslizador deja de actualizar el texto de ese campo hasta que termine de editar, evitando conflictos visuales.

### Comportamiento del Sidetone (v0.9.1+)

El interruptor **Sidetone** y el deslizador **Sidetone volume** controlan tanto el monitor alimentado por DAX de la radio como el generador de sidetone CW de baja latencia del lado del cliente (CwSidetoneGenerator, aproximadamente 10 ms de latencia) de forma sincronizada. En v26.5.3, el sidetone local se enruta a la salida de audio seleccionada por el usuario en lugar de a la salida predeterminada (#2899). No hay un interruptor de sidetone local o un deslizador de volumen independientes. El tono y la panorámica siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio — no se requiere ni está disponible una anulación manual.

El sidetone local es adecuado para transmisiones con paleta, llave recta y generadas por CWX donde la latencia de ida y vuelta de la red haría inutilizable el monitor alimentado por DAX de la radio a velocidades más altas.

El bus de sidetone se comparte con los tonos Quindar. El sidetone y los tonos Quindar son mutuamente excluyentes a nivel de modo.

### Comportamiento de Break-in (v0.9.7)

Las rutas de teclado CW y MIDI ahora respetan completamente la configuración `break_in` de la radio. Con **Breakin** activado (QSK), los flancos de las teclas activan TX y el retardo de break-in mantiene el relé abierto entre elementos. Con **Breakin** desactivado, los caracteres tecleados se ponen en cola y usted activa el PTT manualmente antes de enviar. Se ha eliminado una envolvente de auto-PTT presente en versiones anteriores que enmascaraba el estado Breakin OFF y eliminaba el tiempo de retención QSK.

### Compuerta de recepción del medidor de nivel (v26.5.3)

En v26.5.3, la lógica de supresión del indicador Level durante la recepción se refactorizó en el método dedicado `applyLevelMeterReceiveGate()`. Cuando `met_in_rx` está desactivado y la radio no está transmitiendo, el indicador Level se suprime a -150 dBFS independientemente de la fuente del micrófono. Este método se llama cada vez que cambia el estado de transmisión o el estado MOX, y también cuando se activa o desactiva el modo RADE.

### Inicialización del indicador ALC (v26.5.3)

En v26.5.3, tanto los indicadores ALC del panel Phone como del panel CW se inicializan ahora a -20 dBFS en la construcción usando `setValueImmediate()`. Esto asegura que los indicadores comiencen vacíos cuando el applet aparece por primera vez, en lugar de mostrar un estado indefinido hasta que llegue la primera actualización del medidor desde la radio.

### Actualización del indicador de compresión (v26.5.3)

En v26.5.3, se corrigió la interpretación del indicador Compression. El MeterModel expone COMPPEAK como una cantidad de compresión positiva de 0..25 dB. La cara del indicador P/CW está invertida: 0 = sin compresión, -25 = compresión máxima. El indicador muestra el valor negativo de la compresión, por lo que la aguja o barra se mueve hacia abajo a medida que aumenta la compresión.

### Interacción con el modo RADE (v0.9.7)

Cuando el modo RADE está activo, el deslizador **Mic gain** actúa como un control de ganancia RADE del lado del cliente en lugar de enviar un comando de nivel de micrófono a la radio. El valor del deslizador se almacena bajo la configuración `PcMicGain`, compartida con la ruta de fuente de micrófono PC. La configuración del nivel de micrófono de la radio no se sobrescribe mientras RADE está activo.

El indicador **Level** continúa mostrando el nivel de señal durante RX cuando RADE está activo, independientemente de la configuración `met_in_rx`. Cuando RADE se desactiva, el indicador vuelve al comportamiento de supresión normal y se restablece inmediatamente a -150 dBFS.

### Comportamiento de VOX y atajos de teclado (v0.9.3)

Cuando VOX se activa o desactiva mediante un atajo de teclado, el panel Phone ahora se actualiza inmediatamente para reflejar el nuevo estado de VOX (#2084). En versiones anteriores, el panel no se actualizaba hasta que ocurría algún otro evento de la interfaz de usuario.

### Panel CWX (v0.9.7)

El panel CWX integrado limita sus atajos F1-F12 a la visibilidad del panel (#2464, #2469) para que las asignaciones de teclas F del panel DVK y las teclas rápidas de CWX ya no se activen simultáneamente. Las macros de CWX también liberan TX automáticamente cuando la cola se vacía (#2450, #2507).

## Soporte de temas (v26.6.1)

En v26.6.1, el applet Phone/CW se actualizó para usar el Gestor de Temas para todo el estilo visual. Todos los mangos de deslizadores, etiquetas y botones ahora obtienen sus colores del esquema de colores del tema activo en lugar de valores hexadecimales fijos. El compacto **CwXButton** utilizado en la barra de herramientas CWX ahora usa colores sensibles al tema para su fondo, borde y estado presionado (color de acento).

Cuando cambia el tema de la aplicación a través de `View > Theme`, el applet Phone/CW se actualiza automáticamente. No es necesario reiniciar.

## Consejos

- El valor `PcMicGain` se almacena solo del lado del cliente. Se usa tanto cuando la fuente del micrófono es PC como cuando el modo RADE está activo. Si cambia la fuente del micrófono de PC a otra y vuelve, AetherSDR restaura el valor guardado en lugar de leerlo de la radio.
- Cuando la fuente del micrófono es PC, o cuando el modo RADE está activo, el indicador Level usa la medición del lado del cliente y aparece inmediatamente al conectar, independientemente de la configuración `met_in_rx`.
- El indicador **Compression** lee 0 dB durante RX. Esto es intencional: evita que se muestren lecturas obsoletas de la cadena de TX mientras se recibe.
- Debido a que el tono y la panorámica siempre siguen automáticamente los ajustes de la radio, ajuste el tono CW usando el campo de texto **Pitch < / >** y la panorámica usando el deslizador **L / R pan (CW)** — tanto el monitor de la radio como el sidetone local se actualizan juntos.
- Para escribir un valor CW directamente, haga clic en el número, escriba un valor y pulse Enter. El deslizador se mueve para coincidir.
- El interruptor **Sidetone** activa o desactiva el sidetone local al mismo tiempo que el monitor de la radio. No puede activar uno independientemente del otro.
- Con **Breakin** desactivado, las pulsaciones de teclas se ponen en cola, pero TX no se activa automáticamente. Active el PTT manualmente antes de comenzar a enviar.
- Los indicadores ALC comienzan vacíos (-20 dBFS) cuando el applet aparece por primera vez, así que no se preocupe si no muestran ninguna lectura hasta el primer evento de transmisión.
- Los deslizadores y botones ahora siguen el tema activo. Si tiene problemas para ver los controles, intente cambiar a un tema de mayor contraste a través de `View > Theme`.

## Relacionado

- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal
