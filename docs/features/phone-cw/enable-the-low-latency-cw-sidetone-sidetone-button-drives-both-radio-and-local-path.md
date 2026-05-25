# Habilitar el tono lateral CW de baja latencia (el botón de tono lateral controla tanto la ruta de la radio como la ruta local)

Al activar el tono lateral CW en AetherSDR se habilitan dos rutas simultáneamente: el monitor de la radio alimentado por DAX y un generador de tono del lado del cliente con aproximadamente 10 ms de latencia. Un solo botón y un solo control deslizante de volumen controlan ambas rutas al unísono, por lo que escuchará un tono consistente independientemente de la fluctuación de la red.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Phone/CW requiere una conexión activa con la radio.
- El slice activo debe estar en un modo CW. El panel del applet cambia automáticamente del subpanel Phone al subpanel CW cuando se detecta el modo CW.

## Pasos

1. Si el applet Phone/CW no está visible, haga clic en el botón **P/CW** en la barra lateral derecha para abrirlo.
2. Confirme que se muestra el subpanel CW. Si se muestra el subpanel Phone, cambie el slice activo a un modo CW en la radio; el panel cambia automáticamente.
3. Haga clic en **Sidetone** para activar el tono lateral. El botón se ilumina cuando está activo.
4. Ajuste el control deslizante **Sidetone volume** a un nivel cómodo. El control deslizante ajusta simultáneamente el volumen del monitor de la radio y el volumen del generador de tono del lado del cliente.
5. Opcionalmente, ajuste **Pitch < / >** para establecer la frecuencia del tono lateral. El tono sigue automáticamente el ajuste `cw_pitch` de la radio, pero puede modificarlo en incrementos de 10 Hz usando los controles **<** y **>**. También puede escribir un valor directamente (100–6000) en el campo QLineEdit (v0.9.8).
6. Para **Delay (CW)**, **Speed (CW)**, y **Sidetone volume**, haga clic en el valor numérico y escriba un nuevo número directamente. Presione Enter o Tab para aplicar. El control deslizante y el valor escrito se mantienen sincronizados automáticamente (v0.9.8).

## Qué hace cada control

