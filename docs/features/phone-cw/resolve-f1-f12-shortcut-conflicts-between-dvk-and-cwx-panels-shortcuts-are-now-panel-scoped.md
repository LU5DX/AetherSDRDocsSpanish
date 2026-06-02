# Applet de Teléfono/CW

El applet de Teléfono/CW es un panel de transmisión sensible al modo que muestra controles de micrófono/procesador/monitor en modos de voz y cambia automáticamente a controles de CW (retardo, velocidad, tono local, iámbico, tono) cuando el slice activo está en modo CW. Aparece un indicador ALC tanto en el subpanel de Teléfono como en el de CW, ambos controlados por el medidor ALC por software (MeterModel::swAlcChanged, pico dBFS posterior al medidor SSB), reemplazando la ruta anterior HWALC (voltaje RCA) que producía lecturas sin sentido. Las cuatro etiquetas de valores de CW (Retardo, Velocidad, Volumen del tono local, Tono) ahora son widgets QLineEdit con QIntValidator: haga clic en cualquier valor y escriba un número directamente. El único interruptor de tono local y el control deslizante de volumen controlan tanto el monitor alimentado por DAX de la radio como el tono local de baja latencia del lado del cliente de forma sincronizada: el tono y la panorámica siempre siguen automáticamente los ajustes cw_pitch y mon_pan_cw de la radio. El tono local de CW se enruta a la salida de audio seleccionada por el usuario en lugar de a la salida predeterminada. El indicador de Compresión está controlado por el estado TRANSMITTING del interbloqueo de la radio (no por el flujo del medidor), por lo que lee 0 durante RX; Breakin respeta completamente el ajuste break_in de la radio — ya no hay un sobre de PTT automático que fuerce TX; el bus de tono local se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo). Los accesos directos F1-F12 del panel CWX integrado son controlados por el modo del slice activo a través de MainWindow en lugar de la visibilidad del panel — se activan cuando el slice está en modo CW/CWL independientemente de si el panel es visible, mientras permanecen mutuamente excluyentes con las asignaciones de teclas F del panel DVK. Las macros de CWX también liberan TX automáticamente cuando la cola se vacía.

## Antes de comenzar

- El applet requiere una radio FLEX-8600 conectada que ejecute el firmware 4.2
- El slice activo debe estar en un modo de voz (para el panel de Teléfono) o modo CW (para el panel de CW)

## Abriendo el applet

1. Haga clic en el botón de la bandeja **P/CW** en la barra lateral derecha para abrir el applet de Teléfono/CW.
2. El applet cambia automáticamente entre los paneles de Teléfono y CW según el modo del slice activo.

## Controles de Teléfono

Cuando el slice activo está en un modo de voz, el applet muestra el panel de Teléfono con los siguientes controles:

