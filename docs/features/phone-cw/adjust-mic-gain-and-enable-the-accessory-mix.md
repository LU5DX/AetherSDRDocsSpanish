# Ajuste de la ganancia del micrófono y habilitación de la mezcla de accesorio

Use esta página para establecer el nivel de entrada del micrófono y mezclar la entrada de accesorio junto con la fuente de micrófono principal en el modo Phone.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Phone/CW requiere una conexión de radio activa.
- El slice activo debe estar en un modo de voz (USB, LSB, AM, FM) para que el subpanel Phone sea visible. Si el slice está en modo CW, se muestra el subpanel CW en su lugar. Los modos CWU y CWL también se reconocen como modos CW en las radios que los reportan.

## Pasos

1. Abra el applet Phone/CW en el Panel de applets de la barra lateral derecha. Si no está visible, haga clic en el botón de bandeja **P/CW**.
2. Ubique el cuadro combinado **Mic source**. Confirme que la fuente que desea ajustar esté seleccionada (por ejemplo, MIC, BAL, LINE, ACC o PC).
   - Cuando la modulación del host está activa, el cuadro combinado está deshabilitado y muestra solo "PC". La radio es modulada por AetherSDR, por lo que el micrófono de PC es la única entrada disponible.
3. Arrastre el control deslizante **Mic gain** hacia la izquierda o la derecha para establecer el nivel de entrada. La lectura numérica a la derecha del control se actualiza mientras arrastra. El rango válido es 0–100; el valor predeterminado es 50.
   - Cuando **Mic source** está configurado en PC, el valor se almacena en el lado del cliente como `PcMicGain`. La radio siempre reporta `mic_level=0` para la fuente PC; AetherSDR conserva el valor localmente.
   - Cuando el modo RADE está activo, el control deslizante también actúa como un control de ganancia RADE en el lado del cliente y se almacena bajo la misma clave `PcMicGain`. El valor del control deslizante no se envía a la radio en este estado.
4. Observe el medidor **Level** sobre los controles. Apunte a picos entre −20 y −10 dBFS durante el habla normal. Pase el cursor sobre el medidor para ver la lectura exacta en dB. El medidor se pone rojo por encima de 0 dBFS.
5. Para mezclar la entrada de accesorio junto con la fuente de micrófono activa, haga clic en **+ACC** para que se ilumine. Haga clic nuevamente para deshabilitar la mezcla.

## Qué hace cada control

