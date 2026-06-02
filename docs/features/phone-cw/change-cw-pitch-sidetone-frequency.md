# Applet de fonía/CW

El applet de fonía/CW proporciona un panel de control de transmisión sensible al modo. Cuando el slice activo está en un modo de voz (LSB, USB, AM, FM, etc.), muestra controles de micrófono, procesador y monitor. Cuando el slice activo cambia a modo CW, el panel cambia automáticamente para mostrar controles CW que incluyen ajustes de retardo, velocidad, sintonía lateral (sidetone), iambic y tono (pitch).

En v0.9.8, las cuatro etiquetas de valor CW (Retardo, Velocidad, Volumen de sintonía lateral, Tono) ahora son widgets `QLineEdit` editables con `QIntValidator`. Haga clic en cualquier campo de valor y escriba un número directamente. Cuando presione Enter o Tab, el valor se valida y se aplica tanto al deslizador como a la radio. Deslizar el control mientras el campo de texto no está enfocado aún actualiza el texto de inmediato.

El único conmutador de **Sintonía lateral (Sidetone)** y el deslizador de **Volumen de sintonía lateral** controlan tanto el monitor alimentado por DAX de la radio como el generador de sintonía lateral de baja latencia del lado del cliente (`CwSidetoneGenerator`, aproximadamente 10 ms de latencia) de forma sincronizada. El tono y la panorámica siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio.

En v0.9.7, el indicador de **Compresión** ahora está controlado por el estado TRANSMITTING del interbloqueo de la radio (no por el flujo del medidor), por lo que marca 0 durante la recepción. **Breakin** ahora respeta completamente el ajuste `break_in` de la radio — ya no hay una envolvente automática de PTT que fuerce la transmisión. El bus de sintonía lateral se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).

