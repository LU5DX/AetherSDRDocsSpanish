# Applet de Phone/CW

El applet de Phone/CW muestra controles de transmisión que se seleccionan automáticamente según el modo del slice activo. Cuando el slice activo está en un modo de phone (AM, FM, SSB), el applet muestra controles de micrófono y procesador de voz. Cuando el slice activo está en modo CW, cambia automáticamente a controles de CW (retardo, velocidad, tono lateral, iámbico, tono).

## Abrir el applet de Phone/CW

1. Haga clic en el botón **P/CW** en la bandeja de la barra lateral derecha.

Se abre el panel del applet y muestra los controles adecuados para el modo del slice actual.

## Controles del panel de Phone

### Medidor de nivel de micrófono

Muestra el nivel pico de entrada del micrófono en dBFS (-40 a +10 dBFS, rojo por encima de 0 dBFS).

El medidor se suprime a -150 cuando `met_in_rx` está desactivado y la radio no está transmitiendo.

### Medidor de compresión

Muestra la cantidad de compresión de voz en dB (-25 a 0 dB, con llenado invertido).

El indicador se activa con el estado TRANSMITTING del interbloqueo de la radio. Durante la recepción, el indicador marca 0 dB independientemente de cualquier dato residual del medidor de la cadena de TX. El indicador solo muestra una lectura de compresión mientras la radio está transmitiendo activamente con el procesador de voz habilitado. Esto evita que aparezcan lecturas obsoletas o engañosas cuando no está al aire.

### Medidor de ALC (Panel de Phone)

Muestra la lectura del control automático de nivel del medidor de ALC de software (MeterModel::swAlcChanged). El indicador lee el pico SSB posterior al ALC de software en dBFS, reemplazando la ruta anterior de HWALC (tensión RCA) que producía lecturas sin sentido.

- **Rango:** -20 a 0 dBFS
- **Zona roja:** por encima de -3 dBFS
- **Dirección de llenado:** de derecha a izquierda (vacío en -20 dBFS, lleno en 0 dBFS)

El indicador de ALC del panel de Phone tiene un gemelo idéntico en el panel de CW. Ambos indicadores leen de la misma fuente, por lo que los operadores de SSB que observan la ganancia del micrófono ven el mismo indicador que los operadores de CW usan para verificar la forma correcta de la envolvente de claveo.

### Perfil de micrófono

Seleccione el perfil de procesamiento de micrófono. Haga clic en el cuadro combinado y elija un perfil de la lista, que se completa con los perfiles de micrófono disponibles de la radio.

### Fuente de micrófono

Seleccione la fuente de entrada del micrófono. Haga clic en el cuadro combinado y elija entre MIC, BAL, LINE, ACC, PC o cualquier otra fuente que proporcione la radio.

### Ganancia de micrófono

Ajuste el nivel de entrada del micrófono. Arrastre el control deslizante para establecer el nivel de 0 a 100.

Para la fuente "PC", el valor se almacena localmente en el ajuste `PcMicGain`. La radio siempre informa `mic_level=0` cuando la fuente es PC.

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

Cuando el modo RADE está activo, el control deslizante **Ganancia de micrófono** actúa como un control de ganancia RADE del lado del cliente en lugar de enviar `mic_level` a la radio. El valor del control deslizante se almacena en `PcMicGain` (el mismo ajuste que se usa cuando la fuente de micrófono es **PC**) y no se reenvía a la radio mientras RADE está activo. Esto evita que el ajuste de ganancia RADE sobrescriba silenciosamente el nivel de micrófono de hardware establecido en la radio.

El medidor de **Nivel** permanece activo durante RX cuando se usa RADE, lo que le permite monitorear su nivel de entrada antes de transmitir (comportamiento "Level Meter During Receive"). Cuando el modo RADE se desactiva, el indicador de nivel se suprime y el control deslizante vuelve a mostrar el nivel de micrófono informado por la radio.

## Controles del panel de CW

### Medidor de ALC (Panel de CW)

Muestra la lectura del control automático de nivel del medidor de ALC de software (MeterModel::swAlcChanged). Este indicador es un gemelo del indicador de ALC del panel de Phone, con la misma escala y leyendo de la misma fuente.

