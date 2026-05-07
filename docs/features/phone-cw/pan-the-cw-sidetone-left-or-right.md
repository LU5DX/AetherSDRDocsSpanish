# Applet de Teléfono/CW

El applet de Teléfono/CW muestra los controles de transmisión que se seleccionan automáticamente según el modo del slice activo. Cuando el slice activo está en un modo de teléfono (AM, FM, SSB), el applet muestra los controles de micrófono y procesador de voz. Cuando el slice activo está en modo CW, cambia automáticamente a controles CW (retardo, velocidad, tono local, iámbico, tono).

## Abrir el applet de Teléfono/CW

1. Haga clic en el botón de la bandeja **P/CW** en la barra lateral derecha.

Se abre el panel del applet y muestra los controles adecuados para el modo actual del slice.

## Controles del panel de Teléfono

### Medidor de nivel de micrófono

Muestra el nivel pico de entrada del micrófono en dBFS (-40 a +10 dBFS, rojo por encima de 0 dBFS).

El medidor se suprime a -150 cuando `met_in_rx` está desactivado y la radio no está transmitiendo.

### Medidor de compresión

Muestra la cantidad de compresión de voz en dB (-25 a 0 dB, con relleno invertido).

El indicador está controlado por el estado de TRANSMISIÓN del interlock de la radio. Durante la recepción, el indicador muestra 0 dB independientemente de cualquier dato residual del medidor de la cadena de TX. El indicador solo muestra una lectura de compresión mientras la radio está transmitiendo activamente con el procesador de voz habilitado. Esto evita que aparezcan lecturas obsoletas o engañosas cuando no está al aire.

### Perfil de micrófono

Seleccione el perfil de procesamiento de micrófono. Haga clic en el cuadro combinado y elija un perfil de la lista, que se completa con los perfiles de micrófono disponibles de la radio.

### Fuente de micrófono

Seleccione la fuente de entrada del micrófono. Haga clic en el cuadro combinado y elija entre MIC, BAL, LINE, ACC, PC o cualquier otra fuente adicional proporcionada por la radio.

### Ganancia de micrófono

Ajuste el nivel de entrada del micrófono. Arrastre el control deslizante para establecer el nivel de 0 a 100.

Para la fuente "PC", el valor se almacena localmente en el ajuste `PcMicGain`. La radio siempre informa `mic_level=0` cuando la fuente es PC.

### +ACC

Active o desactive la mezcla de entrada de micrófono auxiliar. Haga clic en **+ACC** para alternar.

### PROC

Active o desactive el procesador de voz. Haga clic en **PROC** para alternar.

### Nivel de procesador NOR/DX/DX+

Establezca el nivel del procesador de voz. Arrastre el control deslizante a una de tres posiciones: 0 (NOR), 1 (DX) o 2 (DX+).

### DAX

Active o desactive DAX como fuente de audio de TX. Haga clic en **DAX** para alternar.

### MON

Active o desactive el monitor de tono local de TX. Haga clic en **MON** para alternar.

### Volumen del monitor

Ajuste el volumen del monitor de banda lateral. Arrastre el control deslizante para establecer el volumen de 0 a 100.

### Medidor ALC

Muestra la lectura de control automático de nivel en el panel CW. El rango es de 0 a 100, con rojo por encima de 80.

## Modo RADE y el control deslizante de nivel de micrófono (v0.9.7)

Cuando el modo RADE está activo, el control deslizante de **Ganancia de micrófono** actúa como un control de ganancia RADE del lado del cliente en lugar de enviar `mic_level` a la radio. El valor del control deslizante se almacena en `PcMicGain`, el mismo ajuste utilizado cuando la fuente de micrófono es **PC**, y no se reenvía a la radio mientras RADE está activo. Esto evita que el ajuste de ganancia RADE sobrescriba silenciosamente el nivel de micrófono de hardware establecido en la radio.

