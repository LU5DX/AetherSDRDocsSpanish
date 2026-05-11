# Applet de Voz/CW

El applet de Voz/CW es un panel de transmisión sensible al modo que muestra controles de Voz (micrófono, procesador, monitor) en modos de voz y cambia automáticamente a controles de CW (retardo, velocidad, tono local, iámbico, tono) cuando el segmento activo está en modo CW.

En v0.9.8, las cuatro etiquetas de valor de CW (Retardo, Velocidad, Volumen de tono local, Tono) ahora son widgets QLineEdit con QIntValidator — haga clic en cualquier valor y escriba un número directamente (paridad con SmartSDR).

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet de Voz/CW requiere una conexión activa a la radio.
- Abra el Panel de Applets. Si no está visible, haga clic en View > Applet Panel.

## Pasos

### Modo Voz: activar el monitor de banda lateral

1. Haga clic en el botón P/CW de la barra lateral derecha para abrir el applet de Voz/CW.
2. Confirme que el applet muestra el panel de Voz (el segmento activo debe estar en un modo de voz como SSB o AM).
3. Haga clic en MON para activar el monitor de banda lateral de TX. El botón se ilumina cuando está activo.
4. Ajuste el control deslizante de volumen del Monitor para establecer el nivel de reproducción (0–100).

### Modo Voz: ajustar la configuración del micrófono

1. Seleccione un perfil de Mic del menú desplegable para cargar un perfil de procesamiento de micrófono con nombre.
2. Seleccione la fuente de Mic del menú desplegable (las opciones incluyen MIC, BAL, LINE, ACC, PC, además de cualquier otra entrada de micrófono disponible en la radio).
3. Ajuste el control deslizante de ganancia de Mic para establecer el nivel de entrada del micrófono (0–100). Cuando la fuente es PC, el valor se almacena localmente en `PcMicGain`.
4. Haga clic en +ACC para activar la mezcla de entrada del micrófono auxiliar.
5. Haga clic en PROC para activar o desactivar el procesador de voz.
6. Use el control deslizante NOR/DX/DX+ para seleccionar el nivel del procesador: 0 (NOR), 1 (DX) o 2 (DX+).
7. Haga clic en DAX para activar DAX como fuente de audio de TX.

### Modo CW: ajustar la configuración de CW

1. Cambie el segmento activo a un modo CW. El applet muestra automáticamente el panel de CW.
2. Ajuste el control deslizante de Retardo para establecer el retardo de inserción de CW (0–2000 ms, paso 10). También puede escribir un valor directamente en el QLineEdit (0–2000).
3. Ajuste el control deslizante de Velocidad para establecer la velocidad de manipulación de CW (5–100 WPM). También puede escribir un valor directamente en el QLineEdit (5–100).
4. Haga clic en Tono local para activar el monitor de CW. El botón se ilumina cuando está activo.
5. Ajuste el control deslizante de volumen del Tono local para establecer el nivel (0–100). También puede escribir un valor directamente en el QLineEdit (0–100).
6. Use el control deslizante de paneo L / R (CW) para establecer el paneo estéreo (doble clic para volver a centrar en 50).
7. Haga clic en Breakin para activar o desactivar la inserción completa (QSK).
8. Haga clic en Iambic para activar o desactivar el manipulador de paletas iámbico.
9. Use los botones Tono < / > para cambiar en pasos de 10 Hz, o escriba un valor directamente en el QLineEdit (100–6000 Hz).

## Qué hace cada control

