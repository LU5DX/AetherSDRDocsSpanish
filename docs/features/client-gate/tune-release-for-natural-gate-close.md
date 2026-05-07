# Soltar para un cierre natural de la puerta

El mando Soltar controla la velocidad con la que la puerta se cierra después de que el audio descienda por debajo del umbral. Ajustarlo correctamente evita que la puerta corte abruptamente los finales de las palabras o que permanezca abierta tanto tiempo que el ruido de fondo se filtre entre palabras.

## Antes de empezar

- La etapa de puerta debe estar habilitada en el lado TX o RX. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md) si la puerta está actualmente omitida. Cuando la etapa de puerta está omitida, todo el mosaico del applet se atenúa aproximadamente al 55 % de opacidad; esto es normal e indica que la etapa de DSP está inactiva.
- Abra el applet Aetherial TX Gate o Aetherial AGC-T para que los mandos sean visibles. El applet aparece dentro del contenedor principal Aetherial Audio (TXDSP) una vez que la etapa de puerta está activa.

## Pasos

1. Localice el mando **Release** en la fila de cinco mandos en la parte inferior del applet. Es el cuarto mando desde la izquierda, entre **Return** y **Floor**.
2. Gire **Release** en el sentido de las agujas del reloj para aumentar el tiempo de soltar (cierre más lento) o en sentido contrario para disminuirlo (cierre más rápido). La etiqueta del mando se actualiza en vivo, mostrando el valor actual en milisegundos, con el formato `X.X ms` por debajo de 100 ms y `X ms` a partir de 100 ms.
3. Hable o pase audio a través de la puerta mientras observa la barra de reducción de ganancia. Después de que el audio descienda por debajo del umbral, observe la rapidez con la que la barra ámbar asciende hasta la atenuación total. Ajuste **Release** hasta que la puerta se cierre suavemente sin recortar los finales de las palabras.
4. Si la puerta se cierra tan lentamente que el ruido es audible entre palabras, reduzca **Release**. Si los finales de las palabras se cortan, aumente **Release**.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| **Release** | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` / `ClientGateRxReleaseMs` |

El mando utiliza un mapeo exponencial (5 × 400^n), por lo que pequeños movimientos en el extremo inferior del rango producen ajustes de temporización más finos, mientras que el rango superior cubre desvanecimientos largos y graduales. Soltar comienza solo después de que la entrada haya caído por debajo de Thresh − Return; por lo tanto, el valor de **Return** afecta cuándo comienza la fase de soltar.

## Consejos

- 100 ms (el valor predeterminado) es adecuado para la mayoría del trabajo de voz TX. Auméntelo a 200–400 ms si las consonantes al final de las palabras se están recortando. Redúzcalo a 20–50 ms si el ruido de fondo es audible en los espacios entre palabras.
- Release interactúa con **Return**: una banda muerta de Return más grande retrasa el inicio de la fase de soltar. Si la puerta parece permanecer abierta, revise **Return** antes de acortar más **Release**.
- La barra de reducción de ganancia se actualiza aproximadamente cada 33 ms. Obsérvela en tiempo real mientras ajusta **Release** para confirmar la velocidad de cierre antes de transmitir.
- Los cambios surten efecto de inmediato y se guardan automáticamente. No se requiere conexión de radio para ajustar esta configuración.
- Si el mosaico del applet aparece atenuado, la etapa de puerta está omitida y no se está realizando procesamiento. Vuelva a habilitar la etapa antes de realizar ajustes. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md).

## Relacionados

- [Set Return to prevent gate chatter near threshold](set-return-to-prevent-gate-chatter-near-threshold.md)
- [Set Floor to avoid unnatural silence between words](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md)
- [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
