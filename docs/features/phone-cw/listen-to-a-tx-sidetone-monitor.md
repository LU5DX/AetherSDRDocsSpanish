# Applet de Phone/CW

El applet de Phone/CW es un panel de transmisión sensible al modo que muestra controles de Phone (micrófono, procesador, monitor) en modos de voz y cambia automáticamente a controles de CW (retardo, velocidad, tono lateral, iámbico, tono) cuando el slice activo está en modo CW.

En v0.9.8, las cuatro etiquetas de valor CW (Delay, Speed, Sidetone Volume, Pitch) ahora son widgets QLineEdit con QIntValidator — haga clic en cualquier valor y escriba un número directamente (paridad con SmartSDR).

En v26.5.3, el tono lateral de CW ahora se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). Los indicadores ALC en ambos paneles ahora se inicializan a -20 dBFS al inicio.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet de Phone/CW requiere una conexión activa a la radio.
- Abra el Panel de Applets. Si no está visible, haga clic en View > Applet Panel.

## Pasos

### Modo Phone: active el monitor de banda lateral

1. Haga clic en el botón de la bandeja P/CW en la barra lateral derecha para abrir el applet de Phone/CW.
2. Confirme que el applet muestra el panel de Phone (el slice activo debe estar en un modo de voz como SSB o AM).
3. Haga clic en MON para activar el monitor de banda lateral de TX. El botón se resalta cuando está activo.
4. Ajuste el deslizador de volumen del monitor para definir el nivel de reproducción (0–100).

### Modo Phone: ajuste la configuración del micrófono

1. Seleccione un perfil de micrófono del menú desplegable para cargar un perfil de procesamiento de micrófono con nombre.
2. Seleccione la fuente de micrófono del menú desplegable (las opciones incluyen MIC, BAL, LINE, ACC, PC, además de cualquier entrada de micrófono disponible en la radio).
3. Ajuste el deslizador de ganancia del micrófono para definir el nivel de entrada del micrófono (0–100). Cuando la fuente es PC, el valor se almacena localmente en `PcMicGain`.
4. Haga clic en +ACC para activar la mezcla de entrada del micrófono auxiliar.
5. Haga clic en PROC para alternar el procesador de voz.
6. Use el deslizador NOR/DX/DX+ para seleccionar el nivel del procesador: 0 (NOR), 1 (DX) o 2 (DX+).
7. Haga clic en DAX para habilitar DAX como fuente de audio de TX.

### Modo CW: ajuste la configuración de CW

1. Cambie el slice activo a un modo CW. El applet muestra automáticamente el panel de CW.
2. Ajuste el deslizador de retardo para definir el retardo de break-in de CW (0–2000 ms, paso 10). También puede escribir un valor directamente en el QLineEdit (0–2000).
3. Ajuste el deslizador de velocidad para definir la velocidad de tecleo CW (5–100 WPM). También puede escribir un valor directamente en el QLineEdit (5–100).
4. Haga clic en Sidetone para activar el monitor de CW. El botón se resalta cuando está activo.
5. Ajuste el deslizador de volumen del tono lateral para definir el nivel (0–100). También puede escribir un valor directamente en el QLineEdit (0–100).
6. Use el deslizador L / R pan (CW) para definir la panorámica estéreo (doble clic para re-centrar en 50).
7. Haga clic en Breakin para alternar el break-in completo (QSK).
8. Haga clic en Iambic para alternar el manipulador de paletas iámbico.
9. Use los botones Pitch < / > para avanzar en pasos de 10 Hz, o escriba un valor directamente en el QLineEdit (100–6000 Hz).

## Qué hace cada control

