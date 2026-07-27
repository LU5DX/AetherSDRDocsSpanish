# Ajustar la ganancia del micrófono y habilitar la mezcla auxiliar

Use esta página para configurar el nivel de entrada del micrófono y mezclar la entrada auxiliar junto con la fuente de micrófono principal en modo Phone.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Phone/CW requiere una conexión activa con la radio.
- El slice activo debe estar en un modo de voz (USB, LSB, AM, FM) para que el subpanel Phone sea visible. Si el slice está en modo CW, se muestra el subpanel CW en su lugar.

## Pasos

1. Abra el applet Phone/CW en el Panel de Applets de la barra lateral derecha. Si no está visible, haga clic en el botón de la bandeja **P/CW**.
2. Localice el cuadro combinado **Mic source**. Confirme que la fuente que desea ajustar esté seleccionada (por ejemplo, MIC, BAL, LINE, ACC o PC).
   - Cuando la modulación por host está activa, el cuadro combinado está deshabilitado y solo muestra "PC". La radio es modulada por AetherSDR, por lo que el micrófono de PC es la única entrada disponible.
3. Arrastre el deslizador **Mic gain** hacia la izquierda o derecha para ajustar el nivel de entrada. La lectura numérica a la derecha del deslizador se actualiza mientras arrastra. El rango válido es 0–100; el valor predeterminado es 50.
   - Cuando **Mic source** está configurado en PC, el valor se almacena del lado del cliente como `PcMicGain`. La radio siempre reporta `mic_level=0` para la fuente PC; AetherSDR conserva el valor localmente.
   - Cuando el modo RADE está activo, el deslizador también actúa como un control de ganancia RADE del lado del cliente y se almacena bajo la misma clave `PcMicGain`. El valor del deslizador no se envía a la radio en este estado.
4. Observe el medidor **Level** sobre los controles. Apunte a picos entre −20 y −10 dBFS durante el habla normal. Pase el cursor sobre el medidor para ver la lectura exacta en dB. El medidor se vuelve rojo por encima de 0 dBFS.
5. Para mezclar la entrada auxiliar junto con la fuente de micrófono activa, haga clic en **+ACC** para que se ilumine. Vuelva a hacer clic para deshabilitar la mezcla.

## Qué hace cada control

| Control               | Qué hace                                                                                                                                                                                                                                                                         | Valor predeterminado                                                                                                      |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| **Mic gain**          | Ajusta el nivel de entrada del micrófono. Cuando Mic source es PC o el modo RADE está activo, el valor se conserva localmente como `PcMicGain` y no se envía a la radio.                                                                                                          | 50                                                                                                                        |
| **+ACC**              | Habilita la mezcla de la entrada de micrófono auxiliar junto con la fuente primaria seleccionada.                                                                                                                                                                                 | —                                                                                                                         |
| Medidor **Level**     | Muestra el nivel pico de entrada del micrófono en dBFS. Pase el cursor sobre el medidor para ver la lectura exacta en dB con un decimal. Se vuelve rojo por encima de 0 dBFS.                                                                                                     | —                                                                                                                         |
| Medidor **Compression** | Muestra la cantidad de compresión de voz que se está aplicando. El llenado es inverso (completamente a la izquierda = 0 dB, sin compresión; completamente a la derecha = -25 dB, compresión máxima). Pase el cursor sobre el medidor para ver la cantidad de compresión en dB con un decimal. En v0.9.7, el medidor está controlado por el estado de interlock TRANSMITTING de la radio y el habilitador del procesador de voz: lee 0 dB durante RX para evitar lecturas obsoletas de la cadena de TX. En v26.5.3, el valor del medidor se invierte con respecto a la visualización anterior: MeterModel expone la compresión como un valor positivo de 0–25 dB, y el medidor lo convierte a la visualización inversa (0 en el borde derecho, -25 en el borde izquierdo). | —                                                                                                                         |
| **ALC (panel Phone)** | Muestra la lectura de control automático de nivel desde MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Pase el cursor sobre el medidor para ver la lectura exacta en dBFS con un decimal. En v26.5.3, el medidor se inicializa a -20 dBFS en la construcción y se establece inmediatamente en su valor mínimo para evitar parpadeos transitorios en la pantalla. | —                                                                                                                         |
| **ALC (panel CW)**    | Refleja el medidor ALC del panel Phone; ambos leen de MeterModel::swAlcChanged para lecturas consistentes tanto en voz como en CW. Pase el cursor sobre el medidor para ver la lectura exacta en dBFS con un decimal. En v26.5.3, el medidor se inicializa a -20 dBFS en la construcción y se establece inmediatamente en su valor mínimo para evitar parpadeos transitorios en la pantalla. | —                                                                                                                         |

