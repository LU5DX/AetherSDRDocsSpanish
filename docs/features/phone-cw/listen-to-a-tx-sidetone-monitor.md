# Applet de Phone/CW

El applet de Phone/CW es un panel de transmisión que reconoce el modo y muestra controles para Phone (micrófono, procesador, monitor) en modos de voz y cambia automáticamente a controles para CW (retardo, velocidad, tono local, iámbico, tono) cuando la franja activa está en modo CW.

En la v0.9.8, las cuatro etiquetas de valor de CW (Retardo, Velocidad, Volumen de tono local, Tono) ahora son widgets QLineEdit con QIntValidator — haga clic en cualquier valor y escriba un número directamente (paridad con SmartSDR).

En la v26.5.3, el tono local de CW ahora se encamina a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). Los indicadores ALC en ambos paneles ahora se inicializan en -20 dBFS al inicio.

En la v26.6.1, todos los estilos de deslizadores y etiquetas ahora usan ThemeManager para un tematizado consistente en toda la aplicación. El widget contenedor aplica una clase de tema de `applet/digi`.

En la v26.7.4, los cuatro indicadores (Nivel, Compresión, ALC Phone, ALC CW) ahora muestran una ventana emergente con el valor al pasar el ratón por encima, mostrando la lectura exacta con un decimal para un monitoreo preciso (#3936). Además, cuando la modulación local está activa, el cuadro combinado de fuente de micrófono está bloqueado en "PC" con un tooltip que explica que solo la entrada de PC está disponible.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet de Phone/CW requiere una conexión activa a la radio.
- Abra el Panel de Applets. Si no está visible, haga clic en View > Applet Panel.

## Pasos

### Modo Phone: habilitar el monitor de banda lateral

1. Haga clic en el botón P/CW en la barra lateral derecha para abrir el applet de Phone/CW.
2. Confirme que el applet muestra el panel de Phone (la franja activa debe estar en un modo de voz como SSB o AM).
3. Haga clic en MON para habilitar el monitor de banda lateral de TX. El botón se resalta cuando está activo.
4. Ajuste el deslizador de volumen del Monitor para establecer el nivel de reproducción (0–100).

### Modo Phone: ajustar la configuración del micrófono

1. Seleccione un perfil de Micrófono del menú desplegable para cargar un perfil de procesamiento de micrófono con nombre.
2. Seleccione la fuente de Micrófono del menú desplegable (las opciones incluyen MIC, BAL, LINE, ACC, PC, además de cualquier entrada de micrófono disponible de la radio). Cuando la modulación local está activa, el cuadro combinado está bloqueado en "PC" con un tooltip que explica que solo la entrada de PC está disponible.
3. Ajuste el deslizador de ganancia de Micrófono para establecer el nivel de entrada del micrófono (0–100). Cuando la fuente es PC, el valor se almacena localmente en `PcMicGain`.
4. Haga clic en +ACC para habilitar la mezcla de entrada de micrófono auxiliar.
5. Haga clic en PROC para alternar el procesador de voz.
6. Use el deslizador NOR/DX/DX+ para seleccionar el nivel del procesador: 0 (NOR), 1 (DX) o 2 (DX+).
7. Haga clic en DAX para habilitar DAX como fuente de audio de TX.

### Modo CW: ajustar la configuración de CW

1. Cambie la franja activa a un modo CW. El applet muestra automáticamente el panel de CW.
2. Ajuste el deslizador de Retardo para establecer el retardo de break-in de CW (0–2000 ms, paso 10). También puede escribir un valor directamente en el QLineEdit (0–2000).
3. Ajuste el deslizador de Velocidad para establecer la velocidad de manipulación de CW (5–100 WPM). También puede escribir un valor directamente en el QLineEdit (5–100).
4. Haga clic en Tono local para habilitar el monitor de CW. El botón se resalta cuando está activo.
5. Ajuste el deslizador de Volumen de tono local para establecer el nivel (0–100). También puede escribir un valor directamente en el QLineEdit (0–100).
6. Use el deslizador L / R pan (CW) para establecer la panorámica estéreo (doble clic para centrar en 50).
7. Haga clic en Breakin para alternar el break-in completo (QSK).
8. Haga clic en Iambic para alternar el manipulador de paletas iámbico.
9. Use los botones Tono < / > para avanzar en pasos de 10 Hz, o escriba un valor directamente en el QLineEdit (100–6000 Hz).

### Lectura de valores de indicadores con el ratón

1. Mueva el cursor del ratón sobre cualquier indicador (Nivel, Compresión, ALC Phone, ALC CW).
2. Aparece una ventana emergente que muestra el valor numérico exacto con un decimal.
3. El indicador de Nivel muestra el valor en dB (ej., "-12.3 dB").
4. El indicador de Compresión muestra la cantidad de compresión como un valor positivo en dB (ej., "15.0 dB" para -15 dB de compresión).
5. Los indicadores ALC muestran el valor en dBFS (ej., "-5.2 dBFS").

## Qué hace cada control

| Control             | Qué hace                                                                                                                                                                                                                                                                                                              | Valor predeterminado                                       |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------|
| MON                 | Habilita el monitor de banda lateral de TX (panel de Phone).                                                                                                                                                                                                                                                          | —                                                          |
| Volumen del monitor | Establece el nivel de reproducción del monitor de banda lateral.                                                                                                                                                                                                                                                      | —                                                          |
| DAX                 | Habilita DAX como fuente de audio de TX.                                                                                                                                                                                                                                                                              | —                                                          |
| Perfil de micrófono | Carga un perfil de procesamiento de micrófono con nombre.                                                                                                                                                                                                                                                             | —                                                          |
| Fuente de micrófono | Selecciona la fuente de entrada del micrófono. Cuando la modulación local está activa, el cuadro combinado está bloqueado en "PC" con un tooltip que explica que solo la entrada de PC está disponible (v26.7.4).                                                                                                       | —                                                          |
| Ganancia de micrófono | Ajusta el nivel de entrada del micrófono. Para fuente PC usa la persistencia local de PcMicGain.                                                                                                                                                                                                                      | 50                                                         |
| +ACC                | Habilita la mezcla de entrada de micrófono auxiliar.                                                                                                                                                                                                                                                                  | —                                                          |
| PROC                | Alterna el procesador de voz.                                                                                                                                                                                                                                                                                         | —                                                          |
| NOR/DX/DX+          | Deslizador de nivel del procesador de tres posiciones.                                                                                                                                                                                                                                                                | 0                                                          |
| Retardo (CW)        | Establece el retardo de break-in de CW. El QLineEdit adyacente acepta valores escritos (0–2000) (v0.9.8, #2429). En v0.9.8, se corrigió setCwDelay para almacenar en caché el valor inmediatamente, de modo que la emisión de la radio no haga que el deslizador vuelva a su posición anterior (#2428).               | 500 ms                                                     |
| Velocidad (CW)      | Establece la velocidad de manipulación de CW. El QLineEdit adyacente acepta valores escritos (5–100) (v0.9.8, #2429).                                                                                                                                                                                                | 20 WPM                                                     |
| Tono local          | Alterna el monitor de tono local de CW. También habilita/deshabilita el CwSidetoneGenerator local de baja latencia del lado del cliente de forma sincronizada (v0.9.1+). Tanto el monitor alimentado por DAX de la radio como el tono local de PortAudio son controlados por este único botón. El tono y la panorámica siempre siguen automáticamente a cw_pitch y mon_pan_cw de la radio. En v26.5.3, el audio del tono local se encamina a la salida de audio seleccionada por el usuario (#2899). | —                                                          |
| Volumen de tono local | Establece el volumen del monitor de CW. También establece el volumen del generador de tono local de forma sincronizada. El QLineEdit adyacente acepta valores escritos (0–100) (v0.9.8, #2429).                                                                                                                       | 50                                                         |
| L / R pan (CW)      | Establece la panorámica estéreo del monitor de CW. Aplica panorámica de potencia constante al generador de tono local (v0.9.1+). Doble clic para centrar en 50.                                                                                                                                                      | 50                                                         |
| Breakin             | Alterna el break-in completo (QSK). En v0.9.7, las rutas de teclado/MIDI de CW ahora respetan completamente esta configuración: con Breakin activado (QSK), los flancos de la tecla activan TX y break_in_delay mantiene el relé; con Breakin desactivado, las teclas se ponen en cola y el operador activa PTT manualmente. | —                                                          |
| Iambic              | Alterna el manipulador de paletas iámbico.                                                                                                                                                                                                                                                                            | —                                                          |
| Tono < / >          | QLineEdit con botones < / > (CwTriBtn). Escriba un valor (100–6000) o haga clic en los botones para avanzar en pasos de 10 Hz (v0.9.8, #2429).                                                                                                                                                                         | 600 Hz                                                     |
| Nivel               | Nivel pico de entrada del micrófono en dBFS (panel de Phone). Suprimido a -150 cuando met_in_rx está desactivado y no se está transmitiendo.                                                                                                                                                                           | —                                                          |
| Compresión          | Cantidad de compresión de voz en dB (panel de Phone). Controlado por el estado de enclavamiento TRANSMITTING de la radio y la habilitación del procesador de voz: lee 0 dB durante RX (v0.9.7). En v26.5.3, el valor del medidor de compresión se invierte: 0 dB = sin compresión, -25 dB = compresión total.         | —                                                          |
| ALC (panel de Phone) | Muestra la lectura del control automático de nivel desde MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Recableado de HWALC (tensión RCA) al medidor SW ALC en v26.5.1 (#2552). En v26.5.3, se inicializa a -20 dBFS al inicio. Reflejado por un indicador idéntico en el subpanel de CW. En v26.7.4, admite ventana emergente con valor al pasar el ratón para una lectura exacta (#3936). | —                                                          |
| ALC (panel de CW)   | Refleja el indicador ALC del panel de Phone; ambos leen de MeterModel::swAlcChanged para lecturas consistentes en voz y CW. Añadido en v26.5.1 (#2552) como parte de la división del medidor SW ALC. Usa el modo HGauge::setFillFromRight. En v26.5.3, se inicializa a -20 dBFS al inicio. En v26.7.4, admite ventana emergente con valor al pasar el ratón para una lectura exacta (#3936). | —                                                          |

## Información de los medidores

| Medidor              | Qué muestra                                                                                                                 | Rango válido              | Notas                                                                                                                                 |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| Indicador de Nivel   | Nivel pico de entrada del micrófono en dBFS. Al pasar el ratón, muestra el valor exacto con un decimal (v26.7.4, #3936).   | -40 a +10 dBFS (rojo > 0) | Suprimido a -150 cuando met_in_rx está desactivado y no se transmite.                                                                |
| Indicador de Compresión | Cantidad de compresión de voz en dB (relleno invertido). En v26.5.3, 0 dB = sin compresión, -25 dB = compresión total. Al pasar el ratón, muestra la cantidad de compresión como un valor positivo (v26.7.4, #3936). | -25 a 0 dB               | Controlado por el estado de enclavamiento TRANSMITTING de la radio y la habilitación del procesador de voz: lee 0 dB durante RX (v0.9.7). En v26.5.3, invertido respecto a versiones anteriores. |
| Indicador ALC (Phone) | Control automático de nivel — pico SSB posterior al ALC de software, leído de MeterModel::swAlcChanged. Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Al pasar el ratón, muestra el valor exacto con un decimal en dBFS (v26.7.4, #3936). | -20 a 0 dBFS (rojo > -3) | Recableado de HWALC (tensión RCA) al medidor SW ALC en v26.5.1 (#2552). En v26.5.3, se inicializa a -20 dBFS al inicio. Reflejado por un indicador idéntico en el panel de CW.                |
| Indicador ALC (CW)   | Reflejo del indicador ALC del panel de Phone, con la misma escala. Ambos leen de MeterModel::swAlcChanged. Al pasar el ratón, muestra el valor exacto con un decimal en dBFS (v26.7.4, #3936). | -20 a 0 dBFS (rojo > -3) | Añadido en v26.5.1 (#2552) como parte de la división del medidor SW ALC. Usa el modo HGauge::setFillFromRight. En v26.5.3, se inicializa a -20 dBFS al inicio.                                      |

## Consejos

- El botón de Tono local y el deslizador de Volumen de tono local controlan ambas rutas de audio (monitor DAX de la radio y generador del lado del cliente) conjuntamente. No hay un control independiente para habilitar o ajustar el tono local por separado.
- El tono siempre sigue automáticamente la configuración de tono de CW de la radio. Use el widget Tono < / > para cambiar el tono de CW de la radio, y tanto el tono de decodificación como el tono local se actualizarán en consecuencia.
- El botón MON y el botón de Tono local son controles separados en paneles separados. MON se aplica a modos de voz; Tono local se aplica al modo CW.
- Cuando la fuente del micrófono está configurada en PC, el indicador de Nivel aparece inmediatamente al conectar. En v0.9.7, lo mismo aplica cuando el modo RADE está activo: el indicador de Nivel se muestra durante RX independientemente de la configuración de `met_in_rx`. En otros modos de fuente de micrófono (sin RADE activo), el indicador se suprime cuando `met_in_rx` está desactivado y la radio no está transmitiendo.
- Cuando el modo RADE está activo, el deslizador de ganancia de Micrófono actúa como un control de ganancia RADE del lado del cliente y su valor se almacena en `PcMicGain`. El deslizador no envía un comando de nivel de micrófono a la radio en este estado, lo que evita sobrescribir la configuración de micrófono de hardware.
- En v0.9.8, los cuatro campos QLineEdit de CW (Retardo, Velocidad, Volumen de tono local, Tono) aceptan entrada numérica directa. Escriba un valor y presione Enter para aplicarlo. Los valores se limitan automáticamente al rango válido.
- El bus de tono local es compartido con los tonos Quindar (mutuamente excluyentes a nivel de modo).
- El indicador ALC tanto en el panel de Phone como en el de CW ahora lee del medidor ALC de software (MeterModel::swAlcChanged).
