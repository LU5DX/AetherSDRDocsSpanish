# Applet de Phone/CW

El applet de Phone/CW proporciona un panel de control de transmisión sensible al modo. Cuando el slice activo está en un modo de voz (LSB, USB, AM, FM, etc.), muestra controles de micrófono, procesador y monitor. Cuando el slice activo cambia al modo CW, el panel cambia automáticamente para mostrar controles de CW, incluyendo ajustes de retardo, velocidad, tono lateral, iámbico y tono.

En la v0.9.8, las cuatro etiquetas de valor de CW (Delay, Speed, Sidetone volume, Pitch) ahora son widgets `QLineEdit` editables con `QIntValidator`. Haga clic en cualquier campo de valor y escriba un número directamente. Cuando presione Enter o Tab, el valor se valida y se aplica tanto al deslizador como a la radio. Deslizar el control mientras el campo de texto no está enfocado aún actualiza el texto inmediatamente.

El único botón **Sidetone** y el deslizador de **Sidetone volume** controlan tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente (`CwSidetoneGenerator`, aproximadamente 10 ms de latencia) de forma sincronizada. El tono y la panorámica siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio.

En la v0.9.7, el indicador de **Compression** ahora está controlado por el estado de TRANSMITTING del interbloqueo de la radio (no por el flujo del medidor), por lo que marca 0 durante la recepción. **Breakin** ahora respeta completamente el ajuste `break_in` de la radio — ya no hay una envolvente de PTT automática que fuerce la transmisión. El bus de tono lateral se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).

