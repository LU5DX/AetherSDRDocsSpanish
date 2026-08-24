# Applet de Phone/CW

El applet de Phone/CW es un panel de transmisión que se adapta al modo. En modos de voz (SSB, AM, FM) muestra los controles de micrófono, procesador y monitor. Cuando la slice activa está en modo CW, cambia automáticamente a los controles de CW (retardo, velocidad, tono lateral, iámbico, tono).

## Abrir el applet de Phone/CW

Haga clic en el botón de la bandeja **P/CW** en la barra lateral derecha.

## Controles del panel de Phone (modos de voz)

| Control           | Tipo                                                                                                                                                              | Comportamiento                                                                                                                                                                                        |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Level             | Medidor                                                                                                                                                           | Muestra el nivel de pico de entrada del micrófono en dBFS (-40 a +10 dBFS; rojo por encima de 0). Se suprime a -150 dBFS cuando `met_in_rx` está desactivado y no se está transmitiendo, excepto cuando la fuente de micrófono es PC o el modo RADE está activo. Pase el cursor sobre el medidor para ver el nivel exacto en dB con un decimal (v26.7.4+). |
| Compression       | Medidor                                                                                                                                                           | Muestra la cantidad de compresión de voz en dB (-25 a 0 dB, relleno invertido). Se activa con el estado TRANSMITTING del interlock de la radio y la habilitación del procesador de voz: lee 0 dB durante RX (v0.9.7+). Pase el cursor sobre el medidor para ver la cantidad exacta de compresión en dB con un decimal (v26.7.4+). |
| ALC (panel de Phone) | Medidor                                                                                                                                                           | Muestra la lectura del control automático de nivel desde `MeterModel::swAlcChanged` (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Umbral rojo a -3 dBFS. Se inicializa a -20 dBFS al inicio. Se reconectó de HWALC (voltaje RCA) al medidor de ALC de software en v26.5.1 (#2552). Lo refleja un medidor idéntico en el subpanel de CW. Pase el cursor sobre el medidor para ver el valor exacto en dBFS con un decimal (v26.7.4+). |
| Mic profile       | Cuadro combinado                                                                                                                                                  | Carga un perfil de procesamiento de micrófono con nombre desde la radio. Haga clic para seleccionar un perfil; se carga inmediatamente.                                                                                       |
| Mic source        | Cuadro combinado                                                                                                                                                  | Selecciona la fuente de entrada del micrófono: MIC, BAL, LINE, ACC o PC. Llama a `TransmitModel::setMicSelection`. Las fuentes disponibles dependen de las capacidades de la radio: en radios cuyo audio de transmisión no puede seleccionarse desde el cliente (la radio toma el audio de este equipo), el cuadro combinado muestra solo "PC" y está deshabilitado (v26.8.4+). |
| Mic gain          | Deslizador (0-100)                                                                                                                                                | Ajusta el nivel de entrada del micrófono. Para la fuente "PC", utiliza la persistencia local `PcMicGain` (la radio siempre informa mic_level=0 cuando la fuente es PC).                                                       |
| +ACC              | Conmutador                                                                                                                                                        | Habilita la mezcla de entrada del micrófono auxiliar. Llama a `TransmitModel::setMicAcc`.                                                                                                                       |
| PROC              | Conmutador                                                                                                                                                        | Activa o desactiva el procesador de voz. Llama a `TransmitModel::setSpeechProcessorEnable`.                                                                                                                      |
| NOR/DX/DX+        | Deslizador (0=NOR, 1=DX, 2=DX+)                                                                                                                                    | Nivel del procesador de tres posiciones. Llama a `TransmitModel::setSpeechProcessorLevel`.                                                                                                                     |
| DAX               | Conmutador                                                                                                                                                        | Habilita DAX como fuente de audio de TX. Llama a `TransmitModel::setDax`. Se oculta cuando la radio no admite DAX como fuente de TX (v26.8.4+).                                                                         |
| MON               | Conmutador                                                                                                                                                        | Habilita el monitor de tono lateral de TX. Llama a `TransmitModel::setSbMonitor`.                                                                                                                                     |
| Monitor volume    | Deslizador (0-100)                                                                                                                                                | Establece el volumen del monitor de banda lateral. Llama a `TransmitModel::setMonGainSb`.                                                                                                                                  |

### Medidor Level — excepciones de fuente de micrófono PC y modo RADE

Cuando la fuente de micrófono es **PC** o el modo **RADE** está activo, el medidor Level permanece activo durante la recepción (RX) incluso cuando `met_in_rx` está desactivado y la radio no está transmitiendo. Para fuentes de micrófono de hardware (MIC, BAL, LINE, ACC), el medidor se suprime a -150 dBFS durante RX a menos que `met_in_rx` esté activado.

### Medidor Level — lectura al pasar el cursor (v26.7.4+)

Pase el cursor del mouse sobre el medidor Level para ver una ventana emergente con el nivel de pico exacto del micrófono en dB con un decimal (#3936).

### Comportamiento del medidor Compression (v0.9.7+)

El medidor Compression solo muestra un valor en vivo mientras la radio está realmente transmitiendo y el procesador de voz está habilitado. Durante la recepción lee 0 dB. Esto evita lecturas obsoletas y confusas de la cadena de TX.

### Medidor Compression — lectura al pasar el cursor (v26.7.4+)

Pase el cursor del mouse sobre el medidor Compression para ver una ventana emergente con la cantidad exacta de compresión en dB con un decimal (#3936).

### Medidor ALC (panel de Phone)

El medidor ALC muestra el pico SSB posterior al ALC de software en dBFS, leído desde `MeterModel::swAlcChanged`. Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. El umbral rojo está a -3 dBFS. El medidor se inicializa a -20 dBFS al inicio. Este medidor refleja el del panel de CW: ambos leen de la misma fuente para obtener lecturas coherentes en modos de voz y CW.

### Medidor ALC — lectura al pasar el cursor (v26.7.4+)

Pase el cursor del mouse sobre el medidor ALC para ver una ventana emergente con el valor exacto en dBFS con un decimal (#3936).

### Comportamiento del modo RADE (v0.9.7+)

Cuando el modo RADE está activo:
- El deslizador **Mic gain** actúa como control de ganancia RADE del lado del cliente utilizando el ajuste `PcMicGain`. Los cambios en el deslizador no se envían a la radio como comandos `mic_level`.
- El medidor **Level** permanece activo durante RX.
- Cuando RADE se desactiva, el deslizador vuelve a mostrar el valor `mic_level` de la radio y el medidor Level se restablece a -150 dBFS.

### Modulación de host y comportamiento de entrada de micrófono del lado del cliente (v26.8.4+)

Cuando la radio toma el audio de transmisión de este equipo (es decir, el cliente no puede seleccionar la entrada de micrófono de hardware de la radio):
- El cuadro combinado **Mic source** muestra solo "PC" y está deshabilitado. Se eliminó el comportamiento anterior de presentar todos los nombres de conectores FlexRadio (MIC, BAL, LINE, ACC) con una selección no-PC atenuada, porque una entrada "MIC" deshabilitada implicaba incorrectamente que la radio tenía una entrada de micrófono de hardware utilizable.
- Una información sobre herramientas en el cuadro combinado deshabilitado explica: "Esta radio toma el audio de transmisión de este equipo. Su propia selección de entrada se realiza en la radio".
- El cliente aplica inmediatamente la selección de micrófono PC al modelo cuando se activa el modo, de modo que las herramientas posteriores que lean el modelo vean la fuente correcta.
- El medidor **Level** se oculta cuando la radio no tiene entrada de micrófono alimentable por el cliente, para que no pueda mostrar una lectura engañosa siempre en silencio.
- El conmutador **DAX** se oculta en radios que no admiten DAX como fuente de TX.
- Estos estados se gestionan automáticamente y se actualizan inmediatamente cuando cambian las capacidades de la radio.

## Controles del panel de CW

| Control | Tipo | Comportamiento |
|---------|------|----------|
| ALC (panel de CW) | Medidor | Refleja el medidor ALC del panel de Phone. Muestra el pico SSB posterior al ALC de software en dBFS (-20 a 0 dBFS; rojo por encima de -3). Se llena de derecha a izquierda. Se inicializa a -20 dBFS al inicio. Se añadió en v26.5.1 (#2552) como parte de la división del medidor de ALC de software. Pase el cursor sobre el medidor para ver el valor exacto en dBFS con un decimal (v26.7.4+). |
| Delay (CW) | Deslizador (0-2000 ms, paso 10) + QLineEdit | Establece el retardo de break-in de CW. Arrastre el deslizador o haga clic en el valor y escriba un número directamente (0-2000). Llama a `TransmitModel::setCwDelay`. Valor predeterminado: 500. En v0.9.8, se corrigió el almacenamiento en caché del valor para evitar que el deslizador retroceda cuando la radio emite (#2428). |
| Speed (CW) | Deslizador (5-100 WPM) + QLineEdit | Establece la velocidad de tecleo de CW. Arrastre el deslizador o haga clic en el valor y escriba un número directamente (5-100). Llama a `TransmitModel::setCwSpeed`. Valor predeterminado: 20. |
| Sidetone | Conmutador | Activa o desactiva el monitor de tono lateral de CW. Controla tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente (CwSidetoneGenerator, ~10 ms de latencia) de forma sincronizada. Llama a `TransmitModel::setCwSidetone`. En v26.5.3, el tono lateral de CW se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). |
| Sidetone volume | Deslizador (0-100) + QLineEdit | Establece el volumen del monitor de CW tanto para la radio (mon_gain_cw) como para el generador de tono lateral local. Arrastre el deslizador o haga clic en el valor y escriba un número directamente (0-100). Valor predeterminado: 50. |
| L / R pan (CW) | Deslizador (0-100) | Establece el paneo estéreo del monitor de CW. Aplica paneo de potencia constante tanto al lado de la radio como al generador de tono lateral local. Doble clic para centrar en 50 (centro). Valor predeterminado: 50. |
| Breakin | Conmutador | Activa o desactiva el break-in completo (QSK). Llama a `TransmitModel::setCwBreakIn`. Respeta completamente el ajuste break_in de la radio (v0.9.7+): con Breakin activado (QSK), los bordes de tecla activan TX inmediatamente; con Breakin desactivado, las teclas se ponen en cola y el operador activa PTT manualmente. |
| Iambic | Conmutador | Activa o desactiva el manipulador de paleta iámbica. Llama a `TransmitModel::setCwIambic`. |
| Pitch < / > | QLineEdit con botones < / > | Establece el tono del tono lateral de CW. Escriba un valor (100-6000 Hz) o haga clic en los botones para cambiar en pasos de 10 Hz. Llama a `TransmitModel::setCwPitch`. Valor predeterminado: 600. |

### Medidor ALC (panel de CW)

El medidor ALC del panel de CW es idéntico al del panel de Phone. Muestra el pico SSB posterior al ALC de software en dBFS (-20 a 0 dBFS), llenándose de derecha a izquierda con umbral rojo a -3 dBFS. El medidor se inicializa a -20 dBFS al inicio. Ambos medidores leen de la misma fuente `MeterModel::swAlcChanged` para que los operadores vean la misma indicación de ALC independientemente de qué panel esté activo para el modo actual.

### Medidor ALC — lectura al pasar el cursor (v26.7.4+)

Pase el cursor del mouse sobre el medidor ALC para ver una ventana emergente con el valor exacto en dBFS con un decimal (#3936).

### Entrada de valor directa (v0.9.8)

En v0.9.8, las cuatro etiquetas de valor de CW se reemplazaron con widgets QLineEdit que aceptan entrada numérica escrita:

- **Delay (CW):** acepta 0-2000 (milisegundos)
- **Speed (CW):** acepta 5-100 (WPM)
- **Sidetone volume:** acepta 0-100
- **Pitch < / >:** acepta 100-6000 (Hz)

Haga clic en cualquier valor, escriba un número y presione Enter. El deslizador correspondiente se actualiza inmediatamente. El deslizador continúa funcionando como antes; el campo de edición se actualiza desde el deslizador excepto mientras lo está editando.

### Comportamiento del tono lateral (v0.9.1+)

El conmutador único **Sidetone** y el deslizador **Sidetone volume** controlan tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente (CwSidetoneGenerator, ~10 ms de latencia) de forma sincronizada. No hay controles separados de tono lateral local.

El tono y el paneo siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio; no se necesita ni está disponible ninguna anulación manual.

### Enrutamiento del tono lateral (v26.5.3)

En v26.5.3, el tono lateral de CW ahora se enruta a la salida de audio seleccionada por el usuario en lugar de la salida de audio predeterminada (#2899). Configure la salida de audio en **File > Settings > Audio** para elegir dónde se reproduce el tono lateral.

### Uso compartido del bus de tono lateral con tonos Quindar (v0.9.7+)

El bus de audio del tono lateral se comparte con los tonos Quindar. Ambos son mutuamente excluyentes a nivel de modo: los tonos Quindar están activos solo fuera del modo CW, y el generador de tono lateral de CW está activo solo en modo CW. El applet gestiona el cambio automáticamente cuando cambia el modo de la slice activa.

### Comportamiento de Breakin (v0.9.7+)

- **Breakin activado (QSK):** los bordes de tecla activan TX inmediatamente; el retardo de break-in establecido por el deslizador **Delay (CW)** mantiene el relé después del último elemento.
- **Breakin desactivado:** los caracteres tecleados se ponen en cola; el operador activa PTT manualmente para transmitir.

### Detección de modo CW (v26.8.4+)

El panel de CW se activa para cualquiera de las variantes de CW que una radio pueda informar: una FlexRadio informa "CW" simple, mientras que otras radios informan "CWU" para el mismo modo y "CWL" para la variante de banda lateral inversa. Las tres grafías activan el subpanel de CW. No se necesita ninguna acción del usuario.

## Gestión de perfiles de micrófono

Para seleccionar un perfil de micrófono:

1. Abra el applet de Phone/CW.
2. Confirme que la slice activa está en un modo de voz (SSB, AM,