| Control             | Qué hace                                                                                                                                                                                                                                                                                                     | Valor predeterminado                                   |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------|
| MON                 | Activa el monitor de banda lateral de TX (panel de Phone).                                                                                                                                                                                                                                                   | —                                                      |
| Monitor volume      | Define el nivel de reproducción del monitor de banda lateral.                                                                                                                                                                                                                                                | —                                                      |
| DAX                 | Activa DAX como fuente de audio de TX.                                                                                                                                                                                                                                                                       | —                                                      |
| Mic profile         | Carga un perfil de procesamiento de micrófono con nombre.                                                                                                                                                                                                                                                    | —                                                      |
| Mic source          | Selecciona la fuente de entrada del micrófono.                                                                                                                                                                                                                                                               | —                                                      |
| Mic gain            | Ajusta el nivel de entrada del micrófono. Para fuente PC, usa la persistencia local de `PcMicGain`.                                                                                                                                                                                                         | 50                                                     |
| +ACC                | Activa la mezcla de entrada del micrófono auxiliar.                                                                                                                                                                                                                                                          | —                                                      |
| PROC                | Alterna el procesador de voz.                                                                                                                                                                                                                                                                                | —                                                      |
| NOR/DX/DX+          | Deslizador de nivel del procesador de tres posiciones.                                                                                                                                                                                                                                                       | 0                                                      |
| Delay (CW)          | Define el retardo de break-in de CW. El QLineEdit adyacente acepta valores escritos (0–2000) (v0.9.8, #2429). En v0.9.8, se corrigió setCwDelay para almacenar en caché el valor inmediatamente, de modo que la emisión de la radio no devuelva el deslizador a su posición anterior (#2428).                 | 500 ms                                                 |
| Speed (CW)          | Define la velocidad de tecleo CW. El QLineEdit adyacente acepta valores escritos (5–100) (v0.9.8, #2429).                                                                                                                                                                                                   | 20 WPM                                                 |
| Sidetone            | Alterna el monitor de tono lateral de CW. También activa/desactiva el CwSidetoneGenerator local de baja latencia del lado del cliente de forma sincronizada (v0.9.1+). Tanto el monitor alimentado por DAX de la radio como el tono lateral local de PortAudio son controlados por este único botón. El tono y la panorámica siguen automáticamente a `cw_pitch` y `mon_pan_cw` de la radio. En v26.5.3, el audio del tono lateral se enruta a la salida de audio seleccionada por el usuario (#2899). | —                                                      |
| Sidetone volume     | Define el volumen del monitor de CW. También define el volumen del generador de tono lateral local de forma sincronizada. El QLineEdit adyacente acepta valores escritos (0–100) (v0.9.8, #2429).                                                                                                            | 50                                                     |
| L / R pan (CW)      | Define la panorámica estéreo del monitor de CW. Aplica panorámica de potencia constante al generador de tono lateral local (v0.9.1+). Doble clic para re-centrar en 50.                                                                                                                                     | 50                                                     |
| Breakin             | Alterna el break-in completo (QSK). En v0.9.7, las rutas de teclado/MIDI de CW ahora respetan completamente esta configuración: con Breakin activado (QSK), los flancos de la tecla activan TX y `break_in_delay` mantiene el relé; con Breakin desactivado, las teclas se ponen en cola y el operador activa PTT manualmente. | —                                                      |
| Iambic              | Alterna el manipulador de paletas iámbico.                                                                                                                                                                                                                                                                   | —                                                      |
| Pitch < / >         | QLineEdit con botones < / > (CwTriBtn). Escriba un valor (100–6000) o haga clic en los botones para avanzar en pasos de 10 Hz (v0.9.8, #2429).                                                                                                                                                                | 600 Hz                                                 |
| Level               | Nivel pico de entrada del micrófono en dBFS (panel de Phone). Suprimido a -150 cuando `met_in_rx` está desactivado y no se está transmitiendo.                                                                                                                                                                | —                                                      |
| Compression         | Cantidad de compresión de voz en dB (panel de Phone). Controlado por el estado de interbloqueo TRANSMITTING de la radio y la activación del procesador de voz: lee 0 dB durante RX (v0.9.7). En v26.5.3, el valor del medidor de compresión está invertido: 0 dB = sin compresión, -25 dB = compresión completa. | —                                                      |
| ALC (panel Phone)   | Muestra la lectura de control automático de nivel de MeterModel::swAlcChanged (pico SSB post-ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Reconectado de HWALC (voltaje RCA) al medidor SW ALC en v26.5.1 (#2552). En v26.5.3, se inicializa a -20 dBFS al inicio. Espejado por un indicador idéntico en el subpanel de CW. | —                                                      |
| ALC (panel CW)      | Espeja el indicador ALC del panel Phone; ambos leen de MeterModel::swAlcChanged para lecturas consistentes entre voz y CW. Añadido en v26.5.1 (#2552) como parte de la división del medidor SW ALC. Usa el modo HGauge::setFillFromRight. En v26.5.3, se inicializa a -20 dBFS al inicio.                   | —                                                      |

## Información de los medidores

| Medidor              | Qué muestra                                                                                                                               | Rango válido             | Notas                                                                                                                           |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Indicador Level      | Nivel pico de entrada del micrófono en dBFS.                                                                                              | -40 a +10 dBFS (rojo > 0) | Suprimido a -150 cuando `met_in_rx` está desactivado y no se está transmitiendo.                                               |
| Indicador Compression| Cantidad de compresión de voz en dB (llenado inverso). En v26.5.3, 0 dB = sin compresión, -25 dB = compresión completa.                   | -25 a 0 dB               | Controlado por el estado de interbloqueo TRANSMITTING de la radio y la activación del procesador de voz: lee 0 dB durante RX (v0.9.7). En v26.5.3, invertido respecto a versiones anteriores. |
| Indicador ALC (Phone)| Control automático de nivel — pico SSB post-ALC de software, leído de MeterModel::swAlcChanged. Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. | -20 a 0 dBFS (rojo > -3) | Reconectado de HWALC (voltaje RCA) al medidor SW ALC en v26.5.1 (#2552). En v26.5.3, se inicializa a -20 dBFS al inicio. Espejado por indicador idéntico en el panel CW. |
| Indicador ALC (CW)   | Espejo del indicador ALC del panel Phone, con la misma escala. Ambos leen de MeterModel::swAlcChanged.                                    | -20 a 0 dBFS (rojo > -3) | Añadido en v26.5.1 (#2552) como parte de la división del medidor SW ALC. Usa el modo HGauge::setFillFromRight. En v26.5.3, se inicializa a -20 dBFS al inicio. |

## Consejos

- El botón Sidetone y el deslizador de volumen del tono lateral controlan ambas rutas de audio (monitor DAX de la radio y generador del lado del cliente) de forma conjunta. No existe un control independiente para activar o ajustar el tono lateral local por separado.
- El tono (Pitch) siempre sigue automáticamente la configuración de tono CW de la radio. Use el widget Pitch < / > para cambiar el tono CW de la radio, y tanto el tono de decodificación como el tono lateral se actualizarán en consecuencia.
- El botón MON y el botón Sidetone son controles separados en paneles separados. MON se aplica a modos de voz; Sidetone se aplica al modo CW.
- Cuando la fuente del micrófono está configurada en PC, el indicador Level aparece inmediatamente al conectar. En v0.9.7, lo mismo aplica cuando el modo RADE está activo: el indicador Level se muestra durante RX independientemente de la configuración `met_in_rx`. En otros modos de fuente de micrófono (sin RADE activo), el indicador se suprime cuando `met_in_rx` está desactivado y la radio no está transmitiendo.
- Cuando el modo RADE está activo, el deslizador de ganancia del micrófono actúa como un control de ganancia RADE del lado del cliente y su valor se almacena en `PcMicGain`. El deslizador no envía un comando de nivel de micrófono a la radio en este estado, lo que evita sobrescribir la configuración de micrófono por hardware.
- En v0.9.8, los cuatro campos QLineEdit de CW (Delay, Speed, Sidetone Volume, Pitch) aceptan entrada numérica directa. Escriba un valor y presione Enter para aplicarlo. Los valores se limitan automáticamente al rango válido.
- El bus de tono lateral se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).
- El indicador ALC en ambos paneles (Phone y CW) ahora lee del medidor ALC de software (MeterModel::swAlcChanged), proporcionando lecturas significativas en dBFS en lugar de los datos sin sentido de HWALC (voltaje RCA) anteriores. Ambos indicadores son idénticos y se actualizan sincronizadamente.
- En v26.5.3, el valor del medidor de compresión está invertido: 0 dB representa sin compresión, y -25 dB representa compresión completa. Esto coincide con la convención de visualización del medidor donde el indicador se llena hacia el lado negativo durante la compresión.

## Solución de problemas

- **El botón MON o Sidetone no tiene efecto** — Confirme que la radio está conectada y que el modo del slice activo coincide con el panel que se muestra (Phone vs. CW). El applet cambia de panel automáticamente según el modo del slice activo.
- **El tono lateral no produce audio** — Verifique que la salida de audio de su sistema esté configurada correctamente. El tono lateral del lado del cliente es generado localmente por AetherSDR; confirme que el botón Sidetone esté activo. En v26.5.3, verifique que el audio del tono lateral esté enrutado al dispositivo de audio correcto en la configuración de su sistema (#2899). En Windows, el flujo de tono lateral ahora comienza inmediatamente al conectar (v0.9.3, #2105).
- **El tono del tono lateral es incorrecto** — El tono se deriva automáticamente de la configuración `cw_pitch` de la radio. Ajuste el tono usando el widget Pitch < / > en el panel de CW.
- **El indicador Level no aparece al conectar** — Si la fuente del micrófono está configurada en PC, o si el modo RADE está activo, el indicador Level aparece inmediatamente al conectar y permanece visible durante RX. Para otras fuentes de micrófono sin RADE activo, el indicador se suprime hasta que se active `met_in_rx` o la radio comience a transmitir.
- **El deslizador de ganancia del micrófono parece no tener efecto con RADE activo** — Cuando el modo RADE está activo, el deslizador de ganancia del micrófono controla solo la ganancia RADE del lado del cliente y no envía comandos a la radio. Este comportamiento es esperado. El valor se guarda como `PcMicGain`.
- **El deslizador vuelve a su posición anterior al ajustar el retardo de CW** — Este problema se corrigió en v0.9.8 (#2428). El valor de retardo ahora se almacena en caché inmediatamente al configurarse, lo que evita que la radio
