# Applet de Teléfono/CW

El applet de Teléfono/CW proporciona un panel de control de transmisión sensible al modo. Cuando el slice activo está en un modo de voz (LSB, USB, AM, FM, etc.), muestra controles de micrófono, procesador y monitor. Cuando el slice activo cambia a modo CW, el panel cambia automáticamente para mostrar controles CW que incluyen ajustes de retardo, velocidad, tono lateral, iámbico y tono.

En la v0.9.8, las cuatro etiquetas de valor CW (Retardo, Velocidad, Volumen de tono lateral, Tono) ahora son widgets `QLineEdit` editables con `QIntValidator`. Haga clic en cualquier campo de valor y escriba un número directamente. Cuando presiona Enter o Tab, el valor se valida y se aplica tanto al deslizador como a la radio. Deslizar el control mientras el campo de texto no está enfocado aún actualiza el texto inmediatamente.

El único interruptor **Sidetone** (Tono lateral) y el deslizador de **Sidetone volume** (Volumen de tono lateral) controlan tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente (`CwSidetoneGenerator`, aproximadamente 10 ms de latencia) de forma sincronizada. El tono y la panoramización siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio.

En la v0.9.7, el indicador de **Compression** (Compresión) ahora está controlado por el estado TRANSMITTING del interbloqueo de la radio (no por el flujo del medidor), por lo que marca 0 durante la recepción. **Breakin** (Inserción) ahora respeta completamente el ajuste `break_in` de la radio — ya no hay una envolvente de PTT automática que fuerce la transmisión. El bus de tono lateral se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).

En la v26.5.1, tanto los subpaneles de Teléfono como de CW ahora cuentan con un indicador **ALC** (Control Automático de Nivel) impulsado por el medidor de ALC por software (pico SSB post-ALC por software en dBFS), reemplazando la ruta HWALC anterior (voltaje RCA) que producía lecturas sin sentido. Los dos indicadores son espejos idénticos entre sí, lo que garantiza que los operadores de SSB que observan la ganancia del micrófono durante la recepción vean el mismo indicador que los operadores de CW usan para verificar la forma correcta de la envolvente de llaveo (#2552).

En la v26.5.3, el tono lateral de CW ahora se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). El indicador de **Compression** (Compresión) ahora interpreta correctamente los valores positivos de dB de `MeterModel::COMPPEAK` y los niega para la visualización invertida del indicador. El indicador **Level** (Nivel) ahora utiliza un método dedicado de compuerta de recepción (`applyLevelMeterReceiveGate()`) que se aplica por igual a todas las fuentes de micrófono, incluyendo PC y RADE, suprimiendo el medidor a -150 cuando `met_in_rx` está desactivado y la radio no está transmitiendo.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet de Teléfono/CW requiere una conexión de radio activa.
- Configure el slice activo en un modo CW para ver los controles CW, o en un modo de voz para ver los controles de Teléfono. El applet cambia automáticamente.
- Abra el applet de Teléfono/CW haciendo clic en el botón de la bandeja **P/CW** en la barra lateral derecha si aún no está visible.

## Pasos

### Cambiar el tono CW de la radio

1. Localice **Pitch < / >** (Tono) en el subpanel CW. Muestra el valor de tono actual con los botones **<** y **>** a cada lado.
2. Para escribir un valor directamente, haga clic en el campo numérico, ingrese un valor entre 100 y 6000, y presione Enter o Tab.
3. Para ajustar en pasos de 10 Hz, haga clic en **<** para disminuir el tono o en **>** para aumentarlo.
4. El nuevo tono se envía a la radio inmediatamente. Valor predeterminado: 600 Hz.

El generador de tono lateral del lado del cliente siempre sigue este valor de tono automáticamente. No hay un control de tono local separado.

### Ajustar el retardo CW

1. Localice **Delay** (Retardo) en el subpanel CW. Tiene un deslizador y un campo de valor editable.
2. Para escribir un valor directamente, haga clic en el campo numérico, ingrese un valor entre 0 y 2000 (milisegundos), y presione Enter o Tab. El deslizador se mueve para coincidir.
3. Deslice el control para ajustar en pasos de 10 ms.
4. Valor predeterminado: 500 ms.

