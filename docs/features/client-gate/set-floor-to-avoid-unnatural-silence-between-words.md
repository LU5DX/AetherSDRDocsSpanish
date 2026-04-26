# Ajustar Floor para evitar el silencio antinatural entre palabras

El control **Floor** establece la atenuación máxima que la puerta puede aplicar cuando se cierra. Subir Floor por encima de su valor predeterminado permite que pase una pequeña cantidad de audio durante las pausas, lo que evita el silencio muerto antinatural que produce un corte brusco entre palabras o frases.

## Antes de comenzar

- La puerta de TX debe estar habilitada. El subcontenedor "Aetherial TX Gate" permanece oculto hasta que la etapa Gate esté activa — consulte [Omitir la puerta desde la cadena](bypass-the-gate-from-the-chain.md).
- Abra el subcontenedor "Aetherial TX Gate" dentro del contenedor principal Aetherial Audio (TXDSP), o haga doble clic en la etapa GATE del widget CHAIN para abrir el editor flotante "Aetherial Gate — TX".

## Pasos

1. Localice el control **Floor** — el más a la derecha de los cinco controles situados debajo de la curva de transferencia.
2. Gire **Floor** en sentido horario (hacia 0 dB) para reducir la profundidad de atenuación. La puerta cortará el audio únicamente hasta el valor de Floor cuando se cierre.
3. Observe la barra de reducción de ganancia mientras hace una pausa al hablar. El relleno ámbar debe dejar de crecer en el punto que corresponde a su ajuste de Floor. Una marca en la barra indica −15.0 dB, que es el valor predeterminado.
4. Pronuncie una frase y luego haga una pausa. Ajuste **Floor** hasta que las pausas suenen naturales — presentes pero silenciosas, no completamente mudas.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| Floor | −15.0 dB | −80.0 a 0.0 dB | `ClientGateTxFloorDb` / `ClientGateRxFloorDb` |
| Thresh | −40.0 dB | −80.0 a 0.0 dB | `ClientGateTxThresholdDb` / `ClientGateRxThresholdDb` |
| Ratio | 2.0 | 1.0 a 10.0 | `ClientGateTxRatio` / `ClientGateRxRatio` |
| Attack | 0.5 ms | 0.1 a 100.0 ms | `ClientGateTxAttackMs` / `ClientGateRxAttackMs` |
| Release | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` / `ClientGateRxReleaseMs` |
| Barra de reducción de ganancia | — | 0 a 40 dB GR mostrados | — |

Floor controla la atenuación máxima aplicada cuando la puerta está cerrada. A −80.0 dB la puerta puede cortar casi por completo; a 0 dB no aplica ninguna atenuación, lo que en la práctica omite la acción de reducción de ganancia.

La barra de reducción de ganancia se llena de ámbar desde la derecha. La marca en −15 dB señala la posición predeterminada de Floor. Cuando Floor se ajusta a un valor menos profundo que −15 dB, el relleno ámbar se detendrá antes de la marca durante las pausas normales.

## Consejos

- Un valor de Floor entre −20.0 dB y −10.0 dB es un rango de partida práctico para la mayoría de los micrófonos. Comience con el valor predeterminado −15.0 dB y ajuste a oído.
- Si el ruido ambiental es audible durante las pausas incluso con Floor elevado, baje **Thresh** para que la puerta se cierre solo ante el silencio genuino y luego suba Floor nuevamente para controlar el nivel residual. Consulte [Ajustar el umbral de TX justo por encima del nivel de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md).
- El mismo control Floor y la clave `ClientGateRxFloorDb` existen en el lado RX ("Aetherial AGC-T"). Ajustar Floor allí controla cuánto ruido de banda se permite pasar durante los períodos de silencio en recepción. Consulte [Usar AGC-T en RX para suprimir el ruido de banda por debajo de un nivel elegido](use-agc-t-on-rx-to-suppress-band-noise-below-a-chosen-floor.md).
- Los cambios surten efecto de inmediato y se guardan automáticamente. No se requiere ningún botón Apply ni OK.

## Solución de problemas

- **Las pausas siguen sonando completamente silenciosas después de subir Floor** — confirme que la puerta no esté siendo anulada también por un Ratio muy alto. Un Ratio cercano a 10:1 actúa como una puerta dura independientemente de Floor. Baje Ratio hacia 2.0:1 para un comportamiento más suave. Consulte [Elegir el comportamiento de puerta frente a expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md).
- **El control Floor no tiene efecto** — es posible que la etapa de puerta esté omitida. Verifique el widget CHAIN y vuelva a habilitar la etapa Gate si aparece atenuada. Consulte [Omitir la puerta desde la cadena](bypass-the-gate-from-the-chain.md).
- **La barra de reducción de ganancia se llena por completo durante las pausas a pesar de tener Floor elevado** — la barra muestra la señal de reducción de ganancia en bruto proveniente del motor; si Floor está configurado pero la barra sigue marcando el máximo, verifique que se esté ajustando el lado correcto (TX frente a RX).

## Relacionados

- [Descripción general de Aetherial TX Gate / Aetherial AGC-T (RX)](overview.md)
- [Ajustar el umbral de TX justo por encima del nivel de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md)
- [Elegir el comportamiento de puerta frente a expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Ajustar attack / release para una apertura/cierre natural](tune-attack-release-for-natural-open-close.md)
- [Observar la reducción de ganancia en vivo mientras no se habla](watch-live-gr-while-not-speaking.md)
- [Omitir la puerta desde la cadena](bypass-the-gate-from-the-chain.md)
- [Usar AGC-T en RX para suprimir el ruido de banda por debajo de un nivel elegido](use-agc-t-on-rx-to-suppress-band-noise-below-a-chosen-floor.md)
