# Ajuste de Release para el cierre natural de la puerta

El mando **Release** controla la rapidez con que se cierra la puerta después de que el audio caiga por debajo del umbral. Ajustarlo correctamente evita que la puerta corte abruptamente los finales de las palabras o que la mantenga abierta tanto tiempo que el ruido de fondo se filtre entre palabras.

## Antes de empezar

- La etapa de puerta debe estar habilitada en el lado TX o RX. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md) si la puerta está actualmente desviada. Cuando la etapa de puerta está desviada, todo el mosaico de la applet se atenúa a aproximadamente un 55% de opacidad; esto es normal e indica que la etapa DSP está inactiva.
- Abra la applet Aetherial TX Gate o Aetherial AGC-G (RX) para que los mandos sean visibles. La applet aparece dentro del contenedor principal Aetherial Audio (TXDSP) una vez que la etapa de puerta está activa.

## Pasos

1. Localice el mando **Release** en la fila de cinco mandos en la parte inferior de la applet. Es el cuarto mando desde la izquierda, entre **Return** y **Floor**.
2. Gire **Release** en el sentido de las agujas del reloj para aumentar el tiempo de liberación (cierre más lento) o en sentido contrario para disminuirlo (cierre más rápido). La etiqueta del mando se actualiza en vivo, mostrando el valor actual en milisegundos, con el formato `X.X ms` por debajo de 100 ms y `X ms` a partir de 100 ms.
3. Hable o pase audio a través de la puerta mientras observa la barra de reducción de ganancia. Después de que el audio caiga por debajo del umbral, observe la rapidez con que la franja ámbar asciende hasta la atenuación total. Ajuste **Release** hasta que la puerta se cierre suavemente sin recortar los finales de las palabras.
4. Si la puerta se cierra tan lentamente que el ruido es audible entre palabras, reduzca **Release**. Si los finales de las palabras se cortan, aumente **Release**.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| **Release** | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` / `ClientGateRxReleaseMs` |

El mando utiliza un mapeo exponencial (5 × 400^n), por lo que pequeños movimientos en el extremo inferior del rango producen ajustes de temporización más finos, mientras que el rango superior cubre desvanecimientos largos y graduales. La liberación comienza solo después de que la entrada haya caído por debajo de Thresh − Return; el valor de **Return** por lo tanto afecta cuándo comienza la fase de liberación.

## Visualización de la curva de transferencia

El widget de curva de transferencia representa la curva de transferencia estática del expansor con una bola en vivo en el nivel de entrada actual. Una superposición de banda de histéresis de color cian suave aparece entre (Thresh − Return) y Thresh, haciendo visible la zona pegajosa. El widget utiliza renderizado en modo compacto cuando la applet está en su estado más pequeño, con las etiquetas de los ejes dibujadas utilizando texto estático en caché para mejorar el rendimiento. Los colores en el widget de curva ahora respetan el tema seleccionado: el color de la curva utiliza el color de advertencia de acento, y los colores de la cuadrícula, fondo y etiquetas siguen la paleta de colores del tema.

## Barra de reducción de ganancia

Una franja horizontal ámbar, rellena desde la derecha, muestra la profundidad de la atenuación aplicada. La escala alcanza un máximo de 40 dB de reducción de ganancia, con una marca en -15 dB que indica la configuración predeterminada de Floor.

## Edición de valor en línea

Cada mando en la fila de cinco mandos admite la entrada numérica directa. Haga clic en el texto del valor debajo de un mando para activar un editor en línea. Escriba un número y presione Enter o haga clic en otro lugar para confirmar el valor. El valor se limita al rango válido del mando. Presione Escape para cancelar la edición y volver al valor anterior. El editor aparece como una inserción oscura sutil con un borde cian cuando está enfocado y coincide con la apariencia de la etiqueta pintada cuando no está enfocado. Los colores de los mandos para el arco del anillo, fondo, manija, etiqueta y texto del valor ahora siguen el espacio de nombres de color designado del tema (`color.knob.*`), con el texto de la etiqueta usando `color.text.secondary` y el texto del valor usando `color.text.primary`.

## Consejos

- 100 ms (el valor predeterminado) es adecuado para la mayoría del trabajo de voz en TX. Aumente hacia 200–400 ms si las consonantes al final de las palabras se están recortando. Disminuya hacia 20–50 ms si el ruido de fondo es audible en los espacios entre palabras.
- Release interactúa con **Return**: una zona muerta de Return más grande retrasa el inicio de la fase de liberación. Si la puerta parece permanecer abierta, verifique **Return** antes de acortar aún más **Release**.
- La barra de reducción de ganancia se actualiza aproximadamente cada 33 ms. La barra se vuelve a pintar continuamente durante la reducción de ganancia activa y deja de repintarse cuando el medidor se ha estabilizado, mejorando el rendimiento. Obsérvela en tiempo real mientras ajusta **Release** para confirmar la velocidad de cierre antes de transmitir.
- Los cambios surten efecto inmediatamente y se guardan automáticamente. No se requiere conexión de radio para ajustar esta configuración.
- Si el mosaico de la applet aparece atenuado, la etapa de puerta está desviada y no se realiza ningún procesamiento. Vuelva a habilitar la etapa antes de realizar ajustes. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md).
- Para ajustes precisos, haga clic en el texto del valor debajo del mando Release para ingresar un valor de milisegundos específico directamente. Esto es útil cuando necesita coincidir con una temporización conocida de otro procesador o guardar una configuración específica para recuperarla más tarde.
- La applet y su widget de curva ahora usan los colores del tema activo. Los arcos del anillo del mando, fondos y manijas se dibujan desde el espacio de nombres de color del mando del tema. El widget de curva utiliza los colores del tema para su fondo, cuadrícula, etiquetas de ejes, línea de identidad y el color de advertencia de acento ámbar para la curva, todo lo cual se actualiza cuando cambia el tema.

## Relacionados

- [Set Return to prevent gate chatter near threshold](set-return-to-prevent-gate-chatter-near-threshold.md)
- [Set Floor to avoid unnatural silence between words](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md)
- [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Customize theme colors for knobs and curves](customize-theme-colors-for-knobs-and-curves.md) (si es aplicable a su configuración de tema)