En v26.5.1, tanto el subpanel de fonía como el de CW ahora cuentan con un indicador de **ALC** impulsado por el medidor de ALC del software (pico SSB post-ALC del software en dBFS), reemplazando la ruta anterior de HWALC (voltaje RCA) que producía lecturas sin sentido. Los dos indicadores son espejos idénticos entre sí, lo que garantiza que los operadores de SSB que observan la ganancia del micrófono durante la recepción vean el mismo indicador que los operadores de CW usan para verificar la forma de la envolvente de manipulación (#2552).

En v26.5.3, la sintonía lateral de CW ahora se enruta a la salida de audio seleccionada por el usuario en lugar de a la salida predeterminada (#2899). El indicador de **Compresión** ahora interpreta correctamente los valores positivos de dB de `MeterModel::COMPPEAK` y los niega para la visualización inversa del indicador. El indicador de **Nivel** ahora utiliza un método de puerta de recepción dedicado (`applyLevelMeterReceiveGate()`) que se aplica por igual a todas las fuentes de micrófono, incluyendo PC y RADE, suprimiendo el medidor a -150 cuando `met_in_rx` está desactivado y la radio no está transmitiendo.

En v26.6.1, todos los estilos de deslizadores y botones se actualizaron para usar el sistema de temas activo a través de `ThemeManager::applyStyleSheet()` y `applyPrimarySliderStyle()`, reemplazando los valores de color codificados. El contenedor del panel ahora usa `theme::setContainer()` para un soporte de temas adecuado. Los estados de hover y presionado de los botones ahora usan colores definidos por el tema (`{{color.background.1}}` y `{{color.accent}}`) en lugar de valores hexadecimales fijos.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet de fonía/CW requiere una conexión activa a la radio.
- Configure el slice activo en un modo CW para ver los controles CW, o en un modo de voz para ver los controles de fonía. El applet cambia automáticamente.
- Abra el applet de fonía/CW haciendo clic en el botón de la bandeja **P/CW** en la barra lateral derecha si no está visible.

## Pasos

### Cambiar el tono CW de la radio

1. Localice **Pitch < / >** en el subpanel CW. Muestra el valor de tono actual con los botones **<** y **>** a cada lado.
2. Para escribir un valor directamente, haga clic en el campo numérico, ingrese un valor entre 100 y 6000, y presione Enter o Tab.
3. Para ajustar en pasos de 10 Hz, haga clic en **<** para disminuir el tono o en **>** para aumentarlo.
4. El nuevo tono se envía a la radio de inmediato. Valor predeterminado: 600 Hz.

El generador de sintonía lateral del lado del cliente siempre sigue este valor de tono automáticamente. No hay un control de tono local separado.

### Ajustar el retardo CW

1. Localice **Delay** en el subpanel CW. Tiene un deslizador y un campo de valor editable.
2. Para escribir un valor directamente, haga clic en el campo numérico, ingrese un valor entre 0 y 2000 (milisegundos), y presione Enter o Tab. El deslizador se mueve para coincidir.
3. Deslice el control para ajustar en pasos de 10 ms.
4. Valor predeterminado: 500 ms.

En v0.9.8, se corrigió el método `setCwDelay` para almacenar en caché el valor de inmediato, de modo que la emisión de la radio no devuelva el deslizador a su posición anterior (#2428).

### Ajustar la velocidad CW

1. Localice **Speed** en el subpanel CW. Tiene un deslizador y un campo de valor editable.
2. Para escribir un valor directamente, haga clic en el campo numérico, ingrese un valor entre 5 y 100 (WPM), y presione Enter o Tab. El deslizador se mueve para coincidir.
3. Deslice el control para ajustar en pasos.
4. Valor predeterminado: 20 WPM.

### Activar o desactivar la sintonía lateral

1. Haga clic en **Sidetone** en el subpanel CW para activarlo o desactivarlo.
2. Tanto el monitor alimentado por DAX de la radio como el generador de sintonía lateral de baja latencia del lado del cliente se activan o desactivan juntos mediante este único botón.

### Ajustar el volumen de la sintonía lateral

1. Localice **Sidetone volume** en el subpanel CW. Tiene un deslizador y un campo de valor editable.
2. Para escribir un valor directamente, haga clic en el campo numérico, ingrese un valor entre 0 y 100, y presione Enter o Tab. El deslizador se mueve para coincidir.
3. Deslice el control para ajustar el volumen.
4. Valor predeterminado: 50.
5. El deslizador establece tanto el volumen del monitor de la radio (`mon_gain_cw`) como el volumen del generador de sintonía lateral del lado del cliente simultáneamente.

### Ajustar la panorámica del monitor CW

1. Localice **L / R pan (CW)** en el subpanel CW. Es un deslizador de 0 (total izquierda) a 100 (total derecha).
2. Deslícelo a la posición estéreo deseada.
3. Haga doble clic en el deslizador para volver a centrarlo en 50 (centro).
4. Valor predeterminado: 50.

### Activar o desactivar break-in (QSK)

1. Haga clic en **Breakin** en el subpanel CW. Cuando está activado (break-in completo, QSK), los bordes de la manipulación activan la transmisión (TX) inmediatamente y el retardo de break-in mantiene el relé abierto entre elementos.
2. Cuando break-in está desactivado, las manipulaciones se ponen en cola y la radio no pasa a TX hasta que active PTT manualmente. La envolvente automática de PTT anterior que enmascaraba BREAKIN OFF se ha eliminado (v0.9.7).

### Activar o desactivar el manipulador iambic

1. Haga clic en **Iambic** en el subpanel CW para activar o desactivar el manipulador de paletas iambic.

### Ajustar los controles del micrófono (Panel de fonía)

1. Seleccione un perfil de micrófono en el cuadro combinado **Mic profile** para cargar el perfil de procesamiento de micrófono nombrado.
2. Seleccione la fuente de micrófono en el cuadro combinado **Mic source** (MIC, BAL, LINE, ACC, PC, más cualquier otra de la lista de entradas de micrófono de la radio).
3. Ajuste el deslizador **Mic gain** (0–100, predeterminado 50) para establecer el nivel de entrada del micrófono. Cuando la fuente está configurada en **PC**, el valor se almacena en el lado del cliente en `PcMicGain` y la radio lo ignora.
4. Haga clic en **+ACC** para activar la mezcla de entrada del micrófono auxiliar.
5. Haga clic en **PROC** para activar o desactivar el procesador de voz.
6. Use el deslizador **NOR/DX/DX+** para seleccionar el nivel del procesador (0 = NOR, 1 = DX, 2 = DX+).
7. Haga clic en **DAX** para habilitar DAX como fuente de audio de TX.
8. Haga clic en **MON** para habilitar el monitor de banda lateral.
9. Ajuste el deslizador **Monitor volume** (0–100) para establecer el volumen del monitor de banda lateral.

### Leer los medidores

- **Level**: Muestra el nivel pico de entrada del micrófono en dBFS (-40 a +10 dBFS, rojo por encima de 0 dBFS). Suprimido a -150 cuando `met_in_rx` está desactivado y no está transmitiendo. Se aplica a todas las fuentes de micrófono, incluyendo PC y RADE (v26.5.3).
- **Compression**: Muestra la cantidad de compresión de voz en dB (0 dB = ninguna, -25 dB = compresión total). Controlado por el estado TRANSMITTING del interbloqueo de la radio y la activación del procesador de voz. Marca 0 dB durante la recepción (v0.9.7). En v26.5.3, convierte correctamente los valores positivos del medidor `COMPPEAK` (0–25 dB) al rango negativo del indicador.
- **ALC (Panel de fonía)**: Muestra la lectura de control automático de nivel del medidor de ALC del software (pico SSB post-ALC del software en dBFS, rango -20 a 0 dBFS, rojo por encima de -3 dBFS). Se llena desde la derecha, con vacío en -20 dBFS y lleno en 0 dBFS (#2552, v26.5.1). Inicializado a -20 dBFS al inicio (v26.5.3).
- **ALC (Panel de CW)**: Espejo idéntico del indicador ALC del panel de fonía, ambos impulsados por la misma fuente (`MeterModel::swAlcChanged`). El rango, la escala y la dirección de llenado coinciden exactamente con la versión del panel de fonía (#2552, v26.5.1). Inicializado a -20 dBFS al inicio (v26.5.3).

## Qué hace cada control

### Controles de fonía

| Control             | Predeterminado | Rango válido      |
|---------------------|----------------|-------------------|
| **Mic profile**     | —              | De la lista de la radio |
| **Mic source**      | —              | MIC, BAL, LINE, ACC, PC |
| **Mic gain**        | 50             | 0–100             |
| **+ACC**            | —              | On / Off          |
| **PROC**            | —              | On / Off          |
| **NOR/DX/DX+**      | 0              | 0, 1, 2           |
| **DAX**             | —              | On / Off          |
| **MON**             | —              | On / Off          |
| **Monitor volume**  | —              | 0–100             |

### Controles CW

| Control             | Predeterminado | Rango válido         |
|---------------------|----------------|----------------------|
| **Delay (CW)**      | 500 ms         | 0–2000 ms (paso 10)  |
| **Speed (CW)**      | 20 WPM         | 5–100 WPM            |
| **Sidetone**        | —              | On / Off             |
| **Sidetone volume** | 50             | 0–100                |
| **L / R pan (CW)**  | 50             | 0–100                |
| **Breakin**         | —              | On / Off             |
| **Iambic**          | —              | On / Off             |
| **Pitch < / >**     | 600 Hz         | 100–6000 Hz (paso 10) |

## Modo RADE y el deslizador de nivel de micrófono

Cuando el modo RADE está activo, el deslizador **Mic gain** actúa como un control de ganancia RADE del lado del cliente en lugar de enviar un comando de nivel de micrófono a la radio. Esto refleja el comportamiento de la fuente de micrófono **PC**, donde la radio no usa el valor de nivel de micrófono. Ambos casos almacenan su ganancia en `PcMicGain`.

Mientras RADE está activo:

- El deslizador **Mic gain** lee y guarda en `PcMicGain` y no envía comandos `mic_level` a la radio.
- El indicador **Level** utiliza el comportamiento de puerta de recepción estándar (v26.5.3). Permanece activo durante la recepción solo si `met_in_rx` está habilitado o la radio está transmitiendo. Cuando el modo RADE está activo, el estado del indicador se actualiza mediante `applyLevelMeterReceiveGate()`.
- Cuando el modo RADE se desactiva, el deslizador vuelve a reflejar el nivel de micrófono de la radio, y el indicador **Level** continúa siguiendo la lógica de puerta de recepción.

## Consejos

- El control **Pitch < / >** afecta tanto la sintonía lateral audible en la radio como la frecuencia utilizada por el decodificador CW. Ajústelo para que coincida con su preferencia de tono personal. La sintonía lateral del lado del cliente siempre lo rastrea automáticamente.
- Debido a que el tono y la panorámica siguen los ajustes de la radio automáticamente, solo necesita ajustar **Pitch < / >** y **L / R pan (CW)** en un solo lugar: tanto el monitor de la radio como el generador local se actualizan juntos.
- El generador de sintonía lateral del lado del cliente funciona con una latencia de aproximadamente 10 ms y funciona con transmisiones generadas por paletas, llave recta y CWX. Si no escucha ninguna sintonía lateral, verifique que **Sidetone** esté activado.
- En v26.5.3, la sintonía lateral de CW se enruta al dispositivo de salida de audio seleccionado en lugar de a la salida predeterminada del sistema. Verifique su selección de salida de audio si la sintonía lateral no es audible.
- El indicador de **Compression** marca 0 dB durante la recepción. Solo muestra un valor mientras el interbloqueo de la radio informa TRANSMITTING y el procesador de voz está activado. Esto evita que aparezcan lecturas obsoletas entre transmisiones.
- Con **Breakin** desactivado, las manipulaciones se ponen en cola y la radio no pasa a TX hasta que active PTT manualmente. Con **Breakin** activado (QSK), los bordes de la manipulación activan TX inmediatamente y el retardo de break-in mantiene el relé abierto entre elementos. Ya no hay una envolvente automática de PTT que anule este ajuste (v0.9.7).
- Para los campos de valor CW (**Delay**, **Speed**, **Sidetone volume**, **Pitch**), haga clic en el campo num
