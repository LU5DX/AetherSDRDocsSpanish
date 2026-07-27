# Applet de Phone/CW

El applet de Phone/CW proporciona controles de transmisión según el modo. En modos de voz (subpanel Phone) muestra controles de micrófono, procesador y monitor. Cambia automáticamente al subpanel CW con controles de retardo, velocidad, sintonía lateral (sidetone), iambic y tono (pitch) cuando el segmento activo está en modo CW.

Ambos subpaneles incluyen un medidor ALC controlado por el medidor ALC de software (MeterModel::swAlcChanged), reemplazando la ruta anterior de ALC por hardware (voltaje RCA) que producía lecturas sin sentido.

## Acceso al applet Phone/CW

Si el applet Phone/CW no está visible, haga clic en el botón de la bandeja **P/CW** en la barra lateral derecha para abrirlo.

El subpanel CW aparece automáticamente cuando el segmento activo está en modo CW. Cambie el segmento activo a CW en la radio para pasar del subpanel Phone al subpanel CW.

## Soporte de estilo temático para sliders (v26.6.1)

En la v26.6.1, todos los sliders dentro del applet Phone/CW ahora usan `applyPrimarySliderStyle()` en lugar de una hoja de estilo codificada. Esto significa que los sliders siguen automáticamente los colores de acento y la paleta de fondo del tema actual. Si cambia el tema, la apariencia del slider se actualiza sin necesidad de reinicio.

## Resumen de la sintonía lateral CW

Activar la sintonía lateral CW habilita dos rutas simultáneamente: el monitor alimentado por DAX de la radio y un generador de tono del lado del cliente con aproximadamente 10 ms de latencia. Un solo botón y un solo slider de volumen controlan ambas al unísono, garantizando un tono consistente independientemente de la fluctuación de la red.

El tono y la panorámica del generador de tono del lado del cliente siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio. No es necesario configurarlos por separado para la ruta local.

## Pasos

1. Si el applet Phone/CW no está visible, haga clic en el botón de la bandeja **P/CW** en la barra lateral derecha para abrirlo.
2. Confirme que se muestra el subpanel CW. Si se muestra el subpanel Phone, cambie el segmento activo a un modo CW en la radio; el panel cambia automáticamente.
3. Haga clic en **Sidetone** para habilitar la sintonía lateral. El botón se ilumina cuando está activo.
4. Ajuste el slider de **Sidetone volume** a un nivel cómodo. El slider controla simultáneamente el volumen del monitor del lado de la radio y el volumen del generador de tono del lado del cliente.
5. Opcionalmente, ajuste **Pitch < / >** para establecer la frecuencia de la sintonía lateral. El tono sigue automáticamente el ajuste `cw_pitch` de la radio, pero puede ajustarlo en incrementos de 10 Hz usando los controles **<** y **>**. También puede escribir un valor directamente (100–6000) en el campo QLineEdit.
6. Para **Delay (CW)**, **Speed (CW)** y **Sidetone volume**, haga clic en el valor numérico y escriba un nuevo número directamente. Presione Enter o Tab para aplicar. El slider y el valor escrito se mantienen sincronizados automáticamente.

## Referencia de controles

