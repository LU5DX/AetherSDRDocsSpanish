# Activar el procesador de voz en nivel NOR, DX o DX+

Use el procesador de voz para aplicar compresión al audio transmitido. Hay tres niveles disponibles: NOR (normal), DX (compresión moderada) y DX+ (compresión máxima).

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Phone/CW solo está activo cuando se establece una conexión con el radio.
- El slice activo debe estar en un modo de voz (SSB, AM, FM). El panel Phone se oculta cuando el slice está en modo CW.

## Pasos

1. Abra el applet Phone/CW. Si el panel Phone no está visible en el panel de applets, haga clic en el botón de bandeja **P/CW** en la barra lateral derecha.
2. Haga clic en **PROC** para activar el procesador de voz. El botón se ilumina en verde cuando está activo.
3. Arrastre el control deslizante **NOR/DX/DX+** para seleccionar el nivel del procesador:
   - Posición 0: **NOR** — normal, compresión ligera.
   - Posición 1: **DX** — compresión moderada.
   - Posición 2: **DX+** — compresión máxima.
4. Observe el medidor **Compression** para confirmar que el procesador está aplicando reducción de ganancia. El medidor se llena de derecha a izquierda; una lectura entre −25 dB y 0 dB indica compresión activa.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Ajuste persistente |
|---|---|---|---|---|
| **PROC** | Botón de alternancia | Desactivado | Activado / Desactivado | — |
| **NOR/DX/DX+** | Deslizador | 0 (NOR) | 0 (NOR), 1 (DX), 2 (DX+) | — |
| **Compression** | Medidor (solo lectura) | — | −25 a 0 dB (relleno invertido) | — |

## Consejos

- El medidor **Compression** solo muestra lecturas significativas mientras está transmitiendo. En otros momentos, la lectura estará cerca de 0 dB.
- Aumentar el deslizador **NOR/DX/DX+** sin activar **PROC** no tiene ningún efecto. Active **PROC** primero.
- Ajuste la ganancia de micrófono (**Mic gain**) antes de aumentar el nivel del procesador. Una ganancia de micrófono excesiva en el procesador puede producir distorsión. El medidor **Level** muestra el nivel pico del micrófono en dBFS; procure mantener los picos por debajo de 0 dBFS (zona roja) en los picos de voz.

## Solución de problemas

- **El medidor Compression no muestra actividad mientras transmite** — Confirme que **PROC** esté activado (el botón está iluminado). Si la fuente de micrófono es **PC**, verifique que el valor de `PcMicGain` no esté en 0; el radio no reporta el nivel de micrófono para la fuente PC, por lo que el valor del deslizador se mantiene solo en el cliente.
- **El botón PROC no está visible** — El panel Phone solo se muestra cuando el slice activo está en un modo de voz. Si el slice está en modo CW, se muestra el panel CW en su lugar. Cambie el slice a SSB, AM o FM para acceder a PROC.

## Relacionados

- [Ajustar la ganancia de micrófono y activar la mezcla de accesorio](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Escuchar un monitor de tono lateral de TX](listen-to-a-tx-sidetone-monitor.md)
