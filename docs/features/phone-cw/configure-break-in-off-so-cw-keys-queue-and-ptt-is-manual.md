# Applet de Phone/CW

El applet de Phone/CW proporciona un panel de transmisión sensible al modo que cambia automáticamente entre controles de Phone y CW según el modo del slice activo. En modos de voz, muestra los controles de micrófono, procesador y monitor. Cuando el slice activo está en modo CW, cambia automáticamente a controles de CW que incluyen retardo, velocidad, tono lateral, iámbico y ajustes de tono.

## Abrir el Applet

1. Haga clic en el botón **P/CW** en la barra lateral derecha o confirme que ya está visible en el Panel de Applets.
2. El applet requiere una conexión activa a una radio FLEX-8600.
3. El applet cambia automáticamente entre subpaneles de Phone y CW según el modo del slice activo.

## Controles del Panel de Phone

El panel de Phone se muestra cuando el slice activo está en un modo de voz (LSB, USB, AM, FM, etc.).

### Sección de Micrófono

| Control | Comportamiento | Valor predeterminado |
|---------|---------------|----------------------|
| **Level** | Muestra el nivel pico de entrada del micrófono en dBFS. Suprimido a -150 cuando `met_in_rx` está desactivado y no se está transmitiendo. | — |
| **Mic profile** | Selecciona un perfil de procesamiento de micrófono con nombre de los perfiles disponibles en la radio. Llama a `TransmitModel::loadMicProfile`. | — |
| **Mic source** | Selecciona la fuente de entrada del micrófono. Las opciones incluyen MIC, BAL, LINE, ACC, PC, más cualquier opción de `micInputList()` de la radio. Llama a `TransmitModel::setMicSelection`. | — |
| **Mic gain** | Ajusta el nivel de entrada del micrófono. Rango 0-100. Para la fuente 'PC', usa persistencia local de `PcMicGain` ya que la radio siempre reporta `mic_level=0` cuando source=PC. | 50 |
| **+ACC** | Alterna la mezcla de entrada del micrófono auxiliar. Llama a `TransmitModel::setMicAcc`. | — |

### Sección del Procesador de Voz

| Control | Comportamiento | Valor predeterminado |
|---------|---------------|----------------------|
| **PROC** | Alterna el procesador de voz. Llama a `TransmitModel::setSpeechProcessorEnable`. | — |
| **NOR/DX/DX+** | Control deslizante de nivel del procesador de tres posiciones: 0 (NOR), 1 (DX), 2 (DX+). Llama a `TransmitModel::setSpeechProcessorLevel`. | 0 |
| **Compression** | Muestra la cantidad de compresión de voz en dB. Bloqueado por el estado de interlock TRANSMITTING de la radio y la habilitación del procesador de voz: lee 0 dB durante RX. Controlado mediante `updateCompression()`, independiente de la ruta del nivel de micrófono. Rango -25 a 0 dB (relleno invertido). | — |

### Sección de Enrutamiento de Audio

| Control | Comportamiento | Valor predeterminado |
|---------|---------------|----------------------|
| **DAX** | Habilita DAX como fuente de audio de TX. Llama a `TransmitModel::setDax`. | — |
| **MON** | Habilita el monitor de tono lateral de TX. Llama a `TransmitModel::setSbMonitor`. | — |
| **Monitor volume** | Establece el volumen del monitor de banda lateral. Llama a `TransmitModel::setMonGainSb`. Rango 0-100. | — |

### Medidor ALC

