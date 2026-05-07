# Ajustar el Piso para evitar el silencio antinatural entre palabras

Una puerta completamente cerrada produce silencio total, lo que puede sonar antinatural durante las pausas en el habla. El control Piso (Floor) limita la profundidad del corte de la puerta, por lo que el audio de fondo se reduce en lugar de eliminarse por completo.

## Antes de comenzar

- La etapa de Puerta de TX o de RX debe estar habilitada en el widget CHAIN. El ClientGateApplet permanece oculto hasta que la etapa Gate esté activa.
- Abra el subcontenedor **Aetherial TX Gate** (lado TX) dentro del contenedor principal Aetherial Audio (TXDSP), o abra el editor flotante haciendo doble clic en la etapa GATE en el widget CHAIN.

## Pasos

1. Localice el control **Floor** en la fila de cinco perillas en la parte inferior del applet **Aetherial TX Gate**.
2. Gire **Floor** en el sentido de las agujas del reloj para subir el piso (menos atenuación, menos silencio) o en sentido contrario para bajarlo (más atenuación, corte más profundo).
3. Observe la **Barra de reducción de ganancia** mientras hace una pausa al hablar. El relleno ámbar debería dejar de crecer antes de alcanzar el piso que configuró; la barra no se extenderá más allá del valor de Floor.
4. Hable con normalidad y haga una pausa. Confirme que las pausas suenan como un fondo reducido en lugar de silencio absoluto.

## Función de cada control

| Control               | Valor predeterminado                                                                                                                                                                                                              | Rango válido                                                                                                                                                                                                                                                                                  |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Floor                 | -15.0 dB                                                                                                                                                                                                                          | -80.0 a 0.0 dB                                                                                                                                                                                                                                                                                |
| Return                | 2.0 dB                                                                                                                                                                                                                            | 0.0 a 20.0 dB                                                                                                                                                                                                                                                                                 |
| Barra de reduc. de ganancia | —                                                                                                                                                                                                                                | 0 a 40 dB GR                                                                                                                                                                                                                                                                                  |
| Flip (Expander / Gate)| Sin marcar = expansor descendente (suave, basado en relación). Marcado = Gate (corte duro). Ajusta la relación y el piso a pares predefinidos al alternar; los demás controles permanecen en su lugar. La etiqueta se actualiza en vivo entre 'Expander' y 'Gate'. | Control solo del editor (ClientGateEditor flotante). Color: sin marcar = verde (Expander), marcado = ámbar (Gate). Información sobre herramientas: 'Alterna entre el modo Expansor descendente (suave) y Gate (duro). Ajusta la relación y el piso a pares predefinidos; los demás controles permanecen donde los dejó.' |
| Peek (lookahead)      | Establece un retardo de prelectura para que la puerta pueda abrirse fraccionalmente antes de que llegue un transitorio, evitando bordes de ataque recortados. 'Off' desactiva por completo la línea de retardo.                   | Control solo del editor. Los valores más altos aumentan la latencia en la ruta TX. 1 y 1.5 ms coinciden con las opciones predefinidas de Ableton; se agregaron 3 y 5 ms para transitorios muy rápidos.                                                                                        |
| Attack                | Mapeo exponencial (0.1 * 1000^n). Define la rapidez con que se abre la puerta después de que la entrada supera Thresh.                                                                                                            | Control solo del editor. Etiqueta 'X.XX ms' por debajo de 10 ms, 'X.X ms' por encima.                                                                                                                                                                                                         |
| Hold                  | Mapeo lineal (n * 500). Después de que la entrada cae por debajo de Thresh − Return, la puerta permanece abierta durante este tiempo antes de comenzar a cerrarse, evitando vibraciones en material rítmico.                      | Control solo del editor. Etiqueta 'X.X ms'.                                                                                                                                                                                                                                                   |

Para el lado RX, la clave persistida equivalente es `ClientGateRxFloorDb`. El control Floor en el applet **Aetherial AGC-T** funciona de manera idéntica.

## Consejos

- El valor predeterminado de Floor de -15.0 dB está marcado por la muesca en la barra de reducción de ganancia. Si la atenuación en ese valor aún suena abrupta, intente subir Floor a -10.0 dB o -6.0 dB.
- Floor solo limita el techo de atenuación; no cambia cuándo ni con qué rapidez se abre o cierra la puerta. Si la puerta se abre y cierra demasiado bruscamente, ajuste también **Release**. Consulte [Ajustar Release para apertura/cierre natural](tune-release-for-natural-open-close.md).
- Si la puerta vibra, abriéndose y cerrándose rápidamente en señales cercanas al umbral, aumente **Return** para ampliar la banda muerta de histéresis. La banda cian en la curva de transferencia se ensancha a medida que Return aumenta, lo que facilita la evaluación visual de la zona pegajosa.
- Configurar Floor en 0.0 dB desactiva toda atenuación, lo que efectivamente evita el efecto de la puerta sin deshabilitarla en la cadena.
- Cuando la etapa Gate está deshabilitada en el widget CHAIN, todo el mosaico del applet se atenúa aproximadamente a la mitad de opacidad. Esto coincide con el efecto de atenuación utilizado en la curva EQ y proporciona una indicación visual rápida de que la etapa está puenteada sin necesidad de verificar directamente el widget CHAIN.

## Solución de problemas

- **La barra de reducción de ganancia se llena completamente independientemente de Floor** — confirme que está ajustando el control Floor en el lado correcto (TX o RX). Los applets TX y RX tienen un estado completamente independiente y claves persistidas separadas.
- **Las pausas aún suenan completamente silenciosas** — Floor podría estar configurado por debajo de -40.0 dB en la escala, o Ratio es muy alto (cercano a 10:1), lo que hace que la puerta se comporte como un corte duro. Eleve Floor hacia -15.0 dB y considere reducir Ratio. Consulte [Elegir comportamiento de puerta vs. expansor suave mediante Ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md).
- **La puerta vibra cerca del umbral** — el control Attack ya no está presente. Use el control **Return** para agregar histéresis. Aumente Return hasta que la puerta permanezca abierta durante las caídas breves en el nivel de entrada.
- **El mosaico del applet se ve atenuado o apagado** — la etapa Gate está puenteada en el widget CHAIN. La opacidad reducida (aproximadamente 55%) es intencional. Habilite la etapa Gate en el widget CHAIN para restaurar el brillo completo y el procesamiento DSP.

## Relacionados

- [Ajustar Release para apertura/cierre natural](tune-release-for-natural-open-close.md)
- [Elegir comportamiento de puerta vs. expansor suave mediante Ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Ver GR en vivo mientras no habla](watch-live-gr-while-not-speaking.md)
- [Configurar el umbral de TX justo por encima del piso de ruido ambiente](set-tx-threshold-just-above-room-noise-floor.md)
