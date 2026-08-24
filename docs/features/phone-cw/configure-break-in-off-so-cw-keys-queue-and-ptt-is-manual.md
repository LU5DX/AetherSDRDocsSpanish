# Applet de Phone/CW

El applet de Phone/CW proporciona un panel de transmisión sensible al modo que cambia automáticamente entre los controles de Phone y CW según el modo de la rodaja activa. En modos de voz, muestra controles de micrófono, procesador y monitor. Cuando la rodaja activa está en modo CW, cambia automáticamente a controles de CW que incluyen retardo, velocidad, tono lateral, iambic y ajustes de tono.

## Abrir el Applet

1. Haga clic en el botón **P/CW** en la barra lateral derecha o confirme que ya es visible en el Panel de Applets.
2. El applet requiere una conexión activa con una radio FLEX-8600.
3. El applet cambia automáticamente entre los subpaneles de Phone y CW según el modo de la rodaja activa.

## Controles del Panel de Phone

El panel de Phone se muestra cuando la rodaja activa está en un modo de voz (LSB, USB, AM, FM, etc.).

### Sección de Micrófono

| Control | Comportamiento | Predeterminado |
|---------|----------|---------|
| **Level** | Muestra el nivel máximo de entrada del micrófono en dBFS. Pase el mouse sobre el indicador para ver la lectura exacta con un decimal (p. ej., "-12.3 dB"). Se suprime a -150 cuando `met_in_rx` está desactivado y no se está transmitiendo. | — |
| **Mic profile** | Selecciona un perfil de procesamiento de micrófono con nombre de los perfiles disponibles en la radio. Llama a `TransmitModel::loadMicProfile`. | — |
| **Mic source** | Selecciona la fuente de entrada del micrófono. Las opciones incluyen MIC, BAL, LINE, ACC, PC, además de cualquier opción de `micInputList()` de la radio. Cuando la radio es modulada por AetherSDR (modulación de host habilitada), el cuadro combinado se limita solo a "PC" y se deshabilita, con una información sobre herramientas que explica que la selección de entrada de la propia radio se realiza en la radio. En v26.8.4, en radios sin entradas de micrófono seleccionables, el modelo se establece explícitamente en PC para coincidir con la interfaz de usuario. Llama a `TransmitModel::setMicSelection`. | — |
| **Mic gain** | Ajusta el nivel de entrada del micrófono. Rango 0-100. Para la fuente 'PC', usa la persistencia local `PcMicGain` ya que la radio siempre informa `mic_level=0` cuando fuente=PC. En v26.8.4, la ganancia local solo se aplica cuando el cliente posee la ganancia (modo PC con entradas seleccionables, o modo RADE). | 50 |
| **+ACC** | Activa la mezcla de entrada del micrófono accesorio. Llama a `TransmitModel::setMicAcc`. | — |

### Sección del Procesador de Voz

| Control | Comportamiento | Predeterminado |
|---------|----------|---------|
| **PROC** | Activa el procesador de voz. Llama a `TransmitModel::setSpeechProcessorEnable`. | — |
| **NOR/DX/DX+** | Deslizador de nivel del procesador de tres posiciones: 0 (NOR), 1 (DX), 2 (DX+). Llama a `TransmitModel::setSpeechProcessorLevel`. | 0 |
| **Compression** | Muestra la cantidad de compresión de voz en dB. Pase el mouse sobre el indicador para ver la lectura de compresión exacta con un decimal (p. ej., "6.5 dB"). Se controla mediante el estado de interbloqueo TRANSMITTING de la radio y la habilitación del procesador de voz: lee 0 dB durante RX. Se acciona mediante `updateCompression()`, independiente de la ruta del nivel de micrófono. Rango -25 a 0 dB (relleno invertido). | — |

### Sección de Enrutamiento de Audio

| Control | Comportamiento | Predeterminado |
|---------|----------|---------|
| **DAX** | Habilita DAX como fuente de audio TX. Llama a `TransmitModel::setDax`. En v26.8.4, este botón se oculta en radios que no admiten DAX TX. | — |
| **MON** | Habilita el monitor de tono lateral TX. Llama a `TransmitModel::setSbMonitor`. | — |
| **Monitor volume** | Establece el volumen del monitor de banda lateral. Llama a `TransmitModel::setMonGainSb`. Rango 0-100. | — |

### Medidor de ALC

