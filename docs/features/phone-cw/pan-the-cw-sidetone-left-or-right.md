# Applet de Teléfono/CW

El applet de Teléfono/CW muestra controles de transmisión que se seleccionan automáticamente según el modo del sector activo. Cuando el sector activo está en un modo de telefonía (AM, FM, SSB), el applet muestra controles de micrófono y procesador de voz. Cuando el sector activo está en modo CW, cambia automáticamente a controles de CW (retardo, velocidad, tono lateral, iámbico, tono).

## Abrir el applet de Teléfono/CW

1. Haga clic en el botón **P/CW** de la bandeja en la barra lateral derecha.

El panel del applet se abre y muestra los controles adecuados para el modo del sector actual.

## Controles del panel de telefonía

### Medidor de nivel de micrófono

Muestra el nivel pico de entrada del micrófono en dBFS (-40 a +10 dBFS, rojo por encima de 0 dBFS). Pase el cursor sobre el indicador para ver el valor exacto en dB con un decimal.

El medidor se suprime a -150 cuando `met_in_rx` está desactivado y la radio no está transmitiendo. En v26.5.3, la aplicación aplica inmediatamente la puerta de recepción cada vez que cambia el estado de transmisión o el estado MOX, evitando que aparezcan lecturas de nivel obsoletas durante la recepción.

### Medidor de compresión

Muestra la cantidad de compresión de voz en dB. La cara del medidor está invertida: 0 dB = sin compresión, -25 dB = compresión total. Pase el cursor sobre el indicador para ver la cantidad exacta de compresión en dB con un decimal (mostrado como un valor positivo).

El indicador lee el medidor COMPPEAK de la radio, que reporta la compresión como un valor positivo de 0–25 dB. El indicador invierte internamente este valor para mostrarlo como -25 a 0 dB (relleno invertido). El indicador solo muestra una lectura de compresión mientras la radio está transmitiendo activamente con el procesador de voz habilitado. Durante la recepción, o cuando el procesador de voz está deshabilitado, el indicador lee 0 dB independientemente de cualquier dato residual del medidor de la cadena de TX.

### Medidor ALC (panel de telefonía)

Muestra la lectura de control automático de nivel del medidor ALC de software (MeterModel::swAlcChanged). El indicador lee el pico SSB posterior al ALC de software en dBFS, reemplazando la ruta anterior HWALC (voltaje RCA) que producía lecturas sin sentido. Pase el cursor sobre el indicador para ver el valor exacto en dBFS con un decimal.

- **Rango:** -20 a 0 dBFS
- **Zona roja:** por encima de -3 dBFS
- **Dirección de relleno:** de derecha a izquierda (vacío en -20 dBFS, lleno en 0 dBFS)

En v26.5.3, el indicador se inicializa a -20 dBFS inmediatamente al construirse, y la constante de piso se comparte entre los indicadores de los paneles de Telefonía y CW. El comportamiento anterior permitía que el indicador permaneciera en 0 dBFS momentáneamente antes de recibir la primera actualización del medidor.

El medidor ALC del panel de telefonía se refleja en un indicador idéntico en el panel de CW. Ambos indicadores leen de la misma fuente, por lo que los operadores de SSB que observan la ganancia del micrófono ven el mismo indicador que los operadores de CW usan para verificar la forma limpia de la envolvente de keying.

### Perfil de micrófono

Seleccione el perfil de procesamiento de micrófono. Haga clic en el cuadro combinado y elija un perfil de la lista, que se completa con los perfiles de micrófono disponibles en la radio.

### Fuente de micrófono

Seleccione la fuente de entrada del micrófono. Haga clic en el cuadro combinado y elija entre MIC, BAL, LINE, ACC, PC o cualquier otra fuente que proporcione la radio.

Cuando la modulación local está activa (la radio es modulada por AetherSDR), el control de fuente de micrófono está deshabilitado y muestra solo "PC". Una información sobre herramientas explica que las otras fuentes son conectores FlexRadio que no están disponibles en este modo.

### Ganancia de micrófono

Ajuste el nivel de entrada del micrófono. Arrastre el control deslizante para establecer el nivel de 0 a 100.

Para la fuente "PC", el valor se almacena localmente en la configuración `PcMicGain`. La radio siempre reporta `mic_level=0` cuando la fuente es PC.

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

