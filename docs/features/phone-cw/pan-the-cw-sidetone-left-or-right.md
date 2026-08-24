# Applet de Phone/CW

El applet de Phone/CW muestra los controles de transmisión que se seleccionan automáticamente según el modo del slice activo. Cuando el slice activo está en un modo de teléfono (AM, FM, SSB), el applet muestra los controles de micrófono y de procesador de voz. Cuando el slice activo está en modo CW, cambia automáticamente a los controles de CW (retardo, velocidad, tono lateral, iambic, tono).

## Abrir el applet de Phone/CW

1. Haga clic en el botón de la bandeja **P/CW** en la barra lateral derecha.

El panel del applet se abre y muestra los controles apropiados para el modo del slice actual.

## Controles del panel de Phone

### Medidor de nivel de micrófono

Muestra el nivel de pico de entrada del micrófono en dBFS (-40 a +10 dBFS, en rojo por encima de 0 dBFS). Pase el cursor sobre el indicador para ver el valor exacto en dB con un decimal.

El medidor se suprime a -150 cuando `met_in_rx` está desactivado y la radio no está transmitiendo. En v26.5.3, la aplicación aplica inmediatamente la compuerta de recepción cada vez que cambia el estado de transmisión o el estado de MOX, evitando que aparezcan lecturas de nivel obsoletas durante la recepción.

### Medidor de compresión

Muestra la cantidad de compresión de voz en dB. La cara del medidor está invertida: 0 dB = sin compresión, -25 dB = compresión completa. Pase el cursor sobre el indicador para ver la cantidad exacta de compresión en dB con un decimal (mostrada como valor positivo).

El indicador lee el medidor COMPPEAK de la radio, que reporta la compresión como un valor positivo de 0 a 25 dB. El indicador niega internamente este valor para mostrarlo como -25 a 0 dB (relleno invertido). El indicador solo muestra una lectura de compresión mientras la radio está transmitiendo activamente con el procesador de voz habilitado. Durante la recepción, o cuando el procesador de voz está deshabilitado, el indicador lee 0 dB independientemente de cualquier dato residual del medidor de la cadena de TX.

### Medidor ALC (panel de Phone)

Muestra la lectura de control automático de nivel del medidor ALC de software (MeterModel::swAlcChanged). El indicador lee el pico SSB posterior al ALC de software en dBFS, reemplazando la ruta anterior de HWALC (voltaje RCA) que producía lecturas sin significado. Pase el cursor sobre el indicador para ver el valor exacto en dBFS con un decimal.

- **Rango:** -20 a 0 dBFS
- **Zona roja:** por encima de -3 dBFS
- **Dirección de relleno:** de derecha a izquierda (vacío a -20 dBFS, lleno a 0 dBFS)

En v26.5.3, el indicador se inicializa a -20 dBFS inmediatamente al construirse, y la constante de piso se comparte entre los indicadores de los paneles de Phone y CW. El comportamiento anterior permitía que el indicador permaneciera en 0 dBFS momentáneamente antes de recibir la primera actualización del medidor.

El indicador ALC del panel de Phone tiene su espejo en un indicador idéntico en el panel de CW. Ambos indicadores leen de la misma fuente, por lo que los operadores de SSB que observan la ganancia del micrófono ven el mismo indicador que los operadores de CW usan para verificar la forma del sobre de manipulación.

### Perfil de micrófono

Seleccione el perfil de procesamiento del micrófono. Haga clic en el cuadro combinado y elija un perfil de la lista, que se completa desde los perfiles de micrófono disponibles en la radio.

### Fuente de micrófono

Seleccione la fuente de entrada del micrófono. Haga clic en el cuadro combinado y elija entre MIC, BAL, LINE, ACC, PC o cualquier otra fuente que proporcione la radio.

Cuando la modulación del host está activa (la radio es modulada por AetherSDR), el control de fuente de micrófono se deshabilita y muestra solo "PC". Una información sobre herramientas explica que las otras fuentes son conectores de FlexRadio que no están disponibles en este modo.

En v26.8.4, cuando la selección de entrada de la radio no está disponible para este cliente, el cuadro combinado de fuente de micrófono se reconstruye para mostrar solo "PC" y el TransmitModel se actualiza para coincidir. Esto evita una lista engañosa de fuentes fantasma y mantiene la verificación de audio de transmisión de radiocert sincronizada con lo que muestra la pantalla.

### Ganancia de micrófono

Ajuste el nivel de entrada del micrófono. Arrastre el control deslizante para establecer el nivel de 0 a 100.

Para la fuente "PC", el valor se almacena localmente en la configuración `PcMicGain`. La radio siempre reporta `mic_level=0` cuando la fuente es PC.

En v26.8.4, la señal de ganancia de micrófono se emite siempre que el cliente posee la ganancia, ya sea en modo RADE o cuando la modulación del host está activa con la fuente PC seleccionada.

