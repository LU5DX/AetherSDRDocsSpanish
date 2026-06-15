# Ajustar el Piso para evitar silencio antinatural entre palabras

Una puerta completamente cerrada produce silencio total, lo que puede sonar antinatural durante las pausas en el habla. El control Piso limita qué tan profundo puede cortar la puerta, reduciendo el audio de fondo en lugar de eliminarlo por completo.

## Antes de comenzar

- La etapa de Puerta de TX o RX debe estar habilitada en el widget CHAIN. El ClientGateApplet permanece oculto hasta que la etapa Puerta esté activa.
- Abra el subcontenedor **Aetherial TX Gate** (lado TX) dentro del contenedor principal Aetherial Audio (TXDSP), o abra el editor flotante haciendo doble clic en la etapa GATE en el widget CHAIN.

## Pasos

1. Localice el control **Floor** en la fila de cinco controles en la parte inferior del applet **Aetherial TX Gate**.
2. Gire **Floor** en sentido horario para elevar el piso (menos atenuación, menos silencio) o en sentido antihorario para bajarlo (más atenuación, corte más profundo).
3. Observe la **Barra de reducción de ganancia** mientras hace una pausa al hablar. El relleno ámbar debe dejar de crecer antes de alcanzar el piso que configuró — la barra no se extenderá más allá del valor de Floor.
4. Hable con normalidad y haga una pausa. Confirme que las pausas suenen como fondo reducido, no como silencio absoluto.

**Edición inline de valores:** Haga clic en el valor mostrado de cualquier control para escribir un número preciso directamente. El campo muestra un borde cian sutil al enfocarse. Presione Enter o haga clic en otro lugar para confirmar el valor; presione Escape para cancelar y volver al valor anterior. El desplazamiento con la rueda del ratón sigue funcionando mientras el editor está enfocado.

## Qué hace cada control

| Control               | Valor predeterminado | Rango válido        |
|-----------------------|----------------------|---------------------|
| Floor                 | -15.0 dB             | -80.0 a 0.0 dB      |
| Thresh                | -40.0 dB             | -80.0 a 0.0 dB      |
| Ratio                 | 2.0                  | 1.0 a 10.0          |
| Return                | 2.0 dB               | 0.0 a 20.0 dB       |
| Release               | 100 ms               | 5 a 2000 ms         |
| Barra de reducción de ganancia | —           | 0 a 40 dB GR        |
| Curva de transferencia | —                    | —                   |

Para el lado RX, la clave persistida equivalente es `ClientGateRxFloorDb`. El control Floor en el applet **Aetherial AGC-G** funciona de manera idéntica.

## Consejos

- El piso predeterminado de -15.0 dB está marcado por la pequeña marca en la barra de reducción de ganancia. Si la atenuación en ese valor aún suena abrupta, intente elevar Floor a -10.0 dB o -6.0 dB.
- Floor solo limita el techo de atenuación — no cambia cuándo ni qué tan rápido se abre o cierra la puerta. Si la puerta se abre y cierra demasiado bruscamente, ajuste también **Release**. Consulte Ajustar release para apertura/cierre natural.
- Si la puerta tiembla — abriéndose y cerrándose rápidamente en señales cercanas al umbral — aumente **Return** para ampliar la banda muerta de histéresis. La banda cian en la curva de transferencia se vuelve más ancha a medida que Return aumenta, facilitando la evaluación visual de la zona pegajosa.
- Establecer Floor en 0.0 dB deshabilita toda atenuación, efectivamente omitiendo el efecto de la puerta sin desactivarla en la cadena.
- Cuando la etapa Gate está deshabilitada en el widget CHAIN, el mosaico completo del applet se atenúa aproximadamente a la mitad de opacidad. Esto coincide con el efecto de atenuación usado en la curva de EQ y proporciona una indicación visual rápida de que la etapa está omitida sin necesidad de verificar directamente el widget CHAIN.
- El indicador de **Curva de transferencia** muestra la curva de transferencia estática del expansor con un punto móvil en el nivel de entrada actual. Una banda de histéresis vertical cian suave aparece entre (Thresh menos Return) y Thresh cuando Return es mayor que 0 dB, haciendo visible la zona pegajosa de la puerta.
- Use la edición inline de valores para establecer controles con precisión decimal — por ejemplo, escriba `2.5` para Ratio y obtenga una relación de expansión de 2.5:1, o `12.5` para Return y establezca exactamente 12.5 dB de histéresis.
- La **Barra de reducción de ganancia** es una franja horizontal ámbar que se llena desde la derecha. Su escala máxima es 40 dB, con una marca en -15.0 dB que indica el piso predeterminado. La animación de la barra ahora es más suave: cuando el estado de la puerta se estabiliza, las actualizaciones de medición se repiten exactamente una vez más para pulir lo visual, de modo que la barra se deslice a su posición final sin una parada abrupta.

## Tematización de colores de los controles

Los controles en los applets Aetherial TX Gate y Aetherial AGC-G usan colores definidos por el tema en el espacio de nombres `color.knob.*`. Cada componente del control — anillo de fondo, arco frontal, manija, texto de etiqueta y texto de valor — lee su color del tema activo. Cuando el contenedor del applet es `applet/gate`, los colores de los controles pueden diferir de aquellos en otros contenedores (por ejemplo, el acento ámbar en la curva de transferencia de la puerta también colorea el arco frontal del control).

Si cambia de tema, todos los colores de los controles se actualizan inmediatamente. Para inspeccionar o personalizar los colores de los controles, consulte las entradas `color.knob.background`, `color.knob.foreground`, `color.knob.handle`, `color.text.primary` y `color.text.secondary` de su archivo de tema.

## Solución de problemas

- **La barra de reducción de ganancia se llena completamente independientemente de Floor** — confirme que está ajustando el control Floor en el lado correcto (TX o RX). Los applets de TX y RX tienen estado totalmente independiente y claves persistidas separadas.
- **Las pausas aún suenan completamente silenciosas** — Floor puede estar configurado por debajo de -40.0 dB en la escala, o Ratio es muy alto (cercano a 10:1), haciendo que la puerta se comporte como un corte brusco. Eleve Floor hacia -15.0 dB y considere reducir Ratio. Consulte [Elegir comportamiento de puerta vs expansor suave mediante ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md).
- **La puerta tiembla cerca del umbral** — Use el control **Return** para agregar histéresis. Aumente Return hasta que la puerta permanezca abierta durante breves caídas en el nivel de entrada.
- **El mosaico del applet se ve desvaído o atenuado** — la etapa Gate está omitida en el widget CHAIN. La opacidad reducida (aproximadamente 55%) es intencional. Habilite la etapa Gate en el widget CHAIN para restaurar el brillo completo y el procesamiento DSP.
- **El editor inline muestra lugares decimales inesperados** — la visualización se adapta al formato de la etiqueta del control. Por ejemplo, Return muestra dos lugares decimales (X.XX dB), mientras que Floor muestra uno (X.X dB). Los valores escritos se analizan usando la configuración regional de su sistema, por lo que `12,5` funciona en regiones que usan coma como separador decimal.

## Relacionado

- Ajustar release para apertura/cierre natural
- [Elegir comportamiento de puerta vs expansor suave mediante ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Observar GR en vivo mientras no habla](watch-live-gr-while-not-speaking.md)
- [Establecer umbral de TX justo por encima del piso de ruido ambiente](set-tx-threshold-just-above-room-noise-floor.md)