| Control | Tipo | Predeterminado | Rango válido | Comportamiento |
|---------|------|---------------|--------------|----------------|
| Level | Medidor | — | -40 a +10 dBFS (rojo > 0 dBFS) | Muestra el nivel pico de entrada del micrófono en dBFS (panel Phone). Suprimido a -150 cuando met_in_rx está desactivado y no está transmitiendo. Pase el cursor sobre el medidor para una lectura numérica exacta en dB con un decimal. |
| Compression | Medidor | — | -25 a 0 dB (relleno invertido) | Muestra la cantidad de compresión de voz en dB (panel Phone). Bloqueado al estado TRANSMITTING del interbloqueo de la radio y a la habilitación del procesador de voz: lee 0 dB durante RX. Pase el cursor sobre el medidor para una lectura numérica exacta en dB con un decimal. |
| ALC (panel Phone) | Medidor | — | -20 a 0 dBFS (rojo > -3 dBFS) | Muestra la lectura de control automático de nivel de MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Pase el cursor sobre el medidor para una lectura numérica exacta en dBFS con un decimal. Se inicializa a -20 dBFS al construirse. |
| ALC (panel CW) | Medidor | — | -20 a 0 dBFS (rojo > -3 dBFS) | Refleja el medidor ALC del panel Phone; ambos leen de MeterModel::swAlcChanged para lecturas consistentes en voz y CW. Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Pase el cursor sobre el medidor para una lectura numérica exacta en dBFS con un decimal. Se inicializa a -20 dBFS al construirse. Usa el modo HGauge::setFillFromRight. |
| Mic profile | Cuadro combinado | — | Poblado desde micProfileList() de la radio | Carga el perfil de procesamiento de micrófono nombrado; llama a TransmitModel::loadMicProfile. |
| Mic source | Cuadro combinado | — | MIC, BAL, LINE, ACC, PC (más cualquier otro de micInputList()) | Selecciona la fuente de entrada del micrófono; llama a TransmitModel::setMicSelection. Cuando la modulación del host está activa, el cuadro combinado está deshabilitado, solo muestra "PC" y muestra una información sobre herramientas explicando que el micrófono del PC es la única entrada disponible. |
| Mic gain | Slider | 50 | 0–100 | Ajusta el nivel de entrada del micrófono. Para la fuente 'PC' usa la persistencia local PcMicGain (clave de ajuste `PcMicGain`). La radio siempre reporta mic_level=0 cuando source=PC; el valor se mantiene del lado del cliente. |
| +ACC | Botón de alternancia | — | — | Habilita la mezcla de entrada del micrófono auxiliar; llama a TransmitModel::setMicAcc. |
| PROC | Botón de alternancia | — | — | Activa/desactiva el procesador de voz; llama a TransmitModel::setSpeechProcessorEnable. |
| NOR/DX/DX+ | Slider | 0 (NOR) | 0 (NOR), 1 (DX), 2 (DX+) | Nivel de procesador de tres posiciones; llama a TransmitModel::setSpeechProcessorLevel. |
| DAX | Botón de alternancia | — | — | Habilita DAX como fuente de audio TX; llama a TransmitModel::setDax. |
| MON | Botón de alternancia | — | — | Habilita el monitor de sintonía lateral TX; llama a TransmitModel::setSbMonitor. |
| Monitor volume | Slider | — | 0–100 | Establece el volumen del monitor de banda lateral; llama a TransmitModel::setMonGainSb. |
| Delay (CW) | Slider con QLineEdit | 500 ms | 0–2000 ms (paso 10) | Establece el retardo de break-in CW; llama a TransmitModel::setCwDelay. El QLineEdit adyacente acepta valores escritos (0–2000). Se almacena en caché inmediatamente al arrastrarse para evitar que la radio vuelva a la posición anterior (#2428). |
| Speed (CW) | Slider con QLineEdit | 20 WPM | 5–100 WPM | Establece la velocidad de tecleo CW; llama a TransmitModel::setCwSpeed. El QLineEdit adyacente acepta valores escritos (5–100). |
| Sidetone | Botón de alternancia | — | — | Activa/desactiva el monitor de sintonía lateral CW; llama a TransmitModel::setCwSidetone. También habilita/deshabilita el CwSidetoneGenerator del lado del cliente al unísono. Se enruta a la salida de audio seleccionada por el usuario (v26.5.3). |
| Sidetone volume | Slider con QLineEdit | 50 | 0–100 | Establece el volumen del monitor CW; llama a TransmitModel::setMonGainCw. También establece el volumen del generador de sintonía lateral local al unísono. El QLineEdit adyacente acepta valores escritos (0–100). |
| L / R pan (CW) | Slider | 50 (centro) | 0–100 | Establece la panorámica estéreo del monitor CW; llama a TransmitModel::setMonPanCw y también aplica panorámica de potencia constante al generador de sintonía lateral local. Haga doble clic para re-centrar en 50 (centro). |
| Breakin | Botón de alternancia | — | — | Activa/desactiva el break-in completo (QSK); llama a TransmitModel::setCwBreakIn. Con Breakin activado, los flancos de tecla activan TX y break_in_delay mantiene el relé. Con Breakin desactivado, las teclas se ponen en cola y el operador activa PTT manualmente. Ninguna envolvente de PTT automática anula este comportamiento. |
| Iambic | Botón de alternancia | — | — | Activa/desactiva el manipulador de paletas iambic; llama a TransmitModel::setCwIambic. |
| Pitch < / > | QLineEdit con botones < / > (CwTriBtn) | 600 Hz | 100–6000 Hz (paso 10) | Escriba un valor (100–6000) o haga clic en los botones para avanzar en pasos de 10 Hz. Llama a TransmitModel::setCwPitch. |

## Entrada de valor directa

Las cuatro etiquetas de valor numérico en el subpanel CW son campos QLineEdit editables:

- **Delay (CW)** — Escriba cualquier valor de 0 a 2000 ms. Presione Enter o Tab para aplicar. El slider adyacente se mueve para coincidir.
- **Speed (CW)** — Escriba cualquier valor de 5 a 100 WPM. Presione Enter o Tab para aplicar. El slider adyacente se mueve para coincidir.
- **Sidetone volume** — Escriba cualquier valor de 0 a 100. Presione Enter o Tab para aplicar. El slider adyacente se mueve para coincidir.
- **Pitch < / >** — Escriba cualquier valor de 100 a 6000 Hz. Presione Enter o Tab para aplicar. Los botones **<** y **>** avanzan en pasos de 10 Hz.

Cuando escribe un valor fuera del rango válido, el campo limita el valor al límite válido más cercano (paridad SmartSDR).

## Medidores ALC

Tanto el subpanel Phone como el CW contienen medidores ALC idénticos que leen del medidor ALC de software (MeterModel::swAlcChanged). Esto reemplaza la ruta anterior de ALC por hardware (voltaje RCA) que producía lecturas sin sentido.

- Ambos medidores muestran en dBFS con un rango de -20 a 0 dBFS.
- La dirección de llenado es de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS.
- Una zona roja aparece por encima de -3 dBFS.
- Los valores fuera del rango [-20, 0] se limitan al extremo más cercano.
- El único slot updateAlc() impulsa ambos medidores simultáneamente, asegurando que los operadores de SSB y CW vean la misma lectura de pico posterior al ALC.
- Ambos medidores se inicializan a -20 dBFS al construirse, evitando un breve destello visual a 0 dBFS durante el inicio.
- Pasar el cursor sobre cualquier medidor ALC muestra una lectura numérica exacta en dBFS con un decimal, permitiendo leer el nivel pico SSB preciso en lugar de estimar contra la escala de -20 a 0.

## Salida de audio de la sintonía lateral CW

El generador de sintonía lateral CW se enruta al dispositivo de salida de audio seleccionado por el usuario en lugar de la salida del sistema predeterminada (#2899). Si tiene múltiples interfaces de audio configuradas en AetherSDR, la sintonía lateral sigue el dispositivo de salida seleccionado en **Settings > Audio > Output device**.

## Bloqueo del medidor de nivel en recepción

La supresión del medidor de nivel de micrófono usa un método dedicado `applyLevelMeterReceiveGate()` llamado cada vez que cambia el estado de transmisión de la radio o cuando se activa o desactiva el modo RADE. Esto asegura que el medidor siempre esté correctamente atenuado o visible independientemente del evento que active el cambio de estado.

## Mapeo del medidor de compresión

El medidor de compresión lee del medidor `COMPPEAK` de MeterModel como una cantidad de compresión positiva de 0–25 dB. La cara del medidor está invertida: 0 dB mostrado significa sin compresión, -25 dB significa compresión completa. El medidor convierte el valor positivo a negativo para su visualización, por lo que -25 corresponde a la compresión máxima y 0 a sin compresión. Pasar el cursor sobre el medidor muestra un valor dB positivo (la cantidad de compresión aplicada), con un decimal.

## Fuente de micrófono en modo de modulación del host

Cuando la radio está siendo modulada por AetherSDR (modulación del host activa), el cuadro combinado **Mic source** se deshabilita automáticamente y solo muestra "PC" como fuente disponible. La información sobre herramientas explica que el micrófono del PC es la única entrada porque la radio es modulada por AetherSDR; las otras fuentes son conectores físicos de FlexRadio y no están disponibles en este modo. Cuando se desactiva la modulación del host, el cuadro combinado vuelve al funcionamiento normal.

## Consejos

- Haga doble clic en el slider **L / R pan (CW)** para restablecerlo al centro (50).
- El medidor **Compression** lee 0 dB durante RX. Solo muestra un valor distinto de cero cuando el interbloqueo de la radio reporta el estado TRANSMITTING y el procesador de voz (**PROC**) está habilitado.
- Con **Breakin** desactivado, las pulsaciones de tecla se ponen en cola y la TX debe activarse manualmente con PTT. Con **Breakin** activado (QSK), los flancos de tecla activan TX directamente y `break_in_delay` controla el tiempo de retención del relé. Ninguna envolvente de PTT automática anula este comportamiento.
- El slider **Delay (CW)** actualiza su valor en caché inmediatamente al arrastrarse, evitando que la radio devuelva el slider a su posición anterior.
- El medidor ALC en ambos paneles lee la misma fuente de medidor, por lo que puede monitorear ALC independientemente de qué subpanel esté visible.
- Los sliders ahora siguen los colores de acento y la paleta de fondo del tema actual (v26.6.1). Cambiar el tema actualiza la apariencia del slider sin necesidad de reinicio.
- Pase el cursor sobre cualquier medidor (Level, Compression, ALC Phone, ALC CW) para una lectura numérica exacta con un decimal (#3936).

## Solución de problemas

- **No se escucha tono a pesar de que Sidetone está habilitado** — Confirme que el slider **Sidetone volume** está por encima de 0. También verifique que su dispositivo de salida de audio del sistema esté correctamente configurado en **Settings > Audio > Output device**, ya que el generador del lado del cliente se enruta a la salida seleccionada por el usuario.
- **El botón Sidetone no está visible** — El subpanel CW solo aparece cuando el segmento activo está en modo CW. Cambie el segmento activo
