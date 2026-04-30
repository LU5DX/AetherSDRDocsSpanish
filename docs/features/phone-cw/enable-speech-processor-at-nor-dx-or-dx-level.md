# Activar el procesador de voz en nivel NOR, DX o DX+

Encienda el procesador de voz integrado de la FLEX-8600 y elija qué tan agresivamente comprime el audio transmitido. NOR proporciona compresión leve; DX y DX+ aumentan el procesamiento para contactos con señales más débiles.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio.
- El slice activo debe estar en un modo de voz (USB, LSB, AM, etc.). El applet Phone/CW muestra controles de voz solo cuando el slice activo no está en modo CW.
- Abra el applet Phone/CW haciendo clic en el botón **P/CW** de la barra lateral derecha si no está visible.

## Pasos

1. En el applet Phone/CW, haga clic en **PROC** para activar el procesador de voz. El botón se ilumina en verde cuando está activo.
2. Arrastre el deslizador **NOR/DX/DX+** al nivel de compresión deseado:
   - Posición 0 — **NOR** (normal, compresión mínima)
   - Posición 1 — **DX**
   - Posición 2 — **DX+** (compresión máxima)
3. Observe el medidor **Compression**. El relleno invertido muestra cuántos dB de compresión se están aplicando (rango: −25 a 0 dB). Mantenga la lectura fuera del extremo izquierdo para evitar un procesamiento excesivo.
4. Observe el medidor **Level** para confirmar que la entrada del micrófono está llegando al procesador. El rango es −40 a +10 dBFS; el medidor se vuelve rojo por encima de 0 dBFS.
5. Para desactivar el procesador, haga clic en **PROC** nuevamente. El botón vuelve a su estado sin iluminación.

## Qué hace cada control

| Control         | Tipo          | Predeterminado |
|-----------------|---------------|---------|
| **PROC**        | Botón de conmutación | Desactivado     |
| **NOR/DX/DX+**  | Deslizador        | 0 (NOR) |
| **Level**       | Medidor         | —       |
| **Compression** | Medidor         | —       |

## Consejos

- Ajuste la ganancia del micrófono antes de activar el procesador. Una lectura **Level** saludable antes de activar **PROC** proporciona al procesador una señal útil con la que trabajar. Consulte [Ajustar ganancia de micrófono y activar la mezcla de accesorios](adjust-mic-gain-and-enable-the-accessory-mix.md).
- Comience en **NOR** y cambie a **DX** o **DX+** solo si los reportes de señal lo justifican. El procesamiento intenso en señales fuertes suena distorsionado en la estación receptora.
- El medidor **Compression** lee 0 dB (sin relleno) cuando **PROC** está desactivado o no hay audio presente.

## Solución de problemas

- **El botón PROC no es visible** — El applet está mostrando el panel CW. El panel Phone, incluido **PROC**, aparece solo cuando el slice activo está en un modo de voz, no en CW.
- **El medidor Compression muestra 0 dB con PROC activado** — La radio no está recibiendo audio de la fuente de micrófono seleccionada. Verifique el medidor **Level** y la configuración **Mic source**. Si **Mic source** es **PC**, la radio siempre reporta el nivel del micrófono como 0; use el medidor **Level** en el applet en su lugar.
- **El deslizador NOR/DX/DX+ se bloquea** — El deslizador tiene tres posiciones válidas (0, 1, 2). Arrastrar entre puntos de bloqueo hace que se posicione en el entero más cercano; este es el comportamiento esperado.
- **El medidor Level no aparece al conectar** — Si **Mic source** es **PC**, el medidor **Level** ahora aparece inmediatamente al conectar sin requerir una transmisión o que `met_in_rx` esté activo (v0.9.3, fix #2086). Si el medidor sigue ausente, verifique que **Mic source** esté configurado en **PC** y que AetherSDR haya terminado de conectarse a la radio.
- **El panel Phone no se actualiza cuando VOX se alterna mediante atajo de teclado** — Esto se resolvió en v0.9.3 (#2084). Actualice a v0.9.3 o posterior si el panel Phone no se actualiza inmediatamente cuando VOX se alterna mediante un atajo de teclado.

## Comportamiento del sidetone de CW (v0.9.1 y posteriores)

El botón **Sidetone** y el deslizador **Sidetone volume** en el panel CW controlan tanto el monitor alimentado por DAX de la radio como el generador de sidetone de baja latencia del lado del cliente de manera sincronizada. Ya no existe un botón **Local STn** separado, un deslizador de volumen local separado ni un botón de alternancia **Follow** de tono. Estos controles se han eliminado.

- Activar **Sidetone** enciende simultáneamente tanto el monitor del lado de la radio como el generador del lado del cliente.
- Ajustar **Sidetone volume** establece tanto `mon_gain_cw` en la radio como el volumen del generador local en el mismo valor.
- El tono y la panoramización estéreo siempre siguen automáticamente las configuraciones `cw_pitch` y `mon_pan_cw` de la radio. No se necesita anulación manual ni botón de alternancia de seguimiento.
- En Windows, la secuencia de audio sidetone ahora comienza inmediatamente al conectar en lugar de requerir una acción manual (v0.9.3, fix #2105).

Si tiene configuraciones de una versión anterior que hacen referencia a `CwLocalSidetoneEnabled`, `CwLocalSidetoneVolume`, `CwLocalSidetonePitchFollow` o `CwLocalSidetonePitchHz`, AetherSDR ya no lee ni escribe esas claves y pueden ignorarse.

## Comportamiento del medidor Level (v0.9.3)

Cuando **Mic source** está configurado en **PC**, el medidor **Level** utiliza medición del lado del cliente y no se suprime por la bandera `met_in_rx` de la radio. El medidor aparece inmediatamente al conectar y muestra el nivel de entrada del micrófono de la PC independientemente de si la radio está transmitiendo o no. Para todas las otras fuentes de micrófono, el medidor se suprime a −150 dBFS cuando `met_in_rx` está desactivado y la radio no está transmitiendo.

## Relacionado

- [Ajustar ganancia de micrófono y activar la mezcla de accesorios](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Elegir una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Escuchar un monitor sidetone de TX](listen-to-a-tx-sidetone-monitor.md)
