# Activar el procesador de voz en nivel NOR, DX o DX+

Use el applet Phone/CW para activar el procesador de voz y seleccionar cuánta compresión aplica el FLEX-8600 al audio transmitido. NOR es el procesamiento normal, DX añade más compresión y DX+ aplica el máximo.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Phone/CW solo está activo cuando se ha establecido una conexión con la radio.
- El slice activo debe estar en un modo de voz (SSB, AM, FM). El panel Phone no se muestra cuando el slice está en modo CW.

## Pasos

1. Haga clic en el botón de bandeja **P/CW** en la barra lateral derecha para abrir el applet Phone/CW si aún no está visible.
2. Haga clic en **PROC** para activar el procesador de voz. El botón se ilumina en verde cuando está activo.
3. Arrastre el control deslizante **NOR/DX/DX+** hasta la posición que corresponda al nivel de compresión deseado:
   - Posición 0 (izquierda): NOR — procesamiento normal
   - Posición 1 (centro): DX — compresión aumentada
   - Posición 2 (derecha): DX+ — compresión máxima
4. Observe el medidor **Compression** para confirmar la cantidad de compresión que se está aplicando. El medidor se llena de derecha a izquierda y cubre de −25 a 0 dB.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistente |
|---|---|---|---|---|
| **PROC** | Botón de alternancia | Off | On / Off | — |
| **NOR/DX/DX+** | Deslizador | 0 (NOR) | 0 (NOR), 1 (DX), 2 (DX+) | — |
| **Compression** | Medidor (solo lectura) | — | −25 a 0 dB (relleno invertido) | — |
| **Level** | Medidor (solo lectura) | — | −40 a +10 dBFS (rojo por encima de 0) | — |

## Consejos

- El medidor **Compression** muestra la compresión en tiempo real únicamente durante la transmisión. Úselo para verificar que el procesador está actuando y para evitar una compresión excesiva.
- El medidor **Level** muestra el nivel de pico del micrófono en dBFS. Ajuste la ganancia del micrófono antes de modificar el nivel del procesador, de modo que este reciba una señal consistente.
- La posición del deslizador **NOR/DX/DX+** se envía a la radio independientemente de si **PROC** está activado, por lo que puede preseleccionar el nivel antes de activar el procesador.

## Solución de problemas

- **El botón PROC es visible pero el medidor Compression nunca se mueve** — confirme que el slice activo no está en modo CW; el panel Phone cambia automáticamente al panel CW cuando se selecciona un modo CW, ocultando los controles del procesador.
- **El medidor Compression indica 0 dB con PROC activado** — el procesador está activo pero no recibe ninguna señal de entrada. Verifique la selección de **Mic source** y el deslizador **Mic gain**. Si la fuente es PC, tenga en cuenta que la radio siempre reporta nivel de micrófono 0 para la fuente PC; la ganancia se mantiene en el lado del cliente mediante `PcMicGain`.

## Relacionados

- [Ajustar la ganancia del micrófono y activar la mezcla de accesorio](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md)
