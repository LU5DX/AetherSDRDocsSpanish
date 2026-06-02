# Activar el procesador de voz en nivel NOR, DX o DX+

Active el procesador de voz integrado del FLEX-8600 y elija el nivel de compresión aplicado al audio transmitido. NOR proporciona una compresión suave; DX y DX+ aumentan el procesamiento para contactos con señales más débiles.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio.
- La porción (slice) activa debe estar en un modo de fonía (USB, LSB, AM, etc.). El applet Phone/CW muestra los controles de Phone solo cuando la porción activa no está en modo CW.
- Abra el applet Phone/CW haciendo clic en el botón **P/CW** de la barra lateral derecha si aún no está visible.

## Pasos

1. En el applet Phone/CW, haga clic en **PROC** para activar el procesador de voz. El botón se ilumina en verde cuando está activo.
2. Arrastre el control deslizante **NOR/DX/DX+** al nivel de compresión deseado:
   - Posición 0 — **NOR** (normal, menos compresión)
   - Posición 1 — **DX**
   - Posición 2 — **DX+** (más compresión)
3. Observe el indicador **Compression**. El relleno invertido muestra cuántos dB de compresión se están aplicando (rango: −25 a 0 dB). Mantenga la lectura alejada del extremo izquierdo para evitar un procesamiento excesivo.
4. Observe el indicador **Level** para confirmar que la entrada del micrófono está llegando al procesador. El rango es de −40 a +10 dBFS; el medidor se vuelve rojo por encima de 0 dBFS.
5. Observe el indicador **ALC** (panel Phone) para confirmar que el nivel posterior al ALC de software está en el rango operativo normal (−20 a 0 dBFS). El indicador se llena desde la derecha; un ALC excesivo se fija en 0 dBFS.
6. Para desactivar el procesador, haga clic en **PROC** nuevamente. El botón vuelve a su estado apagado.

## Función de cada control

