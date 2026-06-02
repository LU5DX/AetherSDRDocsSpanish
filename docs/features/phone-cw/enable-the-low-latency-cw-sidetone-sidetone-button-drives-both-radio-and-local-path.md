# Applet de Phone/CW

El applet de Phone/CW proporciona controles de transmisión según el modo. En modos de voz (subpanel Phone) muestra controles de micrófono, procesador y monitor. Cambia automáticamente al subpanel CW con controles de retardo, velocidad, tono lateral, iambic y tono cuando la banda activa está en modo CW.

Ambos subpaneles incluyen un indicador ALC controlado por el medidor ALC de software (MeterModel::swAlcChanged), reemplazando la ruta anterior de ALC por hardware (voltaje RCA) que producía lecturas sin sentido.

## Acceso al Applet de Phone/CW

Si el applet de Phone/CW no está visible, haga clic en el botón de bandeja **P/CW** en la barra lateral derecha para abrirlo.

El subpanel CW aparece automáticamente cuando la banda activa está en modo CW. Cambie la banda activa a CW en la radio para pasar del subpanel Phone al subpanel CW.

## Soporte de estilo de deslizadores por tema (v26.6.1)

En la v26.6.1, todos los deslizadores dentro del applet de Phone/CW usan `applyPrimarySliderStyle()` en lugar de una hoja de estilo fija. Esto significa que los deslizadores siguen automáticamente los colores de acento y la paleta de fondo del tema actual. Si cambia el tema, la apariencia del deslizador se actualiza sin necesidad de reiniciar.

## Resumen del Tono Lateral CW

Activar el tono lateral CW habilita dos rutas simultáneamente: el monitor alimentado por DAX de la radio y un generador de tono local con una latencia de aproximadamente 10 ms. Un solo botón y un solo deslizador de volumen controlan ambas de forma sincronizada, garantizando un tono consistente independientemente de la fluctuación de la red.

El tono y la panorámica del generador de tono local siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio. No es necesario configurarlos por separado para la ruta local.

## Pasos

1. Si el applet de Phone/CW no está visible, haga clic en el botón de bandeja **P/CW** en la barra lateral derecha para abrirlo.
2. Confirme que se muestra el subpanel CW. Si se muestra el subpanel Phone, cambie la banda activa a un modo CW en la radio; el panel cambiará automáticamente.
3. Haga clic en **Sidetone** para habilitar el tono lateral. El botón se ilumina cuando está activo.
4. Ajuste el deslizador de **Sidetone volume** a un nivel cómodo. El deslizador controla simultáneamente el volumen del monitor del lado de la radio y el volumen del generador de tono local.
5. Opcionalmente, ajuste **Pitch < / >** para establecer la frecuencia del tono lateral. El tono sigue automáticamente el ajuste `cw_pitch` de la radio, pero puede modificarlo en incrementos de 10 Hz usando los controles **<** y **>**. También puede escribir un valor directamente (100–6000) en el campo QLineEdit.
6. Para **Delay (CW)**, **Speed (CW)** y **Sidetone volume**, haga clic en el valor numérico y escriba un nuevo número directamente. Presione Enter o Tab para aplicarlo. El deslizador y el valor escrito se mantienen sincronizados automáticamente.

## Referencia de Controles

