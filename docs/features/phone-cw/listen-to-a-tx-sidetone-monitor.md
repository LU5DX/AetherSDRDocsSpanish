# Applet Phone/CW

El applet Phone/CW es un panel de transmisión sensible al modo que muestra controles de Phone (micrófono, procesador, monitor) en modos de voz y cambia automáticamente a controles de CW (retardo, velocidad, tono lateral, iámbico, tono) cuando la franja activa está en modo CW.

En la v0.9.8, las cuatro etiquetas de valor de CW (Delay, Speed, Sidetone Volume, Pitch) son ahora widgets QLineEdit con QIntValidator: haga clic en cualquier valor y escriba un número directamente (paridad con SmartSDR).

En la v26.5.3, el tono lateral de CW ahora se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). Los indicadores ALC en ambos paneles ahora se inicializan a -20 dBFS al inicio.

En la v26.6.1, todos los estilos de deslizadores y etiquetas ahora usan ThemeManager para una temática consistente en toda la aplicación. El widget contenedor aplica una clase de tema de `applet/digi`.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone/CW requiere una conexión activa con la radio.
- Abra el Applet Panel. Si no está visible, haga clic en View > Applet Panel.

## Pasos

### Modo Phone: activar el monitor de banda lateral

1. Haga clic en el botón de la bandeja P/CW en la barra lateral derecha para abrir el applet Phone/CW.
2. Confirme que el applet muestra el panel Phone (la franja activa debe estar en un modo de voz como SSB o AM).
3. Haga clic en MON para activar el monitor de banda lateral de TX. El botón se resalta cuando está activo.
4. Ajuste el deslizador Monitor volume para establecer el nivel de reproducción (0–100).

### Modo Phone: ajustar la configuración del micrófono

1. Seleccione un perfil Mic del menú desplegable para cargar un perfil de procesamiento de micrófono con nombre.
2. Seleccione la fuente Mic del menú desplegable (las opciones incluyen MIC, BAL, LINE, ACC, PC, además de las que provengan de las entradas de micrófono disponibles de la radio).
3. Ajuste el deslizador Mic gain para establecer el nivel de entrada del micrófono (0–100). Cuando la fuente es PC, el valor se almacena localmente en `PcMicGain`.
4. Haga clic en +ACC para activar la mezcla de entrada del micrófono auxiliar.
5. Haga clic en PROC para activar o desactivar el procesador de voz.
6. Use el deslizador NOR/DX/DX+ para seleccionar el nivel del procesador: 0 (NOR), 1 (DX) o 2 (DX+).
7. Haga clic en DAX para habilitar DAX como fuente de audio de TX.

### Modo CW: ajustar la configuración de CW

1. Cambie la franja activa a un modo CW. El applet muestra automáticamente el panel CW.
2. Ajuste el deslizador Delay para establecer el retardo de inserción de CW (0–2000 ms, paso de 10). También puede escribir un valor directamente en el QLineEdit (0–2000).
3. Ajuste el deslizador Speed para establecer la velocidad de manipulación de CW (5–100 WPM). También puede escribir un valor directamente en el QLineEdit (5–100).
4. Haga clic en Sidetone para activar el monitor de CW. El botón se resalta cuando está activo.
5. Ajuste el deslizador Sidetone volume para establecer el nivel (0–100). También puede escribir un valor directamente en el QLineEdit (0–100).
6. Use el deslizador L / R pan (CW) para establecer el paneo estéreo (haga doble clic para volver a centrar en 50).
7. Haga clic en Breakin para activar o desactivar la inserción completa (QSK).
8. Haga clic en Iambic para activar o desactivar el manipulador de paletas iámbico.
9. Use los botones Pitch < / > para cambiar en pasos de 10 Hz, o escriba un valor directamente en el QLineEdit (100–6000 Hz).

## Qué hace cada control