Cuando el modo RADE está activo, el control deslizante de **Ganancia de micrófono** actúa como un control de ganancia RADE del lado del cliente en lugar de enviar `mic_level` a la radio. El valor del control deslizante se almacena en `PcMicGain`, la misma configuración utilizada cuando la fuente de micrófono es **PC**, y no se reenvía a la radio mientras RADE está activo. Esto evita que el ajuste de ganancia RADE sobrescriba silenciosamente la configuración de nivel de micrófono del hardware en la radio.

El medidor de **Nivel** permanece activo durante RX cuando se usa RADE, permitiéndole monitorear su nivel de entrada antes de transmitir (comportamiento "Medidor de nivel durante recepción"). Cuando se desactiva el modo RADE, el medidor de nivel se suprime y el control deslizante vuelve a mostrar el nivel de micrófono reportado por la radio.

## Controles del panel de CW

### Medidor ALC (panel de CW)

Muestra la lectura de control automático de nivel del medidor ALC de software (MeterModel::swAlcChanged). Este indicador es un reflejo del medidor ALC del panel de Telefonía, con la misma escala y leyendo de la misma fuente. Pase el cursor sobre el indicador para ver el valor exacto en dBFS con un decimal.

- **Rango:** -20 a 0 dBFS
- **Zona roja:** por encima de -3 dBFS
- **Dirección de relleno:** de derecha a izquierda (vacío en -20 dBFS, lleno en 0 dBFS)

En v26.5.3, el indicador se inicializa a -20 dBFS inmediatamente al construirse, evitando una lectura momentánea de 0 dBFS antes de que llegue la primera actualización del medidor.

### Retardo

Establezca el retardo de break-in de CW. Arrastre el control deslizante o escriba un valor directamente en el campo de texto adyacente:

- **Rango del control deslizante:** 0 a 2000 ms (paso 10)
- **Rango del campo de texto:** 0 a 2000 ms (escriba un número y presione Enter)
- **Valor predeterminado:** 500 ms

Haga clic en el campo de texto, escriba el valor de retardo deseado y presione Enter. El control deslizante se actualiza para coincidir con el valor escrito.

> v0.9.8: El campo de valor de retardo ahora es un QLineEdit con un QIntValidator (0–2000). La llamada `setCwDelay` se corrigió para almacenar en caché el valor inmediatamente, de modo que la emisión de la radio no devuelva el control deslizante a su posición anterior (#2428).

### Velocidad

Establezca la velocidad de keying de CW. Arrastre el control deslizante o escriba un valor directamente en el campo de texto adyacente:

- **Rango del control deslizante:** 5 a 100 WPM
- **Rango del campo de texto:** 5 a 100 WPM (escriba un número y presione Enter)
- **Valor predeterminado:** 20 WPM

Haga clic en el campo de texto, escriba el valor de velocidad deseado y presione Enter. El control deslizante se actualiza para coincidir con el valor escrito.

> v0.9.8: El campo de valor de velocidad ahora es un QLineEdit con un QIntValidator (5–100).

### Tono lateral

Active o desactive el monitor de tono lateral de CW. Haga clic en **Tono lateral** para alternar.

Este único botón controla tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente CwSidetoneGenerator (~10 ms de latencia) de forma sincronizada. El tono y la panorámica siempre siguen automáticamente la configuración `cw_pitch` y `mon_pan_cw` de la radio.

En v26.5.3, el tono lateral de CW se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899).

### Volumen de tono lateral

Ajuste el volumen del monitor de CW. Arrastre el control deslizante o escriba un valor directamente en el campo de texto adyacente:

- **Rango del control deslizante:** 0 a 100
- **Rango del campo de texto:** 0 a 100 (escriba un número y presione Enter)
- **Valor predeterminado:** 50

Haga clic en el campo de texto, escriba el valor de volumen deseado y presione Enter. El control deslizante se actualiza para coincidir con el valor escrito.

Un solo control deslizante controla tanto el volumen del tono lateral del lado de la radio (`mon_gain_cw`) como el del lado del cliente de forma sincronizada.

> v0.9.8: El campo de valor de volumen de tono lateral ahora es un QLineEdit con un QIntValidator (0–100).

### Panorámica L / R (CW)

Panoramice el tono lateral de CW hacia la izquierda o la derecha en el campo estéreo. Arrastre el control deslizante para ajustar la panorámica:

- **Rango:** 0 (completamente a la izquierda) a 100 (completamente a la derecha)
- **Valor predeterminado:** 50 (centro)
- **Doble clic** en el control deslizante para volver a centrar en 50.

