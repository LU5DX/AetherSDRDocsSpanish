# Applet de Phone/CW

El applet de Phone/CW proporciona un panel de control de transmisión con detección de modo. Cuando el slice activo está en un modo de voz (LSB, USB, AM, FM, etc.), muestra los controles de micrófono, procesador y monitor. Cuando el slice activo cambia al modo CW, el panel cambia automáticamente para mostrar los controles de CW, incluyendo los ajustes de retardo, velocidad, tono lateral, iámbico y tono.

En la versión v0.9.8, las cuatro etiquetas de valor de CW (Retardo, Velocidad, Volumen de tono lateral, Tono) ahora son widgets `QLineEdit` editables con `QIntValidator`. Haga clic en cualquier campo de valor y escriba un número directamente. Cuando presione Enter o Tab, el valor se valida y se aplica tanto al deslizador como a la radio. Deslizar el control mientras el campo de texto no está enfocado aún actualiza el texto inmediatamente.

El único interruptor **Sidetone** y el deslizador de **Sidetone volume** controlan tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente (`CwSidetoneGenerator`, aproximadamente 10 ms de latencia) de forma sincronizada. El tono y la panoramización siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio.

En la versión v0.9.7, el indicador de **Compresión** ahora se activa únicamente con el estado de TRANSMISIÓN del interbloqueo de la radio (no con el flujo del medidor), por lo que muestra 0 durante la recepción. **Breakin** ahora respeta completamente el ajuste `break_in` de la radio; ya no existe una envolvente de PTT automática que fuerce la transmisión. El bus de tono lateral se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet de Phone/CW requiere una conexión activa con la radio.
- Configure el slice activo en un modo CW para ver los controles de CW, o en un modo de voz para ver los controles de Phone. El applet cambia automáticamente.
- Abra el applet de Phone/CW haciendo clic en el botón de la bandeja **P/CW** en la barra lateral derecha si aún no está visible.

## Pasos

### Cambiar el tono CW de la radio

1. Localice **Pitch < / >** en el subpanel de CW. Muestra el valor de tono actual con los botones **<** y **>** a cada lado.
2. Para escribir un valor directamente, haga clic en el campo numérico, ingrese un valor entre 100 y 6000, y presione Enter o Tab.
3. Para ajustar en pasos de 10 Hz, haga clic en **<** para disminuir el tono o en **>** para aumentarlo.
4. El nuevo tono se envía a la radio inmediatamente. Valor predeterminado: 600 Hz.

El generador de tono lateral del lado del cliente siempre sigue este valor de tono automáticamente. No hay un control de tono local separado.

### Ajustar el retardo CW

1. Localice **Delay** en el subpanel de CW. Tiene un deslizador y un campo de valor editable.
2. Para escribir un valor directamente, haga clic en el campo numérico, ingrese un valor entre 0 y 2000 (milisegundos), y presione Enter o Tab. El deslizador se mueve para coincidir.
3. Deslice el control para ajustar en pasos de 10 ms.
4. Valor predeterminado: 500 ms.

