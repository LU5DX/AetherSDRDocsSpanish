# Applet de Phone/CW

El applet de Phone/CW es un panel de transmisión sensible al modo. Muestra los controles de Phone (micrófono/compresor/monitor) en modos de voz y cambia automáticamente a controles de CW (retardo, velocidad, sintonía lateral, iámbico, tono) cuando el slice activo está en modo CW.

Un indicador ALC aparece tanto en los subpaneles de Phone como de CW, ambos impulsados por el medidor ALC de software. En la v0.9.8, las cuatro etiquetas de valor de CW (Delay, Speed, Sidetone Volume, Pitch) se convirtieron en widgets QLineEdit con QIntValidator: haga clic en cualquier valor y escriba un número directamente. El interruptor de sintonía lateral y el control deslizante de volumen controlan conjuntamente tanto el monitor alimentado por DAX de la radio como la sintonía lateral de baja latencia del lado del cliente; el tono y la panorámica siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet de Phone/CW muestra controles solo cuando hay una conexión de radio activa.
- El slice activo debe estar en modo CW para que se muestre el subpanel de CW. El subpanel de CW reemplaza automáticamente al subpanel de Phone cuando se selecciona CW en el slice activo.

## Cómo acceder al applet

1. Localice el botón de bandeja **P/CW** en la barra lateral derecha y confirme que el applet esté visible. Si el applet no está visible, haga clic en el botón de bandeja **P/CW** para mostrarlo.
2. Confirme que se muestre el subpanel correcto:
   - Los **controles de Phone** se muestran cuando el slice activo está en un modo de voz (LSB, USB, AM, FM, etc.).
   - Los **controles de CW** se muestran cuando el slice activo está en modo CW, CWU o CWL. Un Flex informa "CW" sin más; un Icom y un HL2 escriben el mismo modo CWU, y CWL es el lado inverso. Los tres controlan este applet.

## Qué hace cada control

### Subpanel de Phone

