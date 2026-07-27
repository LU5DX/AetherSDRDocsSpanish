# Applet de Phone/CW

El applet de Phone/CW es un panel de transmisión que reconoce el modo activo. En modos de voz (SSB, AM, FM) muestra los controles de micrófono, procesador y monitor. Cuando el slice activo está en modo CW, cambia automáticamente a los controles de CW (retardo, velocidad, tono lateral, iámbico, tono).

## Abrir el applet de Phone/CW

Haga clic en el botón de bandeja **P/CW** en la barra lateral derecha.

## Controles del panel Phone (modos de voz)

| Control           | Tipo                                                                                                                                                              | Comportamiento                                                                                                                                                                                            |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Level             | Medidor                                                                                                                                                           | Muestra el nivel pico de entrada del micrófono en dBFS (-40 a +10 dBFS; rojo por encima de 0). Se suprime a -150 dBFS cuando `met_in_rx` está desactivado y no se transmite, excepto cuando la fuente de micrófono es PC o el modo RADE está activo. Pase el cursor sobre el indicador para ver el nivel exacto en dB con un decimal (v26.7.4+). |
| Compression       | Medidor                                                                                                                                                           | Muestra la cantidad de compresión de voz en dB (-25 a 0 dB, relleno invertido). Se activa con el estado de TRANSMISIÓN del bloqueo del equipo y la habilitación del procesador de voz: lee 0 dB durante RX (v0.9.7+). Pase el cursor sobre el indicador para ver la cantidad exacta de compresión en dB con un decimal (v26.7.4+). |
| ALC (Panel Phone) | Medidor                                                                                                                                                           | Muestra la lectura de control automático de nivel desde `MeterModel::swAlcChanged` (pico SSB posterior al ALC por software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Umbral rojo a -3 dBFS. Se inicializa a -20 dBFS al inicio. Se reemplazó desde HWALC (voltaje RCA) al medidor ALC por software en v26.5.1 (#2552). Es replicado por un indicador idéntico en el subpanel CW. Pase el cursor sobre el indicador para ver el valor dBFS exacto con un decimal (v26.7.4+). |
| Mic profile       | Cuadro combinado                                                                                                                                                  | Carga un perfil de procesamiento de micrófono nombrado desde el equipo. Haga clic para seleccionar un perfil; se carga inmediatamente.                                                                     |
| Mic source        | Cuadro combinado                                                                                                                                                  | Selecciona la fuente de entrada del micrófono: MIC, BAL, LINE, ACC o PC. Llama a `TransmitModel::setMicSelection`. Cuando la modulación local está habilitada, el cuadro combinado muestra solo "PC" y está deshabilitado (v26.7.4+). |
| Mic gain          | Deslizador (0-100)                                                                                                                                                | Ajusta el nivel de entrada del micrófono. Para la fuente "PC", usa la persistencia local `PcMicGain` (el equipo siempre reporta mic_level=0 cuando source=PC).                                               |
| +ACC              | Alternar                                                                                                                                                          | Habilita la mezcla de entrada de micrófono auxiliar. Llama a `TransmitModel::setMicAcc`.                                                                                                                  |
| PROC              | Alternar                                                                                                                                                          | Alterna el procesador de voz. Llama a `TransmitModel::setSpeechProcessorEnable`.                                                                                                                           |
| NOR/DX/DX+        | Deslizador (0=NOR, 1=DX, 2=DX+)                                                                                                                                   | Nivel de procesador de tres posiciones. Llama a `TransmitModel::setSpeechProcessorLevel`.                                                                                                                  |
| DAX               | Alternar                                                                                                                                                          | Habilita DAX como fuente de audio de TX. Llama a `TransmitModel::setDax`.                                                                                                                                  |
| MON               | Alternar                                                                                                                                                          | Habilita el monitor de tono lateral de TX. Llama a `TransmitModel::setSbMonitor`.                                                                                                                           |
| Monitor volume    | Deslizador (0-100)                                                                                                                                                | Establece el volumen del monitor de banda lateral. Llama a `TransmitModel::setMonGainSb`.                                                                                                                   |

### Indicador Level — excepciones de fuente de micrófono PC y RADE

Cuando la fuente de micrófono es **PC** o el modo **RADE** está activo, el indicador Level permanece activo durante la recepción (RX) incluso cuando `met_in_rx` está desactivado y el equipo no está transmitiendo. Para fuentes de micrófono de hardware (MIC, BAL, LINE, ACC), el indicador se suprime a -150 dBFS durante RX a menos que `met_in_rx` esté activado.

### Indicador Level — lectura al pasar el cursor (v26.7.4+)

Pase el cursor del mouse sobre el indicador Level para ver una ventana emergente que muestra el nivel pico exacto del micrófono en dB con un decimal (#3936).

### Comportamiento del indicador Compression (v0.9.7+)

El indicador Compression solo muestra un valor en vivo mientras el equipo está realmente transmitiendo y el procesador de voz está habilitado. Durante la recepción, lee 0 dB. Esto evita lecturas obsoletas y confusas de la cadena de TX.

### Indicador Compression — lectura al pasar el cursor (v26.7.4+)

Pase el cursor del mouse sobre el indicador Compression para ver una ventana emergente que muestra la cantidad exacta de compresión en dB con un decimal (#3936).

### Indicador ALC (Panel Phone)

El indicador ALC muestra el pico SSB posterior al ALC por software en dBFS, leído desde `MeterModel::swAlcChanged`. Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. El umbral rojo está a -3 dBFS. El indicador se inicializa a -20 dBFS al inicio. Este indicador replica el del panel CW; ambos leen de la misma fuente para obtener lecturas consistentes en todos los modos de voz y CW.

### Indicador ALC — lectura al pasar el cursor (v26.7.4+)

Pase el cursor del mouse sobre el indicador ALC para ver una ventana emergente que muestra el valor dBFS exacto con un decimal (#3936).

### Comportamiento del modo RADE (v0.9.7+)

Cuando el modo RADE está activo:
- El deslizador **Mic gain** actúa como un control de ganancia RADE del lado del cliente usando la configuración `PcMicGain`. Los cambios en el deslizador no se envían al equipo como comandos `mic_level`.
- El indicador **Level** permanece activo durante RX.
- Cuando RADE se desactiva, el deslizador vuelve a mostrar el valor `mic_level` del equipo y el indicador Level se restablece a -150 dBFS.

### Comportamiento de la modulación local (v26.7.4+)

Cuando el equipo está modulado por AetherSDR (modulación local habilitada):
- El cuadro combinado **Mic source** está deshabilitado y muestra solo "PC"; no hay otras opciones de fuente disponibles.
- Una información sobre herramientas en el cuadro combinado explica que el micrófono del PC es la única entrada porque las otras fuentes son conectores del equipo FlexRadio.
- Esto se gestiona automáticamente; no se requiere ninguna acción del usuario.

## Controles del panel CW

| Control | Tipo | Comportamiento |
|---------|------|----------------|
| ALC (Panel CW) | Medidor | Replica el indicador ALC del panel Phone. Muestra el pico SSB posterior al ALC por software en dBFS (-20 a 0 dBFS; rojo por encima de -3). Se llena de derecha a izquierda. Se inicializa a -20 dBFS al inicio. Añadido en v26.5.1 (#2552) como parte de la división del medidor ALC por software. Pase el cursor sobre el indicador para ver el valor dBFS exacto con un decimal (v26.7.4+). |
| Delay (CW) | Deslizador (0-2000 ms, paso 10) + QLineEdit | Establece el retardo de ruptura CW. Arrastre el deslizador o haga clic en el valor y escriba un número directamente (0-2000). Llama a `TransmitModel::setCwDelay`. Valor predeterminado: 500. En v0.9.8, se corrigió el almacenamiento en caché del valor para evitar que el deslizador retroceda cuando el equipo emite (#2428). |
| Speed (CW) | Deslizador (5-100 WPM) + QLineEdit | Establece la velocidad de claveo CW. Arrastre el deslizador o haga clic en el valor y escriba un número directamente (5-100). Llama a `TransmitModel::setCwSpeed`. Valor predeterminado: 20. |
| Sidetone | Alternar | Alterna el monitor de tono lateral CW. Controla tanto el monitor alimentado por DAX del equipo como el generador de tono lateral de baja latencia del lado del cliente (CwSidetoneGenerator, ~10 ms de latencia) al unísono. Llama a `TransmitModel::setCwSidetone`. En v26.5.3, el tono lateral CW se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). |
| Sidetone volume | Deslizador (0-100) + QLineEdit | Establece el volumen del monitor CW tanto para el equipo (mon_gain_cw) como para el generador de tono lateral local. Arrastre el deslizador o haga clic en el valor y escriba un número directamente (0-100). Valor predeterminado: 50. |
| L / R pan (CW) | Deslizador (0-100) | Establece el paneo estéreo del monitor CW. Aplica paneo de potencia constante tanto al lado del equipo como al generador de tono lateral local. Haga doble clic para centrar en 50 (centro). Valor predeterminado: 50. |
| Breakin | Alternar | Alterna la ruptura completa (QSK). Llama a `TransmitModel::setCwBreakIn`. Respeta completamente la configuración break_in del equipo (v0.9.7+): con Breakin activado (QSK), los bordes de la clave activan TX inmediatamente; con Breakin desactivado, las claves se ponen en cola y el operador activa PTT manualmente. |
| Iambic | Alternar | Alterna el manipulador de paletas iámbico. Llama a `TransmitModel::setCwIambic`. |
| Pitch < / > | QLineEdit con botones < / > | Establece el tono del tono lateral CW. Escriba un valor (100-6000 Hz) o haga clic en los botones para avanzar en pasos de 10 Hz. Llama a `TransmitModel::setCwPitch`. Valor predeterminado: 600. |

### Indicador ALC (Panel CW)

El indicador ALC en el panel CW es idéntico al del panel Phone. Muestra el pico SSB posterior al ALC por software en dBFS (-20 a 0 dBFS), llenándose de derecha a izquierda con un umbral rojo a -3 dBFS. El indicador se inicializa a -20 dBFS al inicio. Ambos indicadores leen de la misma fuente `MeterModel::swAlcChanged`, por lo que los operadores ven la misma indicación ALC independientemente de qué panel esté activo para el modo actual.

### Indicador ALC — lectura al pasar el cursor (v26.7.4+)

Pase el cursor del mouse sobre el indicador ALC para ver una ventana emergente que muestra el valor dBFS exacto con un decimal (#3936).

### Entrada directa de valor (v0.9.8)

En v0.9.8, las cuatro etiquetas de valor CW se reemplazaron con widgets QLineEdit que aceptan entrada numérica escrita:

- **Delay (CW):** acepta 0-2000 (milisegundos)
- **Speed (CW):** acepta 5-100 (WPM)
- **Sidetone volume:** acepta 0-100
- **Pitch < / >:** acepta 100-6000 (Hz)

Haga clic en cualquier valor, escriba un número y presione Enter. El deslizador correspondiente se actualiza inmediatamente. El deslizador sigue funcionando como antes; el campo de edición se actualiza desde el deslizador excepto mientras lo está editando.

### Comportamiento del tono lateral (v0.9.1+)

El único alternador **Sidetone** y el deslizador **Sidetone volume** controlan tanto el monitor alimentado por DAX del equipo como el generador de tono lateral de baja latencia del lado del cliente (CwSidetoneGenerator, ~10 ms de latencia) al unísono. No hay controles de tono lateral local separados.

El tono y el paneo siempre siguen automáticamente las configuraciones `cw_pitch` y `mon_pan_cw` del equipo; no se necesita ni está disponible ninguna anulación manual.

### Enrutamiento del tono lateral (v26.5.3)

En v26.5.3, el tono lateral CW ahora se enruta a la salida de audio seleccionada por el usuario en lugar de la salida de audio predeterminada (#2899). Configure la salida de audio en **File > Settings > Audio** para elegir dónde se reproduce el tono lateral.

### Compartición del bus de tono lateral con tonos Quindar (v0.9.7+)

El bus de audio del tono lateral se comparte con los tonos Quindar. Ambos son mutuamente excluyentes a nivel de modo: los tonos Quindar están activos solo fuera del modo CW, y el generador de tono lateral CW está activo solo en modo CW. El applet gestiona el cambio automáticamente cuando cambia el modo del slice activo.

### Comportamiento de Breakin (v0.9.7+)

- **Breakin activado (QSK):** los bordes de la clave activan TX inmediatamente; el retardo de ruptura establecido por el deslizador **Delay (CW)** mantiene el relé después del último elemento.
- **Breakin desactivado:** los caracteres claveados se ponen en cola; el operador activa PTT manualmente para transmitir.

## Gestión de perfiles de micrófono

Para seleccionar un perfil de micrófono:

1. Abra el applet Phone/CW.
2. Confirme que el slice activo está en un modo de voz (SSB, AM, FM). En modo CW, los controles de perfil de micrófono no son visibles.
3. Haga clic en el cuadro combinado **Mic profile**. La lista muestra los perfiles almacenados en el equipo.
4. Seleccione el nombre del perfil para su micrófono. El perfil se carga inmediatamente.

Los nombres de perfil disponibles provienen del equipo. Para crear o renombrar perfiles, use la gestión de perfiles del propio equipo o abra `Profiles > Profile Manager...` en AetherSDR. Seleccionar un perfil no cambia las configuraciones de **Mic source** o **Mic gain**; ajústelas por separado si es necesario.

## Cambios en v0.9.3

### Indicador Level — excepción de fuente de micrófono PC

Cuando la fuente de micrófono es PC, el indicador Level aparece inmediatamente al conectar incluso cuando `met_in_rx` está desactivado. Las fuentes de micrófono de hardware continúan suprimiéndose durante RX.

### Actualización del alternador VOX

Alternar VOX mediante un atajo de teclado ahora actualiza el panel Phone inmediatamente (#2084).

### Flujo de tono lateral en Windows

En Windows, el flujo de tono lateral del lado del cliente se inicia correctamente tan pronto como AetherSDR se conecta al equipo (#2105).

## Cambios en v0.9.7

### Indicador Compression controlado por estado de transmisión

El indicador Compression solo muestra un valor en vivo mientras el equipo está transmitiendo y el procesador de voz está habilitado. Durante la recepción, lee 0 dB.
