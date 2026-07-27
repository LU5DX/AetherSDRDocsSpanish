# Ajustar el Piso para evitar el silencio antinatural entre palabras

Una compuerta completamente cerrada produce un silencio total, que puede sonar antinatural durante las pausas en el habla. El control Piso limita qué tan profundo puede cortar la compuerta, de modo que el audio de fondo se reduce en lugar de eliminarse por completo.

## Antes de comenzar

- La etapa de compuerta de TX o RX debe estar habilitada en el widget CHAIN. El ClientGateApplet permanece oculto hasta que la etapa de compuerta esté activa.
- Abra el subcontenedor **Aetherial TX Gate** (lado TX) dentro del contenedor principal Aetherial Audio (TXDSP), o abra el editor flotante haciendo doble clic en la etapa GATE en el widget CHAIN.

## Pasos

1. Localice el control **Floor** en la fila de cinco perillas en la parte inferior del applet **Aetherial TX Gate**.
2. Gire **Floor** en el sentido de las agujas del reloj para subir el piso (menos atenuación, menos silencio) o en sentido contrario para bajarlo (más atenuación, corte más profundo).
3. Observe la **barra de reducción de ganancia** mientras hace pausas al hablar. El relleno ámbar debe dejar de crecer antes de alcanzar el piso que configuró; la barra no se extenderá más allá del valor de Floor.
4. Hable con normalidad y haga pausas. Confirme que las pausas suenen como fondo reducido, no como silencio absoluto.

**Edición de valor en línea:** Haga clic en el valor mostrado de cualquier perilla para escribir un número preciso directamente. El campo muestra un bestre cian sutil cuando está enfocado. Presione Enter o haga clic en otro lugar para confirmar el valor; presione Escape para cancelar y volver al valor anterior. El desplazamiento con la rueda del ratón sigue funcionando mientras el editor está enfocado.

## Qué hace cada control

| Control                | Valor predeterminado                                                                                                                                                                                         | Rango válido                                                                                                                                                                                                                                                         |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Floor                  | -15.0 dB                                                                                                                                                                                                    | -80.0 a 0.0 dB                                                                                                                                                                                                                                                     |
| Thresh                 | -40.0 dB                                                                                                                                                                                                    | -80.0 a 0.0 dB                                                                                                                                                                                                                                                     |
| Ratio                  | 2.0                                                                                                                                                                                                         | 1.0 a 10.0                                                                                                                                                                                                                                                         |
| Return                 | 2.0 dB                                                                                                                                                                                                      | 0.0 a 20.0 dB                                                                                                                                                                                                                                                      |
| Release                | 100 ms                                                                                                                                                                                                      | 5 a 2000 ms                                                                                                                                                                                                                                                         |
| Barra de reducción de ganancia | —                                                                                                                                                                                                           | 0 a 40 dB GR                                                                                                                                                                                                                                                       |
| Curva de transferencia | —                                                                                                                                                                                                           | —                                                                                                                                                                                                                                                                    |

Para el lado RX, la clave persistida equivalente es `ClientGateRxFloorDb`. El control Floor en el applet **Aetherial AGC-G** funciona de manera idéntica.

## Consejos

