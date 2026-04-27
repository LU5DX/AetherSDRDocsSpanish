# Activar el procesador de voz en nivel NOR, DX o DX+

Active el procesador de voz integrado del FLEX-8600 y elija con qué intensidad comprime el audio transmitido. NOR aplica una compresión moderada; DX y DX+ aumentan el procesamiento para contactos con señales más débiles.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El slice (canal de recepción) activo debe estar en un modo de voz (USB, LSB, AM, etc.). El applet Phone/CW muestra los controles de Phone solo cuando el slice activo no está en modo CW.
- Abra el applet Phone/CW haciendo clic en el botón **P/CW** de la bandeja en la barra lateral derecha, si no está visible todavía.

## Pasos

1. En el applet Phone/CW, haga clic en **PROC** para activar el procesador de voz. El botón se ilumina en verde cuando está activo.
2. Arrastre el control deslizante **NOR/DX/DX+** al nivel de compresión deseado:
   - Posición 0 — **NOR** (normal, menor compresión)
   - Posición 1 — **DX**
   - Posición 2 — **DX+** (mayor compresión)
3. Observe el indicador **Compression**. El relleno invertido muestra cuántos dB de compresión se están aplicando (rango: −25 a 0 dB). Mantenga la lectura fuera del extremo izquierdo para evitar un procesamiento excesivo.
4. Observe el indicador **Level** para confirmar que la entrada del micrófono está llegando al procesador. El rango es −40 a +10 dBFS; el medidor se pone en rojo por encima de 0 dBFS.
5. Para desactivar el procesador, haga clic en **PROC** nuevamente. El botón vuelve a su estado apagado.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango | Clave persistida |
|---|---|---|---|---|
| **PROC** | Botón de alternancia | Apagado | Activado / Apagado | — |
| **NOR/DX/DX+** | Control deslizante | 0 (NOR) | 0 = NOR, 1 = DX, 2 = DX+ | — |
| **Level** | Medidor | — | −40 a +10 dBFS (rojo por encima de 0) | — |
| **Compression** | Medidor | — | −25 a 0 dB (relleno invertido) | — |

## Consejos

- Ajuste la ganancia del micrófono antes de activar el procesador. Una lectura de **Level** adecuada antes de activar **PROC** le proporciona al procesador una señal útil con la que trabajar. Consulte [Ajustar la ganancia del micrófono y activar la mezcla de accesorio](adjust-mic-gain-and-enable-the-accessory-mix.md).
- Comience en **NOR** y pase a **DX** o **DX+** solo si los informes de señal lo justifican. Un procesamiento intenso en señales fuertes suena distorsionado en la estación receptora.
- El indicador **Compression** muestra 0 dB (sin relleno) cuando **PROC** está apagado o no hay audio presente.

## Solución de problemas

- **El botón PROC no está visible** — El applet está mostrando el panel CW. El panel Phone, incluido **PROC**, aparece solo cuando el slice activo está en un modo de voz, no en CW.
- **El indicador Compression muestra 0 dB con PROC activado** — El radio no está recibiendo audio de la fuente de micrófono seleccionada. Verifique el indicador **Level** y la configuración de **Mic source**. Si **Mic source** es **PC**, el radio siempre informa el nivel de micrófono como 0; utilice en su lugar el indicador **Level** del applet.
- **El control deslizante NOR/DX/DX+ regresa a su posición** — El control deslizante tiene tres posiciones válidas (0, 1, 2). Al arrastrar entre los puntos de encaje, se detiene en el entero más cercano; este es el comportamiento esperado.

## Relacionado

- [Ajustar la ganancia del micrófono y activar la mezcla de accesorio](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md)
