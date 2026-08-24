# Applet de Phone/CW

El applet de Phone/CW es un panel de transmisión sensible al modo que muestra los controles de micrófono/procesador/monitor en modos de voz y cambia automáticamente a controles de CW (retardo, velocidad, tono de monitorización, iámbico, tono) cuando el slice activo está en modo CW. Un indicador ALC aparece tanto en el subpanel de Phone como en el de CW, ambos impulsados por el medidor ALC de software (MeterModel::swAlcChanged, post-pico SSB en dBFS), reemplazando la ruta anterior de HWALC (voltaje RCA) que producía lecturas sin sentido. Las cuatro etiquetas de valor CW (Retardo, Velocidad, Volumen del tono de monitorización, Tono) ahora son widgets QLineEdit con QIntValidator: haga clic en cualquier valor y escriba un número directamente. El interruptor único de tono de monitorización y el control deslizante de volumen controlan tanto el monitor alimentado por DAX de la radio como el tono de monitorización de baja latencia del lado del cliente de forma sincronizada; el tono y el paneo siguen automáticamente los ajustes cw_pitch y mon_pan_cw de la radio. El tono de monitorización de CW se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada. El indicador de Compresión está controlado por el estado TRANSMITTING del interlock de la radio (no por el flujo del medidor), por lo que lee 0 durante RX; Breakin respeta completamente el ajuste break_in de la radio — ya no hay una envolvente automática de PTT que fuerce TX; el bus de tono de monitorización es compartido con los tonos Quindar (mutuamente excluyentes a nivel de modo). Los atajos F1-F12 del panel CWX integrado están impulsados por el modo del slice activo a través de MainWindow en lugar de la visibilidad del panel: se activan cuando el slice está en modo CW/CWL independientemente de si el panel es visible, manteniéndose mutuamente excluyentes con las asignaciones de teclas F del panel DVK. Las macros de CWX también liberan TX automáticamente cuando la cola se vacía. En v26.7.4, todos los medidores (Nivel, Compresión, ALC) ganaron popups de lectura al pasar el mouse que muestran el valor numérico exacto con un decimal, y el cuadro combinado de fuente de micrófono se bloquea automáticamente en "PC" cuando la modulación del host está activa, ya que las otras fuentes son conectores de hardware FlexRadio. En v26.8.4, el cuadro combinado de fuente de micrófono y el medidor de Nivel ahora son conscientes de las capacidades: en una radio cuyo audio de transmisión no se puede seleccionar desde el cliente (por ejemplo, modulada por red), el cuadro combinado se reduce a una única entrada "PC" con una información sobre herramientas explicativa, el medidor de Nivel está oculto y el botón DAX se elimina.

## Antes de comenzar

- El applet requiere una radio FLEX-8600 conectada que ejecute el firmware 4.2
- El slice activo debe estar en un modo de voz (para el panel de Phone) o en modo CW (para el panel de CW)

## Abrir el applet

1. Haga clic en el botón de la bandeja **P/CW** en la barra lateral derecha para abrir el applet de Phone/CW.
2. El applet cambia automáticamente entre los paneles de Phone y CW según el modo del slice activo.

## Controles de Phone

Cuando el slice activo está en un modo de voz, el applet muestra el panel de Phone con los siguientes controles:

| Control | Tipo | Rango | Comportamiento |
|---------|------|-------|----------|
| Level | Medidor | -40 a +10 dBFS (rojo > 0) | Muestra el nivel pico de entrada del micrófono en dBFS. Se suprime a -150 cuando met_in_rx está desactivado y no se está transmitiendo. Oculto cuando la radio no expone una entrada de micrófono seleccionable por el cliente (consciente de capacidades, v26.8.4). Pase el mouse sobre el indicador para ver el valor exacto con un decimal (v26.7.4). |
| Compression | Medidor | -25 a 0 dB (relleno invertido) | Muestra la cantidad de compresión de voz en dB. Controlado por el estado TRANSMITTING del interlock de la radio y la habilitación del procesador de voz: lee 0 dB durante RX para evitar lecturas obsoletas confusas de la cadena de TX. Impulsado a través de la ranura updateCompression(), independiente de la ruta del nivel de micrófono. Pase el mouse sobre el indicador para ver el valor de compresión como un número positivo en dB (v26.7.4). |
| Mic profile | Cuadro combinado | Poblado desde radio micProfileList() | Carga el perfil de procesamiento de micrófono nombrado; llama a TransmitModel::loadMicProfile. |
| Mic source | Cuadro combinado | MIC, BAL, LINE, ACC, PC (más cualquiera de micInputList()) | Selecciona la fuente de entrada del micrófono; llama a TransmitModel::setMicSelection. Cuando la radio no expone una entrada de micrófono seleccionable por el cliente, este cuadro combinado se reduce a una única entrada "PC" con una información sobre herramientas que explica que la selección de entrada de la radio se realiza en la propia radio (v26.8.4). |
| Mic gain | Control deslizante | 0–100 | Ajusta el nivel de entrada del micrófono. Para la fuente "PC" utiliza la persistencia local PcMicGain. La radio siempre reporta mic_level=0 cuando source=PC; el valor se mantiene del lado del cliente. |
| +ACC | Alternar | On/Off | Habilita la mezcla de entrada del micrófono auxiliar; llama a TransmitModel::setMicAcc. |
| PROC | Alternar | On/Off | Activa o desactiva el procesador de voz; llama a TransmitModel::setSpeechProcessorEnable. |
| NOR/DX/DX+ | Control deslizante | 0 (NOR), 1 (DX), 2 (DX+) | Nivel de procesador de tres posiciones; llama a TransmitModel::setSpeechProcessorLevel. |
| DAX | Alternar | On/Off | Habilita DAX como fuente de audio de TX; llama a TransmitModel::setDax. Oculto cuando la radio no admite DAX como fuente de TX (v26.8.4). |
| MON | Alternar | On/Off | Habilita el monitor de tono de monitorización de TX; llama a TransmitModel::setSbMonitor. |
| Monitor volume | Control deslizante | 0–100 | Establece el volumen del monitor de banda lateral; llama a TransmitModel::setMonGainSb. |
| ALC (panel de Phone) | Medidor | -20 a 0 dBFS (rojo > -3) | Muestra la lectura de control automático de nivel de MeterModel::swAlcChanged (pico SSB post-ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Reconectado de HWALC (voltaje RCA) al medidor ALC de SW. Reflejado por un indicador idéntico en el subpanel de CW. Pase el mouse sobre el indicador para ver el valor exacto en dBFS con un decimal (v26.7.4). |

## Controles de CW

Cuando el slice activo está en modo CW, el applet muestra el panel de CW con los siguientes controles:

| Control | Tipo | Rango | Comportamiento |
|---------|------|-------|----------|
| Delay | Control deslizante | 0–2000 ms (paso 10) | Establece el retardo de break-in de CW; llama a TransmitModel::setCwDelay. El QLineEdit adyacente acepta valores escritos (0–2000). |
| Speed | Control deslizante | 5–100 WPM | Establece la velocidad de manipulación de CW; llama a TransmitModel::setCwSpeed. El QLineEdit adyacente acepta valores escritos (5–100). |
| Sidetone | Alternar | On/Off | Activa o desactiva el monitor de tono de monitorización de CW; llama a TransmitModel::setCwSidetone. Controla tanto el monitor alimentado por DAX de la radio como el CwSidetoneGenerator de baja latencia del lado del cliente de forma sincronizada. Se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada. El tono y el paneo siguen automáticamente los ajustes cw_pitch y mon_pan_cw de la radio. |
| Sidetone volume | Control deslizante | 0–100 | Establece el volumen del monitor de CW; llama a TransmitModel::setMonGainCw. También establece el volumen del generador de tono de monitorización local de forma sincronizada. El QLineEdit adyacente acepta valores escritos (0–100). |
| L / R pan | Control deslizante | 0–100 | Establece el paneo estéreo del monitor de CW; llama a TransmitModel::setMonPanCw y también aplica paneo de potencia constante al generador de tono de monitorización local. Haga doble clic para centrar en 50 (centro). |
| Breakin | Alternar | On/Off | Activa o desactiva el break-in completo (QSK); llama a TransmitModel::setCwBreakIn. Respeta completamente el ajuste break_in de la radio: con Breakin activado (QSK) los flancos de manipulación activan TX y break_in_delay mantiene el relé; con Breakin desactivado las manipulaciones se ponen en cola y el operador activa PTT manualmente. |
| Iambic | Alternar | On/Off | Activa o desactiva la llave de paletas iámbica; llama a TransmitModel::setCwIambic. |
| Pitch < / > | Campo de texto | 100–6000 Hz (paso 10) | QLineEdit con botones < / > (CwTriBtn). Escriba un valor o haga clic en los botones para avanzar en pasos de 10 Hz. Llama a TransmitModel::setCwPitch. |
| ALC (panel de CW) | Medidor | -20 a 0 dBFS (rojo > -3) | Refleja el indicador ALC del panel de Phone; ambos leen de MeterModel::swAlcChanged para lecturas consistentes entre voz y CW. Utiliza el modo HGauge::setFillFromRight. Pase el mouse sobre el indicador para ver el valor exacto en dBFS con un decimal (v26.7.4). |

## Controles comunes

| Control | Tipo | Rango | Comportamiento |
|---------|------|-------|----------|
| Indicador ALC | Medidor | -20 a 0 dBFS (relleno desde la derecha) | Muestra el control automático de nivel. Tanto el panel de Phone como el de CW muestran lecturas ALC idénticas. Ambos indicadores se inicializan a -20 dBFS (vacío) cuando el applet se abre por primera vez. Pase el mouse sobre el indicador para ver el valor exacto con un decimal (v26.7.4). |

## Popups de lectura al pasar el mouse (v26.7.4)

Los tres indicadores de medidor (Nivel, Compresión, ALC en ambos paneles) ahora muestran un popup con el valor numérico exacto al pasar el mouse sobre ellos:

- **Indicador de Nivel**: muestra el nivel pico del micrófono como un número positivo en dB con un decimal (por ejemplo, "-3.5 dB")
- **Indicador de Compresión**: muestra la cantidad de compresión como un número positivo en dB con un decimal (por ejemplo, "12.0 dB") — el indicador almacena el valor como un desplazamiento negativo (-25 a 0), pero el popup lo convierte a una lectura positiva
- **Indicador ALC (ambos paneles)**: muestra el nivel pico SSB exacto en dBFS con un decimal (por ejemplo, "-8.3 dBFS")

## Fuente de micrófono y medidor de Nivel conscientes de capacidades (v26.8.4)

En v26.8.4, el subpanel de Phone se adapta a las capacidades de entrada de audio de la radio:

- **Cuadro combinado de fuente de micrófono**: cuando la radio no expone una entrada de micrófono seleccionable por el cliente (por ejemplo, una radio que solo toma audio de transmisión del puerto de red), el cuadro combinado se reduce de la lista completa de conectores FlexRadio (MIC, BAL, LINE, ACC, PC) a una única entrada "PC". El cuadro combinado está deshabilitado y muestra una información sobre herramientas: "Esta radio toma el audio de transmisión de esta computadora. Su propia selección de entrada se realiza en la radio." El modelo se actualiza para reportar "PC" para que las herramientas posteriores (como radiocert) no adviertan sobre la captura de audio de transmisión.
- **Medidor de Nivel**: oculto por completo cuando la radio no expone una entrada de micrófono seleccionable por el cliente, ya que el cliente no puede medir ni reportar de manera significativa un nivel de micrófono que no controla.
- **Botón DAX**: oculto cuando la radio no admite DAX como fuente de TX.
- Estos cambios están impulsados por notificaciones de capacidades y se aplican inmediatamente cuando las capacidades de la radio cambian.

## Comportamiento de la fuente de micrófono con modulación del host

Cuando la radio está configurada para modulación del host (AetherSDR modula directamente la radio), el cuadro combinado de fuente de micrófono se bloquea automáticamente para mostrar solo "PC" como entrada disponible. El cuadro combinado se deshabilita y muestra una información sobre herramientas que explica que las otras fuentes son conectores de hardware FlexRadio. Esto evita seleccionar entradas no funcionales mientras la radio es modulada por software.

## Alcance de atajos F1-F12

- Los atajos F1-F12 del panel CWX integrado están impulsados por el modo del slice activo a través de MainWindow (CwxPanel::setShortcutsEnabled) en lugar de la visibilidad del panel: se activan cuando el slice está en modo CW/CWL independientemente de si el panel es visible.
- Las asignaciones de teclas F del panel DVK y los atajos de CWX son mutuamente excluyentes — no se activan simultáneamente.
- Las macros de CWX liberan TX automáticamente cuando la cola se vacía.

## Notas

- El medidor de nivel se suprime correctamente durante la recepción cuando el usuario deshabilita "Level Meter During Receive" (met_in_rx), independientemente de la fuente de micrófono. El método applyLevelMeterReceiveGate() maneja esto de manera consistente para todas las fuentes de micrófono, incluidas las rutas PC y RADE.
- El indicador de compresión está controlado por el estado TRANSMITTING del interlock de la radio y la habilitación del procesador de voz: lee 0 dB durante RX para evitar lecturas obsoletas confusas de la cadena de TX. Impulsado a través de la ranura updateCompression(), independiente de la ruta del nivel de micrófono. Invierte la visualización: 0 dB = sin compresión, -25 dB = compresión completa.
- Ambos indicadores ALC se inicializan a -20 dBFS (vacío) cuando el applet se construye por primera vez, evitando la visualización de lecturas obsoletas de 0 dBFS durante la fase de renderizado inicial.
- El bus de tono de monitorización es compartido con los tonos Quindar (mutuamente excluyentes a nivel de modo).
- En v26.8.4, la detección de modo CW utiliza un único helper `isCwMode()` (VoiceModeGate) en lugar de comparaciones de cadenas de modo CW en línea, por lo que el applet reconoce correctamente "CW" (Flex), "CWU" (Icom, HL2) y "CWL" (lado inverso) como modos CW.
- En v26.8.4, el cuadro combinado de fuente de micrófono reconstruido suprime la ruta de señal de intención del operador durante la reconstrucción, por lo que actualizar el cuadro combinado no dispara accidentalmente un comando de radio que podría sobrescribir una selección válida.