En la v26.5.1, tanto el subpanel de Phone como el de CW ahora cuentan con un indicador de **ALC** impulsado por el medidor ALC de software (pico SSB post-ALC de software en dBFS), reemplazando la ruta anterior de HWALC (voltaje RCA) que producía lecturas sin sentido. Los dos indicadores son espejos idénticos el uno del otro, asegurando que los operadores de SSB que observan la ganancia del micrófono durante la recepción vean el mismo indicador que los operadores de CW usan para verificar la forma correcta de la envolvente de la manipulación (#2552).

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet de Phone/CW requiere una conexión activa a la radio.
- Configure el slice activo en un modo CW para ver los controles de CW, o en un modo de voz para ver los controles de Phone. El applet cambia automáticamente.
- Abra el applet de Phone/CW haciendo clic en el botón de la bandeja **P/CW** en la barra lateral derecha si no está visible.

## Pasos

### Cambiar el tono CW de la radio

1. Localice **Pitch < / >** en el subpanel de CW. Muestra el valor de tono actual con los botones **<** y **>** a cada lado.
2. Para escribir un valor directamente, haga clic en el campo numérico, introduzca un valor entre 100 y 6000, y presione Enter o Tab.
3. Para ajustar en pasos de 10 Hz, haga clic en **<** para disminuir el tono o **>** para aumentarlo.
4. El nuevo tono se envía a la radio inmediatamente. Valor predeterminado: 600 Hz.

El generador de tono lateral del lado del cliente siempre sigue automáticamente este valor de tono. No hay un control de tono local separado.

### Ajustar el retardo de CW

1. Localice **Delay** en el subpanel de CW. Tiene un deslizador y un campo de valor editable.
2. Para escribir un valor directamente, haga clic en el campo numérico, introduzca un valor entre 0 y 2000 (milisegundos), y presione Enter o Tab. El deslizador se mueve para coincidir.
3. Deslice el control para ajustar en pasos de 10 ms.
4. Valor predeterminado: 500 ms.

En la v0.9.8, se corrigió el método `setCwDelay` para almacenar en caché el valor inmediatamente, de modo que la emisión de la radio no devuelva el deslizador a su posición anterior (#2428).

### Ajustar la velocidad de CW

1. Localice **Speed** en el subpanel de CW. Tiene un deslizador y un campo de valor editable.
2. Para escribir un valor directamente, haga clic en el campo numérico, introduzca un valor entre 5 y 100 (PPM), y presione Enter o Tab. El deslizador se mueve para coincidir.
3. Deslice el control para ajustar en pasos.
4. Valor predeterminado: 20 PPM.

### Activar o desactivar el tono lateral

1. Haga clic en **Sidetone** en el subpanel de CW para activarlo o desactivarlo.
2. Tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente se activan o desactivan juntos mediante este único botón.

### Ajustar el volumen del tono lateral

1. Localice **Sidetone volume** en el subpanel de CW. Tiene un deslizador y un campo de valor editable.
2. Para escribir un valor directamente, haga clic en el campo numérico, introduzca un valor entre 0 y 100, y presione Enter o Tab. El deslizador se mueve para coincidir.
3. Deslice el control para ajustar el volumen.
4. Valor predeterminado: 50.
5. El deslizador establece tanto el volumen del monitor de la radio (`mon_gain_cw`) como el volumen del generador de tono lateral del lado del cliente simultáneamente.

### Ajustar la panorámica del monitor CW

1. Localice **L / R pan (CW)** en el subpanel de CW. Es un deslizador de 0 (todo izquierda) a 100 (todo derecha).
2. Deslícelo a la posición estéreo deseada.
3. Haga doble clic en el deslizador para volver a centrarlo en 50 (centro).
4. Valor predeterminado: 50.

### Alternar break-in (QSK)

1. Haga clic en **Breakin** en el subpanel de CW. Cuando está activado (break-in completo, QSK), los flancos de la manipulación activan la transmisión inmediatamente y el retardo de break-in mantiene el relé abierto entre elementos.
2. Cuando break-in está desactivado, las manipulaciones se ponen en cola y la radio no pasa a transmitir hasta que active PTT manualmente. La envolvente de PTT automática anterior que enmascaraba Breakin OFF se ha eliminado (v0.9.7).

### Alternar el manipulador iámbico

1. Haga clic en **Iambic** en el subpanel de CW para activar o desactivar el manipulador de paletas iámbico.

### Ajustar los controles del micrófono (panel Phone)

1. Seleccione un perfil de micrófono en el cuadro combinado **Mic profile** para cargar el perfil de procesamiento de micrófono nombrado.
2. Seleccione la fuente del micrófono en el cuadro combinado **Mic source** (MIC, BAL, LINE, ACC, PC, más cualquier otra de la lista de entradas de micrófono de la radio).
3. Ajuste el deslizador **Mic gain** (0–100, valor predeterminado 50) para establecer el nivel de entrada del micrófono. Cuando la fuente está configurada como **PC**, el valor se almacena en el lado del cliente en `PcMicGain` y la radio lo ignora.
4. Haga clic en **+ACC** para activar la mezcla de entrada del micrófono accesorio.
5. Haga clic en **PROC** para activar o desactivar el procesador de voz.
6. Use el deslizador **NOR/DX/DX+** para seleccionar el nivel del procesador (0 = NOR, 1 = DX, 2 = DX+).
7. Haga clic en **DAX** para activar DAX como fuente de audio de transmisión.
8. Haga clic en **MON** para activar el monitor de banda lateral.
9. Ajuste el deslizador **Monitor volume** (0–100) para establecer el volumen del monitor de banda lateral.

### Leer los medidores

- Indicador **Level**: Muestra el nivel pico de entrada del micrófono en dBFS (-40 a +10 dBFS, rojo por encima de 0 dBFS). Suprimido a -150 cuando `met_in_rx` está desactivado y no está transmitiendo.
- Indicador **Compression**: Muestra la cantidad de compresión de voz en dB (-25 a 0 dB, relleno invertido). Controlado por el estado TRANSMITTING del interbloqueo de la radio y la activación del procesador de voz. Marca 0 dB durante la recepción (v0.9.7).
- Indicador **ALC (panel Phone)**: Muestra la lectura del control automático de nivel desde el medidor ALC de software (pico SSB post-ALC de software en dBFS, rango -20 a 0 dBFS, rojo por encima de -3 dBFS). Se llena desde la derecha, con vacío en -20 dBFS y lleno en 0 dBFS (#2552, v26.5.1).
- Indicador **ALC (panel CW)**: Espejo idéntico del indicador ALC del panel Phone, ambos impulsados por la misma fuente (`MeterModel::swAlcChanged`). El rango, la escala y la dirección de llenado coinciden exactamente con la versión del panel Phone (#2552, v26.5.1).

## Qué hace cada control

### Controles de Phone

| Control             | Valor predeterminado | Rango válido        |
|---------------------|-----------------------|---------------------|
| **Mic profile**     | —                     | De la lista de la radio |
| **Mic source**      | —                     | MIC, BAL, LINE, ACC, PC |
| **Mic gain**        | 50                    | 0–100               |
| **+ACC**            | —                     | Activar / Desactivar |
| **PROC**            | —                     | Activar / Desactivar |
| **NOR/DX/DX+**      | 0                     | 0, 1, 2             |
| **DAX**             | —                     | Activar / Desactivar |
| **MON**             | —                     | Activar / Desactivar |
| **Monitor volume**  | —                     | 0–100               |

### Controles de CW

| Control             | Valor predeterminado | Rango válido            |
|---------------------|-----------------------|-------------------------|
| **Delay (CW)**      | 500 ms                | 0–2000 ms (paso 10)    |
| **Speed (CW)**      | 20 PPM                | 5–100 PPM              |
| **Sidetone**        | —                     | Activar / Desactivar    |
| **Sidetone volume** | 50                    | 0–100                  |
| **L / R pan (CW)**  | 50                    | 0–100                  |
| **Breakin**         | —                     | Activar / Desactivar    |
| **Iambic**          | —                     | Activar / Desactivar    |
| **Pitch < / >**     | 600 Hz                | 100–6000 Hz (paso 10)  |

## Modo RADE y el deslizador de nivel de micrófono

Cuando el modo RADE está activo, el deslizador **Mic gain** actúa como un control de ganancia RADE del lado del cliente en lugar de enviar un comando de nivel de micrófono a la radio. Esto refleja el comportamiento de la fuente de micrófono **PC**, donde la radio no utiliza el valor del nivel de micrófono. Ambos casos almacenan su ganancia en `PcMicGain`.

Mientras RADE está activo:

- El deslizador **Mic gain** lee y guarda en `PcMicGain` y no envía comandos `mic_level` a la radio.
- El indicador **Level** permanece activo durante la recepción. RADE proporciona medición del lado del cliente independientemente del ajuste `met_in_rx` de la radio, para que pueda monitorear su nivel de audio antes de transmitir.
- Cuando el modo RADE se desactiva, el deslizador vuelve a reflejar el nivel de micrófono de la radio, y el indicador **Level** regresa a su comportamiento de supresión normal cuando `met_in_rx` está desactivado y la radio no está transmitiendo.

## Consejos

- El control **Pitch < / >** afecta tanto al tono lateral audible en la radio como a la frecuencia utilizada por el decodificador CW. Ajústelo para que coincida con su preferencia de tono personal. El tono lateral del lado del cliente siempre lo sigue automáticamente.
- Debido a que el tono y la panorámica siguen automáticamente los ajustes de la radio, solo necesita ajustar **Pitch < / >** y **L / R pan (CW)** en un solo lugar — tanto el monitor de la radio como el generador local se actualizan juntos.
- El generador de tono lateral del lado del cliente opera con aproximadamente 10 ms de latencia y funciona con transmisiones generadas por paletas, manipulador vertical y CWX. Si no escucha ningún tono lateral, verifique que **Sidetone** esté activado.
- Cuando **Mic source** está configurado como **PC**, el indicador **Level** refleja la medición del lado del cliente y permanece activo independientemente del ajuste `met_in_rx` de la radio. Lo mismo aplica cuando el modo RADE está activo.
- El indicador **Compression** marca 0 dB durante la recepción. Solo muestra un valor mientras el interbloqueo de la radio informa TRANSMITTING y el procesador de voz está activado. Esto evita que aparezcan lecturas obsoletas entre transmisiones.
- Con **Breakin** desactivado, las manipulaciones se ponen en cola y la radio no pasa a transmitir hasta que active PTT manualmente. Con **Breakin** activado (QSK), los flancos de la manipulación activan la transmisión inmediatamente y el retardo de break-in mantiene el relé abierto entre elementos. Ya no hay una envolvente de PTT automática que anule este ajuste (v0.9.7).
- Para los campos de valor de CW (**Delay**, **Speed**, **Sidetone volume**, **Pitch**), haga clic en el campo numérico, escriba su valor y presione Enter o Tab. El valor se valida y se aplica tanto al deslizador como a la radio (v0.9.8).
- El indicador **ALC** tanto en el panel Phone como en el CW lee de la misma fuente del medidor ALC de software (`swAlcChanged`). Los operadores que usan modos Phone o CW ven lecturas ALC consistentes. El indicador se llena de derecha a izquierda: vacío en -20 dBFS, lleno en 0 dBFS, con un segmento rojo por encima de -3 dBFS (#2552, v26.5.1).

## Solución de problemas

- **No se escucha ningún tono lateral** — Confirme que **Sidetone** está activado y **Sidetone volume** está por encima de cero. Tanto el monitor de la radio como el generador del lado del cliente son controlados por estos dos controles.
- **El tono lateral no se inicia al conectar (Windows)** — Esto se resolvió en la v0.9.3 (#2105). Asegúrese de estar ejecutando la v0.9.3 o posterior.
- **El indicador Level no aparece al conectar** — Si **Mic source** está configurado como **PC** o el modo RADE está activo, el indicador debería aparecer inmediatamente al conectar. Para otras fuentes de micrófono sin RADE, el indicador se suprime cuando `met_in_rx` está desactivado y la radio no está transmitiendo.
- **El indicador Compression muestra 0 dB durante la recepción** — Este es el comportamiento esperado a partir de la v0.9.7. El indicador está controlado por el estado TRANSMITTING del interbloqueo de la radio y solo muestra un valor mientras transmite con el procesador de voz activado.
