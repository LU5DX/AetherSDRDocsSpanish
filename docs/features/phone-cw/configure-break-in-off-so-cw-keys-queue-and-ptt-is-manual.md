# Applet de Teléfono/CW

El applet de Teléfono/CW proporciona un panel de transmisión que reconoce el modo y cambia automáticamente entre los controles de Teléfono y CW según el modo del segmento activo. En modos de voz, muestra los controles de micrófono, procesador y monitor. Cuando el segmento activo está en modo CW, cambia automáticamente a controles CW que incluyen retardo, velocidad, tono local, iámbico y ajustes de tono.

## Abrir el Applet

1. Haga clic en el botón **P/CW** en la barra lateral derecha o confirme que ya está visible en el Panel de Applets.
2. El applet requiere una conexión activa a una radio FLEX-8600.
3. El applet cambia automáticamente entre los subpaneles de Teléfono y CW según el modo del segmento activo.

## Controles del Panel de Teléfono

El panel de Teléfono se muestra cuando el segmento activo está en un modo de voz (LSB, USB, AM, FM, etc.).

### Sección de Micrófono

| Control | Comportamiento | Predeterminado |
|---------|----------------|----------------|
| **Nivel** | Muestra el nivel pico de entrada del micrófono en dBFS. Pase el ratón sobre el indicador para ver la lectura exacta con un decimal (ej., "-12.3 dB"). Suprimido a -150 cuando `met_in_rx` está desactivado y no está transmitiendo. | — |
| **Perfil de mic** | Selecciona un perfil de procesamiento de micrófono con nombre de los perfiles disponibles de la radio. Llama a `TransmitModel::loadMicProfile`. | — |
| **Fuente de mic** | Selecciona la fuente de entrada del micrófono. Las opciones incluyen MIC, BAL, LINE, ACC, PC, más cualquier otra de `micInputList()` de la radio. Cuando la radio es modulada por AetherSDR (modulación por host activada), el cuadro combinado se bloquea en "PC" y muestra un tooltip explicando que solo el micrófono de PC está disponible. Llama a `TransmitModel::setMicSelection`. | — |
| **Ganancia de mic** | Ajusta el nivel de entrada del micrófono. Rango 0-100. Para fuente 'PC', usa persistencia local de `PcMicGain` ya que la radio siempre reporta `mic_level=0` cuando la fuente=PC. | 50 |
| **+ACC** | Alterna la mezcla de entrada del micrófono auxiliar. Llama a `TransmitModel::setMicAcc`. | — |

### Sección del Procesador de Voz

| Control | Comportamiento | Predeterminado |
|---------|----------------|----------------|
| **PROC** | Alterna el procesador de voz. Llama a `TransmitModel::setSpeechProcessorEnable`. | — |
| **NOR/DX/DX+** | Control deslizante de nivel del procesador de tres posiciones: 0 (NOR), 1 (DX), 2 (DX+). Llama a `TransmitModel::setSpeechProcessorLevel`. | 0 |
| **Compresión** | Muestra la cantidad de compresión de voz en dB. Pase el ratón sobre el indicador para ver la lectura exacta de compresión con un decimal (ej., "6.5 dB"). Controlado por el estado de interbloqueo TRANSMITTING de la radio y la habilitación del procesador de voz: lee 0 dB durante RX. Impulsado a través de `updateCompression()`, independiente de la ruta del nivel de micrófono. Rango -25 a 0 dB (relleno invertido). | — |

### Sección de Enrutamiento de Audio

| Control | Comportamiento | Predeterminado |
|---------|----------------|----------------|
| **DAX** | Habilita DAX como fuente de audio TX. Llama a `TransmitModel::setDax`. | — |
| **MON** | Habilita el monitor de tono local TX. Llama a `TransmitModel::setSbMonitor`. | — |
| **Volumen del monitor** | Establece el volumen del monitor de banda lateral. Llama a `TransmitModel::setMonGainSb`. Rango 0-100. | — |

### Medidor ALC

