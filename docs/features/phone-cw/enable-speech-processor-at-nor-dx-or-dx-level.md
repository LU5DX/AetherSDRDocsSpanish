# Activar el procesador de voz en nivel NOR, DX o DX+

Active el procesador de voz integrado del FLEX-8600 y elija con qué intensidad comprime el audio transmitido. NOR aplica una compresión suave; DX y DX+ aumentan el procesamiento para contactos con señales débiles.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El slice activo debe estar en un modo de voz (USB, LSB, AM, etc.). El applet Phone/CW muestra los controles Phone únicamente cuando el slice activo no está en modo CW.
- Abra el applet Phone/CW haciendo clic en el botón **P/CW** de la bandeja en la barra lateral derecha, si no está visible.

## Pasos

1. En el applet Phone/CW, haga clic en **PROC** para activar el procesador de voz. El botón se ilumina en verde cuando está activo.
2. Arrastre el control deslizante **NOR/DX/DX+** al nivel de compresión deseado:
   - Posición 0 — **NOR** (normal, menor compresión)
   - Posición 1 — **DX**
   - Posición 2 — **DX+** (mayor compresión)
3. Observe el indicador **Compression**. El relleno invertido muestra cuántos dB de compresión se están aplicando (rango: −25 a 0 dB). Mantenga la lectura fuera del extremo izquierdo para evitar un procesamiento excesivo.
4. Observe el indicador **Level** para confirmar que la señal del micrófono está llegando al procesador. El rango es de −40 a +10 dBFS; el indicador se pone en rojo por encima de 0 dBFS.
5. Para desactivar el procesador, haga clic en **PROC** nuevamente. El botón vuelve a su estado apagado.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango | Clave persistente |
|---|---|---|---|---|
| **PROC** | Botón de alternancia | Desactivado | Activado / Desactivado | — |
| **NOR/DX/DX+** | Control deslizante | 0 (NOR) | 0 = NOR, 1 = DX, 2 = DX+ | — |
| **Level** | Indicador | — | −40 a +10 dBFS (rojo por encima de 0) | — |
| **Compression** | Indicador | — | −25 a 0 dB (relleno invertido) | — |

## Consejos

- Ajuste la ganancia del micrófono antes de activar el procesador. Una lectura saludable en **Level** antes de activar **PROC** le proporciona al procesador una señal útil con la que trabajar. Consulte [Ajustar la ganancia del micrófono y activar la mezcla de accesorio](adjust-mic-gain-and-enable-the-accessory-mix.md).
- Comience en **NOR** y pase a **DX** o **DX+** solo si los reportes de señal lo justifican. Un procesamiento intenso en señales fuertes suena distorsionado en la estación receptora.
- El indicador **Compression** muestra 0 dB (sin relleno) cuando **PROC** está desactivado o no hay audio presente.

## Solución de problemas

- **El botón PROC no está visible** — El applet está mostrando el panel CW. El panel Phone, incluido **PROC**, aparece únicamente cuando el slice activo está en un modo de voz, no en CW.
- **El indicador Compression muestra 0 dB con PROC activado** — El radio no está recibiendo audio de la fuente de micrófono seleccionada. Verifique el indicador **Level** y la configuración de **Mic source**. Si **Mic source** está en **PC**, el radio siempre reporta el nivel del micrófono como 0; use el indicador **Level** del applet en su lugar.
- **El control deslizante NOR/DX/DX+ vuelve a su posición** — El control tiene tres posiciones válidas (0, 1, 2). Al arrastrar entre los puntos de encaje, se posiciona en el entero más cercano; este es el comportamiento esperado.

## Comportamiento del sidetono en CW (v0.9.1 y posteriores)

El botón de alternancia **Sidetone** y el control deslizante **Sidetone volume** del panel CW controlan de forma sincronizada tanto el monitor del radio alimentado por DAX como el generador de sidetono de baja latencia del lado del cliente. Ya no existe un botón **Local STn** independiente, un control deslizante de volumen local separado ni un botón de alternancia **Follow** para el tono. Esos controles han sido eliminados.

- Al activar **Sidetone** se encienden simultáneamente el monitor del lado del radio y el generador del lado del cliente.
- Al ajustar **Sidetone volume** se establece el mismo valor tanto para `mon_gain_cw` en el radio como para el volumen del generador local.
- El tono y el paneo estéreo siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` del radio. No se necesita ninguna anulación manual ni botón de seguimiento.

Si tiene configuraciones de una versión anterior que hacen referencia a `CwLocalSidetoneEnabled`, `CwLocalSidetoneVolume`, `CwLocalSidetonePitchFollow` o `CwLocalSidetonePitchHz`, esas claves ya no son leídas ni escritas por AetherSDR y pueden ignorarse.

## Relacionados

- [Ajustar la ganancia del micrófono y activar la mezcla de accesorio](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Escuchar un monitor de sidetono de TX](listen-to-a-tx-sidetone-monitor.md)
