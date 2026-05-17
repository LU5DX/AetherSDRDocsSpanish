# Observe la GR en vivo sin hablar

El medidor de reducción de ganancia y la curva de transferencia se actualizan en tiempo real incluso cuando no está transmitiendo. Observarlos mientras la sala está en silencio le indica qué tan profundo está cortando la puerta en cada momento, permitiéndole evaluar si los ajustes de umbral y piso son apropiados antes de activar el micrófono.

## Antes de comenzar

- La etapa Gate debe estar habilitada en el lado que desea observar. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md) si el applet no está visible.
- El subcontenedor "Aetherial TX Gate" o "Aetherial AGC-G (RX)" debe estar abierto dentro del contenedor principal Aetherial Audio (TXDSP).

## Pasos

1. Abra el panel de applets si aún no está visible: `View > Applet Panel`.
2. Localice el subcontenedor "Aetherial TX Gate" (lado TX) o "Aetherial AGC-G (RX)" (lado RX).
3. Permanezca en silencio — no hable ni active el micrófono de la radio.
4. Observe la barra ámbar de reducción de ganancia. Mientras la entrada se mantenga por debajo del nivel Thresh, la barra se llena desde la derecha, mostrando la profundidad de atenuación que se está aplicando.
5. Observe la bola de entrada en la curva de transferencia. La bola se ubica en la región inferior izquierda de la curva cuando la puerta está cerrada (entrada por debajo del umbral) y se mueve hacia arriba y a la derecha cuando la puerta se abre.
6. Note hasta dónde se llena la barra. Si alcanza o supera la marca de -15 dB, la puerta está aplicando al menos 15 dB de atenuación — el valor predeterminado de Floor.

## Atenuación al omitir

Cuando la etapa Gate está desactivada (bypass), todo el mosaico del applet se renderiza con opacidad reducida (aproximadamente 55% del brillo completo). Esto coincide con el efecto de atenuación utilizado en la curva EQ y proporciona una indicación rápida de que la etapa no está procesando audio. El applet vuelve al brillo completo tan pronto como se vuelve a habilitar la etapa.

## Función de cada control

| Control                | Tipo       | Predeterminado | Comportamiento / Notas                                                                                                                                                                                                                             |
|------------------------|------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Curva de transferencia | Indicador  | —              | ClientGateCurveWidget en modo compacto. Traza la curva de transferencia estática del expansor y una bola en vivo en el nivel de entrada actual.                                                                                                     |
| Barra de reducción de ganancia | Medidor | —          | Franja ámbar horizontal que se llena desde la derecha. La escala máxima es de 40 dB (las puertas pueden cortar muy profundo); una marca en -15 dB indica el piso predeterminado del expansor suave.                                                  |
| Thresh                 | Perilla    | -40.0 dB       | Mapeo lineal. Nivel por debajo del cual la puerta comienza a atenuar. Rango: -80.0 a 0.0 dB.                                                                                                                                                       |
| Ratio                  | Perilla    | 2.0           | Mapeo lineal. Las relaciones más altas producen un corte más duro, similar a una puerta; las relaciones más bajas actúan como un expansor de reducción suave. Formato de etiqueta 'X.X:1'. Rango: 1.0 a 10.0.                                          |
| Return                 | Perilla    | 2.0 dB        | Mapeo lineal (n * 20). Establece la banda muerta de histéresis: la puerta se abre por encima de Thresh y no se cierra nuevamente hasta que la entrada cae por debajo de Thresh − Return, evitando el rechinido rápido cerca del umbral. Formato de etiqueta 'X.XX dB'. Rango: 0.0 a 20.0 dB. |
| Release                | Perilla    | 100 ms        | Mapeo exponencial (5 * 400^n). Define qué tan rápido se cierra la puerta después de que la entrada cae por debajo de Thresh − Return. Formato de etiqueta 'X.X ms' por debajo de 100, 'X ms' por encima. Rango: 5 a 2000 ms.                          |
| Floor                  | Perilla    | -15.0 dB      | Mapeo lineal. Atenuación máxima que la puerta puede aplicar. Rango: -80.0 a 0.0 dB.                                                                                                                                                                |