| Control                | Qué hace                                                                                                                                                                                                                                                                            | Valor predeterminado                                                                                                     |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **Mic gain**           | Establece el nivel de entrada del micrófono. Cuando Mic source es PC o el modo RADE está activo, el valor se persiste localmente como `PcMicGain` y no se envía a la radio.                                                                                                          | 50                                                                                                                       |
| **+ACC**               | Habilita la mezcla de entrada de micrófono de accesorio junto con la fuente principal seleccionada.                                                                                                                                                                                 | —                                                                                                                        |
| **Level** (medidor)    | Muestra el nivel de pico de entrada del micrófono en dBFS. Pase el cursor sobre el medidor para ver la lectura exacta en dB con un decimal. Se pone rojo por encima de 0 dBFS. Cuando la radio no puede proporcionar un medidor de nivel de micrófono (por ejemplo, en radios donde el cliente controla la entrada), el medidor se oculta. | —                                                                                                                        |
| **Compression** (medidor) | Muestra la cantidad de compresión de voz que se está aplicando. El relleno está invertido (completamente a la izquierda = 0 dB, sin compresión; completamente a la derecha = -25 dB, compresión máxima). Pase el cursor sobre el medidor para ver la cantidad de compresión en dB con un decimal. En v0.9.7, el medidor está controlado por el estado de interbloqueo TRANSMITTING de la radio y la habilitación del procesador de voz: lee 0 dB durante RX para evitar lecturas obsoletas de la cadena de TX. En v26.5.3, el valor del medidor se invierte con respecto a la visualización anterior: MeterModel expone la compresión como una cantidad positiva de 0–25 dB, y el medidor la convierte a la visualización invertida (0 en el borde derecho, -25 en el borde izquierdo). | —                                                                                                                        |
| **ALC (panel Phone)**  | Muestra la lectura de control automático de nivel de MeterModel::swAlcChanged (pico SSB post-ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Pase el cursor sobre el medidor para ver la lectura exacta en dBFS con un decimal. En v26.5.3, el medidor se inicializa a -20 dBFS en la construcción y se establece inmediatamente a su valor mínimo para evitar parpadeos transitorios en la visualización. | —                                                                                                                        |
| **ALC (panel CW)**     | Refleja el medidor ALC del panel Phone; ambos leen de MeterModel::swAlcChanged para lecturas consistentes entre voz y CW. Pase el cursor sobre el medidor para ver la lectura exacta en dBFS con un decimal. En v26.5.3, el medidor se inicializa a -20 dBFS en la construcción y se establece inmediatamente a su valor mínimo para evitar parpadeos transitorios en la visualización. | —                                                                                                                        |

## Controles de tono lateral CW

Cuando el slice activo está en modo CW (incluyendo CWU y CWL en las radios que los reportan), el subpanel CW reemplaza al subpanel Phone. Los siguientes controles gobiernan el comportamiento del tono lateral CW.

### Cómo funciona el tono lateral (v0.9.1 y posteriores)

Un único interruptor **Sidetone** y un control deslizante **Sidetone volume** controlan tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente (`CwSidetoneGenerator`, aproximadamente 10 ms de latencia) de forma sincronizada. Habilitar o deshabilitar **Sidetone** habilita o deshabilita ambos simultáneamente. Mover **Sidetone volume** establece tanto `mon_gain_cw` en la radio como el volumen del generador local al mismo tiempo.

El tono y la panorámica estéreo siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio. No hay controles locales separados de tono o seguimiento.

El bus de tono lateral se comparte con los tonos Quindar; el tono lateral y los tonos Quindar son mutuamente excluyentes a nivel de modo.

### Cambio en v0.9.2.1: controles locales separados de tono lateral eliminados

Antes de v0.9.2.1, el subpanel CW incluía un interruptor **Local STn** separado, un control deslizante de volumen local, un interruptor **Follow** de seguimiento de tono y un control deslizante de tono manual. Estos controles se eliminaron en v0.9.2.1. El interruptor **Sidetone** y el control deslizante **Sidetone volume** ahora controlan tanto el tono lateral del lado de la radio como el del lado del cliente juntos, y el tono y la panorámica siempre siguen a la radio automáticamente.

Si anteriormente usaba el botón **Local STn** de forma independiente del interruptor principal **Sidetone**, use el interruptor **Sidetone** de ahora en adelante. El generador local de baja latencia permanece disponible y activo siempre que **Sidetone** esté activado.

### Cambios en v0.9.8: campos de valor QLineEdit

En v0.9.8, las cuatro etiquetas de valor CW (Delay, Speed, Sidetone Volume y Pitch) ahora son campos de texto editables. Haga clic en cualquier valor y escriba un número directamente. El control deslizante se mueve para coincidir cuando presiona Enter o hace clic fuera. Esto coincide con el comportamiento de SmartSDR.

### Cambios en v26.5.3: enrutamiento de salida de audio del tono lateral

En v26.5.3, el tono lateral CW ahora se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). Esto garantiza que el tono lateral se escuche en el mismo dispositivo que ha seleccionado para otras transmisiones de audio, en lugar de usar siempre la salida de audio predeterminada del sistema.

### Cambios en v26.6.1: soporte de temas

En v26.6.1, el applet Phone/CW adopta completamente el sistema de temas de AetherSDR. Todos los elementos visuales — incluyendo ranuras y manijas de controles deslizantes, texto de etiquetas y fondos de botones — ahora usan colores del tema en lugar de valores codificados. El contenedor del applet se estiliza con la clase de tema `applet/digi`, garantizando una apariencia consistente en todos los temas compatibles.

### Cambios en v26.7.4: ventanas emergentes de valor al pasar el cursor sobre medidores