En la versión v0.9.8, el método `setCwDelay` se corrigió para almacenar en caché el valor inmediatamente, de modo que la emisión de la radio no devuelva el deslizador a su posición anterior (#2428).

### Ajustar la velocidad CW

1. Localice **Speed** en el subpanel de CW. Tiene un deslizador y un campo de valor editable.
2. Para escribir un valor directamente, haga clic en el campo numérico, ingrese un valor entre 5 y 100 (WPM), y presione Enter o Tab. El deslizador se mueve para coincidir.
3. Deslice el control para ajustar en pasos.
4. Valor predeterminado: 20 WPM.

### Activar o desactivar el tono lateral

1. Haga clic en **Sidetone** en el subpanel de CW para activarlo o desactivarlo.
2. Tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente se activan o desactivan juntos mediante este único botón.

### Ajustar el volumen del tono lateral

1. Localice **Sidetone volume** en el subpanel de CW. Tiene un deslizador y un campo de valor editable.
2. Para escribir un valor directamente, haga clic en el campo numérico, ingrese un valor entre 0 y 100, y presione Enter o Tab. El deslizador se mueve para coincidir.
3. Deslice el control para ajustar el volumen.
4. Valor predeterminado: 50.
5. El deslizador ajusta simultáneamente el volumen del monitor de la radio (`mon_gain_cw`) y el volumen del generador de tono lateral del lado del cliente.

### Ajustar la panoramización del monitor CW

1. Localice **L / R pan (CW)** en el subpanel de CW. Es un deslizador de 0 (totalmente a la izquierda) a 100 (totalmente a la derecha).
2. Deslice hasta la posición estéreo deseada.
3. Haga doble clic en el deslizador para volver a centrarlo en 50 (centro).
4. Valor predeterminado: 50.

### Activar o desactivar break-in (QSK)

1. Haga clic en **Breakin** en el subpanel de CW. Cuando está activado (break-in completo, QSK), los bordes de la tecla activan la transmisión inmediatamente y el retardo de break-in mantiene el relé abierto entre elementos.
2. Cuando break-in está desactivado, las teclas se ponen en cola y la radio no entra en TX hasta que active PTT manualmente. Se ha eliminado la envolvente de PTT automática anterior que enmascaraba Breakin OFF (v0.9.7).

### Activar o desactivar el manipulador iámbico

1. Haga clic en **Iambic** en el subpanel de CW para activar o desactivar el manipulador de paletas iámbico.

### Ajustar los controles del micrófono (panel Phone)

1. Seleccione un perfil de micrófono en el cuadro combinado **Mic profile** para cargar el perfil de procesamiento de micrófono nombrado.
2. Seleccione la fuente de micrófono en el cuadro combinado **Mic source** (MIC, BAL, LINE, ACC, PC, más cualquier otra de la lista de entradas de micrófono de la radio).
3. Ajuste el deslizador **Mic gain** (0–100, valor predeterminado 50) para configurar el nivel de entrada del micrófono. Cuando la fuente está configurada en **PC**, el valor se almacena del lado del cliente en `PcMicGain` y la radio lo ignora.
4. Haga clic en **+ACC** para activar la mezcla de entrada del micrófono auxiliar.
5. Haga clic en **PROC** para activar o desactivar el procesador de voz.
6. Use el deslizador **NOR/DX/DX+** para seleccionar el nivel del procesador (0 = NOR, 1 = DX, 2 = DX+).
7. Haga clic en **DAX** para habilitar DAX como fuente de audio de TX.
8. Haga clic en **MON** para activar el monitor de la banda lateral.
9. Ajuste el deslizador **Monitor volume** (0–100) para configurar el volumen del monitor de la banda lateral.

### Leer los medidores

- **Level** (Nivel): Muestra el nivel pico de entrada del micrófono en dBFS (-40 a +10 dBFS, rojo por encima de 0 dBFS). Suprimido a -150 cuando `met_in_rx` está desactivado y no está transmitiendo.
- **Compression** (Compresión): Muestra la cantidad de compresión de voz en dB (-25 a 0 dB, relleno invertido). Activado únicamente por el estado de TRANSMISIÓN del interbloqueo de la radio y la activación del procesador de voz. Muestra 0 dB durante la recepción (v0.9.7).
- **ALC** (subpanel CW): Muestra la lectura del control automático de nivel (0–100, rojo por encima de 80).

## Qué hace cada control

### Controles Phone

| Control             | Valor predeterminado | Rango válido       |
|---------------------|----------------------|--------------------|
| **Mic profile**     | —                    | Desde la lista de la radio |
| **Mic source**      | —                    | MIC, BAL, LINE, ACC, PC |
| **Mic gain**        | 50                   | 0–100              |
| **+ACC**            | —                    | On / Off           |
| **PROC**            | —                    | On / Off           |
| **NOR/DX/DX+**      | 0                    | 0, 1, 2            |
| **DAX**             | —                    | On / Off           |
| **MON**             | —                    | On / Off           |
| **Monitor volume**  | —                    | 0–100              |

### Controles CW

| Control             | Valor predeterminado | Rango válido            |
|---------------------|----------------------|-------------------------|
| **Delay (CW)**      | 500 ms               | 0–2000 ms (paso 10)     |
| **Speed (CW)**      | 20 WPM               | 5–100 WPM               |
| **Sidetone**        | —                    | On / Off                |
| **Sidetone volume** | 50                   | 0–100                   |
| **L / R pan (CW)**  | 50                   | 0–100                   |
| **Breakin**         | —                    | On / Off                |
| **Iambic**          | —                    | On / Off                |
| **Pitch < / >**     | 600 Hz               | 100–6000 Hz (paso 10)   |

## Modo RADE y el deslizador de nivel de micrófono

Cuando el modo RADE está activo, el deslizador **Mic gain** actúa como un control de ganancia RADE del lado del cliente en lugar de enviar un comando de nivel de micrófono a la radio. Esto refleja el comportamiento de la fuente de micrófono **PC**, donde la radio no utiliza el valor del nivel de micrófono. Ambos casos almacenan su ganancia en `PcMicGain`.

Mientras RADE está activo:

- El deslizador **Mic gain** lee y guarda en `PcMicGain` y no envía comandos `mic_level` a la radio.
- El indicador **Level** permanece activo durante la recepción. RADE proporciona medición del lado del cliente independientemente del ajuste `met_in_rx` de la radio, por lo que puede monitorear su nivel de audio antes de transmitir.
- Cuando el modo RADE está desactivado, el deslizador vuelve a reflejar el nivel de micrófono de la radio, y el indicador **Level** vuelve a su comportamiento de supresión normal cuando `met_in_rx` está desactivado y la radio no está transmitiendo.

## Consejos

- El control **Pitch < / >** afecta tanto al tono lateral audible en la radio como a la frecuencia utilizada por el decodificador CW. Ajústelo para que coincida con su preferencia de tono personal. El tono lateral del lado del cliente siempre lo sigue automáticamente.
- Dado que el tono y la panoramización siguen los ajustes de la radio automáticamente, solo necesita ajustar **Pitch < / >** y **L / R pan (CW)** en un solo lugar; tanto el monitor de la radio como el generador local se actualizan juntos.
- El generador de tono lateral del lado del cliente opera con una latencia de aproximadamente 10 ms y funciona con transmisiones generadas con paletas, llave recta y CWX. Si no escucha ningún tono lateral, verifique que **Sidetone** esté activado.
- Cuando **Mic source** está configurado en **PC**, el indicador **Level** refleja la medición del lado del cliente y permanece activo independientemente del ajuste `met_in_rx` de la radio. Lo mismo se aplica cuando el modo RADE está activo.
- El indicador **Compression** muestra 0 dB durante la recepción. Solo muestra un valor mientras el interbloqueo de la radio informa TRANSMISIÓN y el procesador de voz está activado. Esto evita que aparezcan lecturas obsoletas entre transmisiones.
- Con **Breakin** desactivado, las teclas se ponen en cola y la radio no entra en TX hasta que active PTT manualmente. Con **Breakin** activado (QSK), los bordes de la tecla activan la transmisión inmediatamente y el retardo de break-in mantiene el relé abierto entre elementos. Ya no existe una envolvente de PTT automática que anule esta configuración (v0.9.7).
- Para los campos de valor CW (**Delay**, **Speed**, **Sidetone volume**, **Pitch**), haga clic en el campo numérico, escriba su valor y presione Enter o Tab. El valor se valida y se aplica tanto al deslizador como a la radio (v0.9.8).

## Solución de problemas

- **No se escucha el tono lateral** — Confirme que **Sidetone** está activado y que **Sidetone volume** está por encima de cero. Tanto el monitor de la radio como el generador del lado del cliente son controlados por estos dos controles.
- **El tono lateral no comienza al conectar (Windows)** — Esto se resolvió en la versión v0.9.3 (#2105). Asegúrese de estar ejecutando la versión v0.9.3 o posterior.
- **El indicador Level no aparece al conectar** — Si **Mic source** está configurado en **PC** o el modo RADE está activo, el indicador debería aparecer inmediatamente al conectar. Para otras fuentes de micrófono sin RADE, el indicador se suprime cuando `met_in_rx` está desactivado y la radio no está transmitiendo.
- **El indicador Compression muestra 0 dB durante la recepción** — Este es el comportamiento esperado a partir de la versión v0.9.7. El indicador se activa únicamente con el estado de TRANSMISIÓN del interbloqueo de la radio y solo muestra un valor mientras transmite con el procesador de voz activado.
- **Breakin no activa QSK** — Confirme que **Breakin** está activado en el subpanel de CW. A partir de la versión v0.9.7, las rutas de tecleo por teclado y MIDI respetan completamente esta configuración; ninguna envolvente de PTT automática la anula.
- **El cambio de tono no tiene efecto** — Confirme que el slice activo está en un modo CW. El subpanel de CW y su control de tono solo están activos en modos CW.
- **El subpanel CW no está visible** — El slice activo no está en un modo CW. Cambie el slice a CW; el applet cambia automáticamente.
- **El deslizador de retardo CW vuelve a su posición al ajustarlo** — Esto se resolvió en la versión v0.9.8 (#2428). Asegúrese de estar ejecutando la versión v0.9.8 o posterior.
- **El valor CW escrito no se aplica** — Presione Enter o Tab después de escribir el valor en el campo editable. El valor se valida y se aplica cuando se activa `editingFinished`.
- **El deslizador Mic gain no actualiza la radio en modo RADE** — Esto es correcto. En modo RADE, el deslizador controla solo la ganancia RADE del lado del cliente y almacena el valor en `PcMicGain`. El ajuste del nivel de micrófono de la radio no se ve afectado.

## Relacionado

- [Escuchar un monitor de tono lateral de TX](listen-to-a-tx-sidetone-monitor.md)