El medidor de **Nivel** permanece activo durante RX cuando se usa RADE, lo que le permite monitorear su nivel de entrada antes de transmitir (comportamiento "Medidor de nivel durante recepción"). Cuando el modo RADE se desactiva, el indicador de Nivel se suprime y el control deslizante vuelve a mostrar el nivel de micrófono informado por la radio.

## Controles del panel CW

### Retardo

Ajuste el retardo de break-in CW. Arrastre el control deslizante o escriba un valor directamente en el campo de texto adyacente:

- **Rango del control deslizante:** 0 a 2000 ms (paso 10)
- **Rango del campo de texto:** 0 a 2000 ms (escriba un número y presione Enter)
- **Valor predeterminado:** 500 ms

Haga clic en el campo de texto, escriba el valor de retardo deseado y presione Enter. El control deslizante se actualiza para coincidir con el valor escrito.

> v0.9.8: El campo de valor de retardo ahora es un QLineEdit con un QIntValidator (0–2000). La llamada `setCwDelay` se corrigió para almacenar en caché el valor inmediatamente, de modo que la emisión de la radio no restaure el control deslizante (#2428).

### Velocidad

Ajuste la velocidad de manipulación CW. Arrastre el control deslizante o escriba un valor directamente en el campo de texto adyacente:

- **Rango del control deslizante:** 5 a 100 WPM
- **Rango del campo de texto:** 5 a 100 WPM (escriba un número y presione Enter)
- **Valor predeterminado:** 20 WPM

Haga clic en el campo de texto, escriba el valor de velocidad deseado y presione Enter. El control deslizante se actualiza para coincidir con el valor escrito.

> v0.9.8: El campo de valor de velocidad ahora es un QLineEdit con un QIntValidator (5–100).

### Tono local

Active o desactive el monitor de tono local CW. Haga clic en **Tono local** para alternar.

Este botón único controla tanto el monitor alimentado por DAX de la radio como el generador de tono local de baja latencia del lado del cliente (~10 ms de latencia) de forma sincronizada. El tono y la panorámica siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio.

### Volumen del tono local

Ajuste el volumen del monitor CW. Arrastre el control deslizante o escriba un valor directamente en el campo de texto adyacente:

- **Rango del control deslizante:** 0 a 100
- **Rango del campo de texto:** 0 a 100 (escriba un número y presione Enter)
- **Valor predeterminado:** 50

Haga clic en el campo de texto, escriba el valor de volumen deseado y presione Enter. El control deslizante se actualiza para coincidir con el valor escrito.

Un control deslizante controla tanto el volumen del tono local del lado de la radio (`mon_gain_cw`) como del lado del cliente de forma sincronizada.

> v0.9.8: El campo de valor de volumen del tono local ahora es un QLineEdit con un QIntValidator (0–100).

### Panorámica L / R (CW)

Desplace el tono local CW hacia la izquierda o la derecha en el campo estéreo. Arrastre el control deslizante para ajustar la panorámica:

- **Rango:** 0 (completamente a la izquierda) a 100 (completamente a la derecha)
- **Valor predeterminado:** 50 (centro)
- **Doble clic** en el control deslizante para volver a centrarlo en 50.

El ajuste de panorámica se aplica tanto al monitor alimentado por DAX de la radio como al tono local de baja latencia del lado del cliente simultáneamente. La posición de panorámica sigue siempre el ajuste `mon_pan_cw` de la radio. Si otro cliente o la propia radio cambia `mon_pan_cw`, el control deslizante se actualiza automáticamente.

#### Pasos para ajustar la panorámica

1. Abra el applet de Teléfono/CW si aún no está visible.
2. Confirme que el applet muestra el panel CW: los controles de Tono local, Retardo, Velocidad, Breakin, Iámbico y Tono deben ser visibles. Si se muestra el panel de Teléfono, cambie el slice activo a un modo CW.
3. Localice el control deslizante **L / R pan (CW)**.
4. Arrastre el control deslizante hacia la izquierda para desplazar hacia el canal izquierdo, o hacia la derecha para desplazar hacia el canal derecho.
5. Para volver al centro, haga doble clic en el control deslizante.

### Breakin

Active o desactive el break-in completo (QSK). Haga clic en **Breakin** para alternar.

La alternancia ahora respeta completamente el ajuste `break_in` de la radio:

- **Breakin ON (QSK):** los bordes de la manipulación activan inmediatamente TX; el `break_in_delay` mantiene el relé abierto entre elementos y finaliza TX después del retardo establecido.
- **Breakin OFF:** los caracteres manipulados se ponen en cola y se envían solo mientras PTT se mantiene manualmente. La radio no cambia a TX automáticamente.

Se ha eliminado la envolvente de PTT automático anterior que forzaba TX independientemente del estado de Breakin y suprimía el tiempo de retención de QSK (v0.9.7).

### Iámbico

Active o desactive el modo de manipulador de paletas iámbico. Haga clic en **Iámbico** para alternar.

### Tono

Ajuste el tono del tono local CW. Escriba un valor directamente en el campo de texto, o use los botones **<** y **>** para ajustar:

- **Rango del campo de texto:** 100 a 6000 Hz (escriba un número y presione Enter)
- **Botones de paso:** Haga clic en **<** o **>** para disminuir o aumentar en 10 Hz por clic
- **Valor predeterminado:** 600 Hz

> v0.9.8: El campo de valor de tono ahora es un QLineEdit con un QIntValidator (100–6000), con botones **<** y **>** adyacentes (CwTriBtn).

## Referencia de indicadores

| Indicador | Rango de lectura | Significado |
|-----------|------------------|-------------|
| Indicador de nivel | -40 a +10 dBFS | Nivel pico de micrófono |
| Indicador de compresión | -25 a 0 dB relleno invertido | Cantidad de compresión de voz |
| Indicador ALC | 0 a 100 | Control automático de nivel (CW) |

## Qué hace cada control

| Control | Predeterminado | Rango válido |
|---------|----------------|--------------|
| Medidor de nivel | — | -40 a +10 dBFS (rojo > 0) |
| Medidor de compresión | — | -25 a 0 dB (relleno invertido) |
| Perfil de micrófono | — | completado desde radio micProfileList() |
| Fuente de micrófono | — | MIC, BAL, LINE, ACC, PC |
| Ganancia de micrófono | 50 | 0–100 |
| +ACC | — | alternar |
| PROC | — | alternar |
| NOR/DX/DX+ | 0 | 0 (NOR), 1 (DX), 2 (DX+) |
| DAX | — | alternar |
| MON | — | alternar |
| Volumen del monitor | — | 0–100 |
| Medidor ALC | — | 0–100 (rojo > 80) |
| Retardo (CW) | 500 | 0–2000 ms (paso 10) |
| Velocidad (CW) | 20 | 5–100 WPM |
| Tono local | — | alternar |
| Volumen del tono local | 50 | 0–100 |
| Panorámica L / R (CW) | 50 | 0–100 |
| Breakin | — | alternar |
| Iámbico | — | alternar |
| Tono < / > | 600 | 100–6000 Hz (paso 10) |

## Consejos

- El panel del applet cambia automáticamente entre las vistas de Teléfono y CW según el modo del slice activo. Si no ve los controles esperados, verifique el modo del slice activo.
- El bus de tono local se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).
- El indicador de Compresión solo muestra lecturas mientras la radio está transmitiendo activamente con el procesador de voz habilitado.
- Cuando el modo RADE está activo, el control deslizante de Ganancia de micrófono controla la ganancia RADE del lado del cliente, no el nivel de micrófono de la radio.

## Relacionados

- [Habilitar el tono local CW de baja latencia (el botón de tono local controla tanto la ruta de la radio como la local)](enable-the-low-latency-cw-sidetone-sidetone-button-drives-both-radio-and-local-path.md)
- [Cambiar el tono CW / frecuencia del tono local](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de tono local de TX](listen-to-a-tx-sidetone-monitor.md)
