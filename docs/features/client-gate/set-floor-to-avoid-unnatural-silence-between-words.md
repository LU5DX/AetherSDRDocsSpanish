# Configurar el Floor para evitar el silencio antinatural entre palabras

Un gate completamente cerrado produce silencio total, lo que puede sonar antinatural durante las pausas en el habla. El control **Floor** limita la profundidad máxima de corte del gate, de modo que el audio de fondo se reduce en lugar de eliminarse por completo.

## Antes de comenzar

- La etapa TX Gate o RX Gate debe estar habilitada en el widget CHAIN. El ClientGateApplet permanece oculto hasta que la etapa Gate esté activa.
- Abra el subcontenedor **Aetherial TX Gate** (lado TX) dentro del contenedor principal Aetherial Audio (TXDSP), o abra el editor flotante haciendo doble clic en la etapa GATE del widget CHAIN.

## Pasos

1. Localice el control **Floor** en la fila de cinco mandos situada en la parte inferior del applet **Aetherial TX Gate**.
2. Gire **Floor** hacia la derecha para subir el piso (menos atenuación, menos silencio) o hacia la izquierda para bajarlo (más atenuación, corte más profundo).
3. Observe la **barra de reducción de ganancia** mientras hace una pausa en el habla. El relleno ámbar debe dejar de crecer antes de alcanzar el valor de Floor que configuró — la barra no se extenderá más allá del valor de Floor.
4. Hable con normalidad y haga una pausa. Confirme que las pausas suenan como fondo reducido y no como silencio total.

## Qué hace cada control

| Control                | Valor por defecto                                                                                                                                                                                                                          | Rango válido                                                                                                                                                                                                                                                                                                                   |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Floor                  | -15.0 dB                                                                                                                                                                                                                                   | -80.0 a 0.0 dB                                                                                                                                                                                                                                                                                                                 |
| Return                 | 2.0 dB                                                                                                                                                                                                                                     | 0.0 a 20.0 dB                                                                                                                                                                                                                                                                                                                  |
| Barra de reducción de ganancia | —                                                                                                                                                                                                                                  | 0 a 40 dB GR                                                                                                                                                                                                                                                                                                                   |
| Flip (Expander / Gate) | Sin marcar = expansor descendente (suave, basado en ratio). Marcado = Gate (corte duro). Al conmutar, ajusta automáticamente el ratio y el Floor a pares preestablecidos; los demás controles permanecen en su posición. La etiqueta se actualiza en tiempo real entre 'Expander' y 'Gate'. | Control exclusivo del editor (ClientGateEditor flotante). Color: sin marcar = verde (Expander), marcado = ámbar (Gate). Información de herramienta: 'Flip between downward Expander (gentle) and Gate (hard) modes. Snaps ratio + floor to preset pairs; other knobs stay where you left them.' |
| Peek (lookahead)       | Establece un retardo de prelectura para que el gate pueda abrirse levemente antes de que llegue un transitorio, evitando el recorte de los flancos de ataque. 'Off' deshabilita la línea de retardo por completo.                         | Control exclusivo del editor. Valores más altos aumentan la latencia en la ruta TX. 1 y 1.5 ms coinciden con las opciones preestablecidas de Ableton; 3 y 5 ms se añaden para transitorios muy rápidos.                                                                                                                        |
| Attack                 | Mapeo exponencial (0.1 * 1000^n). Determina la rapidez con que el gate se abre cuando la entrada supera el umbral Thresh.                                                                                                                  | Control exclusivo del editor. Etiqueta 'X.XX ms' por debajo de 10 ms, 'X.X ms' por encima.                                                                                                                                                                                                                                    |
| Hold                   | Mapeo lineal (n * 500). Después de que la entrada cae por debajo de Thresh − Return, el gate permanece abierto durante este tiempo antes de comenzar a cerrarse, evitando el parpadeo en material rítmico.                                | Control exclusivo del editor. Etiqueta 'X.X ms'.                                                                                                                                                                                                                                                                               |

Para el lado RX, la clave persistente equivalente es `ClientGateRxFloorDb`. El control Floor en el applet **Aetherial AGC-T** funciona de manera idéntica.

## Consejos

- El valor de Floor por defecto de -15.0 dB está marcado por la muesca en la barra de reducción de ganancia. Si la atenuación en ese valor sigue sonando abrupta, intente subir Floor a -10.0 dB o -6.0 dB.
- Floor solo limita el techo de atenuación — no modifica cuándo ni con qué rapidez se abre o cierra el gate. Si el gate se abre y cierra con demasiada brusquedad, ajuste también **Release**. Consulte [Ajustar el release para una apertura/cierre natural](tune-release-for-natural-open-close.md).
- Si el gate traquetea — abriéndose y cerrándose rápidamente ante señales cercanas al umbral — aumente **Return** para ampliar la banda muerta de histéresis. La banda cian en la curva de transferencia se amplía a medida que aumenta Return, lo que facilita la evaluación visual de la zona de adherencia.
- Configurar Floor en 0.0 dB deshabilita toda atenuación, lo que en la práctica puentea el efecto del gate sin desactivarlo en la cadena.

## Solución de problemas

- **La barra de reducción de ganancia se llena por completo independientemente del Floor** — confirme que está ajustando el control Floor en el lado correcto (TX o RX). Los applets TX y RX tienen estado completamente independiente y claves persistentes separadas.
- **Las pausas siguen sonando completamente en silencio** — es posible que Floor esté configurado por debajo de -40.0 dB en la escala, o que Ratio sea muy alto (próximo a 10:1), lo que hace que el gate se comporte como un corte duro. Suba Floor hacia -15.0 dB y considere reducir Ratio. Consulte [Elegir el comportamiento de gate o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md).
- **El gate traquetea cerca del umbral** — el control Attack ya no está disponible. Use el control **Return** para añadir histéresis. Aumente Return hasta que el gate permanezca abierto durante las caídas breves en el nivel de entrada.

## Relacionados

- [Ajustar el release para una apertura/cierre natural](tune-release-for-natural-open-close.md)
- [Elegir el comportamiento de gate o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Observar la GR en tiempo real mientras no se habla](watch-live-gr-while-not-speaking.md)
- [Configurar el umbral TX justo por encima del ruido de fondo del entorno](set-tx-threshold-just-above-room-noise-floor.md)
