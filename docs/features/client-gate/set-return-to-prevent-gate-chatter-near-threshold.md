# Configurar Return para evitar el traqueteo del gate cerca del umbral

Cuando los niveles de audio oscilan cerca del umbral, el gate puede abrirse y cerrarse rápidamente, produciendo un efecto de tartamudeo audible llamado traqueteo (chatter). El mando **Return** añade una banda muerta de histéresis para que el gate no vuelva a cerrarse hasta que la señal caiga una cantidad determinada por debajo del umbral en el que se abrió.

## Antes de comenzar

- El gate debe estar habilitado en el lado TX o RX. Consulte [Omitir el gate desde la cadena](bypass-the-gate-from-the-chain.md) para confirmar que la etapa del gate está activa.
- Ajuste Thresh primero para tener un punto de referencia estable. Consulte [Ajustar el umbral TX justo por encima del piso de ruido de la sala](set-tx-threshold-just-above-room-noise-floor.md).

## Pasos

1. Abra el subcontenedor **Aetherial TX Gate** (lado TX) o el subcontenedor **Aetherial AGC-T** (lado RX) dentro del contenedor principal Aetherial Audio (TXDSP). También puede hacer doble clic en la etapa GATE del widget CHAIN para abrir el editor flotante titulado **Aetherial Gate — TX** o **Aetherial Gate — RX**.
2. Localice el mando **Return**.
3. Gire **Return** hacia arriba desde su valor predeterminado de 2.00 dB hasta que el traqueteo se detenga. Comience con incrementos pequeños — entre 3 y 5 dB suele ser suficiente para voz.
4. Observe la curva de transferencia. Aparece una banda vertical de color cian suave entre (Thresh − Return) y Thresh, que muestra la banda muerta de histéresis. Amplíela o redúzcala ajustando **Return** hasta que la banda cubra el rango en el que fluctúa su señal.
5. Hable o pase audio a un nivel que anteriormente provocara traqueteo. Confirme que el gate se abre de forma limpia y no vuelve a cerrarse hasta que su nivel cae por debajo del borde inferior de la banda cian.

## Qué hace cada control

| Control | Valor por defecto | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| **Return** | 2.00 dB | 0.0 a 20.0 dB | `ClientGateTxReturnDb` / `ClientGateRxReturnDb` |
| **Thresh** | −40.0 dB | −80.0 a 0.0 dB | `ClientGateTxThresholdDb` / `ClientGateRxThresholdDb` |

**Return** establece el ancho de la banda muerta de histéresis en decibelios. El gate se abre cuando la entrada supera Thresh y no vuelve a cerrarse hasta que la entrada cae por debajo de Thresh − Return. Ajustar Return a 0.0 dB elimina la banda muerta por completo; el gate se abre y cierra al mismo nivel, lo que maximiza el riesgo de traqueteo cerca del umbral.

La curva de transferencia dibuja una banda vertical de color cian suave entre (Thresh − Return) y Thresh siempre que Return sea mayor que 0.0 dB. Esta banda es la zona de retención del gate — las señales dentro de ella dejan el gate en el estado en que ya se encuentra.

## Consejos

- Si eleva Return tanto que el gate permanece abierto durante las pausas largas en el habla, redúzcalo en pasos pequeños (0.5 dB a la vez) hasta que las pausas cierren el gate de forma natural.
- Use la barra de reducción de ganancia (franja ámbar, escala de 0 a 40 dB) para confirmar que el gate se cierra durante el silencio real. Si la barra nunca se llena durante una pausa, es posible que Return sea demasiado ancho en relación con su piso de ruido real.
- Los cambios en Return tienen efecto inmediato y se guardan automáticamente. No es necesario reiniciar.

## Solución de problemas

- **El traqueteo persiste después de aumentar Return** — Es posible que Thresh esté ajustado demasiado cerca de una señal ruidosa que fluctúa ampliamente. Baje Thresh ligeramente para que el gate solo se abra con voz clara y luego reajuste Return.
- **El gate permanece abierto permanentemente** — Return está ajustado a un valor mayor que la diferencia entre el nivel de su señal y el piso de ruido. Reduzca Return hasta que el gate se cierre de forma fiable durante el silencio.
- **La banda cian no es visible en la curva de transferencia** — Return está ajustado a 0.0 dB. Cualquier valor por encima de 0.0 dB hará que la banda se muestre.

## Relacionado

- [Ajustar el umbral TX justo por encima del piso de ruido de la sala](set-tx-threshold-just-above-room-noise-floor.md)
- [Ajustar el release para un cierre natural del gate](tune-release-for-natural-gate-close.md)
- [Observar la reducción de ganancia en vivo mientras no se habla](watch-live-gr-while-not-speaking.md)
- [Elegir entre comportamiento de gate o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
