# Ajuste de Release para el cierre natural de la compuerta

El mando **Release** controla la rapidez con que se cierra la compuerta después de que el audio cae por debajo del umbral. Ajustarlo correctamente evita que la compuerta corte abruptamente los finales de las palabras o que permanezca abierta tanto tiempo que el ruido de fondo se filtre entre palabras.

## Antes de comenzar

- La etapa de compuerta debe estar habilitada en el lado TX o RX. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md) si la compuerta está actualmente omitida. Cuando la etapa de compuerta está omitida, todo el mosaico del applet se atenúa a aproximadamente un 55 % de opacidad; esto es normal e indica que la etapa de DSP está inactiva.
- Abra el applet Aetherial TX Gate o Aetherial AGC-G (RX) para que los mandos sean visibles. El applet aparece dentro del contenedor principal Aetherial Audio (TXDSP) una vez que la etapa de compuerta está activa.

## Pasos

1. Localice el mando **Release** en la fila de cinco mandos en la parte inferior del applet. Es el cuarto mando desde la izquierda, entre **Return** y **Floor**.
2. Gire **Release** en el sentido de las agujas del reloj para aumentar el tiempo de liberación (cierre más lento) o en sentido contrario para disminuirlo (cierre más rápido). La etiqueta del mando se actualiza en vivo, mostrando el valor actual en milisegundos, con el formato `X.X ms` por debajo de 100 ms y `X ms` a 100 ms y más.
3. Hable o pase audio a través de la compuerta mientras observa la barra de reducción de ganancia. Después de que el audio caiga por debajo del umbral, observe la rapidez con que la franja ámbar sube hasta la atenuación total. Ajuste **Release** hasta que la compuerta se cierre suavemente sin recortar los finales de las palabras.
4. Si la compuerta se cierra tan lentamente que el ruido es audible entre palabras, reduzca **Release**. Si se recortan los finales de las palabras, aumente **Release**.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| **Release** | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` / `ClientGateRxReleaseMs` |

El mando utiliza un mapeo exponencial (5 × 400^n), por lo que los movimientos pequeños en el extremo inferior del rango producen ajustes de temporización más finos, mientras que el rango superior cubre desvanecimientos largos y graduales. La liberación comienza solo después de que la entrada haya caído por debajo de Thresh − Return; por lo tanto, el valor de **Return** afecta cuándo comienza la fase de liberación.

## Visualización de la curva de transferencia

El widget de curva de transferencia representa la curva de transferencia estática del expansor con un punto vivo en el nivel de entrada actual. Una superposición de banda de histéresis en cian suave aparece entre (Thresh − Return) y Thresh, haciendo visible la zona pegajosa. El widget utiliza un renderizado en modo compacto cuando el applet está en su estado más pequeño, con etiquetas de eje dibujadas usando texto estático en caché para un mejor rendimiento.

## Barra de reducción de ganancia

Una barra horizontal de color ámbar, rellena desde la derecha, muestra la profundidad de la atenuación aplicada. La escala llega hasta 40 dB de reducción de ganancia, con una marca en -15 dB que indica la configuración predeterminada de Floor.

## Edición de valor en línea

Cada mando en la fila de cinco admite entrada numérica directa. Haga clic en el texto del valor debajo de un mando para activar un editor en línea. Escriba un número y presione Enter o haga clic en otro lugar para confirmar el valor. El valor se limita al rango válido del mando. Presione Escape para cancelar la edición y volver al valor anterior. El editor aparece como un recuadro oscuro sutil con un borde cian cuando está enfocado, y coincide con la apariencia de la etiqueta pintada cuando no lo está.

## Consejos

- 100 ms (el valor predeterminado) es adecuado para la mayoría del trabajo de voz en TX. Aumente hacia 200–400 ms si se recortan las consonantes al final de las palabras. Disminuya hacia 20–50 ms si el ruido de fondo es audible en los espacios entre palabras.
- **Release** interactúa con **Return**: una banda muerta de Return más grande retrasa el inicio de la fase de liberación. Si la compuerta parece quedarse abierta, revise **Return** antes de acortar **Release** aún más.
- La barra de reducción de ganancia se actualiza aproximadamente cada 33 ms. Obsérvela en tiempo real mientras ajusta **Release** para confirmar la velocidad de cierre antes de transmitir.
- Los cambios surten efecto de inmediato y se guardan automáticamente. No se requiere conexión de radio para ajustar esta configuración.
- Si el mosaico del applet aparece atenuado, la etapa de compuerta está omitida y no se realiza ningún procesamiento. Rehabilite la etapa antes de hacer ajustes. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md).
- Para ajustes precisos, haga clic en el texto del valor debajo del mando Release para ingresar un valor específico en milisegundos directamente. Esto es útil cuando necesita coincidir con una temporización conocida de otro procesador o guardar una configuración específica para su uso posterior.

## Relacionados

- [Set Return to prevent gate chatter near threshold](set-return-to-prevent-gate-chatter-near-threshold.md)
- [Set Floor to avoid unnatural silence between words](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md)
- [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