| Control | Tipo | Rango | Comportamiento |
|---------|------|-------|----------|
| Nivel | Medidor | -40 a +10 dBFS (rojo > 0) | Muestra el nivel pico de entrada del micrófono en dBFS. Se suprime a -150 cuando met_in_rx está desactivado y no está transmitiendo. |
| Compresión | Medidor | -25 a 0 dB (relleno invertido) | Muestra la cantidad de compresión de voz en dB. Controlado por el estado TRANSMITTING del interbloqueo de la radio y la habilitación del procesador de voz: lee 0 dB durante RX para evitar lecturas obsoletas confusas de la cadena de TX. Controlado a través del slot updateCompression(), independiente de la ruta del nivel de micrófono. |
| Perfil de mic | Cuadro combinado | Poblado desde radio micProfileList() | Carga el perfil de procesamiento de micrófono nombrado; llama a TransmitModel::loadMicProfile. |
| Fuente de mic | Cuadro combinado | MIC, BAL, LINE, ACC, PC (más cualquier entrada de micInputList()) | Selecciona la fuente de entrada del micrófono; llama a TransmitModel::setMicSelection. |
| Ganancia de mic | Control deslizante | 0–100 | Ajusta el nivel de entrada del micrófono. Para la fuente "PC" usa la persistencia local PcMicGain. La radio siempre reporta mic_level=0 cuando la fuente=PC; el valor se mantiene del lado del cliente. |
| +ACC | Interruptor | Activado/Desactivado | Habilita la mezcla de entrada de micrófono accesoria; llama a TransmitModel::setMicAcc. |
| PROC | Interruptor | Activado/Desactivado | Activa o desactiva el procesador de voz; llama a TransmitModel::setSpeechProcessorEnable. |
| NOR/DX/DX+ | Control deslizante | 0 (NOR), 1 (DX), 2 (DX+) | Nivel del procesador de tres posiciones; llama a TransmitModel::setSpeechProcessorLevel. |
| DAX | Interruptor | Activado/Desactivado | Habilita DAX como fuente de audio de TX; llama a TransmitModel::setDax. |
| MON | Interruptor | Activado/Desactivado | Habilita el monitor de tono local de TX; llama a TransmitModel::setSbMonitor. |
| Volumen del monitor | Control deslizante | 0–100 | Establece el volumen del monitor de banda lateral; llama a TransmitModel::setMonGainSb. |
| ALC (panel de Teléfono) | Medidor | -20 a 0 dBFS (rojo > -3) | Muestra la lectura de control automático de nivel desde MeterModel::swAlcChanged (pico SSB posterior al ALC por software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, completo a 0 dBFS. Recableado de HWALC (voltaje RCA) al medidor SW ALC. Reflejado por un indicador idéntico en el subpanel de CW. |

## Controles de CW

Cuando el slice activo está en modo CW, el applet muestra el panel de CW con los siguientes controles:

| Control | Tipo | Rango | Comportamiento |
|---------|------|-------|----------|
| Retardo | Control deslizante | 0–2000 ms (paso 10) | Establece el retardo de break-in de CW; llama a TransmitModel::setCwDelay. El QLineEdit adyacente acepta valores escritos (0–2000). |
| Velocidad | Control deslizante | 5–100 WPM | Establece la velocidad de tecleo de CW; llama a TransmitModel::setCwSpeed. El QLineEdit adyacente acepta valores escritos (5–100). |
| Tono local | Interruptor | Activado/Desactivado | Activa o desactiva el monitor de tono local de CW; llama a TransmitModel::setCwSidetone. Controla tanto el monitor alimentado por DAX de la radio como el generador de tono local de baja latencia del lado del cliente de forma sincronizada. Se enruta a la salida de audio seleccionada por el usuario en lugar de a la salida predeterminada. El tono y la panorámica siempre siguen automáticamente los ajustes cw_pitch y mon_pan_cw de la radio. |
| Volumen del tono local | Control deslizante | 0–100 | Establece el volumen del monitor de CW; llama a TransmitModel::setMonGainCw. También establece el volumen del generador de tono local de forma sincronizada. El QLineEdit adyacente acepta valores escritos (0–100). |
| Panorámica L / R | Control deslizante | 0–100 | Establece la panorámica estéreo del monitor de CW; llama a TransmitModel::setMonPanCw y también aplica panorámica de potencia constante al generador de tono local. Doble clic para centrar en 50 (centro). |
| Breakin | Interruptor | Activado/Desactivado | Activa o desactiva el break-in completo (QSK); llama a TransmitModel::setCwBreakIn. Respeta completamente el ajuste break_in de la radio: con Breakin activado (QSK) los bordes de la pulsación activan TX y break_in_delay mantiene el relé; con Breakin desactivado las pulsaciones se ponen en cola y el operador activa PTT manualmente. |
| Iámbico | Interruptor | Activado/Desactivado | Activa o desactiva el manipulador de paletas iámbico; llama a TransmitModel::setCwIambic. |
| Tono < / > | Campo de texto | 100–6000 Hz (paso 10) | QLineEdit con botones < / > (CwTriBtn). Escriba un valor o haga clic en los botones para avanzar en pasos de 10 Hz. Llama a TransmitModel::setCwPitch. |
| ALC (panel de CW) | Medidor | -20 a 0 dBFS (rojo > -3) | Refleja el indicador ALC del panel de Teléfono; ambos leen desde MeterModel::swAlcChanged para lecturas consistentes en voz y CW. Usa el modo HGauge::setFillFromRight. |

## Controles comunes

| Control | Tipo | Rango | Comportamiento |
|---------|------|-------|----------|
| Indicador ALC | Medidor | -20 a 0 dBFS (relleno desde la derecha) | Muestra el control automático de nivel. Tanto los paneles de Teléfono como de CW muestran lecturas ALC idénticas. Ambos indicadores se inicializan a -20 dBFS (vacío) cuando el applet se abre por primera vez. |

## Ámbito de los accesos directos F1-F12

- Los accesos directos F1-F12 del panel CWX integrado son controlados por el modo del slice activo a través de MainWindow (CwxPanel::setShortcutsEnabled) en lugar de la visibilidad del panel — se activan cuando el slice está en modo CW/CWL independientemente de si el panel es visible.
- Las asignaciones de teclas F del panel DVK y las teclas rápidas de CWX son mutuamente excluyentes — no se activan simultáneamente.
- Las macros de CWX liberan TX automáticamente cuando la cola se vacía.

## Notas

- El medidor de nivel se suprime correctamente durante la recepción cuando el usuario desactiva "Medidor de nivel durante recepción" (met_in_rx), independientemente de la fuente del micrófono. El método applyLevelMeterReceiveGate() maneja esto de manera consistente para todas las fuentes de micrófono, incluidas las rutas PC y RADE.
- El indicador de compresión está controlado por el estado TRANSMITTING del interbloqueo de la radio y la habilitación del procesador de voz: lee 0 dB durante RX para evitar lecturas obsoletas confusas de la cadena de TX. Controlado a través del slot updateCompression(), independiente de la ruta del nivel de micrófono. Invierte la visualización: 0 dB = sin compresión, -25 dB = compresión completa.
- Ambos indicadores ALC se inicializan a -20 dBFS (vacío) cuando el applet se construye por primera vez, evitando la visualización de lecturas obsoletas de 0 dBFS durante la fase de renderizado inicial.
- El bus de tono local se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).