| Control | Tipo | Valor predeterminado | Rango válido | Comportamiento |
|---------|------|---------------------|--------------|----------------|
| Level | Medidor | — | -40 a +10 dBFS (rojo > 0 dBFS) | Muestra el nivel pico de entrada del micrófono en dBFS (panel Phone). Suprimido a -150 cuando met_in_rx está desactivado y no se transmite. |
| Compression | Medidor | — | -25 a 0 dB (relleno invertido) | Muestra la cantidad de compresión de voz en dB (panel Phone). Activado por el estado TRANSMITTING del interlock de la radio y la habilitación del procesador de voz: lee 0 dB durante RX. Controlado a través del slot updateCompression(), independiente de la ruta del nivel de micrófono. |
| ALC (panel Phone) | Medidor | — | -20 a 0 dBFS (rojo > -3 dBFS) | Muestra la lectura del control automático de nivel desde MeterModel::swAlcChanged (pico SSB post-ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Se inicializa a -20 dBFS al construirse. |
| ALC (panel CW) | Medidor | — | -20 a 0 dBFS (rojo > -3 dBFS) | Refleja el indicador ALC del panel Phone; ambos leen de MeterModel::swAlcChanged para lecturas consistentes en voz y CW. Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Se inicializa a -20 dBFS al construirse. Usa el modo HGauge::setFillFromRight. |
| Mic profile | Cuadro combinado | — | Poblado desde radio micProfileList() | Carga el perfil de procesamiento de micrófono nombrado; llama a TransmitModel::loadMicProfile. |
| Mic source | Cuadro combinado | — | MIC, BAL, LINE, ACC, PC (más cualquier entrada de micInputList()) | Selecciona la fuente de entrada del micrófono; llama a TransmitModel::setMicSelection. |
| Mic gain | Deslizador | 50 | 0–100 | Ajusta el nivel de entrada del micrófono. Para la fuente 'PC' usa la persistencia local de PcMicGain (clave de configuración `PcMicGain`). La radio siempre reporta mic_level=0 cuando source=PC; el valor se mantiene del lado del cliente. |
| +ACC | Botón de alternancia | — | — | Habilita la mezcla de entrada auxiliar del micrófono; llama a TransmitModel::setMicAcc. |
| PROC | Botón de alternancia | — | — | Activa o desactiva el procesador de voz; llama a TransmitModel::setSpeechProcessorEnable. |
| NOR/DX/DX+ | Deslizador | 0 (NOR) | 0 (NOR), 1 (DX), 2 (DX+) | Nivel del procesador de tres posiciones; llama a TransmitModel::setSpeechProcessorLevel. |
| DAX | Botón de alternancia | — | — | Habilita DAX como fuente de audio TX; llama a TransmitModel::setDax. |
| MON | Botón de alternancia | — | — | Habilita el monitor de tono lateral TX; llama a TransmitModel::setSbMonitor. |
| Monitor volume | Deslizador | — | 0–100 | Establece el volumen del monitor de banda lateral; llama a TransmitModel::setMonGainSb. |
| Delay (CW) | Deslizador con QLineEdit | 500 ms | 0–2000 ms (paso 10) | Establece el retardo de break-in CW; llama a TransmitModel::setCwDelay. El QLineEdit adyacente acepta valores escritos (0–2000). Se almacena en caché inmediatamente al arrastrarse para evitar que la radio revierta (#2428). |
| Speed (CW) | Deslizador con QLineEdit | 20 WPM | 5–100 WPM | Establece la velocidad de manipulación CW; llama a TransmitModel::setCwSpeed. El QLineEdit adyacente acepta valores escritos (5–100). |
| Sidetone | Botón de alternancia | — | — | Activa o desactiva el monitor de tono lateral CW; llama a TransmitModel::setCwSidetone. También habilita o deshabilita el CwSidetoneGenerator local de forma sincronizada. Se dirige a la salida de audio seleccionada por el usuario (v26.5.3). |
| Sidetone volume | Deslizador con QLineEdit | 50 | 0–100 | Establece el volumen del monitor CW; llama a TransmitModel::setMonGainCw. También establece el volumen del generador de tono lateral local de forma sincronizada. El QLineEdit adyacente acepta valores escritos (0–100). |
| L / R pan (CW) | Deslizador | 50 (centro) | 0–100 | Establece la panorámica estéreo del monitor CW; llama a TransmitModel::setMonPanCw y también aplica panorámica de potencia constante al generador de tono lateral local. Doble clic lo recentra a 50 (centro). |
| Breakin | Botón de alternancia | — | — | Activa o desactiva el break-in completo (QSK); llama a TransmitModel::setCwBreakIn. Con Breakin activado, los bordes de la tecla activan TX y break_in_delay mantiene el relé. Con Breakin desactivado, las teclas se encolan y el operador activa PTT manualmente. Ningún sobreenvolvente de PTT automático anula este comportamiento. |
| Iambic | Botón de alternancia | — | — | Activa o desactiva el manipulador de paletas iambic; llama a TransmitModel::setCwIambic. |
| Pitch < / > | QLineEdit con botones < / > (CwTriBtn) | 600 Hz | 100–6000 Hz (paso 10) | Escriba un valor (100–6000) o haga clic en los botones para incrementar o disminuir en 10 Hz. Llama a TransmitModel::setCwPitch. |

## Entrada Directa de Valores

Las cuatro etiquetas de valor numérico en el subpanel CW son campos QLineEdit editables:

- **Delay (CW)** — Escriba cualquier valor de 0 a 2000 ms. Presione Enter o Tab para aplicarlo. El deslizador adyacente se mueve para coincidir.
- **Speed (CW)** — Escriba cualquier valor de 5 a 100 WPM. Presione Enter o Tab para aplicarlo. El deslizador adyacente se mueve para coincidir.
- **Sidetone volume** — Escriba cualquier valor de 0 a 100. Presione Enter o Tab para aplicarlo. El deslizador adyacente se mueve para coincidir.
- **Pitch < / >** — Escriba cualquier valor de 100 a 6000 Hz. Presione Enter o Tab para aplicarlo. Los botones **<** y **>** incrementan o disminuyen en 10 Hz.

Cuando escribe un valor fuera del rango válido, el campo limita el valor al límite válido más cercano (paridad con SmartSDR).

## Medidores ALC

Tanto el subpanel Phone como el CW contienen indicadores ALC idénticos que leen del medidor ALC de software (MeterModel::swAlcChanged). Esto reemplaza la ruta anterior de ALC por hardware (voltaje RCA) que producía lecturas sin sentido.

- Ambos indicadores muestran en dBFS con un rango de -20 a 0 dBFS.
- La dirección de llenado es de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS.
- Una zona roja aparece por encima de -3 dBFS.
- Los valores fuera del rango [-20, 0] se limitan al extremo más cercano.
- El único slot updateAlc() controla ambos indicadores simultáneamente, garantizando que los operadores de SSB y CW vean la misma lectura pico post-ALC.
- Ambos indicadores se inicializan a -20 dBFS al construirse, evitando un breve destello visual a 0 dBFS durante el inicio.

## Salida de Audio del Tono Lateral CW

El generador de tono lateral CW se dirige al dispositivo de salida de audio seleccionado por el usuario en lugar de la salida predeterminada del sistema (#2899). Si tiene múltiples interfaces de audio configuradas en AetherSDR, el tono lateral sigue el dispositivo de salida seleccionado en **Settings > Audio > Output device**.

## Bloqueo del Medidor de Nivel por Recepción

La supresión del medidor de nivel de micrófono usa un método dedicado `applyLevelMeterReceiveGate()` llamado cada vez que cambia el estado de transmisión de la radio o cuando se activa o desactiva el modo RADE. Esto garantiza que el medidor siempre se atenúe o muestre correctamente independientemente de qué evento desencadene el cambio de estado.

## Mapeo del Indicador de Compresión

El indicador de compresión lee del medidor MeterModel `COMPPEAK` como una cantidad de compresión positiva de 0 a 25 dB. La cara del indicador está invertida: 0 dB mostrado significa sin compresión, -25 dB significa compresión total. El indicador convierte el valor positivo a negativo para su visualización, por lo que -25 corresponde a la compresión máxima y 0 a sin compresión.

## Consejos

- Haga doble clic en el deslizador **L / R pan (CW)** para restablecerlo al centro (50).
- El indicador **Compression** lee 0 dB durante RX. Solo muestra un valor distinto de cero cuando el interlock de la radio reporta el estado TRANSMITTING y el procesador de voz (**PROC**) está habilitado.
- Con **Breakin** desactivado, las pulsaciones de tecla se encolan y TX debe activarse manualmente con PTT. Con **Breakin** activado (QSK), los bordes de la tecla activan TX directamente y `break_in_delay` controla el tiempo de retención del relé. Ningún sobreenvolvente de PTT automático anula este comportamiento.
- El deslizador **Delay (CW)** actualiza su valor en caché inmediatamente al arrastrarse, evitando que la radio devuelva el deslizador a su posición anterior.
- El indicador ALC en ambos paneles lee la misma fuente de medidor, por lo que puede monitorear ALC independientemente de qué subpanel esté visible.
- Los deslizadores ahora siguen los colores de acento y la paleta de fondo del tema actual (v26.6.1). Cambiar el tema actualiza la apariencia del deslizador sin necesidad de reiniciar.

## Solución de Problemas

- **No se escucha tono a pesar de que Sidetone está habilitado** — Confirme que el deslizador **Sidetone volume** esté por encima de 0. También verifique que su dispositivo de salida de audio del sistema esté configurado correctamente en **Settings > Audio > Output device**, ya que el generador local se dirige a la salida seleccionada por el usuario.
- **El botón Sidetone no es visible** — El subpanel CW solo aparece cuando la banda activa está en modo CW. Cambie la banda activa a CW en la radio; el panel del applet cambiará automáticamente.
- **El tono no coincide con lo esperado** — El tono sigue el ajuste `cw_pitch` de la radio. Ajústelo usando **Pitch < / >** en el applet, lo que actualiza el ajuste de la radio en pasos de 10 Hz.
- **El indicador de compresión siempre muestra 0** — Esto es esperado durante RX. El indicador está condicionado al estado TRANSMITTING del interlock de la radio. Mostrará compresión solo mientras transmite con **PROC** habilitado.
- **Breakin OFF no mantiene TX entre caracteres** — Con **Breakin** desactivado, AetherSDR ya no aplica un sobreenvolvente de PTT automático. Active PTT manualmente antes de enviar y suéltelo cuando termine.
- **El deslizador Mic gain no tiene efecto en modo RADE** — Cuando el modo RADE está activo, el deslizador Mic gain funciona como un control de ganancia local en lugar de enviar un comando de nivel de micrófono a la radio. El valor del deslizador se almacena bajo `PcMicGain` y no se escribe en la propiedad `mic_level` de la radio mientras RADE está activo. Cuando el modo RADE se desactiva, el deslizador vuelve a reflejar el `mic_level` de la radio.