En v26.7.4, los cuatro medidores del applet Phone/CW (Level, Compression, ALC Phone y ALC CW) muestran lecturas numéricas exactas al pasar el cursor del mouse sobre ellos. Esto permite leer valores precisos sin tener que estimar contra la escala (#3936).

- **Medidor Level**: pase el cursor para ver el nivel de pico exacto del micrófono en dB con un decimal (por ejemplo, "-15.3 dB").
- **Medidor Compression**: pase el cursor para ver la cantidad de compresión en dB con un decimal (por ejemplo, "8.2 dB"). El valor mostrado es la cantidad absoluta de compresión (positiva), no el desplazamiento negativo usado para la visualización.
- **Medidores ALC (Phone y CW)**: pase el cursor para ver la lectura exacta en dBFS con un decimal (por ejemplo, "-6.3 dBFS").

### Cambios en v26.7.4: detección de modulación del host

En v26.7.4, cuando la modulación del host está activa (la radio es modulada por AetherSDR), el cuadro combinado **Mic source** está deshabilitado y muestra solo "PC" como fuente disponible. Una información sobre herramientas explica que las otras fuentes son tomas de FlexRadio y no están disponibles cuando la modulación del host está activa.

### Cambios en v26.8.4: manejo de fuente de micrófono con conocimiento de capacidades

En v26.8.4, el comportamiento del cuadro combinado **Mic source** ahora tiene conocimiento de capacidades. Cuando la selección de entrada de la radio no se puede controlar desde este cliente (por ejemplo, cuando la radio toma el audio de transmisión de la computadora a través de la conexión de red), el cuadro combinado se reconstruye para mostrar solo "PC" como opción seleccionable. Esto evita la apariencia engañosa de una entrada MIC deshabilitada que podría sugerir que hay una entrada de micrófono de radio disponible cuando no lo está.

Cuando el cuadro combinado se reduce a solo "PC", la información sobre herramientas explica: "Esta radio toma el audio de transmisión de esta computadora. Su propia selección de entrada se realiza en la radio." El modelo también se actualiza para reportar "PC" como la selección activa, de modo que cualquier diagnóstico posterior (como radiocert) refleje la ruta de audio real.

### Controles del subpanel CW

| Control                 | Qué hace                                                                                                                                                                                                                                                                             | Valor predeterminado | Rango / Valores        | Clave de ajuste |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|------------------------|-----------------|
| **Delay (CW)**          | Establece el retardo de break-in CW. Arrastre el control deslizante o haga clic en el campo de valor y escriba un número (0–2000). En v0.9.8, el valor se almacena en caché inmediatamente al escribirlo para que la emisión de la radio no haga que el control deslizante vuelva a su posición (#2428). | 500 ms               | 0–2000 ms (paso 10)   | —               |
| **Speed (CW)**          | Establece la velocidad de tecleo CW en palabras por minuto. Arrastre el control deslizante o haga clic en el campo de valor y escriba un número (5–100).                                                                                                                             | 20 PPM               | 5–100 PPM             | —               |
| **Sidetone**            | Alterna el tono lateral CW. Habilita/deshabilita tanto el monitor alimentado por DAX de la radio como el generador de baja latencia del lado del cliente de forma sincronizada. En Windows, la transmisión de tono lateral se inicia inmediatamente al conectar (v0.9.3, #2105). El bus de tono lateral se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo). En v26.5.3, el tono lateral se enruta a la salida de audio seleccionada por el usuario (#2899). | —                    | On / Off               | —               |
| **Sidetone volume**     | Establece el volumen del monitor CW. Controla tanto `mon_gain_cw` en la radio como el volumen del generador de tono lateral local simultáneamente. Arrastre el control deslizante o haga clic en el campo de valor y escriba un número (0–100).                                                              | 50                   | 0–100                  | —               |
| **L / R pan (CW)**      | Establece la panorámica estéreo del monitor CW. Se aplica tanto al monitor del lado de la radio como al generador local de tono lateral. Haga doble clic para recentrar.                                                                                                              | 50                   | 0–100                  | —               |
| **Pitch < / >**         | Establece el tono del tono lateral y la decodificación CW. Escriba un valor (100–6000) en el campo de texto o haga clic en los botones < y > para avanzar en pasos de 10 Hz. El tono también se sigue automáticamente desde el ajuste `cw_pitch` de la radio.                         | 600 Hz               | 100–6000 Hz (paso 10) | —               |
| **Breakin**             | Alterna el modo full break-in (QSK). En v0.9.7, el teclado CW y las rutas MIDI cumplen completamente este ajuste: con Breakin ON (QSK), los bordes de tecla activan TX y el retardo de break-in mantiene el relé; con Breakin OFF, las teclas se ponen en cola y el operador activa PTT manualmente. El anterior sobre envolvente de auto-PTT que enmascaraba Breakin OFF y eliminaba el tiempo de retención QSK se ha eliminado. | —                    | On / Off               | —               |
| **Iambic**              | Alterna el manipulador de paleta iámbica.                                                                                                                                                                                                                                            | —                    | On / Off               | —               |
| **ALC (panel CW)**      | Muestra la lectura de control automático de nivel de MeterModel::swAlcChanged (pico SSB post-ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Pase el cursor sobre el medidor para ver la lectura exacta en dBFS con un decimal. Refleja el medidor ALC del panel Phone. En v26.5.3, el medidor se inicializa a -20 dBFS en la construcción y se establece inmediatamente a su valor mínimo para evitar parpadeos transitorios en la visualización. | —                    | -20 a 0 dBFS (rojo > -3 dBFS) | —               |

## Consejos

- El medidor **Level** se suprime a −150 dBFS cuando la radio no está transmitiendo y el monitor en recepción está desactivado. Esto es normal; el medidor se activa cuando transmite. Cuando **Mic source** está configurado en PC, el medidor usa la medición del lado del cliente y no está sujeto a esta supresión — aparece inmediatamente al conectar (v0.9.3, #2086). Cuando el modo RADE está activo, el medidor también usa la medición del lado del cliente y está activo durante RX.
- El medidor **Compression** lee 0 dB siempre que la radio no esté en el estado de interbloque
