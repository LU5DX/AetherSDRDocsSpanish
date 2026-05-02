# Activar el procesador de voz en nivel NOR, DX o DX+

Active el procesador de voz integrado del FLEX-8600 y elija con qué intensidad comprime el audio transmitido. NOR aplica una compresión suave; DX y DX+ aumentan el procesamiento para contactos con señales débiles.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El slice activo debe estar en un modo de voz (USB, LSB, AM, etc.). El applet Phone/CW muestra los controles de Phone solo cuando el slice activo no está en modo CW.
- Abra el applet Phone/CW haciendo clic en el botón de bandeja **P/CW** en la barra lateral derecha si no está visible.

## Pasos

1. En el applet Phone/CW, haga clic en **PROC** para activar el procesador de voz. El botón se ilumina en verde cuando está activo.
2. Arrastre el control deslizante **NOR/DX/DX+** al nivel de compresión deseado:
   - Posición 0 — **NOR** (normal, menor compresión)
   - Posición 1 — **DX**
   - Posición 2 — **DX+** (mayor compresión)
3. Observe el indicador **Compression**. El relleno invertido muestra cuántos dB de compresión se están aplicando (rango: −25 a 0 dB). Mantenga la lectura fuera del extremo izquierdo para evitar un procesamiento excesivo.
4. Observe el indicador **Level** para confirmar que la entrada del micrófono está llegando al procesador. El rango es de −40 a +10 dBFS; el indicador se pone en rojo por encima de 0 dBFS.
5. Para desactivar el procesador, haga clic en **PROC** nuevamente. El botón vuelve a su estado apagado.

## Qué hace cada control

| Control         | Tipo                  | Valor predeterminado |
|-----------------|-----------------------|----------------------|
| **PROC**        | Botón de alternancia  | Off                  |
| **NOR/DX/DX+**  | Control deslizante    | 0 (NOR)              |
| **Level**       | Indicador             | —                    |
| **Compression** | Indicador             | —                    |

## Consejos

- Ajuste la ganancia del micrófono antes de activar el procesador. Una lectura saludable en **Level** antes de activar **PROC** proporciona al procesador una señal útil con la que trabajar. Consulte [Ajustar la ganancia del micrófono y activar la mezcla de accesorios](adjust-mic-gain-and-enable-the-accessory-mix.md).
- Comience en **NOR** y pase a **DX** o **DX+** solo si los informes de señal lo justifican. Un procesamiento intenso en señales fuertes suena distorsionado en la estación receptora.
- El indicador **Compression** muestra 0 dB (sin relleno) cuando **PROC** está desactivado o no hay audio presente.

## Solución de problemas

- **El botón PROC no es visible** — El applet está mostrando el panel CW. El panel Phone, incluido **PROC**, aparece solo cuando el slice activo está en un modo de voz, no en CW.
- **El indicador Compression muestra 0 dB con PROC activado** — El radio no está recibiendo audio de la fuente de micrófono seleccionada. Verifique el indicador **Level** y la configuración **Mic source**. Si **Mic source** es **PC**, el radio siempre reporta el nivel del micrófono como 0; use el indicador **Level** en el applet en su lugar.
- **El control deslizante NOR/DX/DX+ vuelve a su posición** — El control deslizante tiene tres posiciones válidas (0, 1, 2). Arrastrarlo entre los puntos de ajuste hace que se detenga en el entero más cercano; este es el comportamiento esperado.
- **El indicador Level no aparece al conectar** — Si **Mic source** es **PC**, el indicador **Level** ahora aparece inmediatamente al conectar sin necesidad de transmitir ni de que `met_in_rx` esté activo (v0.9.3, corrección #2086). Si el indicador sigue ausente, verifique que **Mic source** esté configurado como **PC** y que AetherSDR haya terminado de conectarse al radio.
- **El panel Phone no se actualiza cuando VOX se activa mediante un atajo de teclado** — Este problema se resolvió en v0.9.3 (#2084). Actualice a v0.9.3 o posterior si el panel Phone no se actualiza inmediatamente cuando VOX se activa mediante un atajo de teclado.

## Comportamiento del tono lateral en CW (v0.9.1 y posterior)

El botón **Sidetone** y el control deslizante **Sidetone volume** del panel CW controlan tanto el monitor alimentado por DAX del radio como el generador de tono lateral de baja latencia del lado del cliente de forma sincronizada. Ya no existe un botón **Local STn** separado, un control deslizante de volumen local independiente ni un botón de seguimiento de tono **Follow**. Esos controles han sido eliminados.

- Activar **Sidetone** enciende simultáneamente el monitor del lado del radio y el generador del lado del cliente.
- Ajustar **Sidetone volume** establece tanto `mon_gain_cw` en el radio como el volumen del generador local al mismo valor.
- El tono y el paneo estéreo siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` del radio. No se necesita anulación manual ni botón de seguimiento.
- En Windows, el flujo de audio del tono lateral ahora se inicia inmediatamente al conectar en lugar de requerir una acción manual (v0.9.3, corrección #2105).

Si tiene configuraciones de una versión anterior que hacen referencia a `CwLocalSidetoneEnabled`, `CwLocalSidetoneVolume`, `CwLocalSidetonePitchFollow` o `CwLocalSidetonePitchHz`, esas claves ya no son leídas ni escritas por AetherSDR y pueden ignorarse.

## Comportamiento del indicador Level (v0.9.3)

Cuando **Mic source** está configurado como **PC**, el indicador **Level** utiliza la medición del lado del cliente y no es suprimido por el indicador `met_in_rx` del radio. El indicador aparece inmediatamente al conectar y muestra el nivel de entrada del micrófono del PC independientemente de si el radio está transmitiendo. Para todas las demás fuentes de micrófono, el indicador se suprime a −150 dBFS cuando `met_in_rx` está desactivado y el radio no está transmitiendo.

## Temas relacionados

- [Ajustar la ganancia del micrófono y activar la mezcla de accesorios](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Escuchar un monitor de tono lateral de TX](listen-to-a-tx-sidetone-monitor.md)
