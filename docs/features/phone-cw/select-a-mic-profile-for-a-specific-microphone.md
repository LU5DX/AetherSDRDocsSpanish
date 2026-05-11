# Applet de Phone/CW

El applet de Phone/CW es un panel de transmisión sensible al modo. En modos de voz (SSB, AM, FM) muestra controles de micrófono, procesador y monitor. Cuando el slice activo está en modo CW, cambia automáticamente a los controles de CW (retardo, velocidad, tono lateral, iámbico, tono).

## Abrir el applet de Phone/CW

Haga clic en el botón de la bandeja **P/CW** en la barra lateral derecha.

## Controles del panel Phone (modos de voz)

| Control          | Tipo                                                                                                                                    | Comportamiento                                                                                                                                                                                                                     |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Level            | Medidor                                                                                                                                | Muestra el nivel máximo de entrada del micrófono en dBFS (-40 a +10 dBFS; rojo por encima de 0). Se suprime a -150 dBFS cuando `met_in_rx` está desactivado y no se transmite, excepto cuando la fuente de micrófono es PC o el modo RADE está activo. |
| Compression      | Medidor                                                                                                                                | Muestra la cantidad de compresión de voz en dB (-25 a 0 dB, relleno invertido). Se activa con el estado INTERLOCK TRANSMITTING de la radio y el procesador de voz habilitado: muestra 0 dB durante RX (v0.9.7+).                  |
| ALC (panel Phone)| Medidor                                                                                                                                | Muestra la lectura del control automático de nivel de `MeterModel::swAlcChanged` (pico SSB post-ALC por software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Umbral rojo a -3 dBFS. Reconectado desde HWALC (voltaje RCA) al medidor SW ALC en v26.5.1 (#2552). Es reflejado por un medidor idéntico en el subpanel de CW. |
| Mic profile      | Cuadro combinado                                                                                                                       | Carga un perfil de procesamiento de micrófono con nombre desde la radio. Haga clic para seleccionar un perfil; se carga inmediatamente.                                                                                             |
| Mic source       | Cuadro combinado                                                                                                                       | Selecciona la fuente de entrada del micrófono: MIC, BAL, LINE, ACC o PC. Llama a `TransmitModel::setMicSelection`.                                                                                                                 |
| Mic gain         | Deslizador (0-100)                                                                                                                     | Ajusta el nivel de entrada del micrófono. Para la fuente "PC", utiliza la persistencia local `PcMicGain` (la radio siempre reporta mic_level=0 cuando la fuente=PC).                                                               |
| +ACC             | Alternar                                                                                                                               | Activa la mezcla de entrada del micrófono accesorio. Llama a `TransmitModel::setMicAcc`.                                                                                                                                          |
| PROC             | Alternar                                                                                                                               | Activa o desactiva el procesador de voz. Llama a `TransmitModel::setSpeechProcessorEnable`.                                                                                                                                       |
| NOR/DX/DX+       | Deslizador (0=NOR, 1=DX, 2=DX+)                                                                                                        | Nivel del procesador de tres posiciones. Llama a `TransmitModel::setSpeechProcessorLevel`.                                                                                                                                        |
| DAX              | Alternar                                                                                                                               | Activa DAX como fuente de audio de TX. Llama a `TransmitModel::setDax`.                                                                                                                                                           |
| MON              | Alternar                                                                                                                               | Activa el monitor de tono lateral de TX. Llama a `TransmitModel::setSbMonitor`.                                                                                                                                                   |
| Monitor volume   | Deslizador (0-100)                                                                                                                     | Ajusta el volumen del monitor de banda lateral. Llama a `TransmitModel::setMonGainSb`.                                                                                                                                            |

### Medidor de nivel — excepciones de fuente de micrófono PC y modo RADE

Cuando la fuente de micrófono es **PC** o el modo **RADE** está activo, el medidor de nivel permanece activo durante la recepción (RX) incluso si `met_in_rx` está desactivado y la radio no está transmitiendo. Para fuentes de micrófono de hardware (MIC, BAL, LINE, ACC), el medidor se suprime a -150 dBFS durante RX a menos que `met_in_rx` esté activado.

### Comportamiento del medidor de compresión (v0.9.7+)

El medidor de compresión solo muestra un valor en vivo mientras la radio está realmente transmitiendo y el procesador de voz está habilitado. Durante la recepción, muestra 0 dB. Esto evita lecturas obsoletas y confusas de la cadena de TX.

### Medidor ALC (panel Phone)

El medidor ALC muestra el pico SSB post-ALC por software en dBFS, leído de `MeterModel::swAlcChanged`. Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. El umbral rojo está a -3 dBFS. Este medidor refleja el del panel CW, ambos leen de la misma fuente para lecturas consistentes en modos de voz y CW.

### Comportamiento del modo RADE (v0.9.7+)

Cuando el modo RADE está activo:
- El deslizador **Mic gain** actúa como un control de ganancia RADE del lado del cliente usando el ajuste `PcMicGain`. Los cambios en el deslizador no se envían a la radio como comandos `mic_level`.
- El medidor **Level** permanece activo durante RX.
- Cuando RADE se desactiva, el deslizador vuelve a mostrar el valor `mic_level` de la radio y el medidor Level se restablece a -150 dBFS.

## Controles del panel CW

| Control | Tipo | Comportamiento |
|---------|------|----------------|
| ALC (panel CW) | Medidor | Refleja el medidor ALC del panel Phone. Muestra el pico SSB post-ALC por software en dBFS (-20 a 0 dBFS; rojo por encima de -3). Se llena de derecha a izquierda. Añadido en v26.5.1 (#2552) como parte de la división del medidor SW ALC. |
| Delay (CW) | Deslizador (0-2000 ms, paso 10) + QLineEdit | Ajusta el retardo de inserción de CW. Arrastre el deslizador o haga clic en el valor y escriba un número directamente (0-2000). Llama a `TransmitModel::setCwDelay`. Valor predeterminado: 500. En v0.9.8, se corrigió el almacenamiento en caché del valor para evitar que el deslizador retroceda cuando la radio emite (#2428). |
| Speed (CW) | Deslizador (5-100 WPM) + QLineEdit | Ajusta la velocidad de manipulación de CW. Arrastre el deslizador o haga clic en el valor y escriba un número directamente (5-100). Llama a `TransmitModel::setCwSpeed`. Valor predeterminado: 20. |
| Sidetone | Alternar | Activa o desactiva el monitor de tono lateral de CW. Controla tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente (CwSidetoneGenerator, ~10 ms de latencia) de forma sincronizada. Llama a `TransmitModel::setCwSidetone`. |
| Sidetone volume | Deslizador (0-100) + QLineEdit | Ajusta el volumen del monitor de CW tanto para la radio (mon_gain_cw) como para el generador de tono lateral local. Arrastre el deslizador o haga clic en el valor y escriba un número directamente (0-100). Valor predeterminado: 50. |
| L / R pan (CW) | Deslizador (0-100) | Ajusta la panorámica estéreo del monitor de CW. Aplica panorámica de potencia constante tanto al lado de la radio como al generador de tono lateral local. Haga doble clic para centrar en 50 (centro). Valor predeterminado: 50. |
| Breakin | Alternar | Activa o desactiva la inserción completa (QSK). Llama a `TransmitModel::setCwBreakIn`. Respeta completamente el ajuste break_in de la radio (v0.9.7+): con Breakin ON (QSK), los flancos de la tecla activan TX inmediatamente; con Breakin OFF, las teclas se ponen en cola y el operador activa PTT manualmente. |
| Iambic | Alternar | Activa o desactiva el manipulador de paletas iámbico. Llama a `TransmitModel::setCwIambic`. |
| Pitch < / > | QLineEdit con botones < / > | Ajusta el tono del tono lateral de CW. Escriba un valor (100-6000 Hz) o haga clic en los botones para aumentar o disminuir en pasos de 10 Hz. Llama a `TransmitModel::setCwPitch`. Valor predeterminado: 600. |

### Medidor ALC (panel CW)

El medidor ALC del panel CW es idéntico al del panel Phone. Muestra el pico SSB post-ALC por software en dBFS (-20 a 0 dBFS), llenándose de derecha a izquierda con un umbral rojo a -3 dBFS. Ambos medidores leen de la misma fuente `MeterModel::swAlcChanged`, por lo que los operadores ven la misma indicación de ALC independientemente de qué panel esté activo para el modo actual.

### Entrada de valor directa (v0.9.8)

En v0.9.8, las cuatro etiquetas de valor de CW se reemplazaron con widgets QLineEdit que aceptan entrada numérica escrita:

- **Delay (CW):** acepta 0-2000 (milisegundos)
- **Speed (CW):** acepta 5-100 (WPM)
- **Sidetone volume:** acepta 0-100
- **Pitch < / >:** acepta 100-6000 (Hz)

Haga clic en cualquier valor, escriba un número y presione Enter. El deslizador correspondiente se actualiza inmediatamente. El deslizador continúa funcionando como antes; el campo de edición se actualiza desde el deslizador excepto mientras lo está editando.

### Comportamiento del tono lateral (v0.9.1+)

El único alternador **Sidetone** y el deslizador **Sidetone volume** controlan tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente (CwSidetoneGenerator, ~10 ms de latencia) de forma sincronizada. No hay controles de tono lateral local separados.

El tono y la panorámica siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio; no se necesita ni está disponible una anulación manual.

### Compartición del bus de tono lateral con tonos Quindar (v0.9.7+)

El bus de audio del tono lateral se comparte con los tonos Quindar. Ambos son mutuamente excluyentes a nivel de modo: los tonos Quindar están activos solo fuera del modo CW, y el generador de tono lateral de CW está activo solo en modo CW. El applet gestiona el cambio automáticamente cuando cambia el modo del slice activo.

### Comportamiento de Breakin (v0.9.7+)

- **Breakin ON (QSK):** los flancos de la tecla activan TX inmediatamente; el retardo de inserción establecido por el deslizador **Delay (CW)** mantiene el relé después del último elemento.
- **Breakin OFF:** los caracteres tecleados se ponen en cola; el operador activa PTT manualmente para transmitir.

## Gestión de perfiles de micrófono

Para seleccionar un perfil de micrófono:

1. Abra el applet Phone/CW.
2. Confirme que el slice activo esté en un modo de voz (SSB, AM, FM). En modo CW, los controles del perfil de micrófono no son visibles.
3. Haga clic en el cuadro combinado **Mic profile**. La lista muestra los perfiles almacenados en la radio.
4. Seleccione el nombre del perfil para su micrófono. El perfil se carga inmediatamente.

Los nombres de perfil disponibles provienen de la radio. Para crear o renombrar perfiles, use la gestión de perfiles de la propia radio o abra `Profiles > Profile Manager...` en AetherSDR. Seleccionar un perfil no cambia los ajustes de **Mic source** o **Mic gain**; ajústelos por separado si es necesario.

## Cambios en v0.9.3

### Medidor de nivel — excepción de fuente de micrófono PC

Cuando la fuente de micrófono es PC, el medidor de nivel aparece inmediatamente al conectarse incluso cuando `met_in_rx` está desactivado. Las fuentes de micrófono de hardware continúan suprimiéndose durante RX.

### Actualización del alternador VOX

Activar o desactivar VOX mediante un atajo de teclado ahora actualiza el panel Phone inmediatamente (#2084).

### Flujo de tono lateral en Windows

En Windows, el flujo de tono lateral del lado del cliente se inicia correctamente tan pronto como AetherSDR se conecta a la radio (#2105).

## Cambios en v0.9.7

### Medidor de compresión activado por el estado de transmisión

El medidor de compresión solo muestra un valor en vivo mientras la radio está transmitiendo y el procesador de voz está habilitado. Durante la recepción, muestra 0 dB (#2084).

### Breakin respeta completamente el ajuste de la radio

Se ha eliminado la envolvente de PTT automático que enmascaraba Breakin OFF. Breakin ON habilita QSK; Breakin OFF requiere PTT manual.

### Soporte del modo RADE

El modo RADE utiliza la ganancia de micrófono y el medidor de nivel del lado del cliente, compartiendo el ajuste `PcMicGain` con la fuente de micrófono PC.

### Bus de tono lateral compartido con tonos Quindar

Los tonos Quindar y el tono lateral de CW comparten el bus de audio; el applet gestiona el cambio automáticamente.

## Cambios en v0.9.8

- **Entrada de valor directa:** Las etiquetas de Delay, Speed, Sidetone volume y Pitch ahora son widgets QLineEdit con QIntValidator. Haga clic en cualquier valor y escriba un número directamente (#2429).
- **Corrección de caché de Delay:** `setCwDelay` ahora almacena en caché el valor inmediatamente para que la emisión de la radio no haga que el deslizador retroceda (#2428).

## Cambios en v26.5.1

- **Medidor ALC reconectado al medidor SW ALC:** El medidor ALC en los paneles Phone y CW ahora lee de `MeterModel::swAlcChanged` (pico SSB post-ALC por software en dBFS) en lugar de la ruta anterior HWALC (voltaje RCA) (#2552). El rango es de -20 a 0 dBFS con relleno de derecha a izquierda. El medidor ALC del panel CW ahora es idéntico al medidor ALC del panel Phone, proporcionando lecturas consistentes en los modos de voz y CW.

## Relacionado

- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Ajustar la ganancia del micrófono y activar la mezcla accesoria](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Activar el procesador de voz al nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
