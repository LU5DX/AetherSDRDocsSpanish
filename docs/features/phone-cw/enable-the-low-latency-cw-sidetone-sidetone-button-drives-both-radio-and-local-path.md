# Applet de Phone/CW

El applet de Phone/CW proporciona controles de transmisión según el modo. En modos de voz (subpanel Phone) muestra controles de micrófono, procesador y monitor. Cambia automáticamente al subpanel CW con controles de retardo, velocidad, tono lateral (sidetone), iámbico y tono cuando el slice activo está en modo CW.

Ambos subpaneles incluyen un indicador ALC controlado por el medidor ALC de software (MeterModel::swAlcChanged), que reemplaza la ruta anterior de ALC por hardware (voltaje RCA) que producía lecturas sin significado.

## Acceso al applet de Phone/CW

Si el applet de Phone/CW no está visible, haga clic en el botón de bandeja **P/CW** en la barra lateral derecha para abrirlo.

El subpanel CW aparece automáticamente cuando el slice activo está en un modo CW. Cambie el slice activo a CW en la radio para pasar del subpanel Phone al subpanel CW.

## Soporte de estilo de tema para controles deslizantes (v26.6.1)

En v26.6.1, todos los controles deslizantes dentro del applet de Phone/CW usan ahora `applyPrimarySliderStyle()` en lugar de una hoja de estilos codificada. Esto significa que los controles deslizantes siguen automáticamente los colores de acento y la paleta de fondo del tema actual. Si cambia el tema, la apariencia de los controles deslizantes se actualiza sin necesidad de reiniciar.

## Resumen del tono lateral CW

Activar el tono lateral CW habilita dos rutas simultáneamente: el monitor alimentado por DAX de la radio y un generador de tonos del lado del cliente con aproximadamente 10 ms de latencia. Un único botón y un único control deslizante de volumen controlan ambos al unísono, garantizando un tono consistente independientemente de la fluctuación de la red.

El tono y la panoramización del generador de tonos del lado del cliente siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio. No es necesario configurarlos por separado para la ruta local.

## Pasos

1. Si el applet de Phone/CW no está visible, haga clic en el botón de bandeja **P/CW** en la barra lateral derecha para abrirlo.
2. Confirme que se muestra el subpanel CW. Si se muestra el subpanel Phone, cambie el slice activo a un modo CW en la radio; el panel cambiará automáticamente. El applet reconoce **CW**, **CWU** y **CWL** como modos CW.
3. Haga clic en **Sidetone** para habilitar el tono lateral. El botón se ilumina cuando está activo.
4. Ajuste el control deslizante **Sidetone volume** a un nivel cómodo. El control deslizante controla simultáneamente el volumen del monitor del lado de la radio y el volumen del generador de tonos del lado del cliente.
5. Opcionalmente, ajuste **Pitch < / >** para fijar la frecuencia del tono lateral. El tono sigue automáticamente el ajuste `cw_pitch` de la radio, pero puede ajustarlo en incrementos de 10 Hz con los controles **<** y **>**. También puede escribir un valor directamente (100–6000) en el campo QLineEdit.
6. Para **Delay (CW)**, **Speed (CW)** y **Sidetone volume**, haga clic en el valor numérico y escriba un nuevo número directamente. Pulse Enter o Tab para aplicar. El control deslizante y el valor escrito permanecen sincronizados automáticamente.

## Referencia de controles

