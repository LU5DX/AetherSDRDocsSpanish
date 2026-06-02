# Applet de Phone/CW

El applet de Phone/CW es un panel de transmisión sensible al modo. En modos de voz (SSB, AM, FM) muestra los controles de micrófono, procesador y monitor. Cuando el slice activo está en modo CW, cambia automáticamente a controles de CW (retardo, velocidad, sidetone, iambic, tono).

## Abrir el applet de Phone/CW

Haga clic en el botón de la bandeja **P/CW** en la barra lateral derecha.

## Controles del panel de Phone (modos de voz)

| Control          | Tipo                                                                                                                              | Comportamiento                                                                                                                                                                                                                                                                                                                                                                                                    |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Level            | Medidor                                                                                                                                                           | Muestra el nivel pico de entrada del micrófono en dBFS (-40 a +10 dBFS; rojo por encima de 0). Se suprime a -150 dBFS cuando `met_in_rx` está desactivado y no está transmitiendo, excepto cuando la fuente de micrófono es PC o el modo RADE está activo.                                                                                                                           |
| Compression      | Medidor                                                                                                                                                           | Muestra la cantidad de compresión de voz en dB (-25 a 0 dB, relleno invertido). Se activa con el estado TRANSMITTING del interlock del radio y la habilitación del procesador de voz: indica 0 dB durante RX (v0.9.7+).                                                                                                                                                                |
| ALC (Panel Phone)| Medidor                                                                                                                                                           | Muestra la lectura del control automático de nivel desde `MeterModel::swAlcChanged` (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Umbral rojo a -3 dBFS. Se inicializa a -20 dBFS al inicio. Se reemplazó desde HWALC (tensión RCA) al medidor SW ALC en v26.5.1 (#2552). Es reflejado por un medidor idéntico en el subpanel de CW. |
| Mic profile      | Cuadro combinado                                                                                                                                                  | Carga un perfil de procesamiento de micrófono con nombre desde el radio. Haga clic para seleccionar un perfil; se carga inmediatamente.                                                                                                                                                                                                                                                                          |
| Mic source       | Cuadro combinado                                                                                                                                                  | Selecciona la fuente de entrada del micrófono: MIC, BAL, LINE, ACC o PC. Llama a `TransmitModel::setMicSelection`.                                                                                                                                                                                                                                                                                               |
| Mic gain         | Deslizador (0-100)                                                                                                                                                | Ajusta el nivel de entrada del micrófono. Para la fuente "PC", usa la persistencia local `PcMicGain` (el radio siempre reporta mic_level=0 cuando la fuente es PC).                                                                                                                                                                                                                                              |
| +ACC             | Alternar                                                                                                                                                           | Habilita la mezcla de entrada de micrófono auxiliar. Llama a `TransmitModel::setMicAcc`.                                                                                                                                                                                                                                                                                                                         |
| PROC             | Alternar                                                                                                                                                           | Activa o desactiva el procesador de voz. Llama a `TransmitModel::setSpeechProcessorEnable`.                                                                                                                                                                                                                                                                                                                       |
| NOR/DX/DX+       | Deslizador (0=NOR, 1=DX, 2=DX+)                                                                                                                                   | Nivel del procesador de tres posiciones. Llama a `TransmitModel::setSpeechProcessorLevel`.                                                                                                                                                                                                                                                                                                                        |
| DAX              | Alternar                                                                                                                                                           | Habilita DAX como fuente de audio de TX. Llama a `TransmitModel::setDax`.                                                                                                                                                                                                                                                                                                                                         |
| MON              | Alternar                                                                                                                                                           | Habilita el monitor de sidetone de TX. Llama a `TransmitModel::setSbMonitor`.                                                                                                                                                                                                                                                                                                                                     |
| Monitor volume   | Deslizador (0-100)                                                                                                                                                 | Ajusta el volumen del monitor de banda lateral. Llama a `TransmitModel::setMonGainSb`.                                                                                                                                                                                                                                                                                                                            |

### Medidor de nivel — excepciones con fuente de micrófono PC y modo RADE

Cuando la fuente de micrófono es **PC** o el modo **RADE** está activo, el medidor de nivel permanece activo durante la recepción (RX) incluso si `met_in_rx` está desactivado y el radio no está transmitiendo. Para fuentes de micrófono físicas (MIC, BAL, LINE, ACC), el medidor se suprime a -150 dBFS durante RX a menos que `met_in_rx` esté activado.

### Comportamiento del medidor de compresión (v0.9.7+)

El medidor de compresión solo muestra un valor en vivo mientras el radio está realmente transmitiendo y el procesador de voz está habilitado. Durante la recepción indica 0 dB. Esto evita lecturas obsoletas y confusas de la cadena de TX.

### Medidor ALC (Panel Phone)

El medidor ALC muestra el pico SSB posterior al ALC de software en dBFS, leído desde `MeterModel::swAlcChanged`. Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. El umbral rojo está a -3 dBFS. El medidor se inicializa a -20 dBFS al inicio. Este medidor es un reflejo del del panel CW; ambos leen de la misma fuente para obtener lecturas consistentes en modos de voz y CW.

### Comportamiento del modo RADE (v0.9.7+)

Cuando el modo RADE está activo:
- El deslizador **Mic gain** actúa como un control de ganancia RADE del lado del cliente que usa el ajuste `PcMicGain`. Los cambios en el deslizador no se envían al radio como comandos `mic_level`.
- El medidor **Level** permanece activo durante RX.
- Cuando RADE se desactiva, el deslizador vuelve a mostrar el valor `mic_level` del radio y el medidor de nivel se restablece a -150 dBFS.

## Controles del panel CW

| Control         | Tipo | Comportamiento |
|-----------------|------|---------------|
| ALC (Panel CW)  | Medidor | Refleja el medidor ALC del panel Phone. Muestra el pico SSB posterior al ALC de software en dBFS (-20 a 0 dBFS; rojo por encima de -3). Se llena de derecha a izquierda. Se inicializa a -20 dBFS al inicio. Añadido en v26.5.1 (#2552) como parte de la separación del medidor SW ALC. |
| Delay (CW)      | Deslizador (0-2000 ms, paso 10) + QLineEdit | Establece el retardo de break-in de CW. Arrastre el deslizador o haga clic en el valor y escriba un número directamente (0-2000). Llama a `TransmitModel::setCwDelay`. Valor predeterminado: 500. En v0.9.8, se corrigió el almacenamiento en caché del valor para evitar que el deslizador retrocediera cuando el radio emite (#2428). |
| Speed (CW)      | Deslizador (5-100 WPM) + QLineEdit | Establece la velocidad de tecleo CW. Arrastre el deslizador o haga clic en el valor y escriba un número directamente (5-100). Llama a `TransmitModel::setCwSpeed`. Valor predeterminado: 20. |
| Sidetone        | Alternar | Activa o desactiva el monitor de sidetone CW. Controla tanto el monitor alimentado por DAX del radio como el generador de sidetone de baja latencia del lado del cliente (CwSidetoneGenerator, ~10 ms de latencia) de forma sincronizada. Llama a `TransmitModel::setCwSidetone`. En v26.5.3, el sidetone CW se enruta a la salida de audio seleccionada por el usuario en lugar de a la salida predeterminada (#2899). |
| Sidetone volume | Deslizador (0-100) + QLineEdit | Establece el volumen del monitor CW tanto para el radio (mon_gain_cw) como para el generador de sidetone local. Arrastre el deslizador o haga clic en el valor y escriba un número directamente (0-100). Valor predeterminado: 50. |
| L / R pan (CW)  | Deslizador (0-100) | Establece la panorámica estéreo del monitor CW. Aplica panorámica de potencia constante tanto al lado del radio como al generador de sidetone local. Haga doble clic para centrar en 50. Valor predeterminado: 50. |
| Breakin         | Alternar | Activa o desactiva el break-in completo (QSK). Llama a `TransmitModel::setCwBreakIn`. Respeta completamente el ajuste break_in del radio (v0.9.7+): con Breakin ON (QSK) los bordes de la tecla activan TX inmediatamente; con Breakin OFF las teclas se ponen en cola y el operador activa PTT manualmente. |
| Iambic          | Alternar | Activa o desactiva el keyer de paletas iambic. Llama a `TransmitModel::setCwIambic`. |
| Pitch < / >     | QLineEdit con botones < / > | Establece el tono del sidetone CW. Escriba un valor (100-6000 Hz) o haga clic en los botones para incrementar o decrementar en pasos de 10 Hz. Llama a `TransmitModel::setCwPitch`. Valor predeterminado: 600. |

### Medidor ALC (Panel CW)

El medidor ALC en el panel CW es idéntico al del panel Phone. Muestra el pico SSB posterior al ALC de software en dBFS (-20 a 0 dBFS), se llena de derecha a izquierda con un umbral rojo a -3 dBFS. El medidor se inicializa a -20 dBFS al inicio. Ambos medidores leen de la misma fuente `MeterModel::swAlcChanged`, por lo que los operadores ven la misma indicación de ALC independientemente del panel que esté activo para el modo actual.

### Entrada de valor directa (v0.9.8)

En v0.9.8, las cuatro etiquetas de valor de CW fueron reemplazadas por widgets QLineEdit que aceptan entrada numérica escrita:

- **Delay (CW):** acepta 0-2000 (milisegundos)
- **Speed (CW):** acepta 5-100 (WPM)
- **Sidetone volume:** acepta 0-100
- **Pitch < / >:** acepta 100-6000 (Hz)

Haga clic en cualquier valor, escriba un número y presione Enter. El deslizador correspondiente se actualiza inmediatamente. El deslizador sigue funcionando como antes; el campo de edición se actualiza desde el deslizador excepto mientras lo está editando.

### Comportamiento del sidetone (v0.9.1+)

El único alternador **Sidetone** y el deslizador **Sidetone volume** controlan tanto el monitor alimentado por DAX del radio como el generador de sidetone de baja latencia del lado del cliente (CwSidetoneGenerator, ~10 ms de latencia) de forma sincronizada. No hay controles locales de sidetone separados.

El tono y la panorámica siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` del radio; no es necesario ni está disponible una anulación manual.

### Enrutamiento del sidetone (v26.5.3)

En v26.5.3, el sidetone CW ahora se enruta a la salida de audio seleccionada por el usuario en lugar de a la salida de audio predeterminada (#2899). Configure la salida de audio en **File > Settings > Audio** para elegir dónde se reproduce el sidetone.

### Compartición del bus de sidetone con tonos Quindar (v0.9.7+)

El bus de audio del sidetone se comparte con los tonos Quindar. Los dos son mutuamente excluyentes a nivel de modo: los tonos Quindar están activos solo fuera del modo CW, y el generador de sidetone CW está activo solo en modo CW. El applet gestiona el cambio automáticamente cuando cambia el modo del slice activo.

### Comportamiento de break-in (v0.9.7+)

- **Breakin ON (QSK):** los bordes de la tecla activan TX inmediatamente; el retardo de break-in establecido por el deslizador **Delay (CW)** mantiene el relé después del último elemento.
- **Breakin OFF:** los caracteres tecleados se ponen en cola; el operador activa PTT manualmente para transmitir.

## Gestión de perfiles de micrófono

Para seleccionar un perfil de micrófono:

1. Abra el applet Phone/CW.
2. Confirme que el slice activo está en un modo de voz (SSB, AM, FM). En modo CW los controles de perfil de micrófono no son visibles.
3. Haga clic en el cuadro combinado **Mic profile**. La lista muestra los perfiles almacenados en el radio.
4. Seleccione el nombre del perfil para su micrófono. El perfil se carga inmediatamente.

Los nombres de perfil disponibles provienen del radio. Para crear o renombrar perfiles, use la gestión de perfiles del propio radio o abra **Profiles > Profile Manager...** en AetherSDR. Seleccionar un perfil no cambia los ajustes de **Mic source** o **Mic gain**; ajústelos por separado si es necesario.

## Cambios en v0.9.3

### Medidor de nivel — excepción con fuente de micrófono PC

Cuando la fuente de micrófono es PC, el medidor de nivel aparece inmediatamente al conectar incluso si `met_in_rx` está desactivado. Las fuentes de micrófono físicas continúan suprimiéndose durante RX.

### Actualización del alternador VOX

Activar o desactivar VOX mediante un atajo de teclado ahora actualiza el panel Phone inmediatamente (#2084).

### Flujo de sidetone en Windows

En Windows, el flujo de sidetone del lado del cliente se inicia correctamente tan pronto como AetherSDR se conecta al radio (#2105).

## Cambios en v0.9.7

### Medidor de compresión activado por estado de transmisión

El medidor de compresión solo muestra un valor en vivo mientras el radio está transmitiendo y el procesador de voz está habilitado. Durante la recepción indica 0 dB (#2084).

### Breakin respeta completamente el ajuste del radio

Se ha eliminado la envolvente de PTT automática que enmascaraba Breakin OFF. Breakin ON habilita QSK; Breakin OFF requiere PTT manual.

### Soporte para modo RADE

El modo RADE usa la ganancia de micrófono y el medidor de nivel del lado del cliente, compartiendo el ajuste `PcMicGain` con la fuente de micrófono PC.

### Bus de sidetone compartido con tonos Quindar

Los tonos Quindar y el sidetone CW comparten el bus de audio; el applet gestiona el cambio automáticamente.

## Cambios en v0.9.8

- **Entrada de valor directa:** Las etiquetas de Delay, Speed, Sidetone volume y Pitch ahora son widgets QLineEdit con QIntValidator. Haga clic en cualquier valor y escriba un número directamente (#2429).
- **Corrección de almacenamiento en caché de Delay:** `setCwDelay` ahora almacena en caché el valor inmediatamente para que la emisión del radio no haga retroceder el deslizador (#2428).

## Cambios en v26.5.1

- **Medidor ALC reconectado al medidor SW ALC:** El medidor ALC tanto en el panel Phone como en el panel CW ahora lee desde `MeterModel::swAlcChanged` (pico SSB posterior al ALC de software en dBFS) en lugar de la ruta anterior HWALC (tensión RCA) (#2552). El rango es de -20 a 0 dBFS con relleno de derecha a izquierda. El medidor ALC del panel CW ahora es idéntico al medidor ALC del panel Phone, proporcionando lecturas consistentes en ambos modos de voz y CW.

## Cambios en v26.5.3

- **Enrutamiento de salida del sidetone CW:** El sidetone CW ahora se enruta a la salida de audio seleccionada por el usuario en lugar de a la salida predeterminada (#2899). Configure la salida de audio en **File > Settings > Audio**.
- **Inicialización del medidor ALC:** Los medidores ALC tanto del panel Phone como del panel CW ahora se inicializan a -20 dBFS al inicio.