- **Rango:** -20 a 0 dBFS
- **Zona roja:** por encima de -3 dBFS
- **Dirección de llenado:** de derecha a izquierda (vacío en -20 dBFS, lleno en 0 dBFS)

### Retardo

Establezca el retardo de break-in CW. Arrastre el control deslizante o escriba un valor directamente en el campo de texto adyacente:

- **Rango del control deslizante:** 0 a 2000 ms (paso de 10)
- **Rango del campo de texto:** 0 a 2000 ms (escriba un número y presione Enter)
- **Valor predeterminado:** 500 ms

Haga clic en el campo de texto, escriba el valor de retardo deseado y presione Enter. El control deslizante se actualiza para coincidir con el valor escrito.

> v0.9.8: El campo de valor de retardo ahora es un QLineEdit con un QIntValidator (0–2000). Se corrigió la llamada `setCwDelay` para almacenar en caché el valor inmediatamente, de modo que la emisión de la radio no reajuste el control deslizante (#2428).

### Velocidad

Establezca la velocidad de claveo CW. Arrastre el control deslizante o escriba un valor directamente en el campo de texto adyacente:

- **Rango del control deslizante:** 5 a 100 WPM
- **Rango del campo de texto:** 5 a 100 WPM (escriba un número y presione Enter)
- **Valor predeterminado:** 20 WPM

Haga clic en el campo de texto, escriba el valor de velocidad deseado y presione Enter. El control deslizante se actualiza para coincidir con el valor escrito.

> v0.9.8: El campo de valor de velocidad ahora es un QLineEdit con un QIntValidator (5–100).

### Tono lateral

Active o desactive el monitor de tono lateral CW. Haga clic en **Sidetone** para alternar.

Este único botón controla tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente (CwSidetoneGenerator, ~10 ms de latencia) de forma sincronizada. El tono y la panoramización siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio.

### Volumen del tono lateral

Ajuste el volumen del monitor CW. Arrastre el control deslizante o escriba un valor directamente en el campo de texto adyacente:

- **Rango del control deslizante:** 0 a 100
- **Rango del campo de texto:** 0 a 100 (escriba un número y presione Enter)
- **Valor predeterminado:** 50

Haga clic en el campo de texto, escriba el valor de volumen deseado y presione Enter. El control deslizante se actualiza para coincidir con el valor escrito.

Un solo control deslizante controla tanto el volumen del tono lateral del lado de la radio (`mon_gain_cw`) como el del lado del cliente de forma sincronizada.

> v0.9.8: El campo de valor de volumen de tono lateral ahora es un QLineEdit con un QIntValidator (0–100).

### Panorámica L / R (CW)

Panoramice el tono lateral CW hacia la izquierda o la derecha en el campo estéreo. Arrastre el control deslizante para ajustar la panoramización:

- **Rango:** 0 (completamente a la izquierda) a 100 (completamente a la derecha)
- **Valor predeterminado:** 50 (centro)
- **Haga doble clic** en el control deslizante para volver a centrarlo en 50.

El ajuste de panoramización se aplica tanto al monitor alimentado por DAX de la radio como al tono lateral de baja latencia del lado del cliente simultáneamente. La posición de panoramización siempre sigue el ajuste `mon_pan_cw` de la radio. Si otro cliente o la propia radio cambia `mon_pan_cw`, el control deslizante se actualiza automáticamente.

#### Pasos para ajustar la panorámica

1. Abra el applet de Phone/CW si aún no está visible.
2. Confirme que el applet muestra el panel de CW: los controles de Sidetone, Delay, Speed, Breakin, Iambic y Pitch deben estar visibles. Si se muestra el panel de Phone, cambie el slice activo a un modo CW.
3. Localice el control deslizante **L / R pan (CW)**.
4. Arrastre el control deslizante hacia la izquierda para panoramizar hacia el canal izquierdo, o hacia la derecha para panoramizar hacia el canal derecho.
5. Para volver al centro, haga doble clic en el control deslizante.

### Breakin

Active o desactive el break-in completo (QSK). Haga clic en **Breakin** para alternar.

La activación ahora respeta completamente el ajuste `break_in` de la radio:

- **Breakin ON (QSK):** los bordes de clave activan TX inmediatamente; el `break_in_delay` mantiene el relé abierto entre elementos y desactiva TX después del retardo establecido.
- **Breakin OFF:** los caracteres claveados se ponen en cola y se envían solo mientras PTT se mantiene manualmente. La radio no cambia a TX automáticamente.

Se ha eliminado la envolvente de PTT automático anterior que forzaba TX independientemente del estado de Breakin y suprimía el tiempo de retención de QSK (v0.9.7).

### Iambic

Active o desactive el modo de manipulador iámbico. Haga clic en **Iambic** para alternar.

### Tono

Establezca el tono del tono lateral CW. Escriba un valor directamente en el campo de texto, o use los botones **<** y **>** para ajustar:

- **Rango del campo de texto:** 100 a 6000 Hz (escriba un número y presione Enter)
- **Botones de paso:** Haga clic en **<** o **>** para disminuir o aumentar en 10 Hz por clic
- **Valor predeterminado:** 600 Hz

> v0.9.8: El campo de valor de tono ahora es un QLineEdit con un QIntValidator (100–6000), con botones **<** y **>** adyacentes (CwTriBtn).

## Referencia de indicadores

| Indicador | Rango de lectura | Significado |
|-----------|-----------------|-------------|
| Indicador de nivel | -40 a +10 dBFS | Nivel pico de micrófono |
| Indicador de compresión | -25 a 0 dB con llenado invertido | Cantidad de compresión de voz |
| Indicador de ALC (Panel de Phone) | -20 a 0 dBFS (llenado desde la derecha) | Control automático de nivel — pico SSB posterior al ALC de software, leído de MeterModel::swAlcChanged |
| Indicador de ALC (Panel de CW) | -20 a 0 dBFS (llenado desde la derecha) | Gemelo del indicador de ALC del panel de Phone, con la misma escala |

## Función de cada control

| Control | Valor predeterminado | Rango válido |
|---------|---------------------|--------------|
| Medidor de nivel | — | -40 a +10 dBFS (rojo > 0) |
| Medidor de compresión | — | -25 a 0 dB (llenado invertido) |
| Medidor de ALC (Panel de Phone) | — | -20 a 0 dBFS (rojo > -3) |
| Perfil de micrófono | — | completado desde radio micProfileList() |
| Fuente de micrófono | — | MIC, BAL, LINE, ACC, PC |
| Ganancia de micrófono | 50 | 0–100 |
| +ACC | — | alternar |
| PROC | — | alternar |
| NOR/DX/DX+ | 0 | 0 (NOR), 1 (DX), 2 (DX+) |
| DAX | — | alternar |
| MON | — | alternar |
| Volumen del monitor | — | 0–100 |
| Medidor de ALC (Panel de CW) | — | -20 a 0 dBFS (rojo > -3) |
| Retardo (CW) | 500 | 0–2000 ms (paso de 10) |
| Velocidad (CW) | 20 | 5–100 WPM |
| Tono lateral | — | alternar |
| Volumen del tono lateral | 50 | 0–100 |
| Panorámica L / R (CW) | 50 | 0–100 |
| Breakin | — | alternar |
| Iambic | — | alternar |
| Tono < / > | 600 | 100–6000 Hz (paso de 10) |

## Consejos

- El panel del applet cambia automáticamente entre las vistas de Phone y CW según el modo del slice activo. Si no ve los controles esperados, verifique el modo del slice activo.
- El bus de tono lateral se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).
- El indicador de compresión solo muestra lecturas mientras la radio está transmitiendo activamente con el procesador de voz habilitado.
- Cuando el modo RADE está activo, el control deslizante de Ganancia de micrófono controla la ganancia RADE del lado del cliente, no el nivel de micrófono de la radio.
- Los indicadores de ALC en ambos paneles leen de la misma fuente de ALC de software (MeterModel::swAlcChanged). A partir de v26.5.1 (#2552), esto reemplaza la ruta anterior de HWALC (tensión RCA) que producía lecturas sin sentido. El rango del indicador es de -20 a 0 dBFS, llenándose de derecha a izquierda.

## Relacionados

- [Habilitar el tono lateral CW de baja latencia (el botón Sidetone controla tanto la ruta de la radio como la local)](enable-the-low-latency-cw-sidetone-sidetone-button-drives-both-radio-and-local-path.md)
- [Cambiar el tono / frecuencia del tono lateral CW](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de tono lateral de TX](listen-to-a-tx-sidetone-monitor.md)