La configuración de panorámica se aplica tanto al monitor alimentado por DAX de la radio como al tono lateral de baja latencia del lado del cliente simultáneamente. La posición de panorámica siempre sigue la configuración `mon_pan_cw` de la radio. Si otro cliente o la propia radio cambia `mon_pan_cw`, el control deslizante se actualiza automáticamente.

#### Pasos para ajustar la panorámica

1. Abra el applet de Teléfono/CW si aún no está visible.
2. Confirme que el applet muestra el panel de CW — los controles de Tono lateral, Retardo, Velocidad, Breakin, Iámbico y Tono deben estar visibles. Si se muestra el panel de Telefonía en su lugar, cambie el sector activo a un modo CW.
3. Localice el control deslizante **L / R pan (CW)**.
4. Arrastre el control deslizante hacia la izquierda para panoramizar hacia el canal izquierdo, o hacia la derecha para panoramizar hacia el canal derecho.
5. Para volver al centro, haga doble clic en el control deslizante.

### Breakin

Active o desactive el break-in completo (QSK). Haga clic en **Breakin** para alternar.

La alternancia ahora respeta completamente la configuración `break_in` de la radio:

- **Breakin ON (QSK):** los bordes de la tecla activan TX inmediatamente; `break_in_delay` mantiene el relé abierto entre elementos y desactiva TX después del retardo establecido.
- **Breakin OFF:** los caracteres tecleados se ponen en cola y se envían solo mientras se mantiene PTT manualmente. La radio no cambia a TX automáticamente.

La envolvente automática de PTT anterior que forzaba TX independientemente del estado de Breakin y suprimía el tiempo de espera de QSK se ha eliminado (v0.9.7).

### Iámbico

Active o desactive el modo de manipulador de paletas iámbico. Haga clic en **Iámbico** para alternar.

### Tono

Establezca el tono del tono lateral de CW. Escriba un valor directamente en el campo de texto, o use los botones **<** y **>** para ajustar:

- **Rango del campo de texto:** 100 a 6000 Hz (escriba un número y presione Enter)
- **Botones de paso:** Haga clic en **<** o **>** para disminuir o aumentar en 10 Hz por clic
- **Valor predeterminado:** 600 Hz

> v0.9.8: El campo de valor de tono ahora es un QLineEdit con un QIntValidator (100–6000), con botones **<** y **>** adyacentes (CwTriBtn).

## Referencia de indicadores

| Indicador | Rango de lectura | Significado |
|-----------|-----------------|-------------|
| Medidor de nivel | -40 a +10 dBFS | Nivel pico del micrófono (pase el cursor para el valor exacto) |
| Medidor de compresión | -25 a 0 dB relleno invertido | Cantidad de compresión de voz (pase el cursor para el valor positivo exacto en dB) |
| Medidor ALC (panel de Telefonía) | -20 a 0 dBFS (relleno desde la derecha) | Control automático de nivel — pico SSB posterior al ALC de software, leído de MeterModel::swAlcChanged (pase el cursor para el valor exacto en dBFS) |
| Medidor ALC (panel de CW) | -20 a 0 dBFS (relleno desde la derecha) | Reflejo del medidor ALC del panel de Telefonía, con escala idéntica (pase el cursor para el valor exacto en dBFS) |

## Función de cada control

| Control | Predeterminado | Rango válido |
|---------|---------------|--------------|
| Medidor de nivel | — | -40 a +10 dBFS (rojo > 0) |
| Medidor de compresión | — | -25 a 0 dB (relleno invertido) |
| Medidor ALC (panel de Telefonía) | — | -20 a 0 dBFS (rojo > -3) |
| Perfil de micrófono | — | completado desde radio micProfileList() |
| Fuente de micrófono | — | MIC, BAL, LINE, ACC, PC (deshabilitado a solo "PC" cuando la modulación local está activa) |
| Ganancia de micrófono | 50 | 0–100 |
| +ACC | — | alternancia |
| PROC | — | alternancia |
| NOR/DX/DX+ | 0 | 0 (NOR), 1 (DX), 2 (DX+) |
| DAX | — | alternancia |
| MON | — | alternancia |
| Volumen del monitor | — | 0–100 |
| Medidor ALC (panel de CW) | — | -20 a 0 dBFS (rojo > -3) |
| Retardo (CW) | 500 | 0–2000 ms (paso 10) |
| Velocidad (CW) | 20 | 5–100 WPM |
| Tono lateral | — | alternancia |
| Volumen de tono lateral | 50 | 0–100 |
| Panorámica L / R (CW) | 50 | 0–100 |
| Breakin | — | alternancia |
| Iámbico | — | alternancia |
| Tono < / > | 600
