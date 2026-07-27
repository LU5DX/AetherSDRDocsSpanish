# Tiempo de Liberación para el Cierre Natural de la Puerta

El control de **Release** determina la velocidad a la que se cierra la puerta después de que el audio cae por debajo del umbral. Ajustarlo correctamente evita que la puerta corte abruptamente los finales de las palabras o que permanezca abierta tanto tiempo que el ruido de fondo se filtre entre palabras.

## Antes de comenzar

- La etapa de puerta debe estar habilitada en el lado TX o RX. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md) si la puerta está actualmente desviada. Cuando la etapa de puerta está desviada, todo el mosaico del applet se atenúa aproximadamente al 55% de opacidad; esto es normal e indica que la etapa DSP está inactiva.
- Abra el applet de **Aetherial TX Gate** o **Aetherial AGC-G (RX)** para que los controles sean visibles. El applet aparece dentro del contenedor principal de **Aetherial Audio (TXDSP)** una vez que la etapa de puerta está activa.

## Pasos

1. Localice el control **Release** en la fila de cinco controles en la parte inferior del applet. Es el cuarto control desde la izquierda, entre **Return** y **Floor**.
2. Gire **Release** en sentido horario para aumentar el tiempo de liberación (cierre más lento) o en sentido antihorario para disminuirlo (cierre más rápido). La etiqueta del control se actualiza en vivo, mostrando el valor actual en milisegundos — formateado como `X.X ms` por debajo de 100 ms y `X ms` a partir de 100 ms.
3. Hable o pase audio a través de la puerta mientras observa la barra de reducción de ganancia. Después de que el audio caiga por debajo del umbral, observe qué tan rápido la franja ámbar asciende hasta la atenuación completa. Ajuste **Release** hasta que la puerta se cierre suavemente sin recortar los finales de las palabras.
4. Si la puerta se cierra tan lentamente que el ruido es audible entre palabras, reduzca **Release**. Si los finales de las palabras se cortan, aumente **Release**.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| **Thresh** | -40.0 dB | -80.0 a 0.0 dB | `ClientGateTxThresholdDb` / `ClientGateRxThresholdDb` |
| **Ratio** | 2.0 | 1.0 a 10.0 | `ClientGateTxRatio` / `ClientGateRxRatio` |
| **Return** | 2.0 dB | 0.0 a 20.0 dB | `ClientGateTxReturnDb` / `ClientGateRxReturnDb` |
| **Release** | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` / `ClientGateRxReleaseMs` |
| **Floor** | -15.0 dB | -80.0 a 0.0 dB | `ClientGateTxFloorDb` / `ClientGateRxFloorDb` |

El control utiliza un mapeo exponencial (5 × 400^n), por lo que los movimientos pequeños en el extremo inferior del rango producen ajustes de temporización más finos, mientras que el rango superior cubre desvanecimientos largos y graduales. La liberación comienza solo después de que la entrada ha caído por debajo de Thresh − Return; el valor de **Return** por lo tanto afecta cuándo comienza la fase de liberación.

## Visualización de la curva de transferencia

El widget de curva de transferencia traza la curva de transferencia estática del expansor con un punto vivo en el nivel de entrada actual. Una superposición de banda de histéresis en cian suave aparece entre (Thresh − Return) y Thresh, haciendo visible la zona de adherencia. El widget utiliza renderizado en modo compacto cuando el applet está en su estado más pequeño. El widget de curva ahora utiliza los colores del tema activo: el color de la curva utiliza el color de advertencia de acento, y los colores de la cuadrícula, el fondo y las etiquetas siguen la paleta de colores del tema.

## Barra de reducción de ganancia

Una franja horizontal ámbar, llena desde la derecha, muestra la profundidad de la atenuación aplicada. La escala máxima es de 40 dB de reducción de ganancia, con una marca en -15 dB que indica la configuración predeterminada de Floor. La barra se vuelve a dibujar en cada cuadro para mostrar el estado en vivo de forma continua.

## Consejos

- 100 ms (el valor predeterminado) es adecuado para la mayoría del trabajo de voz en TX. Aumente hacia 200–400 ms si las consonantes al final de las palabras se están recortando. Disminuya hacia 20–50 ms si el ruido de fondo es audible en los espacios entre palabras.
- Release interactúa con **Return**: una banda muerta de Return más grande retrasa el inicio de la fase de liberación. Si la puerta parece quedarse abierta, verifique **Return** antes de acortar más **Release**.
- La barra de reducción de ganancia se actualiza en cada cuadro, proporcionando una retroalimentación visual suave y continua mientras la puerta está activa. Obsérvela en tiempo real mientras ajusta **Release** para confirmar la velocidad de cierre antes de transmitir.
- Los cambios surten efecto de inmediato y se guardan automáticamente. No se requiere conexión de radio para ajustar esta configuración.
- Si el mosaico del applet aparece atenuado, la etapa de puerta está desviada y no se está procesando. Vuelva a habilitar la etapa antes de realizar ajustes. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md).
- Para ajustes precisos, haga clic en el texto del valor debajo del control Release para ingresar un valor específico en milisegundos directamente. Esto es útil cuando necesita coincidir con una temporización conocida de otro procesador o guardar una configuración específica para recuperarla más tarde.
- El applet y su widget de curva ahora utilizan los colores del tema activo. Los arcos de los anillos de los controles, los fondos y los mangos se toman del espacio de nombres de color de los controles del tema. El widget de curva utiliza los colores del tema para su fondo, cuadrícula, etiquetas de ejes, línea de identidad y el color de advertencia de acento ámbar para la curva, todo lo cual se actualiza cuando cambia el tema.

## Relacionados

- [Set Return to prevent gate chatter near threshold](set-return-to-prevent-gate-chatter-near-threshold.md)
- [Set Floor to avoid unnatural silence between words](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md)
- [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- Personalice los colores del tema para controles y curvas (si corresponde según su configuración de tema)
