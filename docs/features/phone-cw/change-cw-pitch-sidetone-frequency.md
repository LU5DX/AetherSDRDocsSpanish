# Applet de Phone/CW

El applet de Phone/CW proporciona un panel de control de transmisión consciente del modo. Cuando el slice activo está en un modo de voz (LSB, USB, AM, FM, etc.), muestra controles de micrófono, procesador y monitor. Cuando el slice activo cambia al modo CW, el panel cambia automáticamente para mostrar controles de CW, incluidos ajustes de retardo, velocidad, tono lateral (sidetone), iámbico y pitch (tono).

En la v0.9.8, las cuatro etiquetas de valor de CW (Delay, Speed, Sidetone volume, Pitch) ahora son widgets `QLineEdit` editables con `QIntValidator`. Haga clic en cualquier campo de valor y escriba un número directamente. Cuando presione Enter o Tab, el valor se valida y se aplica tanto al deslizador como a la radio. Mover el control mientras el campo de texto no está enfocado sigue actualizando el texto de inmediato.

El único interruptor **Sidetone** y el deslizador **Sidetone volume** controlan tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente (`CwSidetoneGenerator`, aproximadamente 10 ms de latencia) de forma sincronizada. El pitch y el paneo siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio.

En la v0.9.7, el indicador **Compression** ahora está condicionado al estado TRANSMITTING del interlock de la radio (no al flujo del medidor), por lo que lee 0 durante la recepción. **Breakin** ahora respeta completamente el ajuste `break_in` de la radio — ya no hay ninguna envolvente de auto-PTT que fuerce la transmisión. El bus de tono lateral se comparte con los tonos Quindar (mutuamente exclusivos a nivel de modo).

