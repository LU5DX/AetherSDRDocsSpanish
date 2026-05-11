# Liberación para el Cierre Natural del Gate

El mando **Release** controla la rapidez con la que el gate se cierra después de que el audio caiga por debajo del umbral. Ajustarlo correctamente evita que el gate corte los finales de las palabras de forma abrupta o que lo deje abierto tanto tiempo que el ruido de fondo se filtre entre palabras.

## Antes de comenzar

- La etapa del gate debe estar habilitada en el lado TX o RX. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md) si el gate está actualmente en bypass. Cuando la etapa del gate está en bypass, todo el mosaico del applet se atenúa aproximadamente al 55 % de opacidad; esto es normal e indica que la etapa DSP está inactiva.
- Abra el applet **Aetherial TX Gate** o **Aetherial AGC-G (RX)** para que los mandos sean visibles. El applet aparece dentro del contenedador principal **Aetherial Audio (TXDSP)** una vez que la etapa del gate está activa.

## Pasos

1. Localice el mando **Release** en la fila de cinco mandos en la parte inferior del applet. Es el cuarto mando desde la izquierda, entre **Return** y **Floor**.
2. Gire **Release** en sentido horario para aumentar el tiempo de liberación (cierre más lento) o en sentido antihorario para disminuirlo (cierre más rápido). La etiqueta del mando se actualiza en vivo, mostrando el valor actual en milisegundos — con formato `X.X ms` por debajo de 100 ms y `X ms` a partir de 100 ms.
3. Hable o pase audio a través del gate mientras observa la barra de reducción de ganancia. Después de que el audio caiga por debajo del umbral, observe la rapidez con la que la franja ámbar asciende hasta la atenuación total. Ajuste **Release** hasta que el gate se cierre de forma suave sin recortar los finales de las palabras.
4. Si el gate se cierra tan lentamente que el ruido se vuelve audible entre palabras, reduzca **Release**. Si los finales de las palabras se cortan, aumente **Release**.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| **Release** | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` / `ClientGateRxReleaseMs` |

El mando utiliza un mapeo exponencial (5 × 400^n), por lo que los movimientos pequeños en el extremo inferior del rango producen ajustes de temporización más precisos, mientras que el rango superior cubre desvanecimientos largos y graduales. La liberación comienza solo después de que la entrada haya caído por debajo de Thresh − Return; el valor de **Return** por lo tanto afecta cuándo comienza la fase de liberación.

## Visualización de la curva de transferencia

El widget de la curva de transferencia representa la curva de transferencia estática del expansor con un punto móvil en el nivel de entrada actual. Una superposición de banda de histéresis de color cian suave aparece entre (Thresh − Return) y Thresh, haciendo visible la zona pegajosa. El widget utiliza el modo de renderizado compacto cuando el applet está en su estado más pequeño, con las etiquetas de los ejes dibujadas usando texto estático en caché para mejorar el rendimiento.

## Barra de reducción de ganancia

Una franja horizontal de color ámbar, llena desde la derecha, muestra la profundidad de la atenuación aplicada. La escala alcanza un máximo de 40 dB de reducción de ganancia, con una marca a -15 dB que indica la configuración predeterminada de **Floor**.

## Consejos

- 100 ms (el valor predeterminado) es adecuado para la mayoría del trabajo de voz en TX. Auméntelo hacia 200–400 ms si las consonantes al final de las palabras se están recortando. Redúzcalo hacia 20–50 ms si el ruido de fondo es audible en los espacios entre palabras.
- **Release** interactúa con **Return**: una banda muerta de **Return** más grande retrasa el inicio de la fase de liberación. Si el gate parece quedarse abierto, verifique **Return** antes de acortar aún más **Release**.
- La barra de reducción de ganancia se actualiza aproximadamente cada 33 ms. Obsérvela en tiempo real mientras ajusta **Release** para confirmar la velocidad de cierre antes de transmitir.
- Los cambios surten efecto inmediatamente y se guardan automáticamente. No se requiere conexión de radio para ajustar esta configuración.
- Si el mosaico del applet aparece atenuado, la etapa del gate está en bypass y no se está procesando. Rehabilite la etapa antes de realizar ajustes. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md).

## Relacionados

- [Set Return to prevent gate chatter near threshold](set-return-to-prevent-gate-chatter-near-threshold.md)
- [Set Floor to avoid unnatural silence between words](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md)
- [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
