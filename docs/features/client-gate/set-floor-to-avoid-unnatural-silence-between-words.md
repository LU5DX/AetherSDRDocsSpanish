# Ajustar el piso (Floor) para evitar el silencio antinatural entre palabras

Una compuerta completamente cerrada produce silencio absoluto, lo cual puede sonar antinatural durante las pausas en el habla. El control **Floor** limita la profundidad máxima de corte de la compuerta, de modo que el audio de fondo se reduce en lugar de eliminarse por completo.

## Antes de comenzar

- La etapa TX Gate o RX Gate debe estar habilitada en el widget CHAIN. El ClientGateApplet permanece oculto hasta que la etapa Gate esté activa.
- Abra el subcontenedor **Aetherial TX Gate** (lado TX) dentro del contenedor principal Aetherial Audio (TXDSP), o abra el editor flotante haciendo doble clic en la etapa GATE del widget CHAIN.

## Pasos

1. Localice el control **Floor** en la fila de cinco controles en la parte inferior del applet **Aetherial TX Gate**.
2. Gire **Floor** hacia la derecha para subir el piso (menos atenuación, menos silencio) o hacia la izquierda para bajarlo (más atenuación, corte más profundo).
3. Observe la **barra de reducción de ganancia** mientras hace una pausa en el habla. El relleno ámbar debe dejar de crecer antes de alcanzar el valor de piso establecido — la barra no se extenderá más allá del valor de Floor.
4. Hable con normalidad y haga una pausa. Confirme que las pausas suenen como fondo reducido y no como silencio total.

## Qué hace cada control

| Control                | Valor por defecto                                                                                                                                                                                                                                | Rango válido                                                                                                                                                                                                                                                                    |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Floor                  | -15.0 dB                                                                                                                                                                                                                                         | -80.0 a 0.0 dB                                                                                                                                                                                                                                                                  |
| Return                 | 2.0 dB                                                                                                                                                                                                                                           | 0.0 a 20.0 dB                                                                                                                                                                                                                                                                   |
| Barra de reducción de ganancia | —                                                                                                                                                                                                                                        | 0 a 40 dB GR                                                                                                                                                                                                                                                                    |
| Flip (Expander / Gate) | Sin marcar = expansor descendente (suave, basado en ratio). Marcado = Gate (corte duro). Al conmutar, ajusta automáticamente el ratio y el piso a pares preestablecidos; los demás controles permanecen en su posición. La etiqueta se actualiza en tiempo real entre 'Expander' y 'Gate'. | Control exclusivo del editor (ClientGateEditor flotante). Color: sin marcar = verde (Expander), marcado = ámbar (Gate). Tooltip: 'Flip between downward Expander (gentle) and Gate (hard) modes. Snaps ratio + floor to preset pairs; other knobs stay where you left them.' |
| Peek (lookahead)       | Establece un retardo de prelectura para que la compuerta pueda abrirse de forma anticipada antes de que llegue un transitorio, evitando cortes en el ataque. 'Off' desactiva completamente la línea de retardo.                                  | Control exclusivo del editor. Valores más altos aumentan la latencia en la ruta TX. 1 y 1.5 ms coinciden con las opciones preestablecidas de Ableton; se añaden 3 y 5 ms para transitorios muy rápidos.                                                                          |
| Attack                 | Mapeo exponencial (0.1 * 1000^n). Determina la rapidez con que la compuerta se abre cuando la señal de entrada supera Thresh.                                                                                                                    | Control exclusivo del editor. Etiqueta 'X.XX ms' por debajo de 10 ms, 'X.X ms' por encima.                                                                                                                                                                                      |
| Hold                   | Mapeo lineal (n * 500). Cuando la entrada cae por debajo de Thresh − Return, la compuerta permanece abierta durante este tiempo antes de comenzar a cerrarse, evitando el parpadeo en material rítmico.                                          | Control exclusivo del editor. Etiqueta 'X.X ms'.                                                                                                                                                                                                                                |

Para el lado RX, la clave persistida equivalente es `ClientGateRxFloorDb`. El control Floor en el applet **Aetherial AGC-T** funciona de manera idéntica.

## Consejos

- El valor por defecto de Floor de -15.0 dB está marcado por la muesca en la barra de reducción de ganancia. Si la atenuación en ese valor aún suena abrupta, pruebe a subir Floor a -10.0 dB o -6.0 dB.
- Floor solo limita el techo de atenuación — no modifica cuándo ni con qué rapidez se abre o cierra la compuerta. Si la compuerta abre y cierra de forma demasiado brusca, ajuste también **Release**. Consulte [Ajustar el release para una apertura y cierre naturales](tune-release-for-natural-open-close.md).
- Si la compuerta oscila — abriéndose y cerrándose rápidamente con señales cercanas al umbral — aumente **Return** para ampliar la banda muerta de histéresis. La banda cian en la curva de transferencia se hace más ancha al aumentar Return, lo que facilita la evaluación visual de la zona de estabilidad.
- Ajustar Floor a 0.0 dB desactiva toda atenuación, lo que efectivamente omite el efecto de la compuerta sin deshabilitarla en la cadena.

## Solución de problemas

- **La barra de reducción de ganancia se llena completamente sin importar el valor de Floor** — confirme que está ajustando el control Floor en el lado correcto (TX o RX). Los applets TX y RX tienen estado completamente independiente y claves persistidas separadas.
- **Las pausas aún suenan completamente en silencio** — es posible que Floor esté ajustado por debajo de -40.0 dB en la escala, o que Ratio sea muy alto (cercano a 10:1), haciendo que la compuerta se comporte como un corte duro. Suba Floor hacia -15.0 dB y considere reducir Ratio. Consulte [Elegir el comportamiento de compuerta o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md).
- **La compuerta oscila cerca del umbral** — el control Attack ya no está disponible. Use el control **Return** para agregar histéresis en su lugar. Aumente Return hasta que la compuerta permanezca abierta durante las breves caídas en el nivel de entrada.

## Relacionados

- [Ajustar el release para una apertura y cierre naturales](tune-release-for-natural-open-close.md)
- [Elegir el comportamiento de compuerta o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Ver la reducción de ganancia en tiempo real mientras no se habla](watch-live-gr-while-not-speaking.md)
- [Ajustar el umbral TX justo por encima del piso de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md)
