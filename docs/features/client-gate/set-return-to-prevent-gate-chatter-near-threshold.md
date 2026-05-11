# Ajuste de Retorno para evitar el trémolo del puerta cerca del umbral

Cuando los niveles de audio rondan cerca del umbral, la puerta puede abrirse y cerrarse rápidamente, produciendo un efecto de tartamudeo audible llamado trémolo. El mando de Retorno añade una banda muerta de histéresis para que la puerta no se cierre de nuevo hasta que la señal descienda una cantidad determinada por debajo del umbral en el que se abrió.

## Antes de empezar

- La puerta debe estar habilitada en el lado TX o RX. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md) para confirmar que la etapa de puerta está activa.
- Ajuste primero Thresh para tener un punto de referencia estable. Consulte [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md).

## Pasos

1. Abra el subcontenedor **Aetherial TX Gate** (lado TX) o el subcontenedor **Aetherial AGC-G** (lado RX) dentro del contenedor principal Aetherial Audio (TXDSP). Alternativamente, haga doble clic en la etapa GATE en el widget CHAIN para abrir el editor flotante titulado **Aetherial Gate — TX** o **Aetherial Gate — RX**.
2. Localice el mando **Return**.
3. Gire **Return** hacia arriba desde su valor predeterminado de 2.00 dB hasta que el trémolo cese. Empiece con incrementos pequeños — de 3 a 5 dB suele ser suficiente para voz.
4. Observe la curva de transferencia. Aparece una banda vertical cian suave entre (Thresh − Return) y Thresh, mostrando la banda muerta de histéresis. Amplíe o reduzca ajustando **Return** hasta que la banda cubra el rango donde fluctúa su señal.
5. Hable o pase audio a un nivel que anteriormente causaba trémolo. Confirme que la puerta se abre limpiamente y no se vuelve a cerrar hasta que su nivel descienda por debajo del borde inferior de la banda cian.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| **Return** | 2.00 dB | 0.0 a 20.0 dB | `ClientGateTxReturnDb` / `ClientGateRxReturnDb` |
| **Thresh** | −40.0 dB | −80.0 a 0.0 dB | `ClientGateTxThresholdDb` / `ClientGateRxThresholdDb` |

**Return** establece la anchura de la banda muerta de histéresis en decibelios. La puerta se abre cuando la entrada supera Thresh y no se cierra de nuevo hasta que la entrada cae por debajo de Thresh − Return. Establecer Return a 0.0 dB elimina completamente la banda muerta; la puerta se abre y se cierra al mismo nivel, lo que maximiza el riesgo de trémolo cerca del umbral.

La curva de transferencia dibuja una banda vertical cian suave entre (Thresh − Return) y Thresh cuando Return es mayor que 0.0 dB. Esta banda es la zona de adherencia de la puerta — las señales dentro de ella dejan la puerta en el estado en el que ya se encuentre.

## Apariencia cuando está omitida

Cuando la etapa de puerta está omitida, todo el mosaico del applet se atenúa a una opacidad reducida. Esto coincide con el efecto de atenuación utilizado en la curva del ecualizador y proporciona un recordatorio de un vistazo de que la puerta no está procesando audio. Vuelva a habilitar la etapa de puerta para restaurar la opacidad completa y reanudar el procesamiento. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md).

## Consejos

- Si eleva Return tanto que la puerta permanece abierta durante pausas largas en el habla, redúzcalo en pasos pequeños (0.5 dB cada vez) hasta que las pausas cierren la puerta de forma natural.
- Utilice la barra de reducción de ganancia (franja ámbar, escala de 0 a 40 dB) para confirmar que la puerta se cierra durante el silencio real. Si la barra nunca se llena durante una pausa, Return puede ser demasiado ancho en relación con su suelo de ruido real.
- Los cambios en Return surten efecto inmediatamente y se guardan automáticamente. No es necesario reiniciar.

## Solución de problemas

- **El trémolo persiste después de aumentar Return** — Thresh puede estar ajustado demasiado cerca de una señal ruidosa que fluctúa ampliamente. Reduzca Thresh ligeramente para que la puerta se abra solo con el habla clara, luego reajuste Return.
- **La puerta permanece abierta permanentemente** — Return está ajustado más ancho que la diferencia entre su nivel de señal y el suelo de ruido. Reduzca Return hasta que la puerta se cierre de forma fiable durante el silencio.
- **La banda cian no es visible en la curva de transferencia** — Return está ajustado a 0.0 dB. Cualquier valor superior a 0.0 dB mostrará la banda.
- **El mosaico del applet aparece atenuado** — La etapa de puerta está omitida. Habilite la etapa de puerta para restaurar la opacidad completa y el procesamiento activo.

## Relacionados

- [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md)
- [Tune release for natural gate close](tune-release-for-natural-gate-close.md)
- [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
