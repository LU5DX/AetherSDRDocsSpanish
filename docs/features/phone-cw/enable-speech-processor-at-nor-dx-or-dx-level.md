# Activar el procesador de voz en nivel NOR, DX o DX+

Use el applet Phone/CW para activar el procesador de voz y elegir con qué intensidad comprime el audio de transmisión. Los niveles más altos aumentan la potencia promedio en los picos de voz, lo que puede mejorar la legibilidad en condiciones difíciles.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Phone/CW solo está activo con una conexión de radio.
- El slice activo debe estar en un modo de voz (SSB, AM, FM). En modo CW, el applet cambia al panel CW y los controles del procesador no se muestran.

## Pasos

1. Localice el applet Phone/CW en el Panel de Applets (barra lateral derecha). Si no está visible, haga clic en el botón de bandeja **P/CW** de la barra lateral derecha para mostrarlo.
2. En la fila que contiene **PROC**, haga clic en **PROC** para activar el procesador de voz. El botón se ilumina en verde cuando está activo.
3. Mueva el control deslizante **NOR/DX/DX+** al nivel deseado:
   - Posición 0 (izquierda): **NOR** — compresión normal
   - Posición 1 (centro): **DX** — compresión moderada
   - Posición 2 (derecha): **DX+** — compresión máxima
4. Observe el indicador **Compression** para confirmar que el procesador está aplicando compresión. El indicador se llena de derecha a izquierda; una lectura más hacia la izquierda indica mayor compresión.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistente |
|---|---|---|---|---|
| **PROC** | Botón alternante | Desactivado | Activado / Desactivado | — |
| **NOR/DX/DX+** | Deslizador | 0 (NOR) | 0 (NOR), 1 (DX), 2 (DX+) | — |
| **Compression** | Medidor (solo lectura) | — | −25 a 0 dB (relleno invertido) | — |
| **Level** | Medidor (solo lectura) | — | −40 a +10 dBFS (rojo por encima de 0) | — |

## Consejos

- El indicador **Compression** usa relleno invertido: la barra crece de derecha a izquierda a medida que aumenta la compresión. Una barra que alcanza el borde izquierdo indica limitación intensa.
- El indicador **Level** muestra el pico del micrófono en dBFS. Mantenga los picos por debajo de 0 dBFS (la zona roja comienza por encima de 0) antes de activar una compresión elevada; operar el procesador con una señal de entrada sobrecargada produce distorsión en lugar de mayor potencia promedio de audio.
- Si **Mic source** está configurado en **PC**, el valor de ganancia del micrófono se almacena en el cliente como `PcMicGain` (valor predeterminado 50, rango 0–100) porque el radio siempre reporta un nivel de 0 para esa fuente. Ajuste **Mic gain** antes de aumentar el nivel del procesador para establecer una entrada limpia.

## Solución de problemas

- **El botón PROC no está visible** — El slice activo está en modo CW. Cambie el slice a un modo de voz; el applet mostrará el panel Phone.
- **El indicador Compression muestra 0 dB con PROC activado** — El procesador está habilitado pero recibe poca señal de entrada o ninguna. Confirme que **Mic source** y **Mic gain** estén configurados correctamente y que el radio esté transmitiendo.
- **No hay cambio en la calidad de la señal entre NOR, DX y DX+** — Verifique que PROC esté activado (iluminado en verde). Mover el control deslizante **NOR/DX/DX+** no tiene efecto cuando PROC está desactivado.

## Relacionados

- [Descripción general de Phone/CW](overview.md)
- [Ajustar la ganancia del micrófono y activar la mezcla de accesorio](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
