# Ajustar el Piso para evitar silencio antinatural entre palabras

Una compuerta totalmente cerrada produce silencio completo, lo que puede sonar antinatural durante las pausas en el habla. El control Piso (Floor) limita la profundidad de atenuación de la compuerta, reduciendo el audio de fondo en lugar de eliminarlo por completo.

## Antes de comenzar

- La etapa de compuerta de TX o RX debe estar habilitada en el widget CHAIN. El ClientGateApplet permanece oculto hasta que la etapa de compuerta esté activa.
- Abra el subcontenedor **Aetherial TX Gate** (lado TX) dentro del contenedor principal Aetherial Audio (TXDSP), o abra el editor flotante haciendo doble clic en la etapa GATE en el widget CHAIN.

## Pasos

1. Localice el control **Floor** en la fila de cinco perillas en la parte inferior del applet **Aetherial TX Gate**.
2. Gire **Floor** en sentido horario para elevar el piso (menos atenuación, menos silencio) o en sentido antihorario para bajarlo (más atenuación, corte más profundo).
3. Observe la **barra de reducción de ganancia** mientras hace pausas al hablar. El relleno ámbar debe dejar de crecer antes de alcanzar el piso que configuró — la barra no se extenderá más allá del valor de Floor.
4. Hable normalmente y haga pausas. Confirme que las pausas suenen como fondo reducido y no como silencio absoluto.

## Descripción de cada control

| Control                | Valor predeterminado | Rango válido |
|------------------------|----------------------|--------------|
| Floor                  | -15.0 dB             | -80.0 a 0.0 dB |
| Thresh                 | -40.0 dB             | -80.0 a 0.0 dB |
| Ratio                  | 2.0                  | 1.0 a 10.0   |
| Return                 | 2.0 dB               | 0.0 a 20.0 dB |
| Release                | 100 ms               | 5 a 2000 ms  |
| Barra de reducción de ganancia | —          | 0 a 40 dB GR |
| Curva de transferencia | —                    | —            |

Para el lado RX, la clave persistida equivalente es `ClientGateRxFloorDb`. El control Floor en el applet **Aetherial AGC-G** funciona de manera idéntica.

## Consejos

- El Piso predeterminado de -15.0 dB está marcado por la muesca en la barra de reducción de ganancia. Si la atenuación en ese valor aún suena abrupta, intente elevar Floor a -10.0 dB o -6.0 dB.
- Floor solo limita el techo de atenuación — no cambia cuándo ni qué tan rápido se abre o cierra la compuerta. Si la compuerta se abre y cierra demasiado bruscamente, ajuste también **Release**. Consulte [Ajustar release para apertura/cierre natural](tune-release-for-natural-open-close.md).
- Si la compuerta vibra (chatter) — abriéndose y cerrándose rápidamente en señales cercanas al umbral — aumente **Return** para ampliar la banda muerta de histéresis. La banda cian en la curva de transferencia se ensancha a medida que Return aumenta, facilitando la evaluación visual de la zona pegajosa.
- Configurar Floor a 0.0 dB deshabilita toda atenuación, efectivamente evitando el efecto de la compuerta sin desactivarla en la cadena.
- Cuando la etapa Gate está deshabilitada en el widget CHAIN, todo el mosaico del applet se atenúa aproximadamente a la mitad de opacidad. Esto coincide con el efecto de atenuación usado en la curva EQ y proporciona una indicación visual rápida de que la etapa está omitida sin necesidad de verificar directamente el widget CHAIN.
- El indicador de **curva de transferencia** muestra la curva estática de transferencia del expansor con un punto móvil en el nivel de entrada actual. Una banda vertical de histéresis en cian suave aparece entre (Thresh menos Return) y Thresh cuando Return es mayor que 0 dB, haciendo visible la zona pegajosa de la compuerta.

## Solución de problemas

- **La barra de reducción de ganancia se llena completamente independientemente de Floor** — confirme que está ajustando el control Floor en el lado correcto (TX o RX). Los applets de TX y RX tienen estado completamente independiente y claves persistidas separadas.
- **Las pausas aún suenan completamente silenciosas** — Floor puede estar configurado por debajo de -40.0 dB en la escala, o Ratio es muy alto (cercano a 10:1), haciendo que la compuerta se comporte como un corte duro. Suba Floor hacia -15.0 dB y considere reducir Ratio. Consulte [Elegir comportamiento de compuerta vs expansor suave mediante ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md).
- **La compuerta vibra cerca del umbral** — Use el control **Return** para agregar histéresis. Aumente Return hasta que la compuerta permanezca abierta durante breves caídas en el nivel de entrada.
- **El mosaico del applet se ve descolorido o atenuado** — la etapa Gate está omitida en el widget CHAIN. La opacidad reducida (aproximadamente 55%) es intencional. Habilite la etapa Gate en el widget CHAIN para restaurar el brillo completo y el procesamiento DSP.

## Relacionado

- [Ajustar release para apertura/cierre natural](tune-release-for-natural-open-close.md)
- [Elegir comportamiento de compuerta vs expansor suave mediante ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Observar GR en vivo mientras no habla](watch-live-gr-while-not-speaking.md)
- [Configurar umbral TX justo sobre el piso de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md)
