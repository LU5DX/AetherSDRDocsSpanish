# Activar el procesador de voz en nivel NOR, DX o DX+

Active el procesador de voz integrado del FLEX-8600 y elija cuán agresivamente comprime su audio transmitido. NOR proporciona una compresión suave; DX y DX+ aumentan el procesamiento para contactos con señales más débiles.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio.
- El slice activo debe estar en un modo de telefonía (USB, LSB, AM, etc.). El applet Phone/CW muestra los controles de Phone solo cuando el slice activo no está en modo CW.
- Abra el applet Phone/CW haciendo clic en el botón **P/CW** de la barra lateral derecha si aún no está visible.

## Pasos

1. En el applet Phone/CW, haga clic en **PROC** para activar el procesador de voz. El botón se ilumina en verde cuando está activo.
2. Arrastre el control deslizante **NOR/DX/DX+** al nivel de compresión deseado:
   - Posición 0 — **NOR** (normal, menos compresión)
   - Posición 1 — **DX**
   - Posición 2 — **DX+** (más compresión)
3. Observe el indicador **Compression**. El relleno invertido muestra cuántos dB de compresión se están aplicando (rango: −25 a 0 dB). Mantenga la lectura fuera del extremo izquierdo para evitar un procesamiento excesivo.
4. Observe el indicador **Level** para confirmar que la entrada del micrófono está llegando al procesador. El rango es de −40 a +10 dBFS; el medidor se pone rojo por encima de 0 dBFS.
5. Para desactivar el procesador, haga clic en **PROC** nuevamente. El botón vuelve a su estado apagado.

## Qué hace cada control

| Control          | Tipo            | Predeterminado |
|------------------|-----------------|----------------|
| **PROC**         | Botón de conmutación | Apagado    |
| **NOR/DX/DX+**   | Control deslizante  | 0 (NOR)     |
| **Level**        | Indicador       | —              |
| **Compression**  | Indicador       | —              |

## Consejos

- Ajuste la ganancia del micrófono antes de activar el procesador. Una lectura saludable de **Level** antes de activar **PROC** le proporciona al procesador una señal útil con la que trabajar. Consulte [Adjust mic gain and enable the accessory mix](adjust-mic-gain-and-enable-the-accessory-mix.md).
- Comience en **NOR** y cambie a **DX** o **DX+** solo si los informes de señal lo justifican. Un procesamiento intenso en señales fuertes suena distorsionado para la estación receptora.
- El indicador **Compression** muestra 0 dB (sin relleno) cuando **PROC** está desactivado, cuando la radio no está transmitiendo o cuando no hay audio presente.

## Resolución de problemas