| Control             | Qué hace                                                                                                                                                                                                                                                                                                     | Valor predeterminado                                  |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------|
| MON                 | Activa el monitor de banda lateral de TX (panel de Voz).                                                                                                                                                                                                                                                     | —                                                     |
| Volumen del monitor | Establece el nivel de reproducción del monitor de banda lateral.                                                                                                                                                                                                                                             | —                                                     |
| DAX                 | Activa DAX como fuente de audio de TX.                                                                                                                                                                                                                                                                       | —                                                     |
| Perfil de Mic       | Carga un perfil de procesamiento de micrófono con nombre.                                                                                                                                                                                                                                                    | —                                                     |
| Fuente de Mic       | Selecciona la fuente de entrada del micrófono.                                                                                                                                                                                                                                                               | —                                                     |
| Ganancia de Mic     | Ajusta el nivel de entrada del micrófono. Para fuente PC usa persistencia local de PcMicGain.                                                                                                                                                                                                               | 50                                                    |
| +ACC                | Activa la mezcla de entrada del micrófono auxiliar.                                                                                                                                                                                                                                                          | —                                                     |
| PROC                | Activa o desactiva el procesador de voz.                                                                                                                                                                                                                                                                     | —                                                     |
| NOR/DX/DX+          | Control deslizante de nivel del procesador de tres posiciones.                                                                                                                                                                                                                                              | 0                                                     |
| Retardo (CW)        | Establece el retardo de inserción de CW. El QLineEdit adyacente acepta valores escritos (0–2000) (v0.9.8, #2429). En v0.9.8, se corrigió setCwDelay para almacenar en caché el valor inmediatamente para que la emisión de la radio no devuelva el control deslizante a su posición anterior (#2428).          | 500 ms                                                |
| Velocidad (CW)      | Establece la velocidad de manipulación de CW. El QLineEdit adyacente acepta valores escritos (5–100) (v0.9.8, #2429).                                                                                                                                                                                       | 20 WPM                                                |
| Tono local          | Activa o desactiva el monitor de tono local de CW. También activa/desactiva el CwSidetoneGenerator local de baja latencia del lado del cliente de forma sincronizada (v0.9.1+). Tanto el monitor alimentado por DAX de la radio como el tono local de PortAudio son controlados por este único botón. El tono y el paneo siguen automáticamente a cw_pitch y mon_pan_cw de la radio. | —                                                     |
| Volumen de tono local | Establece el volumen del monitor de CW. También establece el volumen del generador de tono local de forma sincronizada. El QLineEdit adyacente acepta valores escritos (0–100) (v0.9.8, #2429).                                                                                                        | 50                                                    |
| Paneo L / R (CW)    | Establece el paneo estéreo del monitor de CW. Aplica paneo de potencia constante al generador de tono local (v0.9.1+). Doble clic para volver a centrar en 50.                                                                                                                                              | 50                                                    |
| Breakin             | Activa o desactiva la inserción completa (QSK). En v0.9.7, las rutas de teclado/MIDI de CW ahora respetan completamente esta configuración: con Breakin activado (QSK), los flancos de la tecla activan TX y break_in_delay mantiene el relé; con Breakin desactivado, las teclas se ponen en cola y el operador activa PTT manualmente. | —                                                     |
| Iambic              | Activa o desactiva el manipulador de paletas iámbico.                                                                                                                                                                                                                                                        | —                                                     |
| Tono < / >          | QLineEdit con botones < / > (CwTriBtn). Escriba un valor (100–6000) o haga clic en los botones para cambiar en pasos de 10 Hz (v0.9.8, #2429).                                                                                                                                                               | 600 Hz                                                |
| Nivel               | Nivel pico de entrada del micrófono en dBFS (panel de Voz). Suprimido a -150 cuando met_in_rx está desactivado y no se está transmitiendo.                                                                                                                                                                   | —                                                     |
| Compresión          | Cantidad de compresión de voz en dB (panel de Voz). Bloqueado por el estado de INTERLOCK TRANSMITTING de la radio y la activación del procesador de voz: lee 0 dB durante RX (v0.9.7).                                                                                                                       | —                                                     |
| ALC (panel de Voz)  | Muestra la lectura del control automático de nivel desde MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Reconectado de HWALC (tensión RCA) al medidor de ALC de software en v26.5.1 (#2552). Reflejado por un indicador idéntico en el subpanel de CW. | —                                                     |
| ALC (panel de CW)   | Refleja el indicador de ALC del panel de Voz; ambos leen de MeterModel::swAlcChanged para lecturas consistentes en voz y CW. Añadido en v26.5.1 (#2552) como parte de la división del medidor de ALC de software. Usa el modo HGauge::setFillFromRight.                                                       | —                                                     |

## Información de los medidores

| Medidor              | Qué muestra                                                                                                                                | Rango válido             | Notas                                                                                                                           |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Indicador de nivel   | Nivel pico de entrada del micrófono en dBFS.                                                                                               | -40 a +10 dBFS (rojo > 0) | Suprimido a -150 cuando met_in_rx está desactivado y no se está transmitiendo.                                                  |
| Indicador de compresión | Cantidad de compresión de voz en dB (relleno invertido).                                                                                  | -25 a 0 dB               | Bloqueado por el estado de INTERLOCK TRANSMITTING de la radio y la activación del procesador de voz: lee 0 dB durante RX (v0.9.7). |
| Indicador de ALC (Voz) | Control automático de nivel — pico SSB posterior al ALC de software, leído de MeterModel::swAlcChanged. Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. | -20 a 0 dBFS (rojo > -3) | Reconectado de HWALC (tensión RCA) al medidor de ALC de software en v26.5.1 (#2552). Reflejado por indicador idéntico en panel de CW. |
| Indicador de ALC (CW) | Reflejo del indicador de ALC del panel de Voz, escalado idénticamente. Ambos leen de MeterModel::swAlcChanged.                              | -20 a 0 dBFS (rojo > -3) | Añadido en v26.5.1 (#2552) como parte de la división del medidor de ALC de software. Usa el modo HGauge::setFillFromRight.      |

## Consejos

- El botón de Tono local y el control deslizante de Volumen de tono local controlan ambas rutas de audio (monitor DAX de la radio y generador del lado del cliente) juntas. No hay un control separado para activar o ajustar el tono local de forma independiente.
- El tono sigue automáticamente la configuración de tono CW de la radio. Use el widget Tono < / > para cambiar el tono CW de la radio, y tanto el tono de decodificación como el tono local se actualizarán en consecuencia.
- El botón MON y el botón Tono local son controles separados en paneles separados. MON se aplica a modos de voz; Tono local se aplica al modo CW.
- Cuando la fuente de micrófono está configurada en PC, el indicador de Nivel aparece inmediatamente al conectar. En v0.9.7, lo mismo se aplica cuando el modo RADE está activo: el indicador de Nivel se muestra durante RX independientemente de la configuración de `met_in_rx`. En otros modos de fuente de micrófono (sin RADE activo), el indicador se suprime cuando `met_in_rx` está desactivado y la radio no está transmitiendo.
- Cuando el modo RADE está activo, el control deslizante de Ganancia de Mic actúa como un control de ganancia RADE del lado del cliente y su valor se almacena en `PcMicGain`. El control deslizante no envía un comando de nivel de micrófono a la radio en este estado, lo que evita sobrescribir la configuración de su micrófono físico.
- En v0.9.8, los cuatro campos QLineEdit de CW (Retardo, Velocidad, Volumen de tono local, Tono) aceptan entrada numérica directa. Escriba un valor y presione Enter para aplicarlo. Los valores se limitan automáticamente al rango válido.
- El bus de tono local se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).
- El indicador de ALC en los paneles de Voz y CW ahora lee del medidor de ALC de software (MeterModel::swAlcChanged), proporcionando lecturas significativas en dBFS en lugar de los datos sin sentido de HWALC (tensión RCA) anteriores. Ambos indicadores son idénticos y se actualizan sincronizados.

## Solución de problemas

- **El botón MON o Tono local no tiene efecto** — Confirme que la radio está conectada y que el modo del segmento activo coincide con el panel que se muestra (Voz vs. CW). El applet cambia de panel automáticamente según el modo del segmento activo.
- **El tono local no produce audio** — Verifique que la salida de audio de su sistema esté configurada correctamente. El tono local del lado del cliente es generado localmente por AetherSDR; confirme que el botón Tono local esté activo. En Windows, el flujo de tono local ahora se inicia inmediatamente al conectar (v0.9.3, #2105).
- **El tono local es incorrecto** — El tono se deriva automáticamente de la configuración `cw_pitch` de la radio. Ajuste el tono usando el widget Tono < / > en el panel de CW.
- **El indicador de Nivel no aparece al conectar** — Si la fuente de micrófono está configurada en PC, o si el modo RADE está activo, el indicador de Nivel aparece inmediatamente al conectar y permanece visible durante RX. Para otras fuentes de micrófono sin RADE activo, el indicador se suprime hasta que `met_in_rx` esté activado o la radio comience a transmitir.
- **El control deslizante de Ganancia de Mic parece no tener efecto con RADE activo** — Cuando el modo RADE está activo, el control deslizante de Ganancia de Mic controla solo la ganancia RADE del lado del cliente y no envía comandos a la radio. Este es el comportamiento esperado. El valor se guarda como `PcMicGain`.
- **El control deslizante vuelve a su posición anterior al ajustar el retardo de CW** — Este problema se corrigió en v0.9.8 (#2428). El valor de retardo ahora se almacena en caché inmediatamente cuando se configura, evitando que la emisión de la radio devuelva el control deslizante a su posición anterior.
- **El indicador de ALC lee 0 o valores sin sentido** — Este problema se resolvió en v26.5.1 (#2552). Los indicadores de ALC ahora leen de la fuente correcta del medidor de ALC de software. Si aún ve 0 durante la transmisión, asegúrese de que la radio esté en un modo que produzca ALC (SSB o CW).

## Relacionado

- [Escuchar un monitor de tono local de TX](listen-to-a-tx-sidetone-monitor.md)
- [Cambiar el tono CW / la frecuencia del tono local](change-cw-pitch-sidetone-frequency.md)
