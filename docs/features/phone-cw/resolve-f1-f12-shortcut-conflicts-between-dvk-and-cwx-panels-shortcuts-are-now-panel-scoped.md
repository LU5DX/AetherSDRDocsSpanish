# Applet de Phone/CW

El applet de Phone/CW es un panel de transmisión que reconoce el modo y muestra los controles de micrófono/procesador/monitor en modos de voz y cambia automáticamente a controles de CW (retardo, velocidad, sidetone, iámbico, tono) cuando la franja activa está en modo CW. En ambos subpaneles de Phone y CW aparece un indicador ALC, controlado por el medidor ALC por software (MeterModel::swAlcChanged, pico dBFS post-SSBMeter), reemplazando la ruta anterior HWALC (voltaje RCA) que producía lecturas sin sentido. Las cuatro etiquetas de valores de CW (Retardo, Velocidad, Volumen de Sidetone, Tono) ahora son widgets QLineEdit con QIntValidator: haga clic en cualquier valor y escriba un número directamente. El único conmutador de Sidetone y el control deslizante de volumen accionan tanto el monitor alimentado por DAX de la radio como el sidetone de baja latencia del lado del cliente al unísono; el tono y la panorámica siempre siguen automáticamente la configuración de cw_pitch y mon_pan_cw de la radio. El sidetone de CW se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada. El indicador de Compresión se activa con el estado TRANSMITTING del interlock de la radio (no con el flujo del medidor), por lo que lee 0 durante RX; Breakin respeta completamente la configuración break_in de la radio — ya no hay un sobre de PTT automático que fuerce TX; el bus de sidetone se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo). Los atajos F1-F12 del panel CWX integrado son impulsados por el modo de la franja activa a través de MainWindow en lugar de la visibilidad del panel: se activan cuando la franja está en modo CW/CWL independientemente de si el panel es visible, manteniéndose mutuamente excluyentes con las asignaciones de teclas F del panel DVK. Las macros de CWX también liberan TX automáticamente cuando la cola se vacía. En v26.7.4, todos los medidores (Nivel, Compresión, ALC) obtuvieron ventanas emergentes de lectura al pasar el ratón que muestran el valor numérico exacto con un decimal, y el cuadro combinado de fuente de micrófono se bloquea automáticamente a "PC" cuando la modulación del anfitrión está activa, ya que las otras fuentes son conectores de hardware FlexRadio.

## Antes de comenzar

- El applet requiere una radio FLEX-8600 conectada con firmware 4.2
- La franja activa debe estar en un modo de voz (para el panel de Phone) o modo CW (para el panel de CW)

## Abriendo el applet

1. Haga clic en el botón de la bandeja **P/CW** en la barra lateral derecha para abrir el applet de Phone/CW.
2. El applet cambia automáticamente entre los paneles de Phone y CW según el modo de la franja activa.

## Controles de Phone

Cuando la franja activa está en un modo de voz, el applet muestra el panel de Phone con los siguientes controles:

| Control | Tipo | Rango | Comportamiento |
|---------|------|-------|---------------|
| Level | Medidor | -40 a +10 dBFS (rojo > 0) | Muestra el nivel pico de entrada del micrófono en dBFS. Se suprime a -150 cuando met_in_rx está desactivado y no está transmitiendo. Pase el ratón sobre el indicador para ver el valor exacto con un decimal (v26.7.4). |
| Compression | Medidor | -25 a 0 dB (relleno invertido) | Muestra la cantidad de compresión de voz en dB. Se activa con el estado TRANSMITTING del interlock de la radio y la habilitación del procesador de voz: lee 0 dB durante RX para evitar lecturas obsoletas y confusas de la cadena de TX. Se controla a través del slot updateCompression(), independiente de la ruta del nivel de micrófono. Pase el ratón sobre el indicador para ver el valor de compresión como un número dB positivo (v26.7.4). |
| Mic profile | Cuadro combinado | Poblado desde micProfileList() de la radio | Carga el perfil de procesamiento de micrófono nombrado; llama a TransmitModel::loadMicProfile. |
| Mic source | Cuadro combinado | MIC, BAL, LINE, ACC, PC (más cualquiera de micInputList()) | Selecciona la fuente de entrada del micrófono; llama a TransmitModel::setMicSelection. Cuando la modulación del anfitrión está activa, este cuadro combinado está deshabilitado y solo muestra "PC" con una información sobre herramientas que explica que AetherSDR modula la radio directamente. |
| Mic gain | Control deslizante | 0–100 | Ajusta el nivel de entrada del micrófono. Para la fuente "PC" usa la persistencia local PcMicGain. La radio siempre informa mic_level=0 cuando la fuente=PC; el valor se mantiene del lado del cliente. |
| +ACC | Conmutador | On/Off | Habilita la mezcla de entrada de micrófono accesoria; llama a TransmitModel::setMicAcc. |
| PROC | Conmutador | On/Off | Activa o desactiva el procesador de voz; llama a TransmitModel::setSpeechProcessorEnable. |
| NOR/DX/DX+ | Control deslizante | 0 (NOR), 1 (DX), 2 (DX+) | Nivel de procesador de tres posiciones; llama a TransmitModel::setSpeechProcessorLevel. |
| DAX | Conmutador | On/Off | Habilita DAX como fuente de audio de TX; llama a TransmitModel::setDax. |
| MON | Conmutador | On/Off | Habilita el monitor de sidetone de TX; llama a TransmitModel::setSbMonitor. |
| Monitor volume | Control deslizante | 0–100 | Establece el volumen del monitor de banda lateral; llama a TransmitModel::setMonGainSb. |
| ALC (panel Phone) | Medidor | -20 a 0 dBFS (rojo > -3) | Muestra la lectura de control automático de nivel desde MeterModel::swAlcChanged (pico SSB post-ALC por software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Reconfigurado de HWALC (voltaje RCA) al medidor ALC por software. Reflejado por un indicador idéntico en el subpanel de CW. Pase el ratón sobre el indicador para ver el valor dBFS exacto con un decimal (v26.7.4). |

## Controles de CW

Cuando la franja activa está en modo CW, el applet muestra el panel de CW con los siguientes controles:

| Control | Tipo | Rango | Comportamiento |
|---------|------|-------|---------------|
| Delay | Control deslizante | 0–2000 ms (paso 10) | Establece el retardo de break-in de CW; llama a TransmitModel::setCwDelay. El QLineEdit adyacente acepta valores escritos (0–2000). |
| Speed | Control deslizante | 5–100 WPM | Establece la velocidad de tecleo de CW; llama a TransmitModel::setCwSpeed. El QLineEdit adyacente acepta valores escritos (5–100). |
| Sidetone | Conmutador | On/Off | Activa o desactiva el monitor de sidetone de CW; llama a TransmitModel::setCwSidetone. Controla tanto el monitor alimentado por DAX de la radio como el CwSidetoneGenerator de baja latencia del lado del cliente al unísono. Se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada. El tono y la panorámica siempre siguen automáticamente la configuración de cw_pitch y mon_pan_cw de la radio. |
| Sidetone volume | Control deslizante | 0–100 | Establece el volumen del monitor de CW; llama a TransmitModel::setMonGainCw. También establece el volumen del generador de sidetone local al unísono. El QLineEdit adyacente acepta valores escritos (0–100). |
| L / R pan | Control deslizante | 0–100 | Establece la panorámica estéreo del monitor de CW; llama a TransmitModel::setMonPanCw y también aplica panorámica de potencia constante al generador de sidetone local. Haga doble clic para centrar en 50 (centro). |
| Breakin | Conmutador | On/Off | Activa o desactiva el break-in completo (QSK); llama a TransmitModel::setCwBreakIn. Respeta completamente la configuración break_in de la radio: con Breakin ON (QSK), los bordes de la tecla activan TX y break_in_delay mantiene el relé; con Breakin OFF, las teclas se ponen en cola y el operador activa PTT manualmente. |
| Iambic | Conmutador | On/Off | Activa o desactiva el manipulador de paletas iámbico; llama a TransmitModel::setCwIambic. |
| Pitch < / > | Campo de texto | 100–6000 Hz (paso 10) | QLineEdit con botones < / > (CwTriBtn). Escriba un valor o haga clic en los botones para aumentar o disminuir en 10 Hz. Llama a TransmitModel::setCwPitch. |
| ALC (panel CW) | Medidor | -20 a 0 dBFS (rojo > -3) | Refleja el indicador ALC del panel Phone; ambos leen de MeterModel::swAlcChanged para lecturas consistentes en voz y CW. Usa el modo HGauge::setFillFromRight. Pase el ratón sobre el indicador para ver el valor dBFS exacto con un decimal (v26.7.4). |

## Controles comunes

| Control | Tipo | Rango | Comportamiento |
|---------|------|-------|---------------|
| Indicador ALC | Medidor | -20 a 0 dBFS (relleno desde la derecha) | Muestra el control automático de nivel. Ambos paneles, Phone y CW, muestran lecturas ALC idénticas. Ambos indicadores se inicializan a -20 dBFS (vacíos) cuando el applet se abre por primera vez. Pase el ratón sobre el indicador para ver el valor exacto con un decimal (v26.7.4). |

## Ventanas emergentes de lectura al pasar el ratón (v26.7.4)

Los tres indicadores de medidor (Nivel, Compresión, ALC en ambos paneles) ahora muestran una ventana emergente con el valor numérico exacto cuando pasa el ratón sobre ellos:

- **Indicador de Level**: Muestra el nivel pico del micrófono como un número positivo en dB con un decimal (ej., "-3.5 dB")
- **Indicador de Compression**: Muestra la cantidad de compresión como un número positivo en dB con un decimal (ej., "12.0 dB") — el indicador almacena el valor como un desplazamiento negativo (-25 a 0), pero la ventana emergente lo convierte a una lectura positiva
- **Indicador de ALC (ambos paneles)**: Muestra el nivel pico SSB exacto en dBFS con un decimal (ej., "-8.3 dBFS")

## Comportamiento de la fuente de micrófono con modulación del anfitrión

Cuando la radio está configurada para modulación del anfitrión (AetherSDR modula la radio directamente), el cuadro combinado de fuente de micrófono se bloquea automáticamente para mostrar solo "PC" como entrada disponible. El cuadro combinado se deshabilita y muestra una información sobre herramientas que explica que las otras fuentes son conectores de hardware FlexRadio. Esto evita seleccionar entradas no funcionales mientras la radio es modulada por software.

## Ámbito de los atajos F1-F12

- Los atajos F1-F12 del panel CWX integrado son impulsados por el modo de la franja activa a través de MainWindow (CwxPanel::setShortcutsEnabled) en lugar de la visibilidad del panel: se activan cuando la franja está en modo CW/CWL independientemente de si el panel es visible.
- Las asignaciones de teclas F del panel DVK y las teclas rápidas de CWX son mutuamente excluyentes — no se activan simultáneamente.
- Las macros de CWX liberan TX automáticamente cuando la cola se vacía.

## Notas

- El medidor de nivel se suprime correctamente durante la recepción cuando el usuario desactiva "Level Meter During Receive" (met_in_rx), independientemente de la fuente del micrófono. El método applyLevelMeterReceiveGate() maneja esto de manera consistente para todas las fuentes de micrófono, incluidas las rutas PC y RADE.
- El indicador de compresión se activa con el estado TRANSMITTING del interlock de la radio y la habilitación del procesador de voz: lee 0 dB durante RX para evitar lecturas obsoletas y confusas de la cadena de TX. Se controla a través del slot updateCompression(), independiente de la ruta del nivel de micrófono. Invierte la visualización: 0 dB = sin compresión, -25 dB = compresión completa.
- Ambos indicadores ALC se inicializan a -20 dBFS (vacíos) cuando el applet se construye por primera vez, evitando la visualización de lecturas obsoletas de 0 dBFS durante la fase de renderizado inicial.
- El bus de sidetone se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).