En la v0.9.8, el método `setCwDelay` se corrigió para almacenar en caché el valor inmediatamente, de modo que la emisión de la radio no devuelva el deslizador a su posición anterior (#2428).

### Ajustar la velocidad CW

1. Localice **Speed** (Velocidad) en el subpanel CW. Tiene un deslizador y un campo de valor editable.
2. Para escribir un valor directamente, haga clic en el campo numérico, ingrese un valor entre 5 y 100 (WPM), y presione Enter o Tab. El deslizador se mueve para coincidir.
3. Deslice el control para ajustar en pasos.
4. Valor predeterminado: 20 WPM.

### Activar o desactivar el tono lateral

1. Haga clic en **Sidetone** (Tono lateral) en el subpanel CW para activarlo o desactivarlo.
2. Tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente se activan o desactivan juntos mediante este único botón.

### Ajustar el volumen del tono lateral

1. Localice **Sidetone volume** (Volumen de tono lateral) en el subpanel CW. Tiene un deslizador y un campo de valor editable.
2. Para escribir un valor directamente, haga clic en el campo numérico, ingrese un valor entre 0 y 100, y presione Enter o Tab. El deslizador se mueve para coincidir.
3. Deslice el control para ajustar el volumen.
4. Valor predeterminado: 50.
5. El deslizador ajusta simultáneamente el volumen del monitor de la radio (`mon_gain_cw`) y el volumen del generador de tono lateral del lado del cliente.

### Ajustar la panoramización del monitor CW

1. Localice **L / R pan (CW)** (Panorámica I/D (CW)) en el subpanel CW. Es un deslizador de 0 (totalmente a la izquierda) a 100 (totalmente a la derecha).
2. Deslice hasta la posición estéreo deseada.
3. Haga doble clic en el deslizador para volver a centrarlo en 50 (centro).
4. Valor predeterminado: 50.

### Activar/desactivar la inserción (QSK)

1. Haga clic en **Breakin** (Inserción) en el subpanel CW. Cuando está activado (inserción completa, QSK), los flancos de la tecla activan la TX inmediatamente y el retardo de inserción mantiene el relé abierto entre elementos.
2. Cuando la inserción está desactivada, las teclas se ponen en cola y la radio no pasa a TX hasta que active el PTT manualmente. La envolvente de PTT automática anterior que enmascaraba la desactivación de Breakin se ha eliminado (v0.9.7).

### Activar/desactivar el manipulador iámbico

1. Haga clic en **Iambic** (Iámbico) en el subpanel CW para activar o desactivar el manipulador de paletas iámbico.

### Ajustar los controles del micrófono (panel de Teléfono)

1. Seleccione un perfil de micrófono del cuadro combinado **Mic profile** (Perfil de micrófono) para cargar el perfil de procesamiento de micrófono nombrado.
2. Seleccione la fuente de micrófono del cuadro combinado **Mic source** (Fuente de micrófono) (MIC, BAL, LINE, ACC, PC, más cualquier otra de la lista de entrada de micrófono de la radio).
3. Ajuste el deslizador **Mic gain** (Ganancia de micrófono) (0–100, predeterminado 50) para configurar el nivel de entrada del micrófono. Cuando la fuente está configurada en **PC**, el valor se almacena del lado del cliente en `PcMicGain` y la radio lo ignora.
4. Haga clic en **+ACC** para activar la mezcla de entrada del micrófono accesorio.
5. Haga clic en **PROC** para activar o desactivar el procesador de voz.
6. Use el deslizador **NOR/DX/DX+** para seleccionar el nivel del procesador (0 = NOR, 1 = DX, 2 = DX+).
7. Haga clic en **DAX** para activar DAX como fuente de audio de TX.
8. Haga clic en **MON** para activar el monitor de banda lateral.
9. Ajuste el deslizador **Monitor volume** (Volumen del monitor) (0–100) para configurar el volumen del monitor de banda lateral.

### Leer los medidores

- Indicador **Level** (Nivel): Muestra el nivel pico de entrada del micrófono en dBFS (-40 a +10 dBFS, rojo por encima de 0 dBFS). Suprimido a -150 cuando `met_in_rx` está desactivado y no se está transmitiendo. Se aplica a todas las fuentes de micrófono, incluyendo PC y RADE (v26.5.3).
- Indicador **Compression** (Compresión): Muestra la cantidad de compresión de voz en dB (0 dB = ninguna, -25 dB = compresión completa). Controlado por el estado TRANSMITTING del interbloqueo de la radio y la activación del procesador de voz. Marca 0 dB durante la recepción (v0.9.7). En la v26.5.3, convierte correctamente los valores positivos del medidor `COMPPEAK` (0–25 dB) al rango negativo del indicador.
- Indicador **ALC (Phone panel)** (ALC, panel de Teléfono): Muestra la lectura del control automático de nivel del medidor ALC por software (pico SSB post-ALC por software en dBFS, rango -20 a 0 dBFS, rojo por encima de -3 dBFS). Se llena desde la derecha, con vacío en -20 dBFS y lleno en 0 dBFS (#2552, v26.5.1). Inicializado a -20 dBFS al inicio (v26.5.3).
- Indicador **ALC (CW panel)** (ALC, panel de CW): Espejo idéntico del indicador ALC del panel de Teléfono, ambos impulsados por la misma fuente (`MeterModel::swAlcChanged`). El rango, la escala y la dirección de llenado coinciden exactamente con la versión del panel de Teléfono (#2552, v26.5.1). Inicializado a -20 dBFS al inicio (v26.5.3).

## Qué hace cada control

### Controles de Teléfono

| Control             | Predeterminado | Rango válido        |
|---------------------|----------------|---------------------|
| **Mic profile**     | —              | De la lista de la radio |
| **Mic source**      | —              | MIC, BAL, LINE, ACC, PC |
| **Mic gain**        | 50             | 0–100               |
| **+ACC**            | —              | Activado / Desactivado |
| **PROC**            | —              | Activado / Desactivado |
| **NOR/DX/DX+**      | 0              | 0, 1, 2             |
| **DAX**             | —              | Activado / Desactivado |
| **MON**             | —              | Activado / Desactivado |
| **Monitor volume**  | —              | 0–100               |

### Controles CW

| Control             | Predeterminado | Rango válido             |
|---------------------|----------------|--------------------------|
| **Delay (CW)**      | 500 ms         | 0–2000 ms (paso 10)      |
| **Speed (CW)**      | 20 WPM         | 5–100 WPM                |
| **Sidetone**        | —              | Activado / Desactivado   |
| **Sidetone volume** | 50             | 0–100                    |
| **L / R pan (CW)**  | 50             | 0–100                    |
| **Breakin**         | —              | Activado / Desactivado   |
| **Iambic**          | —              | Activado / Desactivado   |
| **Pitch < / >**     | 600 Hz         | 100–6000 Hz (paso 10)    |

## Modo RADE y el deslizador de nivel de micrófono

Cuando el modo RADE está activo, el deslizador **Mic gain** (Ganancia de micrófono) actúa como un control de ganancia RADE del lado del cliente en lugar de enviar un comando de nivel de micrófono a la radio. Esto refleja el comportamiento de la fuente de micrófono **PC**, donde la radio no utiliza el valor del nivel de micrófono. Ambos casos almacenan su ganancia en `PcMicGain`.

Mientras RADE está activo:

- El deslizador **Mic gain** lee y guarda en `PcMicGain` y no envía comandos `mic_level` a la radio.
- El indicador **Level** (Nivel) utiliza el comportamiento de compuerta de recepción estándar (v26.5.3). Permanece activo durante la recepción solo si `met_in_rx` está activado o la radio está transmitiendo. Cuando el modo RADE está activo, el estado del indicador se actualiza mediante `applyLevelMeterReceiveGate()`.
- Cuando el modo RADE se desactiva, el deslizador vuelve a reflejar el nivel de micrófono de la radio, y el indicador **Level** continúa siguiendo la lógica de compuerta de recepción.

## Consejos

- El control **Pitch < / >** (Tono) afecta tanto al tono lateral audible en la radio como a la frecuencia utilizada por el decodificador CW. Ajústelo para que coincida con su preferencia de tono personal. El tono lateral del lado del cliente siempre lo sigue automáticamente.
- Dado que el tono y la panoramización siguen automáticamente los ajustes de la radio, solo necesita ajustar **Pitch < / >** y **L / R pan (CW)** (Panorámica I/D (CW)) en un solo lugar: tanto el monitor de la radio como el generador local se actualizan juntos.
- El generador de tono lateral del lado del cliente opera con una latencia de aproximadamente 10 ms y funciona con transmisiones generadas por paletas, llave recta y CWX. Si no escucha ningún tono lateral, verifique que **Sidetone** (Tono lateral) esté activado.
- En la v26.5.3, el tono lateral de CW se enruta al dispositivo de salida de audio seleccionado en lugar de a la salida predeterminada del sistema. Verifique su selección de salida de audio si el tono lateral no es audible.
- El indicador **Compression** (Compresión) marca 0 dB durante la recepción. Solo muestra un valor mientras el interbloqueo de la radio informa TRANSMITTING y el procesador de voz está activado. Esto evita que aparezcan lecturas obsoletas entre transmisiones.
- Con **Breakin** (Inserción) desactivado, las teclas se ponen en cola y la radio no pasa a TX hasta que active el PTT manualmente. Con **Breakin** activado (QSK), los flancos de la tecla activan la TX inmediatamente y el retardo de inserción mantiene el relé abierto entre elementos
