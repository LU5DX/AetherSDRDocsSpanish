# Observar la reducción de ganancia en vivo sin hablar

El medidor de reducción de ganancia y la curva de transferencia se actualizan en tiempo real incluso cuando no está transmitiendo. Observarlos mientras la sala está en silencio le indica qué tan profundo está cortando el compuerta en cualquier momento dado, permitiéndole evaluar si los ajustes de umbral y piso son adecuados antes de activar el micrófono.

## Antes de comenzar

- La etapa de compuerta debe estar habilitada en el lado que desea observar. Consulte [Omitir la compuerta de la cadena](bypass-the-gate-from-the-chain.md) si el applet no está visible.
- El subcontenedor "Aetherial TX Gate" o "Aetherial AGC-G (RX)" debe estar abierto dentro del contenedor padre Aetherial Audio (TXDSP).

## Pasos

1. Abra el panel de applets si no está visible: `View > Applet Panel`.
2. Localice el subcontenedor "Aetherial TX Gate" (lado TX) o "Aetherial AGC-G (RX)" (lado RX).
3. Permanezca en silencio — no hable ni active el micrófono del radio.
4. Observe la barra ámbar de Reducción de ganancia. Mientras la entrada se mantenga por debajo del nivel Thresh, la barra se llena desde la derecha, mostrando la profundidad de atenuación aplicada.
5. Observe la bola de entrada en la curva de Transferencia. La bola se sitúa en la región inferior izquierda de la curva cuando la compuerta está cerrada (entrada por debajo del umbral) y se mueve hacia arriba y a la derecha cuando la compuerta se abre.
6. Observe hasta dónde se llena la barra. Si alcanza o supera la marca de -15 dB, la compuerta está aplicando al menos 15 dB de atenuación — el valor predeterminado de Floor.

## Atenuación al omitir

Cuando la etapa de compuerta está omitida, todo el mosaico del applet se renderiza con opacidad reducida (aproximadamente 55% del brillo completo). Esto coincide con el efecto de atenuación utilizado en la curva de ecualización y proporciona una indicación rápida de que la etapa no está procesando audio. El applet vuelve al brillo completo tan pronto como la etapa se vuelve a habilitar.

## Qué hace cada control

| Control                | Tipo        | Predeterminado | Comportamiento / Notas                                                                                                                                                                                                                         |
|------------------------|-------------|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Curva de transferencia | Indicador   | —               | ClientGateCurveWidget en modo compacto. Traza la curva de transferencia estática del expansor y una bola en vivo en el nivel de entrada actual.                                                                                                  |
| Barra de reducción de ganancia | Medidor     | —               | Franja horizontal ámbar, relleno desde la derecha. La escala máxima es 40 dB (las compuertas pueden cortar muy profundo); una marca en -15 dB señala el piso predeterminado del expansor suave.                                                         |
| Thresh                 | Perilla     | -40.0 dB        | Mapeo lineal. Nivel por debajo del cual la compuerta comienza a atenuar. Rango: -80.0 a 0.0 dB. Clave de configuración: `ClientGateTxThresholdDb`.                                                                                                |
| Ratio                  | Perilla     | 2.0             | Mapeo lineal. Ratios más altos producen un corte más duro, similar a una compuerta; ratios más bajos actúan como un expansor descendente suave. Formato de etiqueta 'X.X:1'. Rango: 1.0 a 10.0. Clave de configuración: `ClientGateTxRatio`.          |
| Return                 | Perilla     | 2.0 dB          | Mapeo lineal (n * 20). Establece la banda muerta de histéresis: la compuerta se abre por encima de Thresh y no se cierra nuevamente hasta que la entrada cae por debajo de Thresh − Return, evitando el aleteo rápido cerca del umbral. Formato de etiqueta 'X.XX dB'. Rango: 0.0 a 20.0 dB. Clave de configuración: `ClientGateTxReturnDb`. |
| Release                | Perilla     | 100 ms          | Mapeo exponencial (5 * 400^n). Define qué tan rápido se cierra la compuerta después de que la entrada cae por debajo de Thresh − Return. Formato de etiqueta 'X.X ms' por debajo de 100, 'X ms' por encima. Rango: 5 a 2000 ms. Clave de configuración: `ClientGateTxReleaseMs`.            |
| Floor                  | Perilla     | -15.0 dB        | Mapeo lineal. Atenuación máxima que la compuerta puede aplicar. Rango: -80.0 a 0.0 dB. Clave de configuración: `ClientGateTxFloorDb`.                                                                                                              |

**Barra de reducción de ganancia:** Franja horizontal ámbar, relleno desde la derecha. La escala máxima es 40 dB. Una marca en -15 dB señala el valor predeterminado de Floor. Vacía significa que no hay atenuación; llena hasta la derecha significa que la compuerta está cortando a la profundidad máxima establecida por Floor.

