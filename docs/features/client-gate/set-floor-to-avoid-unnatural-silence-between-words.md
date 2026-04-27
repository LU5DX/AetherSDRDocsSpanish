# Configurar Floor para evitar silencios artificiales entre palabras

Una puerta completamente cerrada produce silencio total, lo cual puede sonar artificial durante las pausas en el habla. El mando **Floor** limita la profundidad máxima de corte de la puerta, de modo que el audio de fondo se reduce en lugar de eliminarse por completo.

## Antes de comenzar

- La etapa TX Gate o RX Gate debe estar habilitada en el widget CHAIN. El ClientGateApplet permanece oculto hasta que la etapa Gate esté activa.
- Abra el subcontenedor **Aetherial TX Gate** (lado TX) dentro del contenedor principal Aetherial Audio (TXDSP), o abra el editor flotante haciendo doble clic en la etapa GATE del widget CHAIN.

## Pasos

1. Localice el mando **Floor** en la fila de cinco mandos situada en la parte inferior del applet **Aetherial TX Gate**.
2. Gire **Floor** en sentido horario para subir el piso (menos atenuación, menos silencio) o en sentido antihorario para bajarlo (más atenuación, corte más profundo).
3. Observe la **barra de reducción de ganancia** mientras hace pausas al hablar. El relleno ámbar debe dejar de crecer antes de alcanzar el valor de Floor que ha configurado — la barra no se extenderá más allá de ese valor.
4. Hable con normalidad y haga una pausa. Compruebe que las pausas suenen como reducción del fondo y no como silencio absoluto.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Floor | -15.0 dB | -80.0 a 0.0 dB | `ClientGateTxFloorDb` | Atenuación máxima que la puerta puede aplicar. Valores más altos (más cercanos a 0 dB) preservan más audio durante el cierre; valores más bajos permiten un corte más profundo. |
| Barra de reducción de ganancia | — | 0 a 40 dB GR | — | Franja ámbar horizontal, rellena desde la derecha. Muestra la profundidad actual de atenuación. Una marca de referencia en -15 dB indica la posición predeterminada de Floor. |

En el lado RX, la clave persistida equivalente es `ClientGateRxFloorDb`. El mando Floor del applet **Aetherial AGC-T** funciona de forma idéntica.

## Consejos

- El valor predeterminado de Floor (-15.0 dB) está marcado por la muesca en la barra de reducción de ganancia. Si la atenuación en ese valor aún suena abrupta, intente subir Floor a -10.0 dB o -6.0 dB.
- Floor solo limita el techo de atenuación — no modifica cuándo ni con qué rapidez se abre o cierra la puerta. Si la puerta se abre y cierra con demasiada brusquedad, ajuste también Release. Consulte [Ajustar ataque/liberación para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md).
- Configurar Floor en 0.0 dB deshabilita toda atenuación, lo que en la práctica anula el efecto de la puerta sin desactivarla en la cadena.

## Solución de problemas

- **La barra de reducción de ganancia se llena por completo sin importar el valor de Floor** — confirme que está ajustando el mando Floor en el lado correcto (TX o RX). Los applets TX y RX tienen un estado completamente independiente y claves persistidas separadas.
- **Las pausas siguen sonando completamente silenciosas** — es posible que Floor esté configurado por debajo de -40.0 dB en la escala, o que Ratio sea muy alto (cercano a 10:1), lo que hace que la puerta actúe como un corte abrupto. Suba Floor hacia -15.0 dB y considere reducir Ratio. Consulte [Elegir el comportamiento de puerta o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md).

## Temas relacionados

- [Ajustar ataque/liberación para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md)
- [Elegir el comportamiento de puerta o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Monitorear la reducción de ganancia en tiempo real mientras no habla](watch-live-gr-while-not-speaking.md)
- [Configurar el umbral TX justo por encima del nivel de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md)