**Barra de reducción de ganancia:** Franja ámbar horizontal que se llena desde la derecha. La escala máxima es de 40 dB. Una marca en -15 dB indica el valor predeterminado de Floor. Vacía significa que no hay atenuación; llena completamente hacia la derecha significa que la puerta está cortando a la profundidad máxima establecida por Floor.

**Curva de transferencia / Bola de entrada:** La curva estática muestra la relación entrada-salida del expansor. La bola en vivo rastrea el nivel de entrada actual, moviéndose por debajo o por encima de la rodilla del umbral en tiempo real. La bola es blanca cuando está por debajo del umbral y verde cuando está por encima del umbral.

**Banda de histéresis:** Una banda vertical cian suave dibujada en la curva de transferencia entre (Thresh − Return) y Thresh. Hace visible la zona de bloqueo de la puerta: la puerta se abre cuando la entrada supera Thresh y no se cierra nuevamente hasta que la entrada cae por debajo de Thresh − Return. La banda está ausente cuando Return está configurado en 0.

**Perilla Return:** Establece el ancho de la banda muerta de histéresis en dB. Aumentar Return evita que la puerta rechine cuando la entrada se acerca al umbral. La etiqueta se muestra en el formato X.XX dB.

## Edición de valor en línea

Cada perilla admite la entrada directa de un valor numérico. Haga clic en el texto del valor mostrado debajo de la perilla para activar un editor en el lugar. El editor aparece con un fondo oscuro empotrado y un borde cian para indicar el modo de edición. Escriba un nuevo valor y presione Enter o haga clic en otro lugar para confirmar. El valor se ajusta al rango válido de la perilla al confirmarlo.

- El editor acepta formato decimal según la configuración regional (coma o punto como separador decimal).
- Si el texto ingresado no puede interpretarse como un número, el editor vuelve silenciosamente al valor anterior.
- Presione Escape mientras edita para descartar los cambios y volver al valor anterior.
- Mientras el editor está activo, los eventos de la rueda del ratón aún ajustan el valor de la perilla normalmente.
- El editor está disponible independientemente en las copias de Gate TX y AGC-G RX.

## Consejos

- El medidor se actualiza aproximadamente cada 33 ms, por lo que la barra sigue la reducción de ganancia con suficiente precisión para capturar eventos breves de ruido.
- Los cambios de perilla realizados en el editor flotante de Gate se reflejan en el applet dentro del mismo ciclo de sondeo de 33 ms, por lo que puede dejar el applet visible como un medidor en vivo mientras ajusta en el editor.
- Una barra que nunca se vacía completamente mientras está en silencio significa que la puerta siempre está atenuando — la entrada nunca supera Thresh incluso cuando deja de hablar. Esto es un comportamiento normal y esperado para una puerta de ruido en reposo.
- Si la puerta rechinea — se abre y cierra rápidamente mientras habla cerca del umbral — aumente Return para ampliar la banda muerta de histéresis. La banda cian en la curva de transferencia se vuelve más ancha a medida que lo hace, dándole una indicación visual de cuánta banda muerta está activa.
- Si el mosaico del applet aparece atenuado, la etapa Gate está omitida y no hay procesamiento activo. Vuelva a habilitar la etapa para restaurar el brillo completo y reanudar la atenuación.
- Hacer clic en la etiqueta de valor de una perilla proporciona una forma más rápida de establecer un valor exacto en comparación con arrastrar la perilla, especialmente para ajustes finos o valores cercanos a los límites del rango.

## Relacionados

- [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md)
- [Set Floor to avoid unnatural silence between words](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Tune return / release for natural open/close](tune-attack-release-for-natural-open-close.md)
- [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md)
