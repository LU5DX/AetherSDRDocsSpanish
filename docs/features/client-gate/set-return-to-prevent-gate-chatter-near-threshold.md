# Ajustar Return para evitar el traqueteo del puerta cerca del umbral

Cuando los niveles de audio fluctúan cerca del umbral, el puerta puede abrirse y cerrarse rápidamente, produciendo un efecto de traqueteo audible llamado chatter. El mando Return añade una banda muerta de histéresis para que el puerta no se cierre de nuevo hasta que la señal baje una cantidad determinada por debajo del umbral donde se abrió.

## Antes de comenzar

- El puerta debe estar habilitado en el lado TX o RX. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md) para confirmar que la etapa del puerta esté activa.
- Ajuste primero Thresh para tener un punto de referencia estable. Consulte [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md).

## Pasos

1. Abra el subcontenedor **Aetherial TX Gate** (lado TX) o el subcontenedor **Aetherial AGC-T** (lado RX) dentro del contenedor principal Aetherial Audio (TXDSP). Alternativamente, haga doble clic en la etapa GATE en el widget CHAIN para abrir el editor flotante titulado **Aetherial Gate — TX** o **Aetherial Gate — RX**.
2. Localice el mando **Return**.
3. Gire **Return** hacia arriba desde su valor predeterminado de 2.00 dB hasta que el traqueteo se detenga. Comience con incrementos pequeños: de 3 a 5 dB suele ser suficiente para voz.
4. Observe la curva de transferencia. Aparece una banda vertical cian claro entre (Thresh − Return) y Thresh, que muestra la banda muerta de histéresis. Amplíe o reduzca ajustando **Return** hasta que la banda cubra el rango donde fluctúa su señal.
5. Hable o pase audio a un nivel que anteriormente causaba traqueteo. Confirme que el puerta se abre limpiamente y no se vuelve a cerrar hasta que su nivel baje por debajo del borde inferior de la banda cian.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| **Return** | 2.00 dB | 0.0 a 20.0 dB | `ClientGateTxReturnDb` / `ClientGateRxReturnDb` |
| **Thresh** | −40.0 dB | −80.0 a 0.0 dB | `ClientGateTxThresholdDb` / `ClientGateRxThresholdDb` |

**Return** establece la anchura de la banda muerta de histéresis en decibelios. El puerta se abre cuando la entrada supera Thresh y no se cierra de nuevo hasta que la entrada cae por debajo de Thresh − Return. Establecer Return en 0.0 dB elimina por completo la banda muerta; el puerta se abre y se cierra al mismo nivel, lo que maximiza el riesgo de traqueteo cerca del umbral.

La curva de transferencia dibuja una banda vertical cian claro entre (Thresh − Return) y Thresh siempre que Return sea mayor que 0.0 dB. Esta banda es la zona pegajosa del puerta: las señales dentro de ella dejan el puerta en el estado en que ya se encuentre.

## Apariencia cuando está omitido

Cuando la etapa del puerta está omitida, todo el mosaico del applet se atenúa con opacidad reducida. Esto coincide con el efecto de atenuación utilizado en la curva del ecualizador y proporciona un recordatorio visual de que el puerta no está procesando audio. Vuelva a habilitar la etapa del puerta para restaurar la opacidad completa y reanudar el procesamiento. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md).

## Consejos

- Si sube Return tanto que el puerta permanece abierto durante pausas largas en el habla, reduzca en pequeños pasos (0.5 dB a la vez) hasta que las pausas cierren el puerta de forma natural.
- Utilice la barra de reducción de ganancia (franja ámbar, escala de 0 a 40 dB) para confirmar que el puerta se cierra durante el silencio real. Si la barra nunca se llena durante una pausa, Return puede ser demasiado amplio en relación con su suelo de ruido real.
- Los cambios en Return surten efecto de inmediato y se guardan automáticamente. No es necesario reiniciar.

## Solución de problemas

- **El traqueteo persiste después de aumentar Return** — Thresh puede estar ajustado demasiado cerca de una señal ruidosa que fluctúa ampliamente. Baje ligeramente Thresh para que el puerta se abra solo con el habla clara, luego reajuste Return.
- **El puerta permanece abierto permanentemente** — Return es más amplio que la separación entre el nivel de su señal y el suelo de ruido. Reduzca Return hasta que el puerta se cierre de forma fiable durante el silencio.
- **La banda cian no es visible en la curva de transferencia** — Return está establecido en 0.0 dB. Cualquier valor superior a 0.0 dB mostrará la banda.
- **El mosaico del applet aparece atenuado** — La etapa del puerta está omitida. Habilite la etapa del puerta para restaurar la opacidad completa y el procesamiento activo.

## Relacionados

- [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md)
- [Tune release for natural gate close](tune-release-for-natural-gate-close.md)
- [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