| Control | Tipo | Predeterminado | Rango válido | Comportamiento |
|---------|------|---------|-------------|----------|
| Level | Medidor | — | -40 a +10 dBFS (rojo > 0 dBFS) | Muestra el nivel de pico de entrada del micrófono en dBFS (panel Phone). Se suprime a -150 cuando met_in_rx está desactivado y no se transmite. Se oculta cuando el medidor de nivel de micrófono de la radio no está disponible (p. ej., cuando la radio es modulada por AetherSDR). Pase el cursor sobre el indicador para obtener una lectura numérica exacta en dB con un decimal. |
| Compression | Medidor | — | -25 a 0 dB (relleno invertido) | Muestra la cantidad de compresión de voz en dB (panel Phone). Se activa según el estado TRANSMITTING del interbloqueo de la radio y la habilitación del procesador de voz: lee 0 dB durante RX. Pase el cursor sobre el indicador para obtener una lectura numérica exacta en dB con un decimal. |
| ALC (panel Phone) | Medidor | — | -20 a 0 dBFS (rojo > -3 dBFS) | Muestra la lectura del control automático de nivel de MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío en -20 dBFS, lleno en 0 dBFS. Pase el cursor sobre el indicador para obtener una lectura numérica exacta en dBFS con un decimal. Se inicializa en -20 dBFS al construirse. |
| ALC (panel CW) | Medidor | — | -20 a 0 dBFS (rojo > -3 dBFS) | Refleja el indicador ALC del panel Phone; ambos leen de MeterModel::swAlcChanged para lecturas consistentes entre voz y CW. Se llena de derecha a izquierda: vacío en -20 dBFS, lleno en 0 dBFS. Pase el cursor sobre el indicador para obtener una lectura numérica exacta en dBFS con un decimal. Se inicializa en -20 dBFS al construirse. Usa el modo HGauge::setFillFromRight. |
| Mic profile | Cuadro combinado | — | Se completa desde micProfileList() de la radio | Carga el perfil de procesamiento de micrófono nombrado; llama a TransmitModel::loadMicProfile. |
| Mic source | Cuadro combinado | — | MIC, BAL, LINE, ACC, PC (más los de micInputList()) | Selecciona la fuente de entrada del micrófono; llama a TransmitModel::setMicSelection. Cuando la radio no puede aceptar una selección de fuente de micrófono del lado del cliente, el cuadro está deshabilitado, muestra solo "PC" y muestra una información sobre herramientas que explica que la radio toma el audio de transmisión de este equipo. |
| Mic gain | Control deslizante | 50 | 0–100 | Ajusta el nivel de entrada del micrófono. Para la fuente 'PC' usa la persistencia local PcMicGain (clave de ajuste `PcMicGain`). La radio siempre informa mic_level=0 cuando la fuente es PC; el valor se mantiene del lado del cliente. La señal `micLevelChanged` se emite solo cuando el cliente posee la ganancia (modo RADE, o entradas de micrófono seleccionables con PC seleccionado). |
| +ACC | Botón de conmutación | — | — | Habilita la mezcla de entrada de micrófono auxiliar; llama a TransmitModel::setMicAcc. |
| PROC | Botón de conmutación | — | — | Conmuta el procesador de voz; llama a TransmitModel::setSpeechProcessorEnable. |
| NOR/DX/DX+ | Control deslizante | 0 (NOR) | 0 (NOR), 1 (DX), 2 (DX+) | Nivel de procesador de tres posiciones; llama a TransmitModel::setSpeechProcessorLevel. |
| DAX | Botón de conmutación | — | — | Habilita DAX como fuente de audio TX; llama a TransmitModel::setDax. Se oculta cuando este cliente no puede seleccionar DAX como fuente TX; el botón se fuerza a desactivado cuando está oculto. |
| MON | Botón de conmutación | — | — | Habilita el monitor de tono lateral TX; llama a TransmitModel::setSbMonitor. |
| Monitor volume | Control deslizante | — | 0–100 | Establece el volumen del monitor de banda lateral; llama a TransmitModel::setMonGainSb. |
| Delay (CW) | Control deslizante con QLineEdit | 500 ms | 0–2000 ms (paso 10) | Establece el retardo de break-in CW; llama a TransmitModel::setCwDelay. El QLineEdit adyacente acepta valores escritos (0–2000). Se almacena en caché inmediatamente al arrastrar para evitar que la radio regrese bruscamente (#2428). |
| Speed (CW) | Control deslizante con QLineEdit | 20 WPM | 5–100 WPM | Establece la velocidad de tecleo CW; llama a TransmitModel::setCwSpeed. El QLineEdit adyacente acepta valores escritos (5–100). |
| Sidetone | Botón de conmutación | — | — | Conmuta el monitor de tono lateral CW; llama a TransmitModel::setCwSidetone. También habilita/deshabilita el CwSidetoneGenerator del lado del cliente al unísono. Se enruta a la salida de audio seleccionada por el usuario (v26.5.3). |
| Sidetone volume | Control deslizante con QLineEdit | 50 | 0–100 | Establece el volumen del monitor CW; llama a TransmitModel::setMonGainCw. También establece el volumen del generador de tonos local al unísono. El QLineEdit adyacente acepta valores escritos (0–100). |
| L / R pan (CW) | Control deslizante | 50 (centro) | 0–100 | Establece la panoramización estéreo del monitor CW; llama a TransmitModel::setMonPanCw y también aplica panoramización de potencia constante al generador de tonos local. Doble clic recentra a 50 (centro). |
| Breakin | Botón de conmutación | — | — | Conmuta el break-in completo (QSK); llama a TransmitModel::setCwBreakIn. Con Breakin activado, los flancos de tecla activan TX y break_in_delay mantiene el relé. Con Breakin desactivado, las teclas se ponen en cola y el operador activa PTT manualmente. Ningún sobre envolvente automático de PTT anula este comportamiento. |
| Iambic | Botón de conmutación | — | — | Conmuta el manipulador de paleta iámbico; llama a TransmitModel::setCwIambic. |
| Pitch < / > | QLineEdit con botones < / > (CwTriBtn) | 600 Hz | 100–6000 Hz (paso 10) | Escriba un valor (100–6000) o haga clic en los botones para ajustar en pasos de 10 Hz. Llama a TransmitModel::setCwPitch. |

## Entrada directa de valores

Las cuatro etiquetas de valor numérico en el subpanel CW son campos QLineEdit editables:

- **Delay (CW)** — Escriba cualquier valor de 0 a 2000 ms. Pulse Enter o Tab para aplicar. El control deslizante adyacente se mueve para coincidir.
- **Speed (CW)** — Escriba cualquier valor de 5 a 100 WPM. Pulse Enter o Tab para aplicar. El control deslizante adyacente se mueve para coincidir.
- **Sidetone volume** — Escriba cualquier valor de 0 a 100. Pulse Enter o Tab para aplicar. El control deslizante adyacente se mueve para coincidir.
- **Pitch < / >** — Escriba cualquier valor de 100 a 6000 Hz. Pulse Enter o Tab para aplicar. Los botones **<** y **>** ajustan en pasos de 10 Hz.

Cuando escribe un valor fuera del rango válido, el campo limita el valor al límite válido más cercano (paridad con SmartSDR).

## Medidores ALC

Tanto el subpanel Phone como el CW contienen indicadores ALC idénticos que leen del medidor ALC de software (MeterModel::swAlcChanged). Esto reemplaza la ruta anterior de ALC por hardware (voltaje RCA) que producía lecturas sin significado.

- Ambos indicadores muestran en dBFS con un rango de -20 a 0 dBFS.
- La dirección del relleno es de derecha a izquierda: vacío en -20 dBFS, lleno en 0 dBFS.
- Aparece una zona roja por encima de -3 dBFS.
- Los valores fuera del rango [-20, 0] se limitan al extremo más cercano.
- La única ranura updateAlc() activa ambos indicadores simultáneamente, garantizando que los operadores de SSB y CW vean la misma lectura de pico posterior al ALC.
- Ambos indicadores se inicializan en -20 dBFS al construirse, evitando un destello visual breve en 0 dBFS durante el arranque.
- Pasar el cursor sobre cualquiera de los indicadores ALC muestra una lectura numérica exacta en dBFS con un decimal, lo que permite leer el nivel de pico SSB preciso en lugar de estimar contra la escala de -20 a 0.

## Salida de audio del tono lateral CW

El generador de tono lateral CW se enruta al dispositivo de salida de audio seleccionado por el usuario en lugar de la salida predeterminada del sistema (#2899). Si tiene múltiples interfaces de audio configuradas en AetherSDR, el tono lateral sigue el dispositivo de salida seleccionado en **Settings > Audio > Output device**.

## Activación del medidor de nivel por recepción

La supresión del medidor de nivel de micrófono usa un método dedicado `applyLevelMeterReceiveGate()` que se llama cada vez que cambia el estado de transmisión de la radio o cuando se activa o desactiva el modo RADE. Esto garantiza que el medidor se atenúe o muestre siempre correctamente, independientemente de qué evento active el cambio de estado.

## Mapeo del indicador de compresión

El indicador de compresión lee del medidor `COMPPEAK` de MeterModel como una cantidad positiva de compresión de 0–25 dB. La cara del indicador está invertida: 0 dB mostrado significa sin compresión, -25 dB significa compresión completa. El indicador convierte el valor positivo a negativo para su visualización, de modo que -25 corresponde a compresión máxima y 0 a sin compresión. Pasar el cursor sobre el indicador muestra un valor positivo en dB (la cantidad de compresión aplicada), con un decimal.

## Fuente de micrófono en radios con entrada de audio TX fija

Cuando la radio toma su audio de transmisión de este equipo y su propia selección de entrada se realiza en la radio (por ejemplo, cuando AetherSDR modula la radio a través de la red), el cuadro combinado **Mic source** se deshabilita automáticamente y muestra solo "PC" como fuente disponible. La información sobre herramientas explica que la radio toma el audio de transmisión de este equipo y su propia selección de entrada se realiza en la radio. En este estado, el cuadro combinado no parece averiado: indica la fuente efectiva. Al modelo del lado de la radio se le informa que la fuente es PC para que las comprobaciones posteriores (como las advertencias de radiocert sobre la captura de audio de transmisión) no se activen incorrectamente.

El indicador del medidor **Level** también se oculta en este estado, ya que la radio no informa un nivel de micrófono significativo para la ruta alimentada por red. El botón **DAX** también se oculta cuando DAX no puede seleccionarse como fuente TX para la configuración actual de la radio.

## Consejos

- Hacer doble clic en el control deslizante **L / R pan (CW)** lo restablece al centro (50).
- El indicador **Compression** lee 0 dB durante RX. Solo muestra un valor distinto de cero cuando el interbloqueo de la radio informa el estado TRANSMITTING y el procesador de voz (**PROC**) está habilitado.
- Con **Breakin** desactivado, las pulsaciones de tecla se ponen en cola y TX debe activarse manualmente con PTT. Con **Breakin** activado (QSK), los flancos de tecla activan TX directamente y `break_in_delay` controla el tiempo de mantenimiento del relé. Ningún sobre envolvente automático de PTT anula este comportamiento.
- El control deslizante **Delay (CW)** actualiza su valor almacenado en caché inmediatamente al arrastrarlo, evitando que la radio regrese bruscamente