### +ACC

Active o desactive la mezcla de entrada del micrófono auxiliar. Haga clic en **+ACC** para alternar.

### PROC

Active o desactive el procesador de voz. Haga clic en **PROC** para alternar.

### Nivel de procesador NOR/DX/DX+

Establezca el nivel del procesador de voz. Arrastre el control deslizante a una de tres posiciones: 0 (NOR), 1 (DX) o 2 (DX+).

### DAX

Active o desactive DAX como fuente de audio de TX. Haga clic en **DAX** para alternar.

### MON

Active o desactive el monitor de tono lateral de TX. Haga clic en **MON** para alternar.

### Volumen del monitor

Ajuste el volumen del monitor de banda lateral. Arrastre el control deslizante para establecer el volumen de 0 a 100.

## Modo RADE y el control deslizante de nivel de micrófono (v0.9.7)

Cuando el modo RADE está activo, el control deslizante de **Ganancia de micrófono** actúa como un control de ganancia RADE del lado del cliente en lugar de enviar `mic_level` a la radio. El valor del control deslizante se almacena en `PcMicGain` — la misma configuración utilizada cuando la fuente de micrófono es **PC** — y no se reenvía a la radio mientras RADE está activo. Esto evita que el ajuste de ganancia RADE sobrescriba silenciosamente el nivel de micrófono de hardware en la radio.

El medidor de **Nivel** permanece activo durante RX cuando se usa RADE, lo que le permite monitorear su nivel de entrada antes de transmitir (comportamiento de "Medidor de nivel durante recepción"). Cuando el modo RADE se desactiva, el indicador de nivel se suprime y el control deslizante vuelve a mostrar el nivel de micrófono reportado por la radio.

## Controles del panel de CW

### Medidor ALC (panel de CW)

Muestra la lectura de control automático de nivel del medidor ALC de software (MeterModel::swAlcChanged). Este indicador es un espejo del indicador ALC del panel de Phone, con escala idéntica y leyendo de la misma fuente. Pase el cursor sobre el indicador para ver el valor exacto en dBFS con un decimal.

- **Rango:** -20 a 0 dBFS
- **Zona roja:** por encima de -3 dBFS
- **Dirección de relleno:** de derecha a izquierda (vacío a -20 dBFS, lleno a 0 dBFS)

En v26.5.3, el indicador se inicializa a -20 dBFS inmediatamente al construirse, evitando una lectura momentánea de 0 dBFS antes de que llegue la primera actualización del medidor.

### Retardo

Establezca el retardo de break-in de CW. Arrastre el control deslizante o escriba un valor directamente en el campo de texto adyacente:

- **Rango del control deslizante:** 0 a 2000 ms (paso 10)
- **Rango del campo de texto:** 0 a 2000 ms (escriba un número y presione Enter)
- **Predeterminado:** 500 ms

Haga clic en el campo de texto, escriba el valor de retardo deseado y presione Enter. El control deslizante se actualiza para coincidir con el valor escrito.

> v0.9.8: El campo de valor de retardo ahora es un QLineEdit con un QIntValidator (0–2000). La llamada `setCwDelay` se corrigió para almacenar en caché el valor inmediatamente para que la emisión a la radio no devuelva el control deslizante a su posición anterior (#2428).

### Velocidad

Establezca la velocidad de manipulación de CW. Arrastre el control deslizante o escriba un valor directamente en el campo de texto adyacente:

- **Rango del control deslizante:** 5 a 100 WPM
- **Rango del campo de texto:** 5 a 100 WPM (escriba un número y presione Enter)
- **Predeterminado:** 20 WPM

Haga clic en el campo de texto, escriba el valor de velocidad deseado y presione Enter. El control deslizante se actualiza para coincidir con el valor escrito.

> v0.9.8: El campo de valor de velocidad ahora es un QLineEdit con un QIntValidator (5–100).

### Tono lateral

Active o desactive el monitor de tono lateral de CW. Haga clic en **Sidetone** para alternar.

Este único botón controla tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente CwSidetoneGenerator (~10 ms de latencia) de forma sincronizada. El tono y la panorámica siempre siguen automáticamente las configuraciones `cw_pitch` y `mon_pan_cw` de la radio.

En v26.5.3, el tono lateral de CW se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899).

### Volumen del tono lateral

Ajuste el volumen del monitor de CW. Arrastre el control deslizante o escriba un valor directamente en el campo de texto adyacente:

- **Rango del control deslizante:** 0 a 100
- **Rango del campo de texto:** 0 a 100 (escriba un número y presione Enter)
- **Predeterminado:** 50

Haga clic en el campo de texto, escriba el valor de volumen deseado y presione Enter. El control deslizante se actualiza para coincidir con el valor escrito.

