# Configurar el Floor para evitar silencios antinaturales entre palabras

Una puerta completamente cerrada produce silencio total, lo que puede sonar antinatural durante las pausas en el habla. El mando Floor limita la profundidad del corte de la puerta, de modo que el audio de fondo se reduce en lugar de eliminarse por completo.

## Antes de comenzar

- La etapa TX Gate o RX Gate debe estar habilitada en el widget CHAIN. El ClientGateApplet permanece oculto hasta que la etapa Gate esté activa.
- Abra el subcontenedor **Aetherial TX Gate** (lado TX) dentro del contenedor padre Aetherial Audio (TXDSP), o abra el editor flotante haciendo doble clic en la etapa GATE en el widget CHAIN.

## Pasos

1. Localice el mando **Floor** en la fila de cinco mandos en la parte inferior del applet **Aetherial TX Gate**.
2. Gire **Floor** en el sentido de las agujas del reloj para elevar el piso (menos atenuación, menos silencio) o en sentido contrario para bajarlo (más atenuación, corte más profundo).
3. Observe la **barra de reducción de ganancia** mientras hace pausas al hablar. El relleno ámbar debe dejar de crecer antes de alcanzar el piso que configuró; la barra no se extenderá más allá del valor de Floor.
4. Hable con normalidad y haga pausas. Confirme que las pausas suenan como un fondo reducido y no como silencio absoluto.

**Edición inline del valor:** Haga clic en el valor mostrado de cualquier mando para escribir un número preciso directamente. El campo muestra un borde cian sutil cuando está enfocado. Presione Enter o haga clic en otro lugar para confirmar el valor; presione Escape para cancelar y volver al valor anterior. El desplazamiento con la rueda del ratón sigue funcionando mientras el editor está enfocado.

## Qué hace cada control

| Control                | Valor predeterminado                                                                                                                                                                                        | Rango válido                                                                                                                                                                                                                                                         |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Floor                  | -15.0 dB                                                                                                                                                                                                    | -80.0 a 0.0 dB                                                                                                                                                                                                                                                       |
| Thresh                 | -40.0 dB                                                                                                                                                                                                    | -80.0 a 0.0 dB                                                                                                                                                                                                                                                       |
| Ratio                  | 2.0                                                                                                                                                                                                         | 1.0 a 10.0                                                                                                                                                                                                                                                           |
| Return                 | 2.0 dB                                                                                                                                                                                                      | 0.0 a 20.0 dB                                                                                                                                                                                                                                                        |
| Release                | 100 ms                                                                                                                                                                                                      | 5 a 2000 ms                                                                                                                                                                                                                                                           |
| Barra de reducción de ganancia | —                                                                                                                                                                                                           | 0 a 40 dB GR                                                                                                                                                                                                                                                         |
| Curva de transferencia | —                                                                                                                                                                                                           | —                                                                                                                                                                                                                                                                    |

Para el lado RX, la clave persistida equivalente es `ClientGateRxFloorDb`. El mando Floor en el applet **Aetherial AGC-G** funciona de manera idéntica.

## Consejos

- El Floor predeterminado de -15.0 dB está marcado por la marca en la barra de reducción de ganancia. Si la atenuación en ese valor aún suena abrupta, intente elevar Floor a -10.0 dB o -6.0 dB.
- Floor solo limita el techo de atenuación; no cambia cuándo ni qué tan rápido se abre o cierra la puerta. Si la puerta se abre y cierra de forma demasiado abrupta, también ajuste **Release**. Consulte Ajustar release para una apertura/cierre natural.
- Si la puerta vibra — abriéndose y cerrándose rápidamente en señales cercanas al umbral — aumente **Return** para ampliar la banda muerta de histéresis. La banda cian en la curva de transferencia se ensancha a medida que Return aumenta, lo que facilita la evaluación visual de la zona pegajosa.
- Configurar Floor en 0.0 dB deshabilita toda atenuación, lo que efectivamente evita el efecto de la puerta sin desactivarla en la cadena.
- Cuando la etapa Gate está deshabilitada en el widget CHAIN, el mosaico completo del applet se atenúa aproximadamente a la mitad de opacidad. Esto coincide con el efecto de atenuación utilizado en la curva EQ y proporciona una indicación visual rápida de que la etapa está omitida sin necesidad de verificar directamente el widget CHAIN.
- El indicador **Curva de transferencia** muestra la curva de transferencia estática del expansor con un punto móvil en el nivel de entrada actual. Aparece una banda de histéresis vertical cian suave entre (Thresh menos Return) y Thresh cuando Return es mayor que 0 dB, haciendo visible la zona pegajosa de la puerta.
- Utilice la edición inline del valor para configurar controles con precisión decimal — por ejemplo, escriba `2.5` para Ratio y obtenga una relación de expansión de 2.5:1, o `12.5` para Return y establezca exactamente 12.5 dB de histéresis.

## Tematización de colores de los mandos

Los mandos en los applets Aetherial TX Gate y Aetherial AGC-G utilizan colores conscientes del tema definidos en el espacio de nombres `color.knob.*`. Cada componente del mando — anillo de fondo, arco de primer plano, puntero de la manija, texto de la etiqueta y texto del valor — lee su color del tema activo. Cuando el contenedor del applet es `applet/gate`, los colores de los mandos pueden diferir de los de otros contenedores (por ejemplo, el acento ámbar en la curva de transferencia de la puerta también colorea el arco de primer plano del mando).

Si cambia de tema, todos los colores de los mandos se actualizan de inmediato. Para inspeccionar o personalizar los colores de los mandos, consulte las entradas `color.knob.background`, `color.knob.foreground`, `color.knob.handle`, `color.text.primary` y `color.text.secondary` de su archivo de tema.

## Solución de problemas

- **La barra de reducción de ganancia se llena completamente independientemente del Floor** — confirme que está ajustando el mando Floor en el lado correcto (TX o RX). Los applets TX y RX tienen estado completamente independiente y claves persistidas separadas.
- **Las pausas aún suenan completamente silenciosas** — Floor puede estar configurado por debajo de -40.0 dB en la escala, o Ratio es muy alto (cercano a 10:1), lo que hace que la puerta se comporte como un corte brusco. Eleve Floor hacia -15.0 dB y considere reducir Ratio. Consulte [Elegir comportamiento de puerta vs expansor suave mediante ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md).
- **La puerta vibra cerca del umbral** — Use el mando **Return** para agregar histéresis. Aumente Return hasta que la puerta permanezca abierta durante las breves caídas en el nivel de entrada.
- **El mosaico del applet se ve descolorido o atenuado** — la etapa Gate está omitida en el widget CHAIN. La opacidad reducida (aproximadamente 55%) es intencional. Habilite la etapa Gate en el widget CHAIN para restaurar el brillo completo y el procesamiento DSP.
- **El editor inline muestra decimales inesperados** — la pantalla se adapta al formato de la etiqueta del control. Por ejemplo, Return muestra dos decimales (X.XX dB), mientras que Floor muestra uno (X.X dB). Los valores escritos se analizan según la configuración regional de su sistema, por lo que `12,5` funciona en regiones con coma decimal.

## Relacionado

- Ajustar release para una apertura/cierre natural
- [Elegir comportamiento de puerta vs expansor suave mediante ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Ver GR en vivo mientras no se habla](watch-live-gr-while-not-speaking.md)
- [Configurar el umbral TX justo por encima del piso de ruido de la sala](set-tx-threshold-just-above-room-noise-floor.md)
