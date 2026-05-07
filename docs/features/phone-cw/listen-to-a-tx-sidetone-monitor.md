# Applet de Phone/CW

El applet de Phone/CW es un panel de transmisión sensible al modo que muestra controles de Phone (micrófono, procesador, monitor) en modos de voz y cambia automáticamente a controles de CW (retardo, velocidad, tono local, iámbico, tono) cuando la franja activa está en modo CW.

En la versión v0.9.8, las cuatro etiquetas de valor CW (Retardo, Velocidad, Volumen de tono local, Tono) ahora son widgets QLineEdit con QIntValidator — haga clic en cualquier valor y escriba un número directamente (paridad con SmartSDR).

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet de Phone/CW requiere una conexión activa a la radio.
- Abra el Panel de applets. Si no está visible, haga clic en View > Applet Panel.

## Pasos

### Modo Phone: activar el monitor de banda lateral

1. Haga clic en el botón de la bandeja P/CW en la barra lateral derecha para abrir el applet de Phone/CW.
2. Confirme que el applet muestra el panel de Phone (la franja activa debe estar en un modo de voz como SSB o AM).
3. Haga clic en MON para activar el monitor de banda lateral de TX. El botón se resalta cuando está activo.
4. Ajuste el deslizador de volumen de Monitor para establecer el nivel de reproducción (0–100).

### Modo Phone: ajustar la configuración del micrófono

1. Seleccione un perfil de Mic del menú desplegable para cargar un perfil de procesamiento de micrófono con nombre.
2. Seleccione la fuente de Mic del menú desplegable (las opciones incluyen MIC, BAL, LINE, ACC, PC, además de las entradas de micrófono disponibles de la radio).
3. Ajuste el deslizador de ganancia de Mic para establecer el nivel de entrada del micrófono (0–100). Cuando la fuente es PC, el valor se almacena localmente en `PcMicGain`.
4. Haga clic en +ACC para activar la mezcla de entrada del micrófono auxiliar.
5. Haga clic en PROC para activar o desactivar el procesador de voz.
6. Use el deslizador NOR/DX/DX+ para seleccionar el nivel del procesador: 0 (NOR), 1 (DX) o 2 (DX+).
7. Haga clic en DAX para activar DAX como fuente de audio de TX.

### Modo CW: ajustar la configuración de CW