| Control | Comportamiento | Rango |
|---------|----------------|-------|
| **ALC (panel de Teléfono)** | Muestra la lectura de control automático de nivel desde `MeterModel::swAlcChanged` (pico SSB post-ALC de software en dBFS). Pase el ratón sobre el indicador para ver la lectura exacta con un decimal (ej., "-8.5 dBFS"). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Zona roja por encima de -3 dBFS. Recableado de HWALC (tensión RCA) al medidor ALC de software en v26.5.1 (#2552). | -20 a 0 dBFS |

## Controles del Panel CW

El panel CW se muestra cuando el segmento activo está en modo CW o CWL.

### Sección de Temporización y Velocidad

| Control | Comportamiento | Predeterminado |
|---------|----------------|----------------|
| **Breakin** | Alterna el break-in completo (QSK). Cuando está ENCENDIDO (QSK), los bordes de la manipulación activan TX y `break_in_delay` mantiene el relé. Cuando está APAGADO, las manipulaciones se ponen en cola y el operador activa PTT manualmente. En v0.9.7, las rutas de teclado/MIDI CW ahora respetan completamente esta configuración — se eliminó la envolvente de PTT automático anterior que anulaba Breakin APAGADO y mataba el tiempo de retención QSK. | — |
| **Retardo (CW)** | Establece el retardo de break-in CW en milisegundos. Rango 0-2000 ms (paso 10). El QLineEdit adyacente acepta valores escritos (0–2000) (v0.9.8, #2429). En v0.9.8, se corrigió `setCwDelay` para almacenar en caché el valor inmediatamente para que la emisión de la radio no devuelva el control deslizante (#2428). | 500 ms |
| **Velocidad (CW)** | Establece la velocidad de manipulación CW en palabras por minuto. Rango 5-100 WPM. El QLineEdit adyacente acepta valores escritos (5–100) (v0.9.8, #2429). | 20 WPM |

### Sección de Tono Local

| Control | Comportamiento | Predeterminado |
|---------|----------------|----------------|
| **Tono local** | Alterna el monitor de tono local CW. Controla tanto el monitor alimentado por DAX de la radio como el generador de tono local de baja latencia del lado del cliente (~10 ms de latencia) de forma sincronizada (v0.9.1+). El tono y la panoramización siempre siguen automáticamente `cw_pitch` y `mon_pan_cw` de la radio. En v26.5.3, el tono local CW se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). | — |
| **Volumen del tono local** | Establece el volumen del monitor CW. Controla tanto el volumen del lado de la radio (`mon_gain_cw`) como el volumen del tono local del lado del cliente de forma sincronizada (v0.9.1+). Rango 0-100. El QLineEdit adyacente acepta valores escritos (0–100) (v0.9.8, #2429). | 50 |
| **Panoramización L / R (CW)** | Establece la panoramización estéreo del monitor CW. Llama a `TransmitModel::setMonPanCw` y aplica panoramización de potencia constante al generador de tono local (v0.9.1+). Doble clic para centrar en 50 (centro). Rango 0-100. | 50 |

### Sección de Manipulación

| Control | Comportamiento | Predeterminado |
|---------|----------------|----------------|
| **Iámbico** | Alterna el manipulador de paletas iámbico. Llama a `TransmitModel::setCwIambic`. | — |
| **Tono < / >** | Establece el tono del tono local CW. QLineEdit con botones < / > (CwTriBtn). Escriba un valor (100–6000) o haga clic en los botones para incrementar en pasos de 10 Hz. Llama a `TransmitModel::setCwPitch` (v0.9.8, #2429). | 600 Hz |

### Medidor ALC

| Control | Comportamiento | Rango |
|---------|----------------|-------|
| **ALC (panel CW)** | Refleja el medidor ALC del panel de Teléfono; ambos leen de `MeterModel::swAlcChanged` para lecturas consistentes en voz y CW. Pase el ratón sobre el indicador para ver la lectura exacta con un decimal (ej., "-8.5 dBFS"). Añadido en v26.5.1 (#2552) como parte de la división del medidor ALC de software. Usa el modo `HGauge::setFillFromRight`. Zona roja por encima de -3 dBFS. | -20 a 0 dBFS |

## Integración del Panel CWX

Los atajos F1-F12 del panel CWX integrado son impulsados por el modo del segmento activo a través de `MainWindow (CwxPanel::setShortcutsEnabled)` en lugar de la visibilidad del panel — se activan cuando el segmento está en modo CW/CWL independientemente de si el panel está visible (#2582), mientras permanecen mutuamente excluyentes con las vinculaciones de tecla F del panel DVK. Las macros CWX también liberan TX automáticamente cuando la cola se vacía (#2450, #2507).

## Notas

- En v26.6.1, todo el estilo del applet usa el sistema de temas. Los controles deslizantes y las etiquetas se adaptan al tema seleccionado en lugar de usar colores fijos.
- El medidor ALC en ambos paneles es impulsado por el medidor ALC de software (`MeterModel::swAlcChanged`, pico SSBMeter post-ALC en dBFS, #2552), reemplazando la ruta HWALC anterior (tensión RCA) que producía lecturas sin sentido.
- En v0.9.8, las cuatro etiquetas de valor CW (Retardo, Velocidad, Volumen de tono local, Tono) ahora son widgets QLineEdit con QIntValidator — haga clic en cualquier valor y escriba un número directamente (paridad SmartSDR).
- El bus de tono local se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).
- Con Breakin APAGADO, no se aplica ninguna envolvente de PTT automático. La radio no transmitirá los caracteres en cola hasta que active PTT manualmente. Suelte PTT después de que se envíe el último carácter para volver a RX.
- Si está usando un amplificador externo, Breakin APAGADO le da tiempo para cerrar el relé T/R del amplificador antes de que el manipulador comience a enviar.
- En v26.5.3, el tono local CW se enruta automáticamente al dispositivo de salida de audio seleccionado en la configuración de Audio de AetherSDR, no a la salida predeterminada del sistema. Verifique su selección de salida de audio si no escucha tono local.
- En v26.7.4, todos los indicadores (Nivel, Compresión y ambos indicadores ALC) ahora muestran lecturas numéricas exactas en una ventana emergente cuando pasa el ratón sobre ellos (#3936). El indicador de Nivel muestra dB, el indicador de Compresión muestra compresión positiva en dB, y los indicadores ALC muestran dBFS — todos con un decimal.
- En v26.7.4, cuando la radio es modulada por AetherSDR (modulación por host activada), el cuadro combinado de **Fuente de mic** se bloquea en "PC" y muestra un tooltip explicando que solo la entrada de micrófono de PC está disponible. Esto evita confusiones al seleccionar conectores de radio inexistentes.

## Solución de Problemas

- **La radio transmite inmediatamente cuando se presiona una tecla, incluso con Breakin aparentemente desactivado** — Este era un problema conocido en versiones anteriores a v0.9.7, donde una envolvente de PTT automático anulaba la configuración de Breakin. Confirme que AetherSDR sea v0.9.7 o posterior.
- **El panel CW no está visible; se muestran los controles de Teléfono** — El applet cambia al subpanel CW automáticamente solo cuando el segmento activo está en un modo CW. Cambie el modo del segmento a CW en la radio.
- **El control deslizante de Retardo vuelve a su lugar después de escribir un valor** — Esto se corrigió en v0.9.8 (#2428). El valor ahora se almacena en caché inmediatamente para que la emisión de la radio no fuerce el control deslizante a volver.
- **El medidor ALC muestra una lectura congelada** — En v26.5.3, el medidor ALC se inicializa a -20 dBFS en la construcción. Si la lectura se mantiene en -20 dBFS, verifique que la radio esté transmitiendo y que haya señal de audio presente. Pase el ratón sobre el indicador para ver el valor numérico exacto.
- **El medidor de nivel de micrófono muestra -150 dBFS durante RX** — En v26.5.3, el medidor de nivel se suprime durante la recepción cuando la opción "Nivel de medidor durante recepción" está deshabilitada en la configuración de TransmitModel. Para ver el nivel de micrófono durante RX, habilite esa opción.
- **No se escucha tono local CW** — En v26.5.3, verifique que la salida de audio correcta esté seleccionada en la configuración de Audio de AetherSDR. El tono local ahora se enruta a la salida de audio del usuario, no a la salida predeterminada del sistema (#2899).