| Control | Comportamiento | Rango |
|---------|---------------|-------|
| **ALC (panel de Phone)** | Muestra la lectura de control automático de nivel desde `MeterModel::swAlcChanged` (pico de SSB post-ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Zona roja por encima de -3 dBFS. Reconectado desde HWALC (tensión RCA) al medidor SW ALC en v26.5.1 (#2552). | -20 a 0 dBFS |

## Controles del Panel de CW

El panel de CW se muestra cuando el slice activo está en modo CW o CWL.

### Sección de Temporización y Velocidad

| Control | Comportamiento | Valor predeterminado |
|---------|---------------|----------------------|
| **Breakin** | Alterna el break-in completo (QSK). Cuando está ON (QSK), los bordes de la tecla activan TX y `break_in_delay` mantiene el relé. Cuando está OFF, las teclas se ponen en cola y el operador activa PTT manualmente. En v0.9.7, las rutas de teclado CW/MIDI ahora respetan completamente esta configuración — se eliminó la envolvente automática de PTT que enmascaraba Breakin OFF y eliminaba el tiempo de espera de QSK. | — |
| **Delay (CW)** | Establece el retardo de break-in de CW en milisegundos. Rango 0-2000 ms (paso 10). El QLineEdit adyacente acepta valores escritos (0–2000) (v0.9.8, #2429). En v0.9.8, `setCwDelay` se corrigió para almacenar en caché el valor inmediatamente para que la emisión de la radio no devuelva el control deslizante a su lugar (#2428). | 500 ms |
| **Speed (CW)** | Establece la velocidad de tecleo CW en palabras por minuto. Rango 5-100 WPM. El QLineEdit adyacente acepta valores escritos (5–100) (v0.9.8, #2429). | 20 WPM |

### Sección de Tono Lateral

| Control | Comportamiento | Valor predeterminado |
|---------|---------------|----------------------|
| **Sidetone** | Alterna el monitor de tono lateral CW. Controla tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente (~10 ms de latencia) de forma sincronizada (v0.9.1+). El tono y la panorámica siempre siguen automáticamente a `cw_pitch` y `mon_pan_cw` de la radio. En v26.5.3, el tono lateral CW se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). | — |
| **Sidetone volume** | Establece el volumen del monitor CW. Controla tanto el volumen del lado de la radio (`mon_gain_cw`) como el del tono lateral del lado del cliente de forma sincronizada (v0.9.1+). Rango 0-100. El QLineEdit adyacente acepta valores escritos (0–100) (v0.9.8, #2429). | 50 |
| **L / R pan (CW)** | Establece la panorámica estéreo del monitor CW. Llama a `TransmitModel::setMonPanCw` y aplica panorámica de potencia constante al generador de tono lateral local (v0.9.1+). Haga doble clic para volver a centrar en 50 (centro). Rango 0-100. | 50 |

### Sección de Teclado

| Control | Comportamiento | Valor predeterminado |
|---------|---------------|----------------------|
| **Iambic** | Alterna el tecleo iámbico con paddle. Llama a `TransmitModel::setCwIambic`. | — |
| **Pitch < / >** | Establece el tono del tono lateral CW. QLineEdit con botones < / > (CwTriBtn). Escriba un valor (100–6000) o haga clic en los botones para incrementar en pasos de 10 Hz. Llama a `TransmitModel::setCwPitch` (v0.9.8, #2429). | 600 Hz |

### Medidor ALC

| Control | Comportamiento | Rango |
|---------|---------------|-------|
| **ALC (panel de CW)** | Refleja el indicador ALC del panel de Phone; ambos leen de `MeterModel::swAlcChanged` para lecturas consistentes en voz y CW. Agregado en v26.5.1 (#2552) como parte de la división del medidor SW ALC. Usa modo `HGauge::setFillFromRight`. Zona roja por encima de -3 dBFS. | -20 a 0 dBFS |

## Integración del Panel CWX

Los accesos directos F1-F12 del panel CWX incorporado son controlados por el modo del slice activo a través de `MainWindow (CwxPanel::setShortcutsEnabled)` en lugar de la visibilidad del panel — se activan cuando el slice está en modo CW/CWL independientemente de si el panel es visible (#2582), mientras permanecen mutuamente excluyentes con las vinculaciones de teclas F del panel DVK. Las macros CWX también liberan TX automáticamente cuando la cola se vacía (#2450, #2507).

## Notas

- En v26.6.1, todo el estilo del applet usa el sistema de temas. Los controles deslizantes y las etiquetas se adaptan al tema seleccionado en lugar de usar colores codificados.
- El indicador ALC en ambos paneles es controlado por el medidor ALC de software (`MeterModel::swAlcChanged`, pico post-SSBMeter en dBFS, #2552), reemplazando la ruta anterior HWALC (tensión RCA) que producía lecturas sin sentido.
- En v0.9.8, las cuatro etiquetas de valor CW (Delay, Speed, Sidetone Volume, Pitch) ahora son widgets QLineEdit con QIntValidator — haga clic en cualquier valor y escriba un número directamente (paridad con SmartSDR).
- El bus de tono lateral se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).
- Con Breakin OFF, no se aplica ninguna envolvente automática de PTT. La radio no transmitirá los caracteres en cola hasta que active PTT manualmente. Suelte PTT después de que se envíe el último carácter para volver a RX.
- Si está usando un amplificador externo, Breakin OFF le da tiempo para cerrar el relé T/R del amplificador antes de que el tecleador comience a enviar.
- En v26.5.3, el tono lateral CW se enruta automáticamente al dispositivo de salida de audio seleccionado en la configuración de Audio de AetherSDR, no a la salida predeterminada del sistema. Verifique su selección de salida de audio si no escucha tono lateral.

## Solución de Problemas

- **La radio transmite inmediatamente cuando se presiona una tecla, incluso con Breakin aparentemente desactivado** — Este era un problema conocido en versiones anteriores a v0.9.7, donde una envolvente automática de PTT anulaba la configuración de Breakin. Confirme que AetherSDR sea v0.9.7 o posterior.
- **El panel de CW no es visible; se muestran los controles de Phone** — El applet cambia al subpanel CW automáticamente solo cuando el slice activo está en un modo CW. Cambie el modo del slice a CW en la radio.
- **El control deslizante de Delay vuelve a su lugar después de escribir un valor** — Esto se corrigió en v0.9.8 (#2428). El valor ahora se almacena en caché inmediatamente para que la emisión de la radio no fuerce el control deslizante a volver.
- **El medidor ALC muestra una lectura congelada** — En v26.5.3, el medidor ALC se inicializa a -20 dBFS en la construcción. Si la lectura se mantiene en -20 dBFS, verifique que la radio esté transmitiendo y que haya una señal de audio presente.
- **El medidor de nivel de micrófono muestra -150 dBFS durante RX** — En v26.5.3, el medidor de nivel se suprime durante la recepción cuando la opción "Meter level during receive" está deshabilitada en la configuración de TransmitModel. Para ver el nivel de micrófono durante RX, habilite esa opción.
- **No se escucha tono lateral CW** — En v26.5.3, verifique que la salida de audio correcta esté seleccionada en la configuración de Audio de AetherSDR. El tono lateral ahora se enruta a la salida de audio del usuario, no a la salida predeterminada del sistema (#2899).