| Control             | Qué hace                                                                                                                                                                                                                                                                                                     | Valor predeterminado                                      |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------|
| MON                 | Activa el monitor de banda lateral de TX (panel Phone).                                                                                                                                                                                                                                                       | —                                                        |
| Monitor volume      | Establece el nivel de reproducción del monitor de banda lateral.                                                                                                                                                                                                                                              | —                                                        |
| DAX                 | Habilita DAX como fuente de audio de TX.                                                                                                                                                                                                                                                                      | —                                                        |
| Mic profile         | Carga un perfil de procesamiento de micrófono con nombre.                                                                                                                                                                                                                                                     | —                                                        |
| Mic source          | Selecciona la fuente de entrada del micrófono.                                                                                                                                                                                                                                                                | —                                                        |
| Mic gain            | Ajusta el nivel de entrada del micrófono. Para fuente PC, usa la persistencia local PcMicGain.                                                                                                                                                                                                               | 50                                                       |
| +ACC                | Activa la mezcla de entrada del micrófono auxiliar.                                                                                                                                                                                                                                                           | —                                                        |
| PROC                | Activa o desactiva el procesador de voz.                                                                                                                                                                                                                                                                      | —                                                        |
| NOR/DX/DX+          | Deslizador de nivel del procesador de tres posiciones.                                                                                                                                                                                                                                                        | 0                                                        |
| Delay (CW)          | Establece el retardo de inserción de CW. El QLineEdit adyacente acepta valores escritos (0–2000) (v0.9.8, #2429). En la v0.9.8, se corrigió setCwDelay para almacenar en caché el valor inmediatamente, de modo que la emisión de la radio no devuelva el deslizador a su posición anterior (#2428).          | 500 ms                                                   |
| Speed (CW)          | Establece la velocidad de manipulación de CW. El QLineEdit adyacente acepta valores escritos (5–100) (v0.9.8, #2429).                                                                                                                                                                                        | 20 WPM                                                   |
| Sidetone            | Activa o desactiva el monitor de tono lateral de CW. También habilita/deshabilita el CwSidetoneGenerator de baja latencia del lado del cliente de forma sincronizada (v0.9.1+). Tanto el monitor alimentado por DAX de la radio como el tono lateral local de PortAudio son controlados por este único botón. Pitch y pan siguen automáticamente cw_pitch y mon_pan_cw de la radio. En la v26.5.3, el audio del tono lateral se enruta a la salida de audio seleccionada por el usuario (#2899). | —                                                        |
| Sidetone volume     | Establece el volumen del monitor de CW. También establece el volumen del generador de tono lateral local de forma sincronizada. El QLineEdit adyacente acepta valores escritos (0–100) (v0.9.8, #2429).                                                                                                       | 50                                                       |
| L / R pan (CW)      | Establece el paneo estéreo del monitor de CW. Aplica paneo de potencia constante al generador de tono lateral local (v0.9.1+). Haga doble clic para volver a centrar en 50.                                                                                                                                 | 50                                                       |
| Breakin             | Activa o desactiva la inserción completa (QSK). En la v0.9.7, las rutas de teclado/MIDI de CW ahora respetan completamente esta configuración: con Breakin activado (QSK), los flancos de las teclas activan TX y break_in_delay mantiene el relé; con Breakin desactivado, las teclas se ponen en cola y el operador activa PTT manualmente. | —                                                        |
| Iambic              | Activa o desactiva el manipulador de paletas iámbico.                                                                                                                                                                                                                                                         | —                                                        |
| Pitch < / >         | QLineEdit con botones < / > (CwTriBtn). Escriba un valor (100–6000) o haga clic en los botones para cambiar en pasos de 10 Hz (v0.9.8, #2429).                                                                                                                                                                | 600 Hz                                                   |
| Level               | Nivel máximo de entrada del micrófono en dBFS (panel Phone). Suprimido a -150 cuando met_in_rx está desactivado y no se transmite.                                                                                                                                                                            | —                                                        |
| Compression         | Cantidad de compresión de voz en dB (panel Phone). Controlado por el estado de interbloqueo TRANSMITTING de la radio y la activación del procesador de voz: lee 0 dB durante RX (v0.9.7). En la v26.5.3, el valor del medidor de compresión está invertido: 0 dB = sin compresión, -25 dB = compresión completa. | —                                                        |
| ALC (panel Phone)   | Muestra la lectura de control automático de nivel desde MeterModel::swAlcChanged (pico SSB post-ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Reconectado desde HWALC (voltaje RCA) al medidor SW ALC en la v26.5.1 (#2552). En la v26.5.3, se inicializa a -20 dBFS al inicio. Es reflejado por un indicador idéntico en el subpanel CW. | —                                                        |
| ALC (panel CW)      | Refleja el indicador ALC del panel Phone; ambos leen desde MeterModel::swAlcChanged para obtener lecturas consistentes en voz y CW. Añadido en la v26.5.1 (#2552) como parte de la división del medidor SW ALC. Usa el modo HGauge::setFillFromRight. En la v26.5.3, se inicializa a -20 dBFS al inicio.      | —                                                        |

## Información de los medidores

| Medidor              | Qué muestra                                                                                                                               | Rango válido             | Notas                                                                                                                           |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Level gauge          | Nivel máximo de entrada del micrófono en dBFS.                                                                                            | -40 a +10 dBFS (rojo > 0) | Suprimido a -150 cuando met_in_rx está desactivado y no se transmite.                                                          |
| Compression gauge    | Cantidad de compresión de voz en dB (llenado invertido). En la v26.5.3, 0 dB = sin compresión, -25 dB = compresión completa.             | -25 a 0 dB               | Controlado por el estado de interbloqueo TRANSMITTING de la radio y la activación del procesador de voz: lee 0 dB durante RX (v0.9.7). En la v26.5.3, invertido respecto a versiones anteriores. |
| ALC gauge (Phone)    | Control automático de nivel — pico SSB post-ALC de software, leído de MeterModel::swAlcChanged. Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. | -20 a 0 dBFS (rojo > -3) | Reconectado desde HWALC (voltaje RCA) al medidor SW ALC en la v26.5.1 (#2552). En la v26.5.3, se inicializa a -20 dBFS al inicio. Reflejado por un indicador idéntico en el panel CW. |
| ALC gauge (CW)       | Reflejo del indicador ALC del panel Phone, con la misma escala. Ambos leen desde MeterModel::swAlcChanged.                                 | -20 a 0 dBFS (rojo > -3) | Añadido en la v26.5.1 (#2552) como parte de la división del medidor SW ALC. Usa el modo HGauge::setFillFromRight. En la v26.5.3, se inicializa a -20 dBFS al inicio. |

## Consejos

- El botón Sidetone y el deslizador Sidetone volume controlan ambas rutas de audio (monitor DAX de la radio y generador del lado del cliente) de forma conjunta. No hay un control separado para activar o ajustar el tono lateral local de forma independiente.
- Pitch sigue automáticamente la configuración de tono CW de la radio. Use el widget Pitch < / > para cambiar el tono CW de la radio, y tanto el tono de decodificación como el tono lateral se actualizarán en consecuencia.
- El botón MON y el botón Sidetone son controles separados en paneles separados. MON se aplica a modos de voz; Sidetone se aplica al modo CW.
- Cuando la fuente de micrófono está configurada en PC, el Level gauge aparece inmediatamente al conectar. En la v0.9.7, esto también se aplica cuando el modo RADE está activo: el Level gauge se muestra durante RX independientemente de la configuración `met_in_rx`. En otros modos de fuente de micrófono (sin RADE activo), el indicador se suprime cuando `met_in_rx` está desactivado y la radio no está transmitiendo.
- Cuando el modo RADE está activo, el deslizador Mic gain actúa como un control de ganancia RADE del lado del cliente y su valor se almacena en `PcMicGain`. En este estado, el deslizador no envía un comando de nivel de micrófono a la radio, lo que evita sobrescribir la configuración de micrófono del hardware.
- En la v0.9.8, los cuatro campos QLineEdit de CW (Delay, Speed, Sidetone Volume, Pitch) aceptan entrada numérica directa. Escriba un valor y presione Enter para aplicarlo. Los valores se limitan automáticamente al rango válido.
- El bus de tono lateral se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).
- El indicador ALC en ambos paneles (Phone y CW) ahora lee del medidor ALC de software (MeterModel::swAlcChanged), proporcionando lecturas significativas en dBFS en lugar de los anteriores datos sin sentido de HWALC (voltaje RCA). Ambos indicadores son idénticos y se actualizan de forma sincronizada.
- En la v26.5.3, el valor del medidor de compresión está invertido: 0 dB representa sin compresión, y -25 dB representa compresión completa. Esto coincide con la convención de visualización del medidor donde el indicador se llena hacia el lado negativo durante la compresión.
- En la v26.6.1, todos los estilos de deslizadores y etiquetas ahora usan ThemeManager para una temática consistente en toda la aplicación. El widget contenedor aplica una clase de tema de `applet/digi`.

## Solución de problemas

- **El botón MON o Sidetone no tiene efecto** — Confirme que la radio está conectada y que el modo de la franja activa coincide con el panel que se muestra (Phone vs. CW). El applet cambia de panel automáticamente según el modo de la franja activa.
- **El tono lateral no produce audio** — Verifique que la salida de audio de su sistema esté configurada correctamente. El tono lateral del lado del cliente es generado localmente por AetherSDR; confirme que el botón Sidetone está activo. En la v26.5.3, verifique que la salida de audio del tono lateral esté enrutada al dispositivo de audio correcto en la configuración de su sistema (#2899). En Windows, el flujo de tono lateral ahora se inicia inmediatamente al conectar (v0.9.3, #2105).
- **El tono lateral suena incorrecto** — El tono se deriva automáticamente de la configuración `cw_pitch` de la radio. Ajuste el tono usando el widget Pitch < / > en el panel CW.
- **El Level gauge no aparece al conectar** — Si la fuente de micrófono está configurada en PC, o si el modo RADE está activo, el Level gauge aparece inmediatamente al conectar y permanece visible durante RX. Para otras fuentes de micrófono sin RADE activo, el indicador se suprime hasta que `met_in_rx` esté habilitado o la radio comience a transmitir.
- **El deslizador Mic gain parece no tener efecto con RADE activo** — Cuando R