| Control | Comportamiento | Rango |
|---------|----------|-------|
| **ALC (panel de Phone)** | Muestra la lectura de control automático de nivel de `MeterModel::swAlcChanged` (pico SSB posterior al ALC de software en dBFS). Pase el mouse sobre el indicador para ver la lectura exacta con un decimal (p. ej., "-8.5 dBFS"). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Zona roja por encima de -3 dBFS. Reconectado de HWALC (voltaje RCA) al medidor de ALC de software en v26.5.1 (#2552). | -20 a 0 dBFS |

## Controles del Panel de CW

El panel de CW se muestra cuando la rodaja activa está en modo CW o CWL.

### Sección de Temporización y Velocidad

| Control | Comportamiento | Predeterminado |
|---------|----------|---------|
| **Breakin** | Activa el break-in completo (QSK). Cuando está activado (QSK), los bordes de las teclas disparan TX y `break_in_delay` mantiene el relé. Cuando está desactivado, las teclas se ponen en cola y el operador activa PTT manualmente. En v0.9.7, las rutas de teclado/MIDI de CW ahora respetan completamente esta configuración: se ha eliminado la envolvente automática de PTT que enmascaraba Breakin OFF y eliminaba el tiempo de retención de QSK. | — |
| **Delay (CW)** | Establece el retardo de break-in de CW en milisegundos. Rango 0-2000 ms (paso 10). El QLineEdit adyacente acepta valores escritos (0–2000) (v0.9.8, #2429). En v0.9.8, `setCwDelay` se corrigió para almacenar en caché el valor inmediatamente para que la emisión de la radio no devuelva el deslizador a su posición (#2428). | 500 ms |
| **Speed (CW)** | Establece la velocidad de tecleo de CW en palabras por minuto. Rango 5-100 WPM. El QLineEdit adyacente acepta valores escritos (5–100) (v0.9.8, #2429). | 20 WPM |

### Sección de Tono Lateral

| Control | Comportamiento | Predeterminado |
|---------|----------|---------|
| **Sidetone** | Activa el monitor de tono lateral de CW. Controla tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente CwSidetoneGenerator (~10 ms de latencia) en sincronía (v0.9.1+). El tono y el paneo siempre siguen automáticamente `cw_pitch` y `mon_pan_cw` de la radio. En v26.5.3, el tono lateral de CW se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). | — |
| **Sidetone volume** | Establece el volumen del monitor de CW. Controla tanto el volumen del lado de la radio (`mon_gain_cw`) como el del tono lateral del lado del cliente en sincronía (v0.9.1+). Rango 0-100. El QLineEdit adyacente acepta valores escritos (0–100) (v0.9.8, #2429). | 50 |
| **L / R pan (CW)** | Establece el paneo estéreo del monitor de CW. Llama a `TransmitModel::setMonPanCw` y aplica paneo de potencia constante al generador de tono lateral local (v0.9.1+). Doble clic para volver a centrar en 50 (centro). Rango 0-100. | 50 |

### Sección de Teclado

| Control | Comportamiento | Predeterminado |
|---------|----------|---------|
| **Iambic** | Activa el manipulador de paleta iambic. Llama a `TransmitModel::setCwIambic`. | — |
| **Pitch < / >** | Establece el tono del tono lateral de CW. QLineEdit con botones < / > (CwTriBtn). Escriba un valor (100–6000) o haga clic en los botones para avanzar en pasos de 10 Hz. Llama a `TransmitModel::setCwPitch` (v0.9.8, #2429). | 600 Hz |

### Medidor de ALC

| Control | Comportamiento | Rango |
|---------|----------|-------|
| **ALC (panel de CW)** | Refleja el indicador de ALC del panel de Phone; ambos leen de `MeterModel::swAlcChanged` para lecturas consistentes entre voz y CW. Pase el mouse sobre el indicador para ver la lectura exacta con un decimal (p. ej., "-8.5 dBFS"). Agregado en v26.5.1 (#2552) como parte de la división del medidor de ALC de software. Usa el modo `HGauge::setFillFromRight`. Zona roja por encima de -3 dBFS. | -20 a 0 dBFS |

## Integración del Panel CWX

Los accesos directos F1-F12 del panel CWX integrado se controlan por el modo de la rodaja activa mediante `MainWindow (CwxPanel::setShortcutsEnabled)` en lugar de la visibilidad del panel: se activan cuando la rodaja está en modo CW/CWL independientemente de si el panel es visible (#2582), mientras permanecen mutuamente excluyentes con los enlaces de tecla F del panel DVK. Las macros CWX también liberan TX automáticamente cuando la cola se vacía (#2450, #2507).

## Notas

- En v26.6.1, todo el estilo del applet usa el sistema de temas. Los deslizadores y etiquetas se adaptan al tema seleccionado en lugar de usar colores codificados.
- El indicador de ALC en ambos paneles se acciona mediante el medidor de ALC de software (`MeterModel::swAlcChanged`, pico SSB posterior en dBFS, #2552), reemplazando la ruta anterior de HWALC (voltaje RCA) que producía lecturas sin significado.
- En v0.9.8, las cuatro etiquetas de valor de CW (Delay, Speed, Sidetone Volume, Pitch) ahora son widgets QLineEdit con QIntValidator: haga clic en cualquier valor y escriba un número directamente (paridad con SmartSDR).
- El bus de tono lateral se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).
- Con Breakin OFF, no se aplica ninguna envolvente automática de PTT. La radio no transmitirá los caracteres en cola hasta que active PTT manualmente. Suelte PTT después de que se envíe el último carácter para volver a RX.
- Si está usando un amplificador externo, Breakin OFF le da tiempo para cerrar el relé T/R del amplificador antes de que el teclado comience a enviar.
- En v26.5.3, el tono lateral de CW se enruta automáticamente al dispositivo de salida de audio seleccionado en la configuración de Audio de AetherSDR, no a la salida predeterminada del sistema. Verifique su selección de salida de audio si no escucha tono lateral.
- En v26.7.4, todos los indicadores (Level, Compression y ambos indicadores de ALC) ahora muestran lecturas numéricas exactas en una ventana emergente al pasar el mouse sobre ellos (#3936). El indicador de Level muestra dB, el indicador de Compression muestra compresión positiva en dB y los indicadores de ALC muestran dBFS, todos con un decimal.
- En v26.7.4, cuando la radio es modulada por AetherSDR (modulación de host habilitada), el cuadro combinado **Mic source** está bloqueado en "PC" y muestra una información sobre herramientas que explica que solo la entrada de micrófono de PC está disponible. Esto evita la confusión de seleccionar tomas de radio inexistentes.
- En v26.8.4, cuando la radio es modulada por AetherSDR (modulación de host habilitada), el cuadro combinado **Mic source** se limita solo a "PC" en lugar de mostrar entradas deshabilitadas para otras fuentes. El modelo se establece explícitamente en estado PC para mantener la radio y la interfaz de usuario consistentes. La información sobre herramientas explica que la selección de entrada de la propia radio se realiza en la radio.
- En v26.8.4, en radios donde el medidor de nivel de micrófono no está disponible, el indicador **Level** se oculta en lugar de mostrar una lectura sin significado.
- En v26.8.4, en radios que no admiten DAX TX, el botón **DAX** se oculta y desmarca.
- En v26.8.4, el applet ahora usa una única verificación compartida de modo CW (`isCwMode()`) que reconoce "CW", "CWU" y "CWL" en todas las marcas de radio, reemplazando la verificación anterior codificada de "CW" que solo coincidía con radios Flex.

## Solución de Problemas

- **La radio transmite inmediatamente cuando se presiona una tecla, incluso con Breakin aparentemente desactivado** — Este era un problema conocido en versiones anteriores a v0.9.7, donde una envolvente automática de PTT anulaba la configuración de Breakin. Confirme que AetherSDR sea v0.9.7 o posterior.
- **El panel de CW no es visible; se muestran los controles de Phone** — El applet cambia al subpanel de CW automáticamente solo cuando la rodaja activa está en un modo CW. Cambie el modo de la rodaja a CW en la radio. En v26.8.4, el applet reconoce los modos CW, CWU y CWL en todas las marcas de radio.
- **El deslizador de Delay vuelve a su posición después de escribir un valor** — Esto se corrigió en v0.9.8 (#2428). El valor ahora se almacena en caché inmediatamente para que la emisión de la radio no fuerce el deslizador a volver.
- **El medidor de ALC muestra una lectura congelada** — En v26.5.3, el medidor de ALC se inicializa a -20 dBFS en la construcción. Si la lectura permanece en -20 dBFS, verifique que la radio esté transmitiendo y que haya señal de audio presente. Pase el mouse sobre el indicador para ver el valor numérico exacto.
- **El medidor de nivel de micrófono muestra -150 dBFS durante RX** — En v26.5.3, el medidor de nivel se suprime durante la recepción cuando la opción "Meter level during receive" está deshabilitada en la configuración de TransmitModel. Para ver el nivel de micrófono durante RX, habilite esa opción.
- **No se escucha tono lateral de CW** — En v26.5.3, verifique que la salida de audio correcta esté seleccionada en la configuración de Audio de AetherSDR. El tono lateral ahora se enruta a la salida de audio del usuario, no a la salida predeterminada del sistema (#2899).
- **Mic source muestra solo PC en una radio Flex** — En v26.8.4, esto es esperado cuando la radio recibe audio de transmisión de la computadora a través de la red. La selección de entrada de la propia radio se realiza en la radio misma, no en AetherSDR.
