# Ajuste del Release para un cierre natural del gate

El control **Release** determina la rapidez con que el gate se cierra después de que el audio cae por debajo del umbral. Configurarlo correctamente evita que el gate corte los finales de las palabras de forma brusca o que permanezca abierto tanto tiempo que el ruido de fondo se filtre entre las palabras.

## Antes de comenzar

- La etapa del gate debe estar habilitada en el lado TX o RX. Consulte [Omitir el gate de la cadena](bypass-the-gate-from-the-chain.md) si el gate está actualmente omitido.
- Abra el applet Aetherial TX Gate o Aetherial AGC-T para que los controles sean visibles. El applet aparece dentro del contenedor principal Aetherial Audio (TXDSP) una vez que la etapa del gate está activa.

## Pasos

1. Ubique el control **Release** en la fila de cinco mandos en la parte inferior del applet. Es el cuarto mando desde la izquierda, entre **Return** y **Floor**.
2. Gire **Release** en sentido horario para aumentar el tiempo de release (cierre más lento) o en sentido antihorario para disminuirlo (cierre más rápido). La etiqueta del mando se actualiza en tiempo real y muestra el valor actual en milisegundos: con formato `X.X ms` por debajo de 100 ms y `X ms` a partir de 100 ms.
3. Hable o haga pasar audio a través del gate mientras observa la barra de reducción de ganancia. Después de que el audio caiga por debajo del umbral, observe la rapidez con que la franja ámbar sube hasta la atenuación máxima. Ajuste **Release** hasta que el gate se cierre de forma suave sin cortar los finales de las palabras.
4. Si el gate se cierra tan lentamente que el ruido es audible entre las palabras, reduzca **Release**. Si los finales de las palabras se cortan, aumente **Release**.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| **Release** | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` / `ClientGateRxReleaseMs` |

El mando usa un mapeo exponencial (5 × 400^n), por lo que los movimientos pequeños en el extremo inferior del rango producen ajustes de tiempo más finos, mientras que el extremo superior cubre cierres largos y graduales. El release comienza solo después de que la entrada ha caído por debajo de Thresh − Return; por lo tanto, el valor de **Return** influye en el momento en que comienza la fase de release.

## Consejos

- 100 ms (el valor predeterminado) es adecuado para la mayoría del trabajo de voz en TX. Aumente hacia 200–400 ms si se están cortando las consonantes al final de las palabras. Disminuya hacia 20–50 ms si el ruido de fondo es audible en las pausas entre palabras.
- El **Release** interactúa con **Return**: una banda muerta de Return mayor retrasa el inicio de la fase de release. Si el gate parece quedarse abierto, verifique **Return** antes de acortar aún más **Release**.
- La barra de reducción de ganancia se actualiza aproximadamente cada 33 ms. Obsérvela en tiempo real mientras ajusta **Release** para confirmar la velocidad de cierre antes de transmitir.
- Los cambios surten efecto de inmediato y se guardan automáticamente. No se requiere conexión con la radio para ajustar esta configuración.

## Relacionados

- [Configurar Return para evitar oscilación del gate cerca del umbral](set-return-to-prevent-gate-chatter-near-threshold.md)
- [Configurar Floor para evitar silencios antinaturales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Observar la reducción de ganancia en vivo sin hablar](watch-live-gr-while-not-speaking.md)
- [Ajustar el umbral de TX justo por encima del nivel de ruido ambiente](set-tx-threshold-just-above-room-noise-floor.md)
- [Elegir el comportamiento de gate o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