| Control | Descripción | Rango válido |
|---------|-------------|--------------|
| Indicador de nivel | Muestra el nivel pico de entrada del micrófono en dBFS. Se suprime a -150 cuando `met_in_rx` está desactivado y no se está transmitiendo. | -40 a +10 dBFS (rojo > 0) |
| Indicador de compresión | Muestra la cantidad de compresión de voz en dB. Se activa con el estado TRANSMITTING del interbloqueo de la radio y con el procesador de voz habilitado: lee 0 dB durante la recepción para evitar lecturas obsoletas confusas de la cadena de TX. Se impulsa mediante la nueva ranura updateCompression(), independiente de la ruta del nivel de micrófono. | -25 a 0 dB (relleno invertido) |
| ALC (panel de Phone) | Muestra la lectura del control automático de nivel de MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Comienza en -20 dBFS al inicializar (#2687). Pase el cursor sobre el indicador para ver la lectura dBFS exacta con un decimal (#3936). | -20 a 0 dBFS (rojo > -3). Reconectado de HWALC (voltaje RCA) al medidor ALC de software en v26.5.1 (#2552). Reflejado por un indicador idéntico en el subpanel de CW. |
| Perfil de micrófono | Carga el perfil de procesamiento de micrófono nombrado; llama a TransmitModel::loadMicProfile. | Se completa desde radio micProfileList() |
| Fuente de micrófono | Selecciona la fuente de entrada del micrófono; llama a TransmitModel::setMicSelection. Cuando la radio es modulada por AetherSDR (modulación de host activa), solo se muestra **PC** y el cuadro combinado está deshabilitado. Una información sobre herramientas explica la limitación. | MIC, BAL, LINE, ACC, PC (más cualquier valor de micInputList()). Deshabilitado cuando la modulación de host está activa. |
| Ganancia de micrófono | Ajusta el nivel de entrada del micrófono. Para la fuente 'PC' usa la persistencia local de PcMicGain. | 0-100 |
| +ACC | Habilita la mezcla de entrada de micrófono auxiliar; llama a TransmitModel::setMicAcc. | On / Off |
| PROC | Alterna el procesador de voz; llama a TransmitModel::setSpeechProcessorEnable. | On / Off |
| NOR/DX/DX+ | Nivel de procesador de tres posiciones; llama a TransmitModel::setSpeechProcessorLevel. | 0 (NOR), 1 (DX), 2 (DX+) |
| DAX | Habilita DAX como fuente de audio TX; llama a TransmitModel::setDax. | On / Off |
| MON | Habilita el monitor de sintonía lateral TX; llama a TransmitModel::setSbMonitor. | On / Off |
| Volumen del monitor | Establece el volumen del monitor de banda lateral; llama a TransmitModel::setMonGainSb. | 0-100 |

### Subpanel de CW

| Control | Descripción | Rango válido |
|---------|-------------|--------------|
| Delay (CW) | Establece el retardo de break-in de CW; llama a TransmitModel::setCwDelay. El QLineEdit adyacente acepta valores escritos (0-2000). El QLineEdit usa QIntValidator para restringir la entrada al rango válido. | 0-2000 ms (paso 10) |
| Speed (CW) | Establece la velocidad de tecleo CW; llama a TransmitModel::setCwSpeed. El QLineEdit adyacente acepta valores escritos (5-100). | 5-100 WPM |
| Sidetone | Alterna el monitor de sintonía lateral CW; llama a TransmitModel::setCwSidetone. También habilita/deshabilita el CwSidetoneGenerator de baja latencia del lado del cliente en sincronía. Tanto el monitor alimentado por DAX de la radio como la sintonía lateral local de PortAudio se controlan con este único botón. La sintonía lateral ahora se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). | On / Off |
| Sidetone volume | Establece el volumen del monitor CW; llama a TransmitModel::setMonGainCw. También establece el volumen del generador de sintonía lateral local en sincronía. El QLineEdit adyacente acepta valores escritos (0-100). | 0-100 |
| L / R pan (CW) | Establece la panorámica estéreo del monitor CW; llama a TransmitModel::setMonPanCw y también aplica panorámica de potencia constante al generador de sintonía lateral local. Doble clic para centrar en 50 (centro). | 0-100 |
| Breakin | Alterna el break-in completo (QSK). Con **Breakin** ON, los bordes de tecla activan TX y el retardo de break-in mantiene el relé antes de volver a recibir. Con **Breakin** OFF, los caracteres tecleados se ponen en cola y el operador activa PTT manualmente. | On / Off |
| Iambic | Alterna el manipulador de paleta iámbico; llama a TransmitModel::setCwIambic. | On / Off |
| Pitch < / > | QLineEdit con botones < / > (CwTriBtn). Escriba un valor (100-6000) o haga clic en los botones para avanzar en pasos de 10 Hz. Llama a TransmitModel::setCwPitch. | 100-6000 Hz (paso 10) |
| ALC (panel de CW) | Refleja el indicador ALC del panel de Phone; ambos leen de MeterModel::swAlcChanged para lecturas consistentes entre voz y CW. Usa el modo HGauge::setFillFromRight: vacío a -20 dBFS, se llena hacia la izquierda hasta 0 dBFS. Comienza en -20 dBFS al inicializar (#2687). Pase el cursor sobre el indicador para ver la lectura dBFS exacta con un decimal (#3936). | -20 a 0 dBFS (rojo > -3) |

## Consejos

- Un retardo de 0 ms con **Breakin** habilitado proporciona operación QSK completa. Aumente el retardo para reducir el desgaste del relé durante el envío rápido.
- El control deslizante **Delay (CW)** avanza en incrementos de 10 ms. Para un ajuste fino, haga clic en la pista del control deslizante y use las teclas de flecha (si los atajos de teclado están habilitados en `View > Keyboard Shortcuts`).
- Las pantallas de valor de Delay, Speed, Sidetone Volume y Pitch son widgets QLineEdit editables. Haga clic en cualquier valor para escribir un número preciso y luego presione Enter. El control deslizante se moverá para coincidir.
- Pase el cursor sobre cualquier indicador (Level, Compression o ALC) para ver la lectura numérica exacta con un decimal en una información sobre herramientas emergente. Esto evita tener que estimar el valor solo con la barra.
- Cuando la radio está siendo modulada por AetherSDR (modulación de host activa), el cuadro combinado **Mic source** cambia automáticamente y se bloquea en **PC**. Los otros conectores de entrada de hardware no están disponibles en este modo.

## Notas para v26.8.4

- **Fuente de micrófono reducida cuando la entrada de la radio no es seleccionable por el cliente:** En radios cuyo audio de transmisión proviene de esta computadora (modulación de host), el cuadro combinado **Mic source** ahora muestra solo **PC** — las otras entradas (MIC, BAL, LINE, ACC) se eliminan en lugar de mostrarse atenuadas. Una entrada atenuada aún se lee como "esta radio tiene una entrada de micrófono que podríamos usar", lo cual es engañoso cuando la radio está escuchando su puerto de red. Al modelo se le indica que la selección es PC para que las herramientas posteriores (como radiocert) no adviertan que la captura de audio de transmisión no está en ejecución. Una información sobre herramientas explica: "Esta radio toma audio de transmisión de esta computadora. Su propia selección de entrada se realiza en la radio." Cuando la entrada de la radio es seleccionable por el cliente, la lista completa regresa y el cuadro combinado se vuelve a habilitar.
- **El botón DAX se oculta cuando no es configurable:** La alternancia **DAX** se oculta en radios donde DAX como fuente TX no se puede configurar desde el cliente. Cuando está oculto, el botón se fuerza a un estado desmarcado.
- **Emisión de ganancia de micrófono limitada por propiedad de la fuente:** El valor de ganancia de micrófono se emite al resto del cliente solo cuando el cliente realmente posee la ganancia — es decir, cuando RADE está activo, o cuando la entrada de micrófono de la radio es seleccionable por el cliente y la fuente actual es **PC**. Esto evita que valores de ganancia obsoletos o engañosos se propaguen fuera del applet.

## Notas para v26.7.4

- **Lectura al pasar el cursor sobre los indicadores:** Los cuatro indicadores (Level, Compression, ALC Phone, ALC CW) ahora muestran un valor numérico exacto en una ventana emergente al pasar el cursor del mouse sobre ellos. Los indicadores de Level y Compression muestran valores en dB con un decimal. Los indicadores ALC muestran valores en dBFS con un decimal (#3936).
- **Bloqueo de fuente de micrófono en modulación de host:** Cuando la radio entra en modo de modulación de host (modulada por AetherSDR), el cuadro combinado **Mic source** borra automáticamente todas las entradas excepto **PC**, establece esa entrada como actual y deshabilita el cuadro combinado. Una información sobre herramientas explica que las otras fuentes son conectores de hardware FlexRadio y no están disponibles. Cuando la modulación de host termina, el cuadro combinado vuelve a su comportamiento normal y se vuelve a habilitar.

## Notas para v26.6.1

- **Estilo consciente del tema:** Todos los controles deslizantes del applet de Phone/CW ahora usan una función `applyPrimarySliderStyle()` que respeta el tema activo en lugar de una hoja de estilo codificada. Los botones de alternancia CwTriBtn y las etiquetas QLabel (Delay, Speed) también usan `ThemeManager::applyStyleSheet()` para coloreado consciente del tema. Se ha eliminado la constante `kSliderStyle`. El contenedor del applet usa `theme::setContainer()` para soporte de tema.
- **Color de acento del tema:** El estado presionado de CwTriBtn ahora usa el color de acento del tema (`{{color.accent}}`) en lugar de un `#00b4d8` codificado.

## Notas para v26.5.3

- **Enrutamiento de salida de audio de sintonía lateral CW:** La sintonía lateral CW generada por el CwSidetoneGenerator de baja latencia ahora se enruta a la salida de audio seleccionada por el usuario en lugar del dispositivo de salida predeterminado (#2899). Al configurar la salida de audio, la sintonía lateral seguirá al dispositivo seleccionado.
- **Escala del indicador de compresión corregida:** El indicador de compresión ahora espera una cantidad de compresión positiva de 0-25 dB del MeterModel. La cara del indicador está invertida: 0 representa sin compresión y -25 representa compresión completa. Esto corrige un problema anterior donde el indicador mostraba la dirección incorrecta (#2692).
- **Puerta de recepción del medidor de nivel aplicada consistentemente:** La supresión del medidor de nivel durante la recepción ahora se maneja a través de un método dedicado `applyLevelMeterReceiveGate()`. Esto garantiza que el indicador se suprima correctamente a -150 dBFS en todos los escenarios cuando `met_in_rx` está desactivado y la radio no está transmitiendo, independientemente de la fuente de micrófono o el estado de activación de RADE.
- **Inicialización del indicador ALC:** Ambos indicadores ALC (paneles de Phone y CW) ahora comienzan en -20 dBFS en la carga inicial, proporcionando un estado vacío limpio antes de que lleguen las actualizaciones del medidor (#2687).

## Notas para v26.5.1

- **Reemplazo del medidor ALC de SW:** Ambos indicadores ALC (panel de Phone y panel de CW) ahora leen de MeterModel::swAlcChanged, que proporciona el pico SSB posterior al ALC de software en dBFS. Esto reemplaza la ruta anterior HWALC (voltaje RCA) que producía lecturas sin significado. Los nuevos indicadores usan un rango de -20 a 0 dBFS con visualización de relleno desde la derecha y un umbral rojo a -3 dBFS.
- **Reflejo ALC de doble panel:** El panel de Phone ahora tiene su propio indicador ALC (m_alcGaugePhone) que refleja el indicador ALC del panel de CW (m_alcGaugeCw). Ambos indicadores reciben los mismos datos de la única actualización updateAl
