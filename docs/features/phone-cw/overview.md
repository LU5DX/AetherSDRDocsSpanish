# Descripción general de Phone/CW

El applet Phone/CW es un panel de transmisión sensible al modo que proporciona controles de micrófono, procesador y monitor en modos de voz, y cambia automáticamente a controles CW cuando la franja activa está en un modo CW. Ábralo para ajustar el audio de transmisión o configurar los parámetros de tecleo.

## Cómo funciona

El applet está siempre presente en el Panel de Applets de la barra lateral derecha. Actívelo o desactívelo usando el botón de la bandeja **P/CW**. Contiene dos subpaneles gestionados mediante un diseño apilado:

- **Subpanel Phone** — visible cuando la franja activa está en un modo de voz (SSB, AM, FM y similares).
- **Subpanel CW** — visible cuando la franja activa está en un modo CW.

AetherSDR cambia automáticamente entre subpaneles al cambiar el modo de la franja. No es necesario cambiarlos manualmente.

### Subpanel Phone

| Control          | Tipo         | Función                                                                                                                                                                                                                                                                                                                                                  |
|------------------|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Level            | Medidor      | Muestra el nivel pico de entrada del micrófono en dBFS. Se suprime a -150 cuando met_in_rx está desactivado y no se está transmitiendo. Pase el ratón sobre el medidor para ver el nivel pico exacto en dB con un decimal (#3936).                                                                                                                         |
| Compression      | Medidor      | Muestra la cantidad de compresión de voz en dB. Se activa según el estado TRANSMITTING del interlock de la radio y el procesador de voz: marca 0 dB durante RX para evitar lecturas obsoletas de la cadena de TX. En v26.5.3, el rango del medidor está invertido: 0 = sin compresión, -25 = compresión total. Pase el ratón sobre el medidor para ver la cantidad exacta de compresión en dB (#3936). |
| Mic profile      | Cuadro combinado | Carga el perfil de procesamiento de micrófono desde la lista de perfiles de la radio.                                                                                                                                                                                                                                                               |
| Mic source       | Cuadro combinado | Selecciona la fuente de entrada del micrófono. Cuando la radio es modulada por AetherSDR (modulación host activa), este cuadro combinado está deshabilitado y muestra solo "PC" como fuente disponible, con un tooltip que explica la limitación.                                                                                                      |
| Mic gain         | Deslizador   | Ajusta el nivel de entrada del micrófono. Cuando la fuente es PC, el valor se mantiene en el lado del cliente (almacenado como `PcMicGain`).                                                                                                                                                                                                             |
| +ACC             | Botón de alternancia | Activa la mezcla de entrada del micrófono accesorio.                                                                                                                                                                                                                                                                                               |
| PROC             | Botón de alternancia | Activa o desactiva el procesador de voz.                                                                                                                                                                                                                                                                                                                 |
| NOR/DX/DX+       | Deslizador   | Establece el nivel del procesador de voz. Tres posiciones: NOR (0), DX (1), DX+ (2).                                                                                                                                                                                                                                                                    |
| DAX              | Botón de alternancia | Activa DAX como fuente de audio de TX.                                                                                                                                                                                                                                                                                                                   |
| MON              | Botón de alternancia | Activa el monitor de TX de banda lateral.                                                                                                                                                                                                                                                                                                            |
| Monitor volume   | Deslizador   | Ajusta el volumen del monitor de banda lateral.                                                                                                                                                                                                                                                                                                      |
| ALC (panel Phone)| Medidor      | Muestra la lectura del control automático de nivel desde MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS, rango -20 a 0 dBFS, rojo por encima de -3). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Pase el ratón sobre el medidor para ver el nivel exacto en dBFS con un decimal (#3936). Reconfigurado desde HWALC (tensión RCA) al medidor de ALC de software en v26.5.1 (#2552). En v26.5.3, el medidor se inicializa a -20 dBFS al construirse. Es reflejado por un medidor idéntico en el subpanel CW. |

### Subpanel CW

| Control           | Tipo          | Función                                                                                                                                                                                                                                                                                                                          | Valor pred. | Rango / Opciones       | Clave de configuración |
|-------------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|------------------------|------------------------|
| ALC (panel CW)    | Medidor       | Muestra la lectura del control automático de nivel desde MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS, rango -20 a 0 dBFS, rojo por encima de -3). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Pase el ratón sobre el medidor para ver el nivel exacto en dBFS con un decimal (#3936). En v26.5.3, el medidor se inicializa a -20 dBFS al construirse. Es idéntico al medidor ALC del panel Phone. | —           | -20 a 0 dBFS             | —                      |
| Delay             | Deslizador    | Ajusta el retardo de inserción de CW en milisegundos. El QLineEdit adyacente acepta valores escritos (0–2000). Al escribir un valor y presionar Enter, el deslizador se actualiza para coincidir. El deslizador no retrocede inesperadamente porque el valor se almacena en caché inmediatamente (v0.9.8, #2428).                    | 500         | 0–2000 ms (paso 10)        | —                      |
| Speed             | Deslizador    | Ajusta la velocidad de tecleo CW. El QLineEdit adyacente acepta valores escritos (5–100). Al escribir un valor y presionar Enter, el deslizador se actualiza para coincidir.                                                                                                                                                     | 20          | 5–100 WPM              | —                      |
| Breakin           | Botón de alternancia | Activa o desactiva la inserción completa (QSK). Con Breakin activado, los flancos de tecla activan TX y el retardo de inserción mantiene el relé. Con Breakin desactivado, las teclas se ponen en cola y el operador activa PTT manualmente. El sobre de PTT automático anterior que enmascaraba Breakin desactivado e interfería con el tiempo de retención QSK se eliminó en v0.9.7. | —           | On / Off               | —                      |
| Iambic            | Botón de alternancia | Activa o desactiva el manipulador de paleta iámbica.                                                                                                                                                                                                                                                                             | —           | On / Off               | —                      |
| Pitch < / >       | Campo de texto | QLineEdit con botones < / > (CwTriBtn). Escriba un valor (100–6000) o haga clic en los botones para cambiar en pasos de 10 Hz. Cambia el tono de la señal lateral y el tono de decodificación CW.                                                                                                                                | 600 Hz      | 100–6000 Hz (paso 10) | —                      |
| Sidetone          | Botón de alternancia | Activa o desactiva simultáneamente el monitor de señal lateral CW de la radio (alimentado por DAX) y el generador de señal lateral CW de baja latencia del lado del cliente. En v26.5.3, la señal lateral se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). En Windows, el flujo de señal lateral se inicia inmediatamente al conectar (#2105). | —           | On / Off               | —                      |
| Sidetone volume   | Deslizador    | Ajusta simultáneamente el volumen del monitor CW de la radio (mon_gain_cw) y el volumen del generador de señal lateral del lado del cliente. El QLineEdit adyacente acepta valores escritos (0–100). Al escribir un valor y presionar Enter, el deslizador se actualiza para coincidir.                                             | 50          | 0–100                  | —                      |
| L / R pan (CW)    | Deslizador    | Posición panorámica del monitor CW. Aplica panorámica de potencia constante tanto al monitor de la radio como al generador de señal lateral local. Haga doble clic para recentrar.                                                                                                                                                | 50          | 0–100                  | —                      |

### Edición de valor en línea (v0.9.8)

En v0.9.8, las cuatro etiquetas de valor CW (Delay, Speed, Sidetone Volume, Pitch) son ahora widgets QLineEdit con QIntValidator. Haga clic en cualquier valor y escriba un número directamente, luego presione Enter. El deslizador o control se actualiza para coincidir con el valor escrito. Esto proporciona paridad con SmartSDR para la entrada numérica directa. Los campos editables son:

- **Delay (CW)** — acepta 0–2000
- **Speed (CW)** — acepta 5–100
- **Sidetone volume** — acepta 0–100
- **Pitch < / >** — acepta 100–6000

Mientras está editando activamente un campo, el deslizador deja de actualizar el texto de ese campo hasta que termine de editar, evitando conflictos visuales.

### Comportamiento de la señal lateral (v0.9.1+)

El botón de alternancia **Sidetone** y el deslizador **Sidetone volume** controlan simultáneamente el monitor alimentado por DAX de la radio y el generador de señal lateral CW de baja latencia del lado del cliente (CwSidetoneGenerator, aproximadamente 10 ms de latencia). En v26.5.3, la señal lateral local se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). No hay un botón de alternancia ni un deslizador de volumen separados para la señal lateral local. El tono y la panorámica siempre siguen automáticamente la configuración de `cw_pitch` y `mon_pan_cw` de la radio; no se requiere ni está disponible una anulación manual.

La señal lateral local es adecuada para transmisiones con paleta, manipulador recto y generadas por CWX donde la latencia de ida y vuelta de la red haría inutilizable el monitor alimentado por DAX de la radio a velocidades más altas.

El bus de señal lateral se comparte con los tonos Quindar. La señal lateral y los tonos Quindar son mutuamente excluyentes a nivel de modo.

### Comportamiento de inserción (v0.9.7)

Las rutas de teclado CW y MIDI ahora respetan completamente la configuración `break_in` de la radio. Con **Breakin** activado (QSK), los flancos de tecla activan TX y el retardo de inserción mantiene el relé abierto entre elementos. Con **Breakin** desactivado, los caracteres tecleados se ponen en cola y usted activa PTT manualmente antes de enviar. Se ha eliminado un sobre de PTT automático presente en versiones anteriores que enmascaraba el estado Breakin desactivado y eliminaba el tiempo de retención QSK.

### Puerta de recepción del medidor de nivel (v26.5.3)

En v26.5.3, la lógica de supresión del medidor Level durante la recepción se refactorizó en el método dedicado `applyLevelMeterReceiveGate()`. Cuando `met_in_rx` está desactivado y la radio no está transmitiendo, el medidor Level se suprime a -150 dBFS independientemente de la fuente del micrófono. Este método se llama cada vez que cambia el estado de transmisión o el estado MOX, y también cuando el modo RADE se activa o desactiva.

### Inicialización del medidor ALC (v26.5.3)

En v26.5.3, tanto el medidor ALC del panel Phone como el del panel CW se inicializan ahora a -20 dBFS al construirse usando `setValueImmediate()`. Esto asegura que los medidores comiencen vacíos cuando el applet aparece por primera vez, en lugar de mostrar un estado indefinido hasta que llegue la primera actualización del medidor desde la radio.

### Actualización del medidor de compresión (v26.5.3)

En v26.5.3, se corrigió la interpretación del medidor Compression. MeterModel expone COMPPEAK como una cantidad de compresión positiva de 0..25 dB. La cara del medidor P/CW está invertida: 0 = sin compresión, -25 = compresión total. El medidor muestra el valor negativo del valor de compresión, por lo que la aguja o barra se mueve hacia abajo a medida que aumenta la compresión.

### Interacción con el modo RADE (v0.9.7)

Cuando el modo RADE está activo, el deslizador **Mic gain** actúa como un control de ganancia RADE del lado del cliente en lugar de enviar un comando de nivel de micrófono a la radio. El valor del deslizador se almacena bajo la configuración `PcMicGain`, compartida con la ruta de fuente de micrófono PC. El nivel de micrófono de la radio no se sobrescribe mientras RADE está activo.

El medidor **Level** continúa mostrando el nivel de señal durante RX cuando RADE está activo, independientemente de la configuración `met_in_rx`. Cuando RADE se desactiva, el medidor vuelve al comportamiento de supresión normal y se restablece a -150 dBFS inmediatamente.

### Comportamiento de VOX y atajos de teclado (v0.9.3)

Cuando VOX se activa o desactiva mediante un atajo de teclado, el panel Phone ahora se actualiza inmediatamente para reflejar el nuevo estado de VOX (#2084). En versiones anteriores, el panel no se actualizaba hasta que ocurría algún otro evento de interfaz de usuario.

### Panel CWX (v0.9.7)

El panel CWX incorporado limita sus atajos F1-F12 a la visibilidad del panel (#2464, #2469), por lo que las asignaciones de teclas F del panel DVK y las teclas rápidas de CWX ya no se activan simultáneamente. Las macros de CWX también liberan TX automáticamente cuando la cola se vacía (#2450, #2507).

### Modo de modulación host (v26.7.4)

Cuando la radio es modulada directamente por AetherSDR (modulación host activa), el cuadro combinado **Mic source** está deshabilitado y muestra solo "PC" como entrada disponible. Un tooltip explica que las otras fuentes son conectores físicos de FlexRadio que no están disponibles en este modo. Esto evita confusiones al eliminar la opción de fuentes de entrada inexistentes.

### Lecturas al pasar el ratón sobre los medidores (v26.7.4)

En v26.7.4, los cuatro medidores del applet Phone/CW ahora muestran lecturas numéricas al pasar el cursor del ratón sobre ellos:

- **Level gauge** — muestra el nivel pico exacto del micrófono en dB con un decimal (p. ej., "-12.5 dB")
- **Compression gauge** — muestra la cantidad exacta de compresión en dB con un decimal (p. ej., "8.3 dB")
- **ALC gauge (panel Phone)** — muestra el nivel exacto en dBFS con un decimal (p. ej., "-5.2 dBFS")
- **ALC gauge (panel CW)** — muestra el nivel exacto en dBFS con un decimal (p. ej., "-5.2 dBFS")

Esto le permite leer el valor preciso de cada medidor sin tener que estimar contra las marcas de escala.

## Soporte de temas (v26.6.1)

En v26.6.1, el applet Phone/CW se actualizó para usar el Gestor de Temas para todo el estilo visual. Todos los mangos de deslizadores, etiquetas y botones ahora derivan sus colores del esquema de colores del tema activo en lugar de valores hexadecimales fijos. El **CwXButton** compacto utilizado en la barra de herramientas CWX ahora usa colores conscientes del tema para su fondo, borde y estado presionado (color de acento).

Cuando cambia el tema de la aplicación mediante `View > Theme`, el applet Phone/CW se actualiza