## Controles de tono lateral CW

Cuando el slice activo está en modo CW, el subpanel CW reemplaza al subpanel Phone. Los siguientes controles rigen el comportamiento del tono lateral CW.

### Cómo funciona el tono lateral (v0.9.1 y posteriores)

Un único interruptor **Sidetone** y un deslizador **Sidetone volume** controlan tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente (`CwSidetoneGenerator`, aproximadamente 10 ms de latencia) de forma sincronizada. Habilitar o deshabilitar **Sidetone** habilita o deshabilita ambos simultáneamente. Mover **Sidetone volume** establece tanto `mon_gain_cw` en la radio como el volumen del generador local al mismo tiempo.

El tono y la panorámica estéreo siguen automáticamente la configuración `cw_pitch` y `mon_pan_cw` de la radio. No hay controles locales separados de tono o seguimiento.

El bus de tono lateral se comparte con los tonos Quindar; el tono lateral y los tonos Quindar son mutuamente excluyentes a nivel de modo.

### Cambio en v0.9.2.1: controles de tono lateral local separados eliminados

Antes de v0.9.2.1, el subpanel CW incluía un interruptor **Local STn** separado, un deslizador de volumen local, un interruptor de seguimiento de tono **Follow** y un deslizador de tono manual. Estos controles se eliminaron en v0.9.2.1. El interruptor **Sidetone** y el deslizador **Sidetone volume** ahora controlan tanto el tono lateral del lado de la radio como el del lado del cliente juntos, y el tono y la panorámica siempre siguen automáticamente la radio.

Si anteriormente usaba el botón **Local STn** independientemente del interruptor principal **Sidetone**, use el interruptor **Sidetone** en adelante. El generador local de baja latencia permanece disponible y activo siempre que **Sidetone** esté encendido.

### Cambios en v0.9.8: campos de valor QLineEdit

En v0.9.8, las cuatro etiquetas de valor CW (Delay, Speed, Sidetone Volume y Pitch) ahora son campos de texto editables. Haga clic en cualquier valor y escriba un número directamente. El deslizador se mueve para coincidir cuando presiona Enter o tabula para salir. Esto coincide con el comportamiento de SmartSDR.

### Cambios en v26.5.3: enrutamiento de salida de audio de tono lateral

En v26.5.3, el tono lateral CW ahora se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). Esto asegura que el tono lateral se escuche en el mismo dispositivo que ha seleccionado para otras transmisiones de audio, en lugar de usar siempre la salida de audio predeterminada del sistema.

### Cambios en v26.6.1: soporte de temas

En v26.6.1, el applet Phone/CW adopta completamente el sistema de temas de AetherSDR. Todos los elementos visuales — incluidas las ranuras y manijas de los deslizadores, el texto de las etiquetas y los fondos de los botones — ahora usan colores del tema en lugar de valores codificados. El contenedor del applet en sí está estilizado con la clase de tema `applet/digi`, lo que garantiza una apariencia consistente en todos los temas compatibles.

### Cambios en v26.7.4: ventanas emergentes de valor al pasar el cursor sobre los medidores