- **El botón PROC no está visible** — El applet está mostrando el panel CW. El panel Phone, incluido **PROC**, aparece solo cuando el slice activo está en un modo de telefonía, no CW.
- **El indicador de Compresión muestra 0 dB con PROC activado** — En v0.9.7 y posteriores, el indicador **Compression** está controlado por el estado de TRANSMITTING del enclavamiento de la radio: intencionalmente muestra 0 dB durante la recepción para evitar lecturas obsoletas de la cadena de TX. Si el indicador aún muestra 0 dB mientras transmite, la radio no está recibiendo audio de la fuente de micrófono seleccionada. Verifique el indicador **Level** y la configuración **Mic source**. Si **Mic source** está en **PC**, la radio siempre informa el nivel del micrófono como 0; use el indicador **Level** en el applet en su lugar.
- **El control deslizante NOR/DX/DX+ vuelve a su posición** — El control deslizante tiene tres posiciones válidas (0, 1, 2). Arrastrarlo entre puntos de ajuste hace que aterrice en el entero más cercano; este es un comportamiento esperado.
- **El indicador Level no aparece al conectar** — Si **Mic source** está en **PC**, el indicador **Level** aparece inmediatamente al conectar sin requerir transmisión ni que `met_in_rx` esté activo (v0.9.3, corrección #2086). Cuando el modo RADE está activo, el indicador **Level** también aparece durante la recepción (consulte [Comportamiento del indicador Level](#comportamiento-del-indicador-level-v093)). Si el indicador aún está ausente, verifique que **Mic source** esté configurado en **PC** y que AetherSDR haya terminado de conectarse a la radio.
- **El panel Phone no se actualiza cuando VOX se activa mediante un atajo de teclado** — Esto se resolvió en v0.9.3 (#2084). Actualice a v0.9.3 o posterior si el panel Phone no se actualiza inmediatamente cuando VOX se activa mediante un atajo de teclado.

## Controles del panel CW (v0.9.8)

En v0.9.8, las cuatro etiquetas de valor para los parámetros CW se reemplazaron con widgets QLineEdit. Los controles deslizantes y botones adyacentes permanecen sin cambios. Haga clic en cualquier valor y escriba un número directamente para configurarlo. Los valores se limitan al rango válido cuando presiona Enter o Tab.

| Control                 | Tipo               | Predeterminado | Rango válido       |
|-------------------------|--------------------|----------------|--------------------|
| **Delay (CW)**          | Deslizante + edición | 500          | 0–2000 ms         |
| **Speed (CW)**          | Deslizante + edición | 20           | 5–100 WPM         |
| **Sidetone volume**     | Deslizante + edición | 50           | 0–100             |
| **Pitch < / >**         | Texto + botones    | 600           | 100–6000 Hz       |

- Los widgets QLineEdit de **Delay (CW)**, **Speed (CW)** y **Sidetone volume** usan `QIntValidator` para restringir la entrada al rango válido.
- El widget **Pitch < / >** (CwTriBtn) permite escribir un valor (100–6000) o hacer clic en los botones < / > para aumentar/disminuir en pasos de 10 Hz.
- El control deslizante **Delay (CW)** se corrigió en v0.9.8 (#2428) para que `setCwDelay` almacene en caché el valor inmediatamente, evitando que la emisión de la radio devuelva el control deslizante a su posición anterior.
- El control deslizante **Sidetone volume** controla tanto el volumen del lado de la radio (`mon_gain_cw`) como el del generador de tono lateral del lado del cliente al unísono.

## Comportamiento del tono lateral CW (v0.9.1 y posteriores)

El conmutador **Sidetone** y el control deslizante **Sidetone volume** en el panel CW controlan tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente al unísono. Ya no hay un botón separado **Local STn**, un control deslizante de volumen local separado ni un conmutador **Follow** de tono. Esos controles se han eliminado.

- Activar **Sidetone** enciende tanto el monitor del lado de la radio como el generador del lado del cliente simultáneamente.
- Ajustar **Sidetone volume** establece tanto `mon_gain_cw` en la radio como el volumen del generador local al mismo valor.
- El tono y el paneo estéreo siempre siguen automáticamente la configuración de `cw_pitch` y `mon_pan_cw` de la radio. No se necesita anulación manual ni conmutador de seguimiento.
- En Windows, el flujo de audio del tono lateral ahora comienza inmediatamente al conectar, sin requerir una acción manual (v0.9.3, corrección #2105).
- El bus de tono lateral se comparte con los tonos Quindar. El tono lateral y los tonos Quindar son mutuamente excluyentes a nivel de modo.

Si tiene configuraciones de una versión anterior que hacen referencia a `CwLocalSidetoneEnabled`, `CwLocalSidetoneVolume`, `CwLocalSidetonePitchFollow` o `CwLocalSidetonePitchHz`, esas claves ya no son leídas ni escritas por AetherSDR y pueden ignorarse.

## Comportamiento de break-in (v0.9.7)

El conmutador **Breakin** ahora respeta completamente la configuración `break_in` de la radio.

- Con **Breakin** activado (modo QSK), los bordes de las teclas del teclado CW o del teclado MIDI activan la transmisión inmediatamente; el valor `break_in_delay` mantiene el relé abierto entre caracteres según lo esperado.
- Con **Breakin** desactivado, los caracteres tecleados se ponen en cola y el operador activa PTT manualmente. Se ha eliminado la envolvente automática de PTT anterior que forzaba la transmisión independientemente de esta configuración y que eliminaba el tiempo de retención QSK.

## Comportamiento del indicador Level (v0.9.3)

Cuando **Mic source** está configurado en **PC**, el indicador **Level** utiliza la medición del lado del cliente y no es suprimido por la bandera `met_in_rx` de la radio. El indicador aparece inmediatamente al conectar y muestra el nivel de entrada del micrófono de PC, ya sea que la radio esté transmitiendo o no.

Cuando el modo RADE está activo, el indicador **Level** se comporta de la misma manera: utiliza la medición del lado del cliente y no es suprimido por `met_in_rx`, por lo que muestra el nivel de entrada RADE durante la recepción y también durante la transmisión.

Para todas las demás fuentes de micrófono con RADE inactivo, el indicador se suprime a −150 dBFS cuando `met_in_rx` está desactivado y la radio no está transmitiendo.

## Comportamiento del modo RADE (v0.9.7)

Cuando AetherSDR activa el modo RADE, el applet Phone/CW ajusta varios comportamientos automáticamente. No se requieren pasos manuales.

- El control deslizante **Mic gain** actúa como un control de ganancia RADE del lado del cliente. Su valor se almacena en `PcMicGain` y no se envía a la radio como `mic_level`. Esto evita que el control deslizante sobrescriba silenciosamente la configuración del micrófono de hardware en la radio.
- La configuración `PcMicGain` se comparte entre la fuente de micrófono PC y el modo RADE. Ambas rutas son autoritativas del lado del cliente; la radio no informa un nivel de micrófono para ninguna de las dos.
- El indicador **Level** muestra el nivel de entrada RADE durante la recepción (medición del lado del cliente, no controlada por `met_in_rx`).
- Cuando el modo RADE se desactiva, el applet resincroniza el control deslizante **Mic gain** a partir del valor informado por la radio, y el indicador **Level** vuelve al comportamiento de supresión estándar para la fuente de micrófono activa.

## Relacionados

- [Adjust mic gain and enable the accessory mix](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Pick a mic source (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Select a mic profile for a specific microphone](select-a-mic-profile-for-a-specific-microphone.md)
- [Listen to a TX sidetone monitor](listen-to-a-tx-sidetone-monitor.md)