- El piso predeterminado de -15.0 dB está marcado por la marca en la barra de reducción de ganancia. Si la atenuación en ese valor aún suena abrupta, intente subir Floor a -10.0 dB o -6.0 dB.
- Floor solo limita el techo de atenuación: no cambia cuándo ni con qué rapidez se abre o cierra la compuerta. Si la compuerta se abre y cierra demasiado bruscamente, ajuste también **Release**. Consulte Ajustar Release para una apertura/cierre natural.
- Si la compuerta oscila (se abre y cierra rápidamente en señales cercanas al umbral), aumente **Return** para ampliar la banda muerta de histéresis. La banda cian en la curva de transferencia se ensancha a medida que Return aumenta, lo que facilita la evaluación visual de la zona de adherencia.
- Configurar Floor en 0.0 dB deshabilita toda atenuación, lo que efectivamente evita el efecto de la compuerta sin desactivarla en la cadena.
- Cuando la etapa Gate está deshabilitada en el widget CHAIN, el mosaico completo del applet se oscurece a aproximadamente la mitad de opacidad. Esto coincide con el efecto de atenuación utilizado en la curva EQ y proporciona una indicación visual rápida de que la etapa está omitida sin necesidad de verificar directamente el widget CHAIN.
- El indicador de **curva de transferencia** muestra la curva de transferencia estática del expansor con un punto móvil en el nivel de entrada actual. Aparece una banda de histéresis vertical cian suave entre (Thresh menos Return) y Thresh cuando Return es mayor que 0 dB, lo que hace visible la zona de adherencia de la compuerta.
- Use la edición de valor en línea para configurar controles con precisión decimal; por ejemplo, escriba `2.5` para Ratio y obtenga una relación de expansión de 2.5:1, o `12.5` para Return y establezca exactamente 12.5 dB de histéresis.
- La **barra de reducción de ganancia** es una franja horizontal ámbar que se llena desde la derecha. Su escala llega hasta 40 dB, con una marca en -15.0 dB que indica el piso predeterminado. La medición se actualiza continuamente para una animación suave: la barra se desliza hasta su posición final sin una parada abrupta.

## Tematización de colores de las perillas

Las perillas en los applets Aetherial TX Gate y Aetherial AGC-G usan colores sensibles al tema definidos en el espacio de nombres `color.knob.*`. Cada componente de la perilla (anillo de fondo, arco de primer plano, indicador de posición, texto de etiqueta y texto de valor) lee su color del tema activo. Cuando el contenedor del applet es `applet/gate`, los colores de las perillas pueden diferir de los de otros contenedores (por ejemplo, el acento ámbar en la curva de transferencia de la compuerta también colorea el arco de primer plano de la perilla).

Si cambia de tema, todos los colores de las perillas se actualizan de inmediato. Para inspeccionar o personalizar los colores de las perillas, consulte las entradas `color.knob.background`, `color.knob.foreground`, `color.knob.handle`, `color.text.primary` y `color.text.secondary` en su archivo de tema.

## Solución de problemas

- **La barra de reducción de ganancia se llena por completo independientemente de Floor**: confirme que está ajustando el control Floor en el lado correcto (TX o RX). Los applets de TX y RX tienen estado completamente independiente y claves persistidas separadas.
- **Las pausas aún suenan completamente silenciosas**: Floor puede estar configurado por debajo de -40.0 dB en la escala, o Ratio es muy alto (cercano a 10:1), lo que hace que la compuerta se comporte como un corte brusco. Suba Floor hacia -15.0 dB y considere bajar Ratio. Consulte [Elegir comportamiento de compuerta vs. expansor suave mediante la relación](choose-gate-vs-soft-expander-behaviour-via-ratio.md).
- **La compuerta oscila cerca del umbral**: Use el control **Return** para agregar histéresis. Aumente Return hasta que la compuerta permanezca abierta durante caídas breves en el nivel de entrada.
- **El mosaico del applet se ve descolorido o atenuado**: la etapa Gate está desactivada en el widget CHAIN. La opacidad reducida (aproximadamente 55 %) es intencional. Habilite la etapa Gate en el widget CHAIN para restaurar el brillo completo y el procesamiento DSP.
- **El editor en línea muestra decimales inesperados**: la pantalla se adapta al formato de etiqueta del control. Por ejemplo, Return muestra dos decimales (X.XX dB), mientras que Floor muestra uno (X.X dB). Los valores escritos se analizan usando la configuración regional de su sistema, por lo que `12,5` funciona en regiones que usan coma como decimal.

## Relacionado

- Ajustar Release para una apertura/cierre natural
- [Elegir comportamiento de compuerta vs. expansor suave mediante la relación](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Observar GR en vivo mientras no habla](watch-live-gr-while-not-speaking.md)
- [Configurar el umbral TX justo por encima del piso de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md)
