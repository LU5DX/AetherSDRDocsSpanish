# Applet de Phone/CW

El applet de Phone/CW es un panel de transmisión que reconoce el modo activo. En modos de voz (SSB, AM, FM) muestra los controles de micrófono, procesador y monitor. Cuando el slice activo está en modo CW, cambia automáticamente a los controles de CW (retardo, velocidad, sidetone, iambic, tono).

## Abrir el applet de Phone/CW

Haga clic en el botón de la bandeja **P/CW** en la barra lateral derecha.

## Controles del panel Phone (modos de voz)

| Control | Tipo | Comportamiento |
|---------|------|----------------|
| Level | Medidor | Muestra el nivel pico de entrada del micrófono en dBFS (-40 a +10 dBFS; rojo por encima de 0). Se suprime a -150 dBFS cuando `met_in_rx` está desactivado y no está transmitiendo, excepto cuando la fuente del micrófono es PC o el modo RADE está activo. |
| Compression | Medidor | Muestra la cantidad de compresión de voz en dB (-25 a 0 dB, relleno invertido). Se activa con el estado de TRANSMITTING del interlock de la radio y con el procesador de voz habilitado: muestra 0 dB durante RX (v0.9.7+). |
| Mic profile | Cuadro combinado | Carga un perfil de procesamiento de micrófono con nombre desde la radio. Haga clic para seleccionar un perfil; se carga inmediatamente. |
| Mic source | Cuadro combinado | Selecciona la fuente de entrada del micrófono: MIC, BAL, LINE, ACC o PC. Llama a `TransmitModel::setMicSelection`. |
| Mic gain | Control deslizante (0-100) | Ajusta el nivel de entrada del micrófono. Para la fuente "PC", usa la persistencia local `PcMicGain` (la radio siempre reporta mic_level=0 cuando la fuente=PC). |
| +ACC | Interruptor | Habilita la mezcla de entrada del micrófono auxiliar. Llama a `TransmitModel::setMicAcc`. |
| PROC | Interruptor | Activa o desactiva el procesador de voz. Llama a `TransmitModel::setSpeechProcessorEnable`. |
| NOR/DX/DX+ | Control deslizante (0=NOR, 1=DX, 2=DX+) | Nivel del procesador de tres posiciones. Llama a `TransmitModel::setSpeechProcessorLevel`. |
| DAX | Interruptor | Habilita DAX como fuente de audio de TX. Llama a `TransmitModel::setDax`. |
| MON | Interruptor | Habilita el monitor de sidetone de TX. Llama a `TransmitModel::setSbMonitor`. |
| Monitor volume | Control deslizante (0-100) | Establece el volumen del monitor de banda lateral. Llama a `TransmitModel::setMonGainSb`. |

### Medidor Level — excepciones para fuente de micrófono PC y RADE

Cuando la fuente del micrófono es **PC** o el modo **RADE** está activo, el medidor Level permanece activo durante la recepción (RX) incluso si `met_in_rx` está desactivado y la radio no está transmitiendo. Para fuentes de micrófono de hardware (MIC, BAL, LINE, ACC), el medidor se suprime a -150 dBFS durante RX a menos que `met_in_rx` esté activado.

### Comportamiento del medidor Compression (v0.9.7+)

El medidor Compression solo muestra un valor en vivo mientras la radio está realmente transmitiendo y el procesador de voz está habilitado. Durante la recepción muestra 0 dB. Esto evita lecturas obsoletas y confusas de la cadena de TX.

### Comportamiento del modo RADE (v0.9.7+)

Cuando el modo RADE está activo:
- El control deslizante **Mic gain** actúa como un control de ganancia RADE del lado del cliente usando la configuración `PcMicGain`. Los cambios en el control deslizante no se envían a la radio como comandos `mic_level`.
- El medidor **Level** permanece activo durante RX.
- Cuando RADE se desactiva, el control deslizante vuelve a mostrar el valor `mic_level` de la radio y el medidor Level se restablece a -150 dBFS.

## Controles del panel CW