Un solo control deslizante controla tanto el volumen del lado de la radio (`mon_gain_cw`) como el del lado del cliente de forma sincronizada.

> v0.9.8: El campo de valor de volumen del tono lateral ahora es un QLineEdit con un QIntValidator (0–100).

### Panorámica L / R (CW)

Panoramice el tono lateral de CW a la izquierda o la derecha en el campo estéreo. Arrastre el control deslizante para ajustar la panorámica:

- **Rango:** 0 (todo a la izquierda) a 100 (todo a la derecha)
- **Predeterminado:** 50 (centro)
- **Doble clic** en el control deslizante para volver a centrar en 50.

La configuración de panorámica se aplica simultáneamente al monitor alimentado por DAX de la radio y al tono lateral de baja latencia del lado del cliente. La posición de panorámica siempre sigue la configuración `mon_pan_cw` de la radio. Si otro cliente o la propia radio cambia `mon_pan_cw`, el control deslizante se actualiza automáticamente.

#### Pasos para ajustar la panorámica

1. Abra el applet de Phone/CW si aún no está visible.
2. Confirme que el applet muestra el panel de CW — los controles de Sidetone, Delay, Speed, Breakin, Iambic y Pitch deben estar visibles. Si se muestra el panel de Phone en su lugar, cambie el slice activo a un modo CW.
3. Localice el control deslizante **L / R pan (CW)**.
4. Arrastre el control deslizante a la izquierda para panoramizar hacia el canal izquierdo, o a la derecha para panoramizar hacia el canal derecho.
5. Para volver al centro, haga doble clic en el control deslizante.

### Breakin

Active o desactive el break-in completo (QSK). Haga clic en **Breakin** para alternar.

La alternancia ahora respeta completamente la configuración `break_in` de la radio:

- **Breakin activado (QSK):** los bordes de manipulación activan TX inmediatamente; el `break_in_delay` mantiene el relé abierto entre elementos y suelta TX después del retardo configurado.
- **Breakin desactivado:** los caracteres manipulados se ponen en cola y se envían solo mientras PTT se mantiene manualmente. La radio no cambia a TX automáticamente.

El sobre de auto-PTT anterior que forzaba TX independientemente del estado de Breakin y suprimía el tiempo de retención de QSK se ha eliminado (v0.9.7).

### Iambic

Active o desactive el modo iambic del manipulador de paletas. Haga clic en **Iambic** para alternar.

### Tono (Pitch)

Establezca el tono del tono lateral de CW. Escriba un valor directamente en el campo de texto, o use los botones **<** y **>** para ajustar:

- **Rango del campo de texto:** 100 a 6000 Hz (escriba un número y presione Enter)
- **Botones de paso:** haga clic en **<** o **>** para disminuir o aumentar en 10 Hz por clic
- **Predeterminado:** 600 Hz

> v0.9.8: El campo de valor de tono ahora es un QLineEdit con un QIntValidator (100–6000), con botones adyacentes **<** y **>** (CwTriBtn).

## Referencia de indicadores

| Indicador | Rango de lectura | Significado |
|-----------|---------------|---------|
| Indicador de nivel | -40 a +10 dBFS | Nivel de pico del micrófono (pase el cursor para el valor exacto) |
| Indicador de compresión | -25 a 0 dB con relleno invertido | Cantidad de compresión de voz (pase el cursor para el valor dB positivo exacto) |
| Indicador ALC (panel de Phone) | -20 a 0 dBFS (relleno desde la derecha) | Control automático de nivel — pico SSB posterior al ALC de software, leído de MeterModel::swAlcChanged (pase el cursor para el valor dBFS exacto) |
| Indicador ALC (panel de CW) | -20 a 0 dBFS (relleno desde la derecha) | Espejo del indicador ALC del panel de Phone, con escala idéntica (pase el cursor para el valor dBFS exacto) |

## Qué hace cada control

| Control | Predeterminado | Rango válido |
|---------|---------|-------------|
| Medidor de nivel | — | -40 a +10 dBFS (rojo > 0) |
| Medidor de compresión | — | -25 a 0 dB (relleno invertido) |
| Medidor ALC (panel de Phone) | — | -20 a 0 dBFS (rojo > -3) |
| Perfil de micrófono | — | completado desde radio micProfileList() |
| Fuente de micrófono | — | MIC, BAL, LINE, ACC, PC (deshabilitado a solo "PC" cuando la modulación del host está activa) |
| Ganancia de micrófono | 50 | 0–100 |
| +ACC | — | alternar |
| PROC | — | alternar |
| NOR/DX/DX+ | 0 | 0 (NOR), 1 (DX), 2 (DX+) |
| DAX | — | alternar |
| MON | — | alternar |
| Volumen del monitor | — | 0–100 |
| Medidor ALC (panel de CW) | — | -20 a 0 dBFS (rojo > -3) |
| Retardo (
