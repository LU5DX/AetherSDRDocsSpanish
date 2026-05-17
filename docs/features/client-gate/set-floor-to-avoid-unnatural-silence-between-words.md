# Ajustar el Piso para evitar silencios antinaturales entre palabras

Una compuerta completamente cerrada genera silencio total, lo que puede sonar antinatural durante las pausas en el habla. El mando **Floor** (Piso) limita la profundidad con la que la compuerta puede cortar, de modo que el audio de fondo se reduce en lugar de eliminarse por completo.

## Antes de empezar

- La etapa TX Gate o RX Gate debe estar habilitada en el widget CHAIN. El ClientGateApplet permanece oculto hasta que la etapa Gate esté activa.
- Abra el subcontenedor **Aetherial TX Gate** (lado TX) dentro del contenedor principal Aetherial Audio (TXDSP), o abra el editor flotante haciendo doble clic en la etapa GATE del widget CHAIN.

## Pasos

1. Localice el mando **Floor** en la fila de cinco mandos en la parte inferior del applet **Aetherial TX Gate**.
2. Gire **Floor** en el sentido de las agujas del reloj para elevar el piso (menos atenuación, menos silencio) o en sentido contrario para bajarlo (más atenuación, corte más profundo).
3. Observe la **barra de reducción de ganancia** mientras hace una pausa al hablar. El relleno ámbar debe dejar de crecer antes de alcanzar el piso que configuró; la barra no se extenderá más allá del valor de Floor.
4. Hable con normalidad y haga una pausa. Confirme que las pausas suenan como fondo reducido, no como silencio absoluto.

**Edición de valor en línea:** Haga clic en el valor mostrado de cualquier mando para escribir un número preciso directamente. El campo muestra un borde cian tenue cuando está enfocado. Presione Enter o haga clic en otro lugar para confirmar el valor; presione Escape para cancelar y revertir al valor anterior. El desplazamiento con la rueda del ratón sigue funcionando mientras el editor está enfocado.

## Función de cada control

| Control               | Valor predeterminado                                                                                                                                                                                        | Rango válido                                                                                                                                                                                                                                                         |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Floor                 | -15.0 dB                                                                                                                                                                                                    | -80.0 a 0.0 dB                                                                                                                                                                                                                                                      |
| Thresh                | -40.0 dB                                                                                                                                                                                                    | -80.0 a 0.0 dB                                                                                                                                                                                                                                                      |
| Ratio                 | 2.0                                                                                                                                                                                                         | 1.0 a 10.0                                                                                                                                                                                                                                                          |
| Return                | 2.0 dB                                                                                                                                                                                                      | 0.0 a 20.0 dB                                                                                                                                                                                                                                                       |
| Release               | 100 ms                                                                                                                                                                                                      | 5 a 2000 ms                                                                                                                                                                                                                                                          |
| Barra de reducción de ganancia | —                                                                                                                                                                                                           | 0 a 40 dB GR                                                                                                                                                                                                                                                        |
| Curva de transferencia | —                                                                                                                                                                                                           | —                                                                                                                                                                                                                                                                    |

Para el lado RX, la clave persistida equivalente es `ClientGateRxFloorDb`. El mando Floor en el applet **Aetherial AGC-G** funciona de forma idéntica.

## Consejos

- El valor predeterminado de Floor de -15.0 dB está marcado por la marca en la barra de reducción de ganancia. Si la atenuación en ese valor aún suena abrupta, intente elevar Floor a -10.0 dB o -6.0 dB.
- Floor solo limita el techo de atenuación; no cambia cuándo ni con qué rapidez se abre o cierra la compuerta. Si la compuerta se abre y cierra demasiado bruscamente, ajuste también **Release**. Consulte [Ajustar Release para apertura/cierre natural](tune-release-for-natural-open-close.md).
- Si la compuerta vibra (se abre y cierra rápidamente con señales cercanas al umbral), aumente **Return** para ampliar la banda muerta de histéresis. La banda cian en la curva de transferencia se ensancha a medida que Return aumenta, lo que facilita la evaluación visual de la zona de retención.
- Establecer Floor en 0.0 dB desactiva toda atenuación, lo que efectivamente anula el efecto de la compuerta sin deshabilitarla en la cadena.
- Cuando la etapa Gate está deshabilitada en el widget CHAIN, todo el mosaico del applet se atenúa aproximadamente a la mitad de su opacidad. Esto coincide con el efecto de atenuación utilizado en la curva EQ y proporciona una indicación visual rápida de que la etapa está omitida, sin necesidad de verificar directamente el widget CHAIN.
- El indicador **Transfer curve** muestra la curva de transferencia estática del expansor con un punto móvil en el nivel de entrada actual. Una banda de histéresis vertical cian suave aparece entre (Thresh menos Return) y Thresh cuando Return es mayor que 0 dB, lo que hace visible la zona de retención de la compuerta.
- Utilice la edición de valor en línea para establecer controles con precisión decimal; por ejemplo, escriba `2.5` para Ratio y obtenga una relación de expansión de 2.5:1, o `12.5` para Return y establezca exactamente 12.5 dB de histéresis.

## Solución de problemas

- **La barra de reducción de ganancia se llena completamente independientemente de Floor**: confirme que está ajustando el mando Floor en el lado correcto (TX o RX). Los applets TX y RX tienen estado completamente independiente y claves persistentes separadas.
- **Las pausas aún suenan completamente silenciosas**: es posible que Floor esté configurado por debajo de -40.0 dB en la escala, o que Ratio sea muy alto (cercano a 10:1), lo que hace que la compuerta se comporte como un corte brusco. Eleve Floor hacia -15.0 dB y considere reducir Ratio. Consulte [Elegir comportamiento de compuerta vs. expansor suave mediante Ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md).
- **La compuerta vibra cerca del umbral**: use el mando **Return** para agregar histéresis. Aumente Return hasta que la compuerta permanezca abierta durante caídas breves en el nivel de entrada.
- **El mosaico del applet se ve descolorido o atenuado**: la etapa Gate está omitida en el widget CHAIN. La opacidad reducida (aproximadamente 55%) es intencional. Habilite la etapa Gate en el widget CHAIN para restaurar el brillo completo y el procesamiento DSP.
- **El editor en línea muestra decimales inesperados**: la pantalla se adapta al formato de etiqueta del control. Por ejemplo, Return muestra dos decimales (X.XX dB), mientras que Floor muestra uno (X.X dB). Los valores escritos se analizan utilizando la configuración regional de su sistema, por lo que `12,5` funciona en regiones con coma decimal.

## Relacionados

- [Ajustar Release para apertura/cierre natural](tune-release-for-natural-open-close.md)
- [Elegir comportamiento de compuerta vs. expansor suave mediante Ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Observar GR en vivo sin hablar](watch-live-gr-while-not-speaking.md)
- [Establecer umbral TX justo por encima del piso de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md)