| Control | Tipo | Comportamiento |
|---------|------|----------------|
| ALC | Medidor | Muestra la lectura del control automático de nivel (0-100; rojo por encima de 80). |
| Delay (CW) | Control deslizante (0-2000 ms, paso 10) + QLineEdit | Establece el retardo de break-in CW. Arrastre el control deslizante o haga clic en el valor y escriba un número directamente (0-2000). Llama a `TransmitModel::setCwDelay`. Valor predeterminado: 500. En v0.9.8, se corrigió el almacenamiento en caché del valor para evitar que el control deslizante retrocediera cuando la radio emite (#2428). |
| Speed (CW) | Control deslizante (5-100 WPM) + QLineEdit | Establece la velocidad de tecleo CW. Arrastre el control deslizante o haga clic en el valor y escriba un número directamente (5-100). Llama a `TransmitModel::setCwSpeed`. Valor predeterminado: 20. |
| Sidetone | Interruptor | Activa o desactiva el monitor de sidetone CW. Controla tanto el monitor alimentado por DAX de la radio como el generador de sidetone de baja latencia del lado del cliente (CwSidetoneGenerator, ~10 ms de latencia) al unísono. Llama a `TransmitModel::setCwSidetone`. |
| Sidetone volume | Control deslizante (0-100) + QLineEdit | Establece el volumen del monitor CW tanto para la radio (mon_gain_cw) como para el generador de sidetone local. Arrastre el control deslizante o haga clic en el valor y escriba un número directamente (0-100). Valor predeterminado: 50. |
| L / R pan (CW) | Control deslizante (0-100) | Establece la panorámica estéreo del monitor CW. Aplica panorámica de potencia constante tanto al lado de la radio como al generador de sidetone local. Haga doble clic para centrar en 50 (centro). Valor predeterminado: 50. |
| Breakin | Interruptor | Activa o desactiva el break-in completo (QSK). Llama a `TransmitModel::setCwBreakIn`. Respeta completamente la configuración break_in de la radio (v0.9.7+): con Breakin activado (QSK), los bordes de la tecla activan TX inmediatamente; con Breakin desactivado, los caracteres tecleados se ponen en cola y el operador activa el PTT manualmente. |
| Iambic | Interruptor | Activa o desactiva el manipulador de paletas iambic. Llama a `TransmitModel::setCwIambic`. |
| Pitch < / > | QLineEdit con botones < / > | Establece el tono del sidetone CW. Escriba un valor (100-6000 Hz) o haga clic en los botones para cambiar en pasos de 10 Hz. Llama a `TransmitModel::setCwPitch`. Valor predeterminado: 600. |

### Entrada directa de valores (v0.9.8)

En v0.9.8, las cuatro etiquetas de valor de CW se reemplazaron con widgets QLineEdit que aceptan entrada numérica escrita:

- **Delay (CW):** acepta 0-2000 (milisegundos)
- **Speed (CW):** acepta 5-100 (WPM)
- **Sidetone volume:** acepta 0-100
- **Pitch < / >:** acepta 100-6000 (Hz)

Haga clic en cualquier valor, escriba un número y presione Enter. El control deslizante correspondiente se actualiza inmediatamente. El control deslizante continúa funcionando como antes; el campo de edición se actualiza desde el control deslizante excepto mientras lo está editando.

### Comportamiento del Sidetone (v0.9.1+)

El único interruptor **Sidetone** y el control deslizante **Sidetone volume** controlan tanto el monitor alimentado por DAX de la radio como el generador de sidetone de baja latencia del lado del cliente (CwSidetoneGenerator, ~10 ms de latencia) al unísono. No hay controles de sidetone local separados.

El tono y la panorámica siguen automáticamente las configuraciones `cw_pitch` y `mon_pan_cw` de la radio; no se necesita ni está disponible una anulación manual.

### Compartición del bus de sidetone con tonos Quindar (v0.9.7+)

El bus de audio de sidetone se comparte con los tonos Quindar. Ambos son mutuamente excluyentes a nivel de modo: los tonos Quindar están activos solo fuera del modo CW, y el generador de sidetone CW está activo solo en modo CW. El applet gestiona el cambio automáticamente cuando cambia el modo del slice activo.

### Comportamiento de Breakin (v0.9.7+)

- **Breakin activado (QSK):** los bordes de la tecla activan TX inmediatamente; el retardo de break-in establecido por el control deslizante **Delay (CW)** mantiene el relé después del último elemento.
- **Breakin desactivado:** los caracteres tecleados se ponen en cola; el operador activa el PTT manualmente para transmitir.

## Gestión de perfiles de micrófono

Para seleccionar un perfil de micrófono:

1. Abra el applet de Phone/CW.
2. Confirme que el slice activo está en un modo de voz (SSB, AM, FM). En modo CW, los controles del perfil de micrófono no son visibles.
3. Haga clic en el cuadro combinado **Mic profile**. La lista muestra los perfiles almacenados en la radio.
4. Seleccione el nombre del perfil para su micrófono. El perfil se carga inmediatamente.

Los nombres de perfil disponibles provienen de la radio. Para crear o renombrar perfiles, use la gestión de perfiles de la propia radio o abra `Profiles > Profile Manager...` en AetherSDR. Seleccionar un perfil no cambia la configuración de **Mic source** o **Mic gain**; ajústelas por separado si es necesario.

## Cambios en v0.9.3

### Medidor Level — excepción para fuente de micrófono PC

Cuando la fuente del micrófono es PC, el medidor Level aparece inmediatamente al conectarse incluso si `met_in_rx` está desactivado. Las fuentes de micrófono de hardware continúan suprimiéndose durante RX.

### Actualización del interruptor VOX

Activar o desactivar VOX mediante un atajo de teclado ahora actualiza el panel Phone inmediatamente (#2084).

### Flujo de sidetone en Windows

En Windows, el flujo de sidetone del lado del cliente se inicia correctamente tan pronto como AetherSDR se conecta a la radio (#2105).

## Cambios en v0.9.7

### Medidor Compression controlado por estado de transmisión

El medidor Compression solo muestra un valor en vivo mientras la radio está transmitiendo y el procesador de voz está habilitado. Durante la recepción muestra 0 dB (#2084).

### Breakin respeta completamente la configuración de la radio

Se ha eliminado la envolvente de PTT automático que enmascaraba Breakin desactivado. Breakin activado habilita QSK; Breakin desactivado requiere PTT manual.

### Soporte para modo RADE

El modo RADE usa la ganancia de micrófono y el medidor Level del lado del cliente, compartiendo la configuración `PcMicGain` con la fuente de micrófono PC.

### Bus de sidetone compartido con tonos Quindar

Los tonos Quindar y el sidetone CW comparten el bus de audio; el applet gestiona el cambio automáticamente.

## Cambios en v0.9.8

- **Entrada directa de valores:** Las etiquetas de Delay, Speed, Sidetone volume y Pitch ahora son widgets QLineEdit con QIntValidator. Haga clic en cualquier valor y escriba un número directamente (#2429).
- **Corrección de almacenamiento en caché de Delay:** `setCwDelay` ahora almacena en caché el valor inmediatamente para que la emisión de la radio no haga retroceder el control deslizante (#2428).

## Relacionado

- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Ajustar la ganancia del micrófono y habilitar la mezcla auxiliar](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Habilitar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