1. Cambie la franja activa a un modo CW. El applet muestra automáticamente el panel de CW.
2. Ajuste el deslizador de Delay para establecer el retardo de inserción de CW (0–2000 ms, paso 10). También puede escribir un valor directamente en el QLineEdit (0–2000).
3. Ajuste el deslizador de Speed para establecer la velocidad de tecleo CW (5–100 WPM). También puede escribir un valor directamente en el QLineEdit (5–100).
4. Haga clic en Sidetone para activar el monitor de CW. El botón se resalta cuando está activo.
5. Ajuste el deslizador de volumen de Sidetone para establecer el nivel (0–100). También puede escribir un valor directamente en el QLineEdit (0–100).
6. Use el deslizador de paneo L / R (CW) para establecer el paneo estéreo (doble clic para centrar en 50).
7. Haga clic en Breakin para activar o desactivar la inserción completa (QSK).
8. Haga clic en Iambic para activar o desactivar el manipulador de paletas iámbico.
9. Use los botones de Pitch < / > para avanzar en pasos de 10 Hz, o escriba un valor directamente en el QLineEdit (100–6000 Hz).

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Rango válido |
|---------|----------|----------------------|--------------|
| MON | Activa el monitor de banda lateral de TX (panel de Phone). | — | — |
| Monitor volume | Establece el nivel de reproducción del monitor de banda lateral. | — | 0–100 |
| DAX | Activa DAX como fuente de audio de TX. | — | — |
| Mic profile | Carga un perfil de procesamiento de micrófono con nombre. | — | Se completa desde la radio |
| Mic source | Selecciona la fuente de entrada del micrófono. | — | MIC, BAL, LINE, ACC, PC, más entradas de la radio |
| Mic gain | Ajusta el nivel de entrada del micrófono. Para fuente PC usa la persistencia local PcMicGain. | 50 | 0–100 |
| +ACC | Activa la mezcla de entrada del micrófono auxiliar. | — | — |
| PROC | Activa o desactiva el procesador de voz. | — | — |
| NOR/DX/DX+ | Deslizador de nivel del procesador de tres posiciones. | 0 | 0 (NOR), 1 (DX), 2 (DX+) |
| Delay (CW) | Establece el retardo de inserción de CW. El QLineEdit adyacente acepta valores escritos (0–2000) (v0.9.8, #2429). En v0.9.8, se corrigió setCwDelay para almacenar en caché el valor inmediatamente, de modo que la emisión de la radio no devuelva el deslizador a su posición anterior (#2428). | 500 ms | 0–2000 ms (paso 10) |
| Speed (CW) | Establece la velocidad de tecleo CW. El QLineEdit adyacente acepta valores escritos (5–100) (v0.9.8, #2429). | 20 WPM | 5–100 WPM |
| Sidetone | Activa o desactiva el monitor de tono local CW. También activa/desactiva el CwSidetoneGenerator local de baja latencia del lado del cliente de forma sincronizada (v0.9.1+). Tanto el monitor alimentado por DAX de la radio como el tono local de PortAudio se controlan mediante este único botón. El tono y el paneo siempre siguen automáticamente cw_pitch y mon_pan_cw de la radio. | — | — |
| Sidetone volume | Establece el volumen del monitor de CW. También establece el volumen del generador de tono local de forma sincronizada. El QLineEdit adyacente acepta valores escritos (0–100) (v0.9.8, #2429). | 50 | 0–100 |
| L / R pan (CW) | Establece el paneo estéreo del monitor de CW. Aplica paneo de potencia constante al generador de tono local (v0.9.1+). Doble clic para centrar en 50. | 50 | 0–100 |
| Breakin | Activa o desactiva la inserción completa (QSK). En v0.9.7, las rutas de teclado/MIDI CW ahora respetan completamente esta configuración: con Breakin activado (QSK), los flancos de tecla activan TX y break_in_delay mantiene el relé; con Breakin desactivado, las teclas se ponen en cola y el operador activa PTT manualmente. | — | — |
| Iambic | Activa o desactiva el manipulador de paletas iámbico. | — | — |
| Pitch < / > | QLineEdit con botones < / > (CwTriBtn). Escriba un valor (100–6000) o haga clic en los botones para avanzar en pasos de 10 Hz (v0.9.8, #2429). | 600 Hz | 100–6000 Hz (paso 10) |

## Información de los medidores

| Medidor | Qué muestra | Rango válido | Notas |
|---------|-------------|--------------|-------|
| Level gauge | Nivel máximo de entrada del micrófono en dBFS. | -40 a +10 dBFS (rojo > 0) | Se suprime a -150 cuando met_in_rx está desactivado y no se está transmitiendo. |
| Compression gauge | Cantidad de compresión de voz en dB (relleno invertido). | -25 a 0 dB | En v0.9.7, controlado por el estado TRANSMITTING del interbloqueo de la radio y la activación del procesador de voz: muestra 0 dB durante RX. Se actualiza mediante el slot updateCompression(), independiente de la ruta del nivel de micrófono. |
| ALC gauge | Control automático de nivel (subpanel de CW). | 0–100 (rojo > 80) | — |

## Consejos

- El botón Sidetone y el deslizador de volumen de Sidetone controlan ambas rutas de audio (monitor DAX de la radio y generador del lado del cliente) juntas. No existe un control separado para activar o ajustar el tono local de forma independiente.
- El tono siempre sigue automáticamente la configuración de tono CW de la radio. Use el widget de Pitch < / > para cambiar el tono CW de la radio, y tanto el tono de decodificación como el tono local se actualizarán en consecuencia.
- El botón MON y el botón Sidetone son controles separados en paneles separados. MON se aplica a los modos de voz; Sidetone se aplica al modo CW.
- Cuando la fuente del micrófono está configurada en PC, el Level gauge aparece inmediatamente al conectar. En v0.9.7, lo mismo se aplica cuando el modo RADE está activo: el Level gauge se muestra durante RX independientemente de la configuración `met_in_rx`. En otros modos de fuente de micrófono (sin RADE activo), el medidor se suprime cuando `met_in_rx` está desactivado y la radio no está transmitiendo.
- Cuando el modo RADE está activo, el deslizador de ganancia de Mic actúa como un control de ganancia RADE del lado del cliente y su valor se almacena en `PcMicGain`. El deslizador no envía un comando de nivel de micrófono a la radio en este estado, lo que evita sobrescribir la configuración de su micrófono físico.
- En v0.9.8, los cuatro campos QLineEdit de CW (Delay, Speed, Sidetone Volume, Pitch) aceptan entrada numérica directa. Escriba un valor y presione Enter para aplicarlo. Los valores se limitan automáticamente al rango válido.
- El bus de tono local se comparte con los tonos de Quindar (mutuamente excluyentes a nivel de modo).

## Solución de problemas

- **El botón MON o Sidetone no tiene efecto** — Confirme que la radio está conectada y que el modo de la franja activa coincide con el panel que se muestra (Phone vs. CW). El applet cambia de panel automáticamente según el modo de la franja activa.
- **El tono local no produce audio** — Verifique que la salida de audio de su sistema esté configurada correctamente. El tono local del lado del cliente lo genera AetherSDR localmente; confirme que el botón Sidetone está activo. En Windows, la transmisión de tono local ahora se inicia inmediatamente al conectar (v0.9.3, #2105).
- **El tono local tiene el tono incorrecto** — El tono se deriva automáticamente de la configuración `cw_pitch` de la radio. Ajuste el tono usando el widget de Pitch < / > en el panel de CW.
- **El Level gauge no aparece al conectar** — Si la fuente del micrófono está configurada en PC, o si el modo RADE está activo, el Level gauge aparece inmediatamente al conectar y permanece visible durante RX. Para otras fuentes de micrófono sin RADE activo, el medidor se suprime hasta que `met_in_rx` esté habilitado o la radio comience a transmitir.
- **El deslizador de ganancia de Mic parece no tener efecto con RADE activo** — Cuando el modo RADE está activo, el deslizador de ganancia de Mic controla solo la ganancia RADE del lado del cliente y no envía comandos a la radio. Este es el comportamiento esperado. El valor se guarda como `PcMicGain`.
- **El deslizador vuelve a su posición anterior al ajustar el retardo de CW** — Este problema se solucionó en v0.9.8 (#2428). El valor de retardo ahora se almacena en caché inmediatamente cuando se establece, lo que evita que la emisión de la radio devuelva el deslizador a su posición anterior.

## Relacionado

- [Escuchar un monitor de tono local de TX](listen-to-a-tx-sidetone-monitor.md)
- [Cambiar el tono CW / frecuencia del tono local](change-cw-pitch-sidetone-frequency.md)