**Curva de transferencia / Bola de entrada:** La curva estática muestra la relación entrada-salida del expansor. La bola en vivo rastrea el nivel de entrada actual, moviéndose por debajo o por encima del punto de inflexión del umbral en tiempo real. La bola es blanca cuando está por debajo del umbral y verde cuando está por encima.

**Banda de histéresis:** Una banda vertical cian claro dibujada en la curva de transferencia entre (Thresh − Return) y Thresh. Hace visible la zona de retención de la compuerta: la compuerta se abre cuando la entrada supera Thresh y no se cierra nuevamente hasta que la entrada cae por debajo de Thresh − Return. La banda está ausente cuando Return está configurado en 0.

**Perilla Return:** Establece el ancho de la banda muerta de histéresis en dB. Aumentar Return evita que la compuerta aletee cuando la entrada ronda cerca del umbral. La etiqueta se muestra en el formato X.XX dB.

## Comportamiento de actualización de animación

El medidor de reducción de ganancia y la curva de transferencia utilizan un temporizador de animación suave que actualiza la pantalla aproximadamente cada 33 ms. Cuando los niveles de audio están estables (sin cambios en el nivel de entrada), el temporizador de animación se detiene para ahorrar recursos de CPU. La curva de transferencia y la barra de reducción de ganancia se redibujan en cada tic de animación mientras los valores están cambiando, asegurando que no se omitan fotogramas visuales. La barra de reducción de ganancia y el widget de curva siempre renderizan el estado más reciente en cada redibujado, por lo que la pantalla se mantiene receptiva y nunca muestra datos obsoletos.

## Edición de valor en línea

Cada perilla admite la entrada directa de un valor numérico. Haga clic en el texto del valor mostrado debajo de la perilla para activar un editor en el lugar. El editor aparece con un fondo oscuro empotrado y un borde cian para indicar el modo de edición. Escriba un nuevo valor y presione Enter o haga clic en otro lugar para confirmar. El valor se ajusta al rango válido de la perilla al confirmarse.

- El editor acepta formato decimal compatible con la configuración regional (coma o punto como separador decimal).
- Si el texto ingresado no puede interpretarse como un número, el editor se revierte silenciosamente al valor anterior.
- Presione Escape mientras edita para descartar los cambios y volver al valor anterior.
- Mientras el editor está activo, los eventos de la rueda del ratón aún ajustan el valor de la perilla normalmente.
- El editor está disponible de forma independiente tanto en la copia de TX Gate como en la de RX AGC-G.

## Colores del tema

Los componentes de la perilla y el widget de curva de transferencia utilizan colores del tema de los espacios de nombres `color.knob.*` y `color.background.*`. Los elementos de la perilla tienen una anulación de contenedor dedicada `applet/gate` que permite el estilo por applet (por ejemplo, el color de primer plano ámbar de la perilla utilizado en el applet de compuerta). El texto de la etiqueta y el valor debajo de las perillas permanecen en `color.text.secondary` y `color.text.primary` respectivamente, mientras que el fondo, la cuadrícula, las etiquetas de los ejes y la línea de la curva del widget de curva usan `color.background.0`, `color.background.1`, `color.text.label` y `color.accent.warning` (ámbar). Esto garantiza una apariencia consistente con el tema actual sin valores de color codificados.

## Consejos

- El medidor se actualiza aproximadamente cada 33 ms, por lo que la barra sigue la reducción de ganancia lo suficientemente de cerca como para capturar eventos breves de ruido.
- Los cambios de perilla realizados en el editor flotante de Gate se reflejan en el applet dentro del mismo ciclo de sondeo de 33 ms, por lo que puede dejar el applet visible como un medidor en vivo mientras ajusta en el editor.
- Una barra que nunca se vacía por completo mientras está en silencio significa que la compuerta siempre está atenuando — la entrada nunca supera Thresh incluso cuando deja de hablar. Esto es un comportamiento normal y esperado para una compuerta de ruido en reposo.
- Si la compuerta aletea — se abre y cierra rápidamente mientras habla cerca del umbral — aumente Return para ampliar la banda muerta de histéresis. La banda cian en la curva de transferencia se ensancha a medida que lo hace, brindándole una indicación visual de cuánta banda muerta está en efecto.
- Si el mosaico del applet aparece atenuado, la etapa de compuerta está omitida y no hay procesamiento activo. Vuelva a habilitar la etapa para restaurar el brillo completo y reanudar la atenuación.
- Hacer clic en la etiqueta de valor de una perilla proporciona una forma más rápida de establecer un valor exacto en comparación con arrastrar la perilla, especialmente para ajustes finos o valores cercanos a los límites del rango.

## Relacionado

- [Establecer el umbral de TX justo por encima del piso de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md)
- Establecer Floor para evitar silencios antinaturales entre palabras
- [Elegir comportamiento de compuerta vs expansor suave mediante ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Ajustar return/release para apertura/cierre natural](tune-attack-release-for-natural-open-close.md)
- [Omitir la compuerta de la cadena](bypass-the-gate-from-the-chain.md)
