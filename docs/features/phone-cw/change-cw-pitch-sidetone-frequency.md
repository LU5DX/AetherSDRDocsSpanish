# Applet de Phone/CW

El applet de Phone/CW proporciona un panel de control de transmisión sensible al modo. Cuando el slice activo está en un modo de voz (LSB, USB, AM, FM, etc.), muestra controles de micrófono, procesador y monitor. Cuando el slice activo cambia al modo CW, el panel cambia automáticamente para mostrar controles CW que incluyen ajustes de retardo, velocidad, sidetone, iambic y tono.

En la v0.9.8, las cuatro etiquetas de valor CW (Retardo, Velocidad, Volumen de sidetone, Tono) ahora son widgets `QLineEdit` editables con `QIntValidator`. Haga clic en cualquier campo de valor y escriba un número directamente. Cuando presiona Enter o Tab, el valor se valida y se aplica tanto al deslizador como al radio. Deslizar el control mientras el campo de texto no está enfocado aún actualiza el texto inmediatamente.

El único interruptor **Sidetone** y el deslizador de **Volumen de sidetone** controlan tanto el monitor alimentado por DAX del radio como el generador de sidetone de baja latencia del lado del cliente (`CwSidetoneGenerator`, aproximadamente 10 ms de latencia) de forma sincronizada. El tono y la panoramización siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` del radio.

En la v0.9.7, el indicador de **Compresión** ahora está controlado por el estado de TRANSMISIÓN del interlock del radio (no por el flujo del medidor), por lo que marca 0 durante la recepción. **Breakin** ahora respeta completamente el ajuste `break_in` del radio — ya no hay una envolvente de PTT automática que fuerce la TX. El bus de sidetone se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).

En la v26.5.1, tanto los subpaneles de Phone como de CW ahora cuentan con un indicador de **ALC** impulsado por el medidor de ALC por software (pico SSB post-ALC por software en dBFS), reemplazando la ruta anterior de HWALC (voltaje RCA) que producía lecturas sin significado. Los dos indicadores son espejos idénticos el uno del otro, asegurando que los operadores de SSB que observan la ganancia de micrófono durante la recepción vean el mismo indicador que los operadores de CW usan para verificar la forma de la envolvente de llaveo limpia (#2552).

En la v26.5.3, el sidetone de CW ahora se enruta a la salida de audio seleccionada por el usuario en lugar de a la salida predeterminada (#2899). El indicador de **Compresión** ahora interpreta correctamente los valores positivos de dB de `MeterModel::COMPPEAK` y los niega para la visualización invertida del indicador. El indicador de **Nivel** ahora utiliza un método de compuerta de recepción dedicado (`applyLevelMeterReceiveGate()`) que se aplica por igual a todas las fuentes de micrófono, incluyendo PC y RADE, suprimiendo el medidor a -150 cuando `met_in_rx` está desactivado y el radio no está transmitiendo.

En la v26.6.1, todos los estilos de deslizadores y botones se actualizaron para usar el sistema de tema activo a través de `ThemeManager::applyStyleSheet()` y `applyPrimarySliderStyle()`, reemplazando los valores de color codificados. El contenedor del panel ahora usa `theme::setContainer()` para soporte de tematización adecuado. Los estados de hover y presionado de los botones ahora usan colores definidos por el tema (`{{color.background.1}}` y `{{color.accent}}`) en lugar de valores hexadecimales fijos.

En la v26.7.4, los indicadores de **Nivel**, **Compresión** y ambos de **ALC** ahora muestran una ventana emergente al pasar el ratón que muestra el valor numérico exacto en dB o dBFS cuando pasa el ratón sobre el indicador. El cuadro combinado de **Fuente de mic** se deshabilita automáticamente y se establece en **PC** cuando el radio está siendo modulado por AetherSDR (modo de modulación del anfitrión), ya que ningún conector físico de FlexRadio es utilizable en ese modo.

## Antes de comenzar

- Conéctese a un radio FLEX-8600. El applet de Phone/CW requiere una conexión de radio activa.
- Establezca el slice activo en un modo CW para ver los controles CW, o en un modo de voz para ver los controles Phone. El applet cambia automáticamente.
- Abra el applet de Phone/CW haciendo clic en el botón de la bandeja **P/CW** en la barra lateral derecha si no está visible.

## Pasos

### Cambiar el tono CW del radio

1. Localice **Tono < / >** en el subpanel CW. Muestra el valor de tono actual con botones **<** y **>** a cada lado.
2. Para escribir un valor directamente, haga clic en el campo numérico, ingrese un valor entre 100 y 6000, y presione Enter o Tab.
3. Para ajustar en pasos de 10 Hz, haga clic en **<** para disminuir el tono o **>** para aumentarlo.
4. El nuevo tono se envía al radio inmediatamente. Valor predeterminado: 600 Hz.

El generador de sidetone del lado del cliente siempre sigue automáticamente este valor de tono. No hay un control de tono local separado.

### Ajustar el retardo CW

1. Localice **Retardo** en el subpanel CW. Tiene un deslizador y un campo de valor editable.
2. Para escribir un valor directamente, haga clic en el campo numérico, ingrese un valor entre 0 y 2000 (milisegundos), y presione Enter o Tab. El deslizador se mueve para coincidir.
3. Deslice el control para ajustar en pasos de 10 ms.
4. Valor predeterminado: 500 ms.

En la v0.9.8, el método `setCwDelay` se corrigió para almacenar en caché el valor inmediatamente para que la emisión del radio no devuelva el deslizador a su posición anterior (#2428).

### Ajustar la velocidad CW

1. Localice **Velocidad** en el subpanel CW. Tiene un deslizador y un campo de valor editable.
2. Para escribir un valor directamente, haga clic en el campo numérico, ingrese un valor entre 5 y 100 (WPM), y presione Enter o Tab. El deslizador se mueve para coincidir.
3. Deslice el control para ajustar en pasos.
4. Valor predeterminado: 20 WPM.

### Activar o desactivar el sidetone

1. Haga clic en **Sidetone** en el subpanel CW para activarlo o desactivarlo.
2. Tanto el monitor alimentado por DAX del radio como el generador de sidetone de baja latencia del lado del cliente se activan o desactivan juntos mediante este único botón.

### Ajustar el volumen del sidetone

1. Localice **Volumen de sidetone** en el subpanel CW. Tiene un deslizador y un campo de valor editable.
2. Para escribir un valor directamente, haga clic en el campo numérico, ingrese un valor entre 0 y 100, y presione Enter o Tab. El deslizador se mueve para coincidir.
3. Deslice el control para ajustar el volumen.
4. Valor predeterminado: 50.
5. El deslizador establece tanto el volumen del monitor del radio (`mon_gain_cw`) como el volumen del generador de sidetone del lado del cliente simultáneamente.

### Ajustar la panoramización del monitor CW

1. Localice **Pan L / R (CW)** en el subpanel CW. Es un deslizador de 0 (completamente a la izquierda) a 100 (completamente a la derecha).
2. Deslice hasta la posición estéreo deseada.
3. Haga doble clic en el deslizador para volver a centrarlo en 50 (centro).
4. Valor predeterminado: 50.

### Activar o desactivar break-in (QSK)

1. Haga clic en **Breakin** en el subpanel CW. Cuando está activado (break-in completo, QSK), los bordes de la llave activan la TX inmediatamente y el retardo de break-in mantiene el relé abierto entre elementos.
2. Cuando break-in está desactivado, las llaves se ponen en cola y el radio no pasa a TX hasta que active el PTT manualmente. La envolvente de PTT automática anterior que enmascaraba Breakin OFF ha sido eliminada (v0.9.7).

### Activar o desactivar el manipulador iambic

1. Haga clic en **Iambic** en el subpanel CW para activar o desactivar el manipulador de paletas iambic.

### Ajustar los controles de micrófono (panel Phone)

1. Seleccione un perfil de micrófono del cuadro combinado **Perfil de mic** para cargar el perfil de procesamiento de micrófono nombrado.
2. Seleccione la fuente de micrófono del cuadro combinado **Fuente de mic** (MIC, BAL, LINE, ACC, PC, más cualquier otra de la lista de entradas de micrófono del radio). Cuando AetherSDR está modulando el radio, el cuadro combinado **Fuente de mic** se deshabilita automáticamente y se establece solo en **PC**, ya que los conectores físicos de FlexRadio no están disponibles en este modo.
3. Ajuste el deslizador de **Ganancia de mic** (0–100, predeterminado 50) para establecer el nivel de entrada del micrófono. Cuando la fuente está configurada en **PC**, el valor se almacena del lado del cliente en `PcMicGain` y el radio lo ignora.
4. Haga clic en **+ACC** para activar la mezcla de entrada de micrófono accesorio.
5. Haga clic en **PROC** para activar o desactivar el procesador de voz.
6. Use el deslizador **NOR/DX/DX+** para seleccionar el nivel del procesador (0 = NOR, 1 = DX, 2 = DX+).
7. Haga clic en **DAX** para habilitar DAX como fuente de audio de TX.
8. Haga clic en **MON** para habilitar el monitor de banda lateral.
9. Ajuste el deslizador de **Volumen del monitor** (0–100) para establecer el volumen del monitor de banda lateral.

### Leer los medidores

- Indicador de **Nivel**: Muestra el nivel pico de entrada del micrófono en dBFS (-40 a +10 dBFS, rojo por encima de 0 dBFS). Suprimido a -150 cuando `met_in_rx` está desactivado y no está transmitiendo. Se aplica a todas las fuentes de micrófono incluyendo PC y RADE (v26.5.3). Pase el ratón sobre el indicador para ver el valor exacto en dB en una ventana emergente (#3936, v26.7.4).
- Indicador de **Compresión**: Muestra la cantidad de compresión de voz en dB (0 dB = ninguna, -25 dB = compresión completa). Controlado por el estado de TRANSMISIÓN del interlock del radio y la activación del procesador de voz. Marca 0 dB durante la recepción (v0.9.7). En la v26.5.3, convierte correctamente los valores positivos del medidor `COMPPEAK` (0–25 dB) al rango negativo del indicador. Pase el ratón sobre el indicador para ver el valor de compresión positivo exacto en dB (#3936, v26.7.4).
- Indicador de **ALC (panel Phone)**: Muestra la lectura de control automático de nivel del medidor de ALC por software (pico SSB post-ALC por software en dBFS, rango -20 a 0 dBFS, rojo por encima de -3 dBFS). Se llena desde la derecha, con vacío en -20 dBFS y lleno en 0 dBFS (#2552, v26.5.1). Inicializado a -20 dBFS al inicio (v26.5.3). Pase el ratón sobre el indicador para ver el valor exacto en dBFS con un decimal (#3936, v26.7.4).
- Indicador de **ALC (panel CW)**: Espejo idéntico del indicador de ALC del panel Phone, ambos impulsados por la misma fuente (`MeterModel::swAlcChanged`). El rango, la escala y la dirección de llenado coinciden exactamente con la versión del panel Phone (#2552, v26.5.1). Inicializado a -20 dBFS al inicio (v26.5.3). Pase el ratón sobre el indicador para ver el valor exacto en dBFS con un decimal (#3936, v26.7.4).

## Qué hace cada control

### Controles de Phone

| Control               | Predeterminado | Rango válido       |
|-----------------------|----------------|---------------------|
| **Perfil de mic**     | —              | De la lista del radio |
| **Fuente de mic**     | —              | MIC, BAL, LINE, ACC, PC |
| **Ganancia de mic**   | 50             | 0–100               |
| **+ACC**              | —              | On / Off            |
| **PROC**              | —              | On / Off            |
| **NOR/DX/DX+**        | 0              | 0, 1, 2             |
| **DAX**               | —              | On / Off            |
| **MON**               | —              | On / Off            |
| **Volumen del monitor**| —             | 0–100               |

### Controles de CW

| Control               | Predeterminado | Rango válido           |
|-----------------------|----------------|------------------------|
| **Retardo (CW)**      | 500 ms         | 0–2000 ms (paso 10)    |
| **Velocidad (CW)**    | 20 WPM         | 5–100 WPM              |
| **Sidetone**          | —              | On / Off               |
| **Volumen de sidetone**| 50            | 0–100                  |
| **Pan L / R (CW)**    | 50             | 0–100                  |
| **Breakin**           | —              | On / Off               |
| **Iambic**            | —              | On / Off               |
| **Tono < / >**        | 600 Hz         | 100–6000 Hz (paso 10)  |

## Modo RADE y el deslizador de nivel de mic

Cuando el modo RADE está activo, el deslizador de **Ganancia de mic** actúa como un control de ganancia RADE del lado del cliente en lugar de enviar un comando de nivel de micrófono al radio. Esto refleja el comportamiento de la fuente de micrófono **PC**, donde el radio no usa el valor del nivel de micrófono. Ambos casos almacenan su ganancia en `PcMicGain`.

Mientras RADE está activo:

- El deslizador de **Ganancia de mic** lee y guarda en `PcMicGain` y no envía comandos `mic_level` al radio.
- El indicador de **Nivel** usa el comportamiento de compuerta de recepción estándar (v26.5.3). Permanece activo durante la recepción solo si `met_in_rx` está activado o el radio está transmitiendo. Cuando el modo RADE está activo, el estado del indicador se actualiza mediante `applyLevelMeterReceiveGate()`.
- Cuando el modo RADE se desactiva, el deslizador vuelve a reflejar el nivel de micrófono del radio, y el indicador de **Nivel** continúa siguiendo la lógica de compuerta de recepción.

## Consejos

- El control **Tono < / >** afecta tanto al sidetone audible en el radio como a la frecuencia utilizada por el decodificador CW. Ajústelo para que coincida con su preferencia de tono personal. El sidetone del lado del cliente siempre lo sigue automáticamente.
- Dado que el tono y la panoramización siguen los ajustes del radio automáticamente, solo necesita ajustar **Tono < / >** y **Pan L / R (CW)** en un solo lugar — tanto el monitor del radio como el generador local se actualizan juntos.
- El generador de sidetone del lado del cliente opera a