En la v26.5.1, tanto el subpanel de Phone como el de CW ahora cuentan con un indicador **ALC** impulsado por el medidor de ALC por software (pico SSB posterior al ALC por software en dBFS), que reemplaza la ruta anterior de HWALC (voltaje RCA) que producía lecturas sin sentido. Los dos indicadores son espejos idénticos entre sí, lo que garantiza que los operadores de SSB que observan la ganancia de micrófono durante la recepción vean el mismo indicador que los operadores de CW utilizan para verificar la forma correcta de la envolvente de manipulación (#2552).

En la v26.5.3, el tono lateral de CW ahora se enruta a la salida de audio seleccionada por el usuario en lugar de a la salida predeterminada (#2899). El indicador **Compression** ahora interpreta correctamente los valores positivos en dB de `MeterModel::COMPPEAK` y los niega para la visualización invertida del indicador. El indicador **Level** ahora utiliza un método dedicado de compuerta de recepción (`applyLevelMeterReceiveGate()`) que se aplica por igual a todas las fuentes de micrófono, incluidas PC y RADE, suprimiendo el medidor a -150 cuando `met_in_rx` está desactivado y la radio no está transmitiendo.

En la v26.6.1, todos los estilos de deslizadores y botones se actualizaron para usar el sistema de tema activo mediante `ThemeManager::applyStyleSheet()` y `applyPrimarySliderStyle()`, reemplazando los valores de color codificados. El contenedor del panel ahora usa `theme::setContainer()` para un soporte de temas adecuado. Los estados de desplazamiento y pulsación de los botones ahora usan colores definidos por el tema (`{{color.background.1}}` y `{{color.accent}}`) en lugar de valores hexadecimales fijos.

En la v26.7.4, los indicadores **Level**, **Compression** y ambos indicadores **ALC** ahora muestran una ventana emergente al pasar el mouse que muestra el valor numérico exacto en dB o dBFS al pasar el cursor sobre el indicador.

En la v26.8.4, la detección del modo CW ahora usa una sola lista compartida de modos CW (`isCwMode()`) en lugar de trece comparaciones ad hoc, reconociendo correctamente los nombres de modo CW, CWU y CWL en radios Flex, Icom y HL2. El cuadro combinado **Mic source** ahora es consciente de las capacidades: en una radio cuyo audio de transmisión proviene de esta computadora, el cuadro se limita solo a **PC**, se deshabilita y se le asigna una información sobre herramientas que explica que la selección de entrada de la propia radio se realiza en la radio. Cuando la entrada de la radio no puede ser seleccionada por el cliente, el cuadro presenta **PC** como única entrada e informa directamente al modelo de transmisión para que radiocert no informe una captura de audio de transmisión faltante.

En la v26.7.4, el cuadro combinado **Mic source** se deshabilita automáticamente y se establece en **PC** cuando la radio está siendo modulada por AetherSDR (modo de modulación del host), ya que ninguna toma física de FlexRadio se puede usar en ese modo.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet de Phone/CW requiere una conexión activa a la radio.
- Configure el slice activo a un modo CW para ver los controles de CW, o a un modo de voz para ver los controles de Phone. El applet cambia automáticamente.
- Abra el applet de Phone/CW haciendo clic en el botón de bandeja **P/CW** en la barra lateral derecha si aún no está visible.

## Pasos

### Cambiar el pitch de CW de la radio

1. Localice **Pitch < / >** en el subpanel de CW. Muestra el valor de pitch actual con botones **<** y **>** a cada lado.
2. Para escribir un valor directamente, haga clic en el campo numérico, ingrese un valor entre 100 y 6000, y presione Enter o Tab.
3. Para ajustar en pasos de 10 Hz, haga clic en **<** para disminuir el pitch o en **>** para aumentarlo.
4. El nuevo pitch se envía a la radio de inmediato. Valor predeterminado: 600 Hz.

El generador de tono lateral del lado del cliente siempre sigue este valor de pitch automáticamente. No hay un control de pitch local separado.

### Ajustar el retardo de CW

1. Localice **Delay** en el subpanel de CW. Tiene un deslizador y un campo de valor editable.
2. Para escribir un valor directamente, haga clic en el campo numérico, ingrese un valor entre 0 y 2000 (milisegundos), y presione Enter o Tab. El deslizador se mueve para coincidir.
3. Deslice el control para ajustar en pasos de 10 ms.
4. Valor predeterminado: 500 ms.

En la v0.9.8, el método `setCwDelay` se corrigió para almacenar en caché el valor de inmediato para que la emisión de la radio no haga que el deslizador vuelva a su posición (#2428).

### Ajustar la velocidad de CW

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
5. El deslizador establece simultáneamente el volumen del monitor de la radio (`mon_gain_cw`) y el volumen del generador de tono lateral del lado del cliente.

### Ajustar el paneo del monitor de CW

1. Localice **L / R pan (CW)** en el subpanel de CW. Es un deslizador de 0 (todo a la izquierda) a 100 (todo a la derecha).
2. Deslícelo hasta la posición estéreo deseada.
3. Haga doble clic en el deslizador para centrarlo nuevamente en 50 (centro).
4. Valor predeterminado: 50.

### Activar o desactivar break-in (QSK)

1. Haga clic en **Breakin** en el subpanel de CW. Cuando está activado (break-in completo, QSK), los bordes de manipulación activan la transmisión de inmediato y el retardo de break-in mantiene el relé abierto entre elementos.
2. Cuando break-in está desactivado, las manipulaciones se ponen en cola y la radio no pasa a TX hasta que active PTT manualmente. La envolvente de auto-PTT anterior que enmascaraba el estado OFF de Breakin se ha eliminado (v0.9.7).

### Activar o desactivar el manipulador iámbico

1. Haga clic en **Iambic** en el subpanel de CW para activar o desactivar el manipulador de paletas iámbico.

### Ajustar los controles de micrófono (panel Phone)

1. Seleccione un perfil de micrófono en el cuadro combinado **Mic profile** para cargar el perfil de procesamiento de micrófono nombrado.
2. Seleccione la fuente de micrófono en el cuadro combinado **Mic source** (MIC, BAL, LINE, ACC, PC, más cualquiera de la lista de entrada de micrófono de la radio).

Cuando AetherSDR está modulando la radio, el cuadro combinado **Mic source** se deshabilita automáticamente y se establece solo en **PC**, ya que las tomas físicas de FlexRadio no están disponibles en este modo (v26.7.4).

En la v26.8.4, el cuadro combinado **Mic source** también es consciente de las capacidades. En una radio cuyo audio de transmisión proviene de esta computadora, el cuadro se limita a **PC** como única entrada y se deshabilita. Una información sobre herramientas explica que la selección de entrada de la propia radio se realiza en la radio. Esto evita la situación engañosa en la que una entrada **MIC** atenuada sugiere que existe una entrada de micrófono física cuando la radio en realidad está escuchando su puerto de red. El modelo de transmisión se actualiza directamente a **PC** en este estado para que radiocert no informe una captura de audio de transmisión faltante.

3. Ajuste el deslizador **Mic gain** (0–100, valor predeterminado 50) para establecer el nivel de entrada del micrófono. Cuando la fuente está configurada en **PC**, el valor se almacena del lado del cliente en `PcMicGain` y la radio lo ignora. En la v26.8.4, la propiedad de la ganancia del lado del cliente está determinada por la sincronización del modelo consciente de capacidades: la señal `micLevelChanged` se emite solo cuando el cliente posee la ganancia (modo RADE, o entradas de micrófono seleccionables con **PC** seleccionado), para que otros componentes no apliquen la ganancia dos veces.
4. Haga clic en **+ACC** para activar la mezcla de entrada de micrófono auxiliar.
5. Haga clic en **PROC** para activar o desactivar el procesador de voz.
6. Use el deslizador **NOR/DX/DX+** para seleccionar el nivel del procesador (0 = NOR, 1 = DX, 2 = DX+).
7. Haga clic en **DAX** para activar DAX como fuente de audio de TX.
8. Haga clic en **MON** para activar el monitor de banda lateral.
9. Ajuste el deslizador **Monitor volume** (0–100) para establecer el volumen del monitor de banda lateral.

### Leer los medidores

- Indicador **Level**: Muestra el nivel pico de entrada del micrófono en dBFS (-40 a +10 dBFS, rojo por encima de 0 dBFS). Se suprime a -150 cuando `met_in_rx` está desactivado y no se está transmitiendo. Se aplica a todas las fuentes de micrófono, incluidas PC y RADE (v26.5.3). Pase el mouse sobre el indicador para ver el valor exacto en dB en una ventana emergente (#3936, v26.7.4).
- Indicador **Compression**: Muestra la cantidad de compresión de voz en dB (0 dB = ninguna, -25 dB = compresión completa). Condicionado al estado TRANSMITTING del interlock de la radio y a la activación del procesador de voz. Lee 0 dB durante la recepción (v0.9.7). En la v26.5.3, convierte correctamente los valores positivos del medidor `COMPPEAK` (0–25 dB) al rango negativo del indicador. Pase el mouse sobre el indicador para ver el valor de compresión positivo exacto en dB (#3936, v26.7.4).
- Indicador **ALC (panel Phone)**: Muestra la lectura de control automático de nivel del medidor de ALC por software (pico SSB posterior al ALC por software en dBFS, rango -20 a 0 dBFS, rojo por encima de -3 dBFS). Se llena desde la derecha, con vacío en -20 dBFS y lleno en 0 dBFS (#2552, v26.5.1). Se inicializa en -20 dBFS al inicio (v26.5.3). Pase el mouse sobre el indicador para ver el valor exacto en dBFS con un decimal (#3936, v26.7.4).
- Indicador **ALC (panel CW)**: Espejo idéntico del indicador ALC del panel Phone, ambos impulsados por la misma fuente (`MeterModel::swAlcChanged`). El rango, la escala y la dirección de llenado coinciden exactamente con la versión del panel Phone (#2552, v26.5.1). Se inicializa en -20 dBFS al inicio (v26.5.3). Pase el mouse sobre el indicador para ver el valor exacto en dBFS con un decimal (#3936, v26.7.4).

## Qué hace cada control

### Controles de Phone

| Control             | Predeterminado | Rango válido         |
|---------------------|----------------|----------------------|
| **Mic profile**     | —              | De la lista de la radio |
| **Mic source**      | —              | MIC, BAL, LINE, ACC, PC |
| **Mic gain**        | 50             | 0–100                |
| **+ACC**            | —              | On / Off             |
| **PROC**            | —              | On / Off             |
| **NOR/DX/DX+**      | 0              | 0, 1, 2              |
| **DAX**             | —              | On / Off             |
| **MON**             | —              | On / Off             |
| **Monitor volume**  | —              | 0–100                |

### Controles de CW

| Control                 | Predeterminado | Rango válido             |
|-------------------------|----------------|--------------------------|
| **Delay (CW)**          | 500 ms         | 0–2000 ms (paso 10)      |
| **Speed (CW)**          | 20 WPM         | 5–100 WPM                |
| **Sidetone**            | —              | On / Off                 |
| **Sidetone volume**     | 50             | 0–100                    |
| **L / R pan (CW)**      | 50             | 0–100                    |
| **Breakin**             | —              | On / Off                 |
| **Iambic**              | —              | On / Off                 |