En v26.7.4, los cuatro medidores en el applet Phone/CW (Level, Compression, ALC Phone y ALC CW) muestran lecturas numéricas exactas cuando pasa el cursor del mouse sobre ellos. Esto le permite leer valores precisos sin tener que estimar en la escala (#3936).

- **Medidor Level**: Pase el cursor para ver el nivel pico exacto del micrófono en dB con un decimal (por ejemplo, "-15.3 dB").
- **Medidor Compression**: Pase el cursor para ver la cantidad de compresión en dB con un decimal (por ejemplo, "8.2 dB"). El valor mostrado es la cantidad absoluta de compresión (positivo), no el desplazamiento negativo utilizado para la visualización.
- **Medidores ALC (Phone y CW)**: Pase el cursor para ver la lectura exacta en dBFS con un decimal (por ejemplo, "-6.3 dBFS").

### Cambios en v26.7.4: detección de modulación por host

En v26.7.4, cuando la modulación por host está activa (la radio es modulada por AetherSDR), el cuadro combinado **Mic source** está deshabilitado y solo muestra "PC" como la fuente disponible. Un tooltip explica que las otras fuentes son conectores FlexRadio y no están disponibles cuando la modulación por host está activa.

### Controles del subpanel CW

| Control | Qué hace | Valor predeterminado | Rango / Valores | Clave de configuración |
|---|---|---|---|---|
| **Delay (CW)** | Establece el retardo de break-in CW. Arrastre el deslizador o haga clic en el campo de valor y escriba un número (0–2000). En v0.9.8, el valor se almacena en caché inmediatamente cuando se escribe para que la emisión de la radio no devuelva el deslizador a su posición (#2428). | 500 ms | 0–2000 ms (paso 10) | — |
| **Speed (CW)** | Establece la velocidad de tecleo CW en palabras por minuto. Arrastre el deslizador o haga clic en el campo de valor y escriba un número (5–100). | 20 WPM | 5–100 WPM | — |
| **Sidetone** | Activa/desactiva el tono lateral CW. Habilita/deshabilita tanto el monitor alimentado por DAX de la radio como el generador de baja latencia del lado del cliente de forma sincronizada. En Windows, la transmisión de tono lateral se inicia inmediatamente al conectar (v0.9.3, #2105). El bus de tono lateral se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo). En v26.5.3, el tono lateral se enruta a la salida de audio seleccionada por el usuario (#2899). | — | On / Off | — |
| **Sidetone volume** | Establece el volumen del monitor CW. Controla tanto `mon_gain_cw` en la radio como el volumen del generador de tono lateral local simultáneamente. Arrastre el deslizador o haga clic en el campo de valor y escriba un número (0–100). | 50 | 0–100 | — |
| **L / R pan (CW)** | Establece la panorámica estéreo del monitor CW. Se aplica tanto al monitor del lado de la radio como al generador de tono lateral local. Haga doble clic para recentrar. | 50 | 0–100 | — |
| **Pitch < / >** | Establece el tono lateral CW y el tono de decodificación. Escriba un valor (100–6000) en el campo de texto o haga clic en los botones < y > para avanzar en pasos de 10 Hz. El tono también se sigue automáticamente desde la configuración `cw_pitch` de la radio. | 600 Hz | 100–6000 Hz (paso 10) | — |
| **Breakin** | Activa/desactiva el break-in completo (QSK). En v0.9.7, el teclado CW y las rutas MIDI respetan completamente esta configuración: con Breakin ON (QSK), los bordes de las teclas activan TX y el retardo de break-in mantiene el relé; con Breakin OFF, las teclas se ponen en cola y el operador activa PTT manualmente. Se ha eliminado la envolvente de PTT automática anterior que enmascaraba Breakin OFF y eliminaba el tiempo de espera de QSK. | — | On / Off | — |
| **Iambic** | Activa/desactiva el manipulador de paletas iámbico. | — | On / Off | — |
| **ALC (panel CW)** | Muestra la lectura de control automático de nivel desde MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Pase el cursor sobre el medidor para ver la lectura exacta en dBFS con un decimal. Refleja el medidor ALC del panel Phone. En v26.5.3, el medidor se inicializa a -20 dBFS en la construcción y se establece inmediatamente en su valor mínimo para evitar parpadeos transitorios en la pantalla. | — | -20 a 0 dBFS (rojo > -3 dBFS) | — |

## Consejos

- El medidor **Level** se suprime a −150 dBFS cuando la radio no está transmitiendo y la monitorización en recepción está desactivada. Esto es normal; el medidor se activa cuando transmite. Cuando **Mic source** está configurado en PC, el medidor utiliza la medición del lado del cliente y no está sujeto a esta supresión — aparece inmediatamente al conectar (v0.9.3, #2086). Cuando el modo RADE está activo, el medidor también utiliza la medición del lado del cliente y está activo durante RX.
- El medidor **Compression** lee 0 dB siempre que la radio no esté en el estado de interlock TRANSMITTING (v0.9.7). Esto evita que aparezcan lecturas obsoletas de la cadena de TX durante RX. El medidor se activa tan pronto como transmite con el procesador de voz habilitado. En v26.5.3, el valor del medidor de compresión se invierte: MeterModel expone la compresión como un valor positivo de 0–25 dB, y el medidor lo convierte a la visualización inversa (0 en el borde derecho, -25 en el borde izquierdo). El medidor ahora muestra correctamente cero compresión a 0 dB y compresión máxima a -25 dB.
- Si usa la fuente PC, tenga en cuenta que el valor `PcMicGain` no se envía a la radio — es gestionado completamente por AetherSDR. Cambiar de la fuente PC y volver restaura el valor guardado. El modo RADE comparte esta misma configuración `PcMicGain`.
- Con **Breakin** desactivado en v0.9.7, las pulsaciones de teclas se ponen en cola y TX no se activa automáticamente. Active PTT manualmente antes de enviar. Si espera una operación QSK completa, confirme que **Breakin** esté iluminado antes de teclear.
- El generador de tono lateral del lado del cliente proporciona aproximadamente 10 ms de latencia, lo cual es útil a velocidades CW más altas donde