| Control             | Tipo                                                                                                                                                                                                                                                           | Valor predeterminado                                                                                                      |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| Level               | Medidor. Muestra el nivel pico de entrada del micrófono en dBFS (panel Phone). Suprimido a -150 cuando met_in_rx está desactivado y no está transmitiendo.                                                                                                     | —                                                                                                                         |
| Compression         | Medidor. Muestra la cantidad de compresión de voz en dB (panel Phone). Relleno invertido. Activado por el estado TRANSMITTING del interbloqueo de la radio y la habilitación del procesador de voz.                                                             | —                                                                                                                         |
| ALC (panel Phone)   | Medidor. Muestra la lectura del control automático de nivel desde MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS). Se rellena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Se inicializa a -20 dBFS al construirse.          | Reconfigurado desde HWALC (tensión RCA) al medidor SW ALC en v26.5.1 (#2552). Reflejado por un medidor idéntico en el subpanel CW. |
| ALC (panel CW)      | Medidor. Refleja el medidor ALC del panel Phone; ambos leen desde MeterModel::swAlcChanged para lecturas consistentes en voz y CW. Se rellena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Se inicializa a -20 dBFS al construirse.                | Añadido en v26.5.1 (#2552) como parte de la división del medidor SW ALC. Usa el modo HGauge::setFillFromRight. Actualizado en v26.5.3 para inicializar a -20 dBFS. |
| Mic profile         | Cuadro combinado. Carga el perfil de procesamiento de micrófono nombrado; llama a TransmitModel::loadMicProfile.                                                                                                                                               | —                                                                                                                         |
| Mic source          | Cuadro combinado. Selecciona la fuente de entrada del micrófono (MIC, BAL, LINE, ACC, PC, más las de micInputList()); llama a TransmitModel::setMicSelection.                                                                                                  | —                                                                                                                         |
| Mic gain            | Control deslizante. Ajusta el nivel de entrada del micrófono (0–100). Para la fuente 'PC' usa la persistencia local PcMicGain. Valor predeterminado: 50. Clave de configuración: `PcMicGain`.                                                                  | 50                                                                                                                        |
| +ACC                | Botón de alternancia. Habilita la mezcla de entrada del micrófono auxiliar; llama a TransmitModel::setMicAcc.                                                                                                                                                  | —                                                                                                                         |
| PROC                | Botón de alternancia. Activa o desactiva el procesador de voz; llama a TransmitModel::setSpeechProcessorEnable.                                                                                                                                               | —                                                                                                                         |
| NOR/DX/DX+          | Control deslizante. Nivel del procesador de tres posiciones (0=NOR, 1=DX, 2=DX+); llama a TransmitModel::setSpeechProcessorLevel.                                                                                                                              | 0 (NOR)                                                                                                                   |
| DAX                 | Botón de alternancia. Habilita DAX como fuente de audio de TX; llama a TransmitModel::setDax.                                                                                                                                                                 | —                                                                                                                         |
| MON                 | Botón de alternancia. Habilita el monitor de tono lateral de TX; llama a TransmitModel::setSbMonitor.                                                                                                                                                         | —                                                                                                                         |
| Monitor volume      | Control deslizante. Establece el volumen del monitor de banda lateral (0–100); llama a TransmitModel::setMonGainSb.                                                                                                                                            | —                                                                                                                         |
| Delay (CW)          | Control deslizante con QLineEdit (v0.9.8). Escriba un valor (0–2000 ms) directamente en el campo, o arrastre el control deslizante. Llama a TransmitModel::setCwDelay.                                                                                          | 500 ms                                                                                                                    |
| Speed (CW)          | Control deslizante con QLineEdit (v0.9.8). Escriba un valor (5–100 WPM) directamente en el campo, o arrastre el control deslizante. Llama a TransmitModel::setCwSpeed.                                                                                         | 20 WPM                                                                                                                    |
| Sidetone            | Botón de alternancia. Activa o desactiva el monitor de tono lateral CW; llama a TransmitModel::setCwSidetone. También habilita/deshabilita el CwSidetoneGenerator del lado del cliente al unísono (v0.9.1+). Se enruta a la salida de audio seleccionada por el usuario (v26.5.3). | —                                                                                                                         |
| Sidetone volume     | Control deslizante con QLineEdit (v0.9.8). Escriba un valor (0–100) directamente en el campo, o arrastre el control deslizante. Llama a TransmitModel::setMonGainCw. También establece el volumen del generador de tono local al unísono.                         | 50                                                                                                                        |
| Pitch < / >         | QLineEdit con botones < / > (CwTriBtn). Escriba un valor (100–6000) o haga clic en los botones para incrementar en pasos de 10 Hz. Llama a TransmitModel::setCwPitch (v0.9.8, #2429).                                                                         | 600 Hz                                                                                                                    |
| L / R pan (CW)      | Control deslizante. Establece la panorámica estéreo del monitor CW (0–100); llama a TransmitModel::setMonPanCw y aplica panorámica de potencia constante al generador de tono local (v0.9.1+).                                                                  | 50 (centro)                                                                                                               |
| Breakin             | Botón de alternancia. Activa o desactiva el break-in completo (QSK); llama a TransmitModel::setCwBreakIn.                                                                                                                                                     | —                                                                                                                         |
| Iambic              | Botón de alternancia. Activa o desactiva el manipulador de paleta iámbica; llama a TransmitModel::setCwIambic.                                                                                                                                                 | —                                                                                                                         |

## Entrada directa de valores (v0.9.8)

En v0.9.8, las cuatro etiquetas de valor numérico en el subpanel CW se actualizaron de etiquetas de solo lectura a campos editables QLineEdit:

- **Delay (CW)** — Escriba cualquier valor de 0 a 2000 ms. Presione Enter o Tab para aplicar. El control deslizante adyacente se mueve para coincidir.
- **Speed (CW)** — Escriba cualquier valor de 5 a 100 WPM. Presione Enter o Tab para aplicar. El control deslizante adyacente se mueve para coincidir.
- **Sidetone volume** — Escriba cualquier valor de 0 a 100. Presione Enter o Tab para aplicar. El control deslizante adyacente se mueve para coincidir.
- **Pitch < / >** — Escriba cualquier valor de 100 a 6000 Hz. Presione Enter o Tab para aplicar. Los botones **<** y **>** incrementan en pasos de 10 Hz.

Cuando escribe un valor que está fuera del rango válido, el campo lo ajusta al límite válido más cercano (paridad con SmartSDR).

## Medidores ALC (v26.5.1+)

En v26.5.1, tanto el subpanel Phone como el CW recibieron medidores ALC idénticos que leen desde el medidor ALC de software (MeterModel::swAlcChanged). Esto reemplaza la ruta anterior de ALC por hardware (tensión RCA) que producía lecturas sin significado.

- Ambos medidores muestran en dBFS con un rango de -20 a 0 dBFS.
- La dirección de relleno es de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS.
- Aparece una zona roja por encima de -3 dBFS.
- Los valores fuera del rango [-20, 0] se ajustan al extremo más cercano.
- El único método updateAlc() controla ambos medidores simultáneamente, asegurando que los operadores de SSB y CW vean la misma lectura pico posterior al ALC.
- En v26.5.3, ambos medidores se inicializan a -20 dBFS al construirse, evitando un breve destello visual a 0 dBFS durante el inicio.

## Modo RADE y el control deslizante de nivel de micrófono

Cuando el modo RADE está activo, el control deslizante **Mic gain** funciona como un control de ganancia del lado del cliente en lugar de enviar un comando de nivel de micrófono a la radio. El valor del control deslizante se almacena bajo `PcMicGain` (la misma configuración utilizada cuando la fuente del micrófono es PC) y no se escribe en la propiedad `mic_level` de la radio mientras RADE está activo. Esto evita que el modo RADE sobrescriba silenciosamente su configuración de micrófono de hardware en la radio.

- El medidor **Level** permanece activo durante RX cuando RADE está habilitado, por lo que puede monitorear el nivel de entrada sin transmitir.
- Cuando el modo RADE se desactiva, el control deslizante vuelve a reflejar el `mic_level` de la radio y el medidor Level vuelve a su comportamiento de supresión normal (oculto durante RX a menos que `met_in_rx` esté activado).

## Salida de audio del tono lateral CW (v26.5.3)

En v26.5.3, el generador de tono lateral CW ahora se enruta al dispositivo de salida de audio seleccionado por el usuario en lugar de la salida predeterminada del sistema (#2899). Si tiene múltiples interfaces de audio configuradas en AetherSDR, el tono lateral sigue el dispositivo de salida seleccionado en **Settings > Audio > Output device**.

## Supresión del medidor de nivel durante recepción (v26.5.3)

En v26.5.3, la lógica de supresión del medidor de nivel de micrófono fue refactorizada. Anteriormente, el medidor Level se suprimía en línea dentro de `updateMeters()`, con excepciones para los modos PC mic y RADE. Ahora la verificación de supresión reside en un método dedicado `applyLevelMeterReceiveGate()` que se llama cada vez que el estado de transmisión de la radio cambia o cuando el modo RADE se activa o desactiva. Esto asegura que el medidor esté siempre correctamente atenuado o mostrado independientemente de qué evento desencadene el cambio de estado.

## Mapeo del medidor de compresión (v26.5.3)

En v26.5.3, el mapeo del medidor de compresión fue corregido. El MeterModel expone el medidor `COMPPEAK` como una cantidad de compresión positiva de 0–25 dB. La cara del medidor está invertida: 0 dB mostrado significa sin compresión, -25 dB significa compresión total. El medidor ahora convierte el valor positivo a negativo para la visualización, por lo que -25 corresponde a la compresión máxima y 0 a ninguna compresión.

## Consejos

- El tono y la panorámica del generador de tono del lado del cliente siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio. No necesita configurarlos por separado para la ruta local.
- Hacer doble clic en el control deslizante **L / R pan (CW)** lo restablece al centro (50).
- El medidor **Compression** lee 0 dB durante RX. Solo muestra un valor distinto de cero cuando el interbloqueo de la radio reporta el estado TRANSMITTING y el procesador de voz (**PROC**) está habilitado. Esto evita que se muestren lecturas obsoletas de la cadena de TX mientras está recibiendo.
- Con **Breakin** desactivado, las pulsaciones de tecla se ponen en cola y la TX debe activarse manualmente con PTT. Con **Breakin** activado (QSK), los flancos de las teclas activan la TX directamente y `break_in_delay` controla el tiempo de retención del relé. Ninguna envolvente PTT automática anula este comportamiento.
- El control deslizante **Delay (CW)** ahora actualiza su valor en caché inmediatamente cuando se arrastra, evitando que la radio devuelva el control deslizante a su posición anterior (v0.9.8, #2428).
- El medidor ALC en ambos paneles lee la misma fuente de medidor, por lo que puede monitorear el ALC independientemente de qué subpanel esté visible.

## Solución de problemas

- **No se escucha tono a pesar de que Sidetone está habilitado** — Confirme que el control deslizante **Sidetone volume** esté por encima de 0. También verifique que su dispositivo de salida de audio del sistema esté configurado correctamente en **Settings > Audio > Output device**, ya que el generador del lado del cliente ahora se enruta a la salida seleccionada por el usuario.
- **El botón Sidetone no está visible** — El subpanel CW solo aparece cuando el slice activo está en modo CW. Cambie el slice activo a CW en la radio; el panel del applet cambia automáticamente.
- **El tono no coincide con lo esperado** — El tono sigue el ajuste `cw_pitch` de la radio. Ajústelo usando **Pitch < / >** en el applet, que actualiza el ajuste de la radio en pasos de 10 Hz.
- **El medidor de compresión siempre muestra 0** — Esto es normal durante RX. El medidor está controlado por el estado TRANSMITTING del interbloqueo de la radio. Mostrará compresión solo mientras está transmitiendo con **PROC** habilitado.
- **Breakin OFF no mantiene la TX entre caracteres** — Con **Breakin** desactivado, AetherSDR ya no aplica una envolvente PTT automática. Active PTT manualmente antes de enviar y libérelo cuando termine.
- **El control deslizante Mic gain no tiene efecto en modo RADE**