| Control           | Tipo                                                                                                                                                              | Valor predeterminado                                                                                                      |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| **PROC**          | Botón de conmutación                                                                                                                                              | Apagado                                                                                                                   |
| **NOR/DX/DX+**    | Control deslizante                                                                                                                                                | 0 (NOR)                                                                                                                   |
| **Level**         | Indicador                                                                                                                                                         | —                                                                                                                         |
| **Compression**   | Indicador                                                                                                                                                         | —                                                                                                                         |
| **ALC (panel Phone)** | Indicador que muestra la lectura del control automático de nivel desde MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío en −20 dBFS, lleno en 0 dBFS. | Reconectado desde HWALC (tensión RCA) al medidor SW ALC en v26.5.1 (#2552). Es reflejado por un indicador idéntico en el subpanel CW. |
| **ALC (panel CW)**    | Indicador que refleja el medidor ALC del panel Phone; ambos leen desde MeterModel::swAlcChanged para lecturas coherentes tanto en voz como en CW. Se llena de derecha a izquierda: vacío en −20 dBFS, lleno en 0 dBFS. | Añadido en v26.5.1 (#2552) como parte de la división del medidor SW ALC. Utiliza el modo HGauge::setFillFromRight.                          |

## Consejos

- Ajuste la ganancia del micrófono antes de activar el procesador. Una lectura saludable de **Level** antes de activar **PROC** proporciona al procesador una señal útil para trabajar. Consulte [Ajustar la ganancia del micrófono y activar la mezcla de accesorios](adjust-mic-gain-and-enable-the-accessory-mix.md).
- Comience en **NOR** y pase a **DX** o **DX+** solo si los informes de señal lo justifican. Un procesamiento intenso en señales fuertes suena distorsionado para la estación receptora.
- El indicador **Compression** marca 0 dB (sin relleno) cuando **PROC** está apagado, cuando la radio no está transmitiendo o cuando no hay audio presente.
- Ambos indicadores **ALC** (paneles Phone y CW) utilizan la misma fuente del medidor ALC de software. Para operación en SSB, apunte a −10 a −5 dBFS en el indicador ALC para una calidad de audio de transmisión óptima.

## Solución de problemas

- **El botón PROC no es visible** — El applet está mostrando el panel CW. El panel Phone, incluido **PROC**, aparece solo cuando la porción activa está en un modo de fonía, no en CW.
- **El indicador Compression muestra 0 dB con PROC activado** — En v0.9.7 y posteriores, el indicador **Compression** está controlado por el estado de interbloqueo TRANSMITTING de la radio: intencionalmente marca 0 dB durante la recepción para evitar lecturas obsoletas de la cadena de TX. Si el indicador aún marca 0 dB durante la transmisión, la radio no está recibiendo audio de la fuente de micrófono seleccionada. Verifique el indicador **Level** y la configuración de **Mic source**. Si **Mic source** es **PC**, la radio siempre reporta el nivel del micrófono como 0; utilice el indicador **Level** en el applet en su lugar.
- **El control deslizante NOR/DX/DX+ vuelve a su posición** — El control deslizante tiene tres posiciones válidas (0, 1, 2). Arrastrar entre puntos de ajuste lo lleva al número entero más cercano; este es el comportamiento esperado.
- **El indicador Level no aparece al conectar** — Si **Mic source** es **PC**, el indicador **Level** aparece inmediatamente al conectar sin necesidad de transmitir o de que `met_in_rx` esté activo (v0.9.3, corrección #2086). Cuando el modo RADE está activo, el indicador **Level** también aparece durante la recepción (consulte [Comportamiento del indicador Level](#comportamiento-del-indicador-level-v093)). Si el indicador aún está ausente, verifique que **Mic source** esté configurado como **PC** y que AetherSDR haya terminado de conectarse a la radio.
- **El panel Phone no se actualiza cuando VOX se activa mediante un atajo de teclado** — Esto se resolvió en v0.9.3 (#2084). Actualice a v0.9.3 o posterior si el panel Phone no se actualiza inmediatamente cuando se activa VOX mediante un atajo de teclado.
- **El indicador ALC muestra valores inesperados** — Los medidores ALC ahora leen del medidor ALC de software (MeterModel::swAlcChanged) en rangos de dBFS. Los valores fuera de −20 a 0 dBFS no se muestran; el indicador simplemente se fija en el extremo más cercano. Esto reemplaza la ruta HWALC anterior que producía lecturas sin significado.

## Controles del panel CW (v0.9.8)

En v0.9.8, las cuatro etiquetas de valor para los parámetros CW fueron reemplazadas por widgets QLineEdit. Los controles deslizantes y botones adyacentes permanecen sin cambios. Haga clic en cualquier valor y escriba un número directamente para configurarlo. Los valores se limitan al rango válido cuando presiona Enter o Tab.

| Control               | Tipo          | Valor predeterminado | Rango válido       |
|-----------------------|---------------|----------------------|--------------------|
| **Delay (CW)**        | Control deslizante + edición | 500                  | 0–2000 ms          |
| **Speed (CW)**        | Control deslizante + edición | 20                   | 5–100 WPM          |
| **Sidetone volume**   | Control deslizante + edición | 50                   | 0–100              |
| **Pitch < / >**       | Texto + botones| 600                  | 100–6000 Hz        |

- Los widgets QLineEdit de **Delay (CW)**, **Speed (CW)** y **Sidetone volume** utilizan `QIntValidator` para restringir la entrada al rango válido.
- El widget **Pitch < / >** (CwTriBtn) permite escribir un valor (100–6000) o hacer clic en los botones < / > para avanzar en pasos de 10 Hz.
- El control deslizante **Delay (CW)** se corrigió en v0.9.8 (#2428) para que `setCwDelay` almacene en caché el valor inmediatamente, evitando que la emisión de la radio devuelva el control deslizante a su posición.
- El control deslizante **Sidetone volume** controla tanto el monitor del lado de la radio (`mon_gain_cw`) como el volumen del generador de tono lateral del lado del cliente de forma sincronizada.

## Comportamiento del tono lateral CW (v0.9.1 y posteriores)

El conmutador **Sidetone** y el control deslizante **Sidetone volume** en el panel CW controlan tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente de forma sincronizada. Ya no hay un botón **Local STn** separado, un control deslizante de volumen local separado o un conmutador **Follow** de tono. Esos controles han sido eliminados.

- Activar **Sidetone** enciende tanto el monitor del lado de la radio como el generador del lado del cliente simultáneamente.
- Ajustar **Sidetone volume** establece tanto `mon_gain_cw` en la radio como el volumen del generador local al mismo valor.
- El tono y la panorámica estéreo siguen automáticamente las configuraciones `cw_pitch` y `mon_pan_cw` de la radio. No es necesario ningún anulación manual ni conmutador de seguimiento.
- En Windows, el flujo de audio del tono lateral ahora comienza inmediatamente al conectar en lugar de requerir una acción manual (v0.9.3, corrección #2105).
- El bus de tono lateral se comparte con los tonos Quindar. El tono lateral y los tonos Quindar son mutuamente excluyentes a nivel de modo.
- En v26.5.3, el tono lateral CW se enruta al dispositivo de salida de audio seleccionado por el usuario en lugar del dispositivo de salida predeterminado (#2899). No se requiere ninguna acción del usuario; el tono lateral sigue automáticamente la selección de salida de audio en la configuración de audio de la aplicación.

Si tiene configuraciones de una versión anterior que hacen referencia a `CwLocalSidetoneEnabled`, `CwLocalSidetoneVolume`, `CwLocalSidetonePitchFollow` o `CwLocalSidetonePitchHz`, esas claves ya no son leídas ni escritas por AetherSDR y pueden ignorarse.

## Comportamiento de Break-in (v0.9.7)

El conmutador **Breakin** ahora respeta completamente la configuración `break_in` de la radio.

- Con **Breakin** activado (modo QSK), los bordes de las teclas del teclado CW o del keyer MIDI activan la transmisión inmediatamente; el valor `break_in_delay` mantiene el relé abierto entre caracteres según lo esperado.
- Con **Breakin** desactivado, los caracteres tecleados se ponen en cola y el operador activa PTT manualmente. Se ha eliminado la envolvente automática de PTT que forzaba la transmisión independientemente de esta configuración y que eliminaba el tiempo de retención QSK.

## Comportamiento del indicador ALC (v26.5.1)

A partir de v26.5.1 (#2552), tanto el indicador ALC del panel Phone como el del panel CW leen del medidor ALC de software (MeterModel::swAlcChanged) en lugar de la ruta de tensión RCA de ALC de hardware (HWALC). La ruta HWALC producía lecturas sin significado; la nueva ruta proporciona valores significativos de pico SSB posteriores al ALC de software en dBFS.

- Ambos indicadores muestran un rango de −20 a 0 dBFS.
- La dirección de llenado es de derecha a izquierda: el indicador aparece vacío en −20 dBFS y se llena hacia la izquierda a medida que el nivel aumenta, alcanzando el lleno en 0 dBFS.
- Un ALC excesivo se fija en 0 dBFS.
- Los indicadores están reflejados: ajustar la ganancia del micrófono afecta a ambos indicadores de manera idéntica cuando se opera en el modo respectivo.
- Los indicadores utilizan `HGauge::setFillFromRight(true)` para una representación visual adecuada.

## Comportamiento del indicador Level (v0.9.3)

Cuando **Mic source** está configurado como **PC**, el indicador **Level** utiliza la medición del lado del cliente y no es suprimido por la bandera `met_in_rx` de la radio. El indicador aparece inmediatamente al conectar y muestra el nivel de entrada del micrófono del PC ya sea que la radio esté transmitiendo o no.

Cuando el modo RADE está activo, el indicador **Level** se comporta de la misma manera: utiliza la medición del lado del cliente y no es suprimido por `met_in_rx`, por lo que muestra el nivel de entrada RADE durante la recepción y también durante la transmisión.

Para todas las demás fuentes de micrófono con RADE inactivo, el indicador se suprime a −150 dBFS cuando `met_in_rx` está desactivado y la radio no está transmitiendo.

## Comportamiento del indicador Level (v26.5.3)

En v26.5.3, la lógica que suprime el indicador **Level** durante la recepción se ha refactorizado en un método `applyLevelMeterReceiveGate()` dedicado. Esto reemplaza la verificación de supresión en línea en `updateMeters()`. El comportamiento es funcionalmente idéntico a versiones anteriores:

- Cuando `met_in_rx` está desactivado y la radio no está transmitiendo, el indicador **Level** se establece en −150 dBFS independientemente de la fuente del micrófono. Se ha eliminado la excepción anterior para la fuente de micrófono PC y el modo RADE; esas fuentes ahora también se suprimen durante la recepción cuando el medidor de nivel durante la recepción está deshabilitado.
- Para mostrar el indicador **Level** durante la recepción para la fuente de micrófono PC o el modo RADE, active **Level Meter During Receive** en la configuración de la radio o en la configuración del applet.

## Comportamiento del modo RADE (v0.9.7)

Cuando AetherSDR activa el modo RADE, el applet Phone/CW ajusta varios comportamientos automáticamente. No se requieren pasos manuales.

- El control deslizante **Mic gain** actúa como un control de ganancia RADE del lado del cliente. Su valor se almacena en `PcMicGain` y no se envía a la radio como `mic_level`. Esto evita que el control deslizante sobrescriba silenciosamente la configuración de hardware del micrófono en la radio.
- La configuración `PcMicGain` se comparte entre la fuente de micrófono PC y el modo RADE. Ambas rutas tienen autoridad del cliente; la radio no reporta un nivel de micrófono para ninguna de las dos.
- El indicador **Level** muestra el nivel de entrada RADE durante la recepción (medición del lado del cliente, no controlada por `met_in_rx`).
- Cuando el modo RADE se desactiva, el applet resincroniza el control deslizante **Mic gain** a partir del valor reportado por la radio, y el indicador **Level** vuelve al comportamiento de supresión estándar para la fuente de micrófono activa.

## Comportamiento del indicador de compresión (v26.5.3)

En v26.5.3, el cálculo del indicador **Compression** se actualizó para interpretar correctamente el valor bruto del medidor COMPPEAK de MeterModel. El indicador ahora espera un valor positivo (compresión de 0 a 25 dB) y lo invierte para la visualización del indicador de relleno invertido.
