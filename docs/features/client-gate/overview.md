# Descripción general de Aetherial TX Gate / Aetherial AGC-T (RX)

AetherSDR incluye un expansor descendente y puerta de ruido del lado del cliente que opera de forma independiente en las rutas de audio de transmisión y recepción. Utilícelo para suprimir el ruido de fondo entre palabras en TX, o para reducir el ruido de banda por debajo de un nivel mínimo elegido en RX.

## Antes de comenzar

- La etapa Gate debe habilitarse mediante el widget CHAIN o el editor flotante en el lado correspondiente antes de que el applet sea visible.
- AetherSDR no necesita estar conectado a un radio para ajustar los controles de la puerta, pero el audio debe estar activo para que los indicadores en tiempo real sean significativos.

## Cómo funciona

AetherSDR instancia dos copias completamente independientes del applet de puerta:

- **Aetherial TX Gate** — actúa sobre el audio de transmisión saliente. Se encuentra en el contenedor principal Aetherial Audio (TXDSP).
- **Aetherial AGC-T** — actúa sobre el audio de recepción entrante. Se encuentra en el mismo contenedor principal como un subcontenedor separado.

Ambas copias comparten controles e indicadores idénticos. Los ajustes de cada lado se almacenan de forma independiente. Los cambios realizados en el panel del applet anclado y los cambios realizados en el editor flotante se mantienen sincronizados; el applet consulta el motor aproximadamente cada 33 ms y actualiza las posiciones de los mandos y la barra de reducción de ganancia para reflejar el lado activo.

### Flujo de señal

La puerta es un **expansor descendente**. Cuando el nivel de entrada cae por debajo del punto Thresh, la puerta atenúa la señal. La cantidad de atenuación depende de Ratio, y el corte máximo permitido lo establece Floor. Return define una banda muerta de histéresis: la puerta se abre cuando la señal supera Thresh y no se cierra hasta que la señal cae por debajo de Thresh − Return. Release controla con qué rapidez se cierra la puerta una vez que la señal cae por debajo de ese límite inferior.

Establecer Ratio en un valor bajo (cercano a 1.0:1) produce un efecto de expansor suave que reduce el nivel gradualmente. Establecer Ratio en un valor alto (cercano a 10.0:1) produce una puerta dura que corta de forma agresiva.

### Abrir el applet

Haga doble clic en la etapa GATE en el widget CHAIN del lado TX o RX para abrir el editor sin marco correspondiente, titulado **Aetherial Gate — TX** o **Aetherial Gate — RX**. Las barras de título de los subcontenedores anclados de **Aetherial TX Gate** y **Aetherial AGC-T** se pueden pulsar con el botón derecho para flotar, extraer u ocultar el panel.

## Qué hace cada control

Los controles listados a continuación aparecen de forma idéntica en los applets de TX y RX. Las claves de configuración indicadas corresponden al lado TX; el lado RX utiliza las claves equivalentes `ClientGateRx*`.

| Control                | Tipo                                                                                                                                                                                                                        | Valor predeterminado                                                                                                                                                                                                                                                                      |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Transfer curve         | Indicador                                                                                                                                                                                                                   | —                                                                                                                                                                                                                                                                                         |
| Gain-reduction bar     | Medidor                                                                                                                                                                                                                     | —                                                                                                                                                                                                                                                                                         |
| Thresh                 | Mando                                                                                                                                                                                                                       | −40.0 dB                                                                                                                                                                                                                                                                                  |
| Ratio                  | Mando                                                                                                                                                                                                                       | 2.0:1                                                                                                                                                                                                                                                                                     |
| Return                 | Mando                                                                                                                                                                                                                       | 2.0 dB                                                                                                                                                                                                                                                                                    |
| Release                | Mando                                                                                                                                                                                                                       | 100 ms                                                                                                                                                                                                                                                                                    |
| Floor                  | Mando                                                                                                                                                                                                                       | −15.0 dB                                                                                                                                                                                                                                                                                  |
| Flip (Expander / Gate) | Sin marcar = expansor descendente (suave, basado en ratio). Marcado = Gate (corte duro). Ajusta ratio y floor a pares preestablecidos al conmutar; los demás mandos permanecen en su posición. La etiqueta cambia en tiempo real entre 'Expander' y 'Gate'. | Control exclusivo del editor (flotante ClientGateEditor). Color: sin marcar = verde (Expander), marcado = ámbar (Gate). Tooltip: 'Flip between downward Expander (gentle) and Gate (hard) modes. Snaps ratio + floor to preset pairs; other knobs stay where you left them.' |
| Peek (lookahead)       | Establece un retardo de prelectura para que la puerta pueda abrirse fraccionalmente antes de que llegue un transitorio, evitando bordes de ataque recortados. 'Off' deshabilita la línea de retardo por completo.           | Control exclusivo del editor. Los valores más altos aumentan la latencia en la ruta TX. Los valores de 1 y 1.5 ms coinciden con las opciones preestablecidas de Ableton; se agregaron 3 y 5 ms para transitorios muy rápidos.                                                              |
| Attack                 | Mapeo exponencial (0.1 * 1000^n). Establece con qué rapidez se abre la puerta después de que la entrada supera Thresh.                                                                                                     | Control exclusivo del editor. Etiqueta 'X.XX ms' por debajo de 10 ms, 'X.X ms' por encima.                                                                                                                                                                                               |
| Hold                   | Mapeo lineal (n * 500). Después de que la entrada cae por debajo de Thresh − Return, la puerta permanece abierta durante este tiempo antes de comenzar a cerrarse, evitando el traqueteo en material rítmico.              | Control exclusivo del editor. Etiqueta 'X.X ms'.                                                                                                                                                                                                                                          |

El estado de habilitación/bypass de cada lado se guarda en `ClientGateTxEnabled` (TX) y `ClientGateRxEnabled` (RX).

## Indicadores visuales

| Indicador | Estados | Significado |
|---|---|---|
| Bola de entrada | Por debajo del umbral / por encima del umbral | Muestra si la puerta está actualmente abierta o cerrada. |
| Banda de histéresis | Ausente (Return = 0) / banda vertical cian suave | Visualiza la banda muerta de Return en el eje de entrada de la curva de transferencia — la zona de adhesión de la puerta entre (Thresh − Return) y Thresh. |
| Barra de reducción de ganancia | Vacía / relleno ámbar / marca −15 dB | Profundidad de atenuación mientras la puerta está cerrada. |

## Consejos

- Observe la barra de reducción de ganancia mientras no habla (TX) o durante un momento de solo ruido de banda (RX). Si la barra no se llena, Thresh está configurado por debajo del piso de ruido y la puerta no se está activando. Consulte [Observe la GR en tiempo real mientras no habla](watch-live-gr-while-not-speaking.md).
- La marca de −15 dB en la barra de reducción de ganancia señala el valor predeterminado de Floor. Si la barra se llena completamente más allá de esa marca, Floor está configurado por debajo de −15 dB o Ratio es suficientemente alto para empujar la reducción más allá de ese punto.
- Use la banda de histéresis cian en la curva de transferencia para evaluar si el valor de Return es suficientemente amplio para evitar el traqueteo sin hacer que la puerta sea lenta al cerrarse.
- Los cambios en cualquier mando surten efecto inmediatamente y se guardan de forma automática. No se necesita ningún botón Apply.

## Solución de problemas

- **El applet no es visible** — La etapa Gate no ha sido habilitada en ese lado. Habilítela mediante el widget CHAIN o el editor flotante para el lado TX o RX.
- **La puerta no atenúa el ruido entre palabras** — Thresh puede estar configurado demasiado bajo, por debajo del piso de ruido ambiental. Suba Thresh hasta que la barra de reducción de ganancia muestre movimiento durante los silencios. Consulte [Configure el umbral TX justo por encima del piso de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md).
- **La puerta traquetea rápidamente cerca del umbral** — Return está configurado demasiado bajo. Aumente Return para que la puerta no se reabra hasta que la señal esté claramente por encima de Thresh, ampliando la banda muerta que muestra la banda cian en la curva de transferencia.
- **Silencio antinatural entre palabras** — Floor está configurado demasiado profundo. Suba Floor hacia 0 dB para que algo de audio residual pase durante los períodos cerrados. Consulte [Configure Floor para evitar el silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md).
- **Las posiciones de los mandos en el panel no coinciden con el editor flotante** — El panel se sincroniza cada ~33 ms. Si aparecen desalineados inmediatamente después de abrir el editor, espere un ciclo de actualización o mueva un mando para forzar la sincronización.

## Relacionados

- [Configure el umbral TX justo por encima del piso de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md)
- [Use AGC-T en RX para suprimir el ruido de banda por debajo de un nivel mínimo elegido](use-agc-t-on-rx-to-suppress-band-noise-below-a-chosen-floor.md)
- [Elija el comportamiento de puerta o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Configure Floor para evitar el silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Observe la GR en tiempo real mientras no habla](watch-live-gr-while-not-speaking.md)
- [Omita la puerta desde la cadena](bypass-the-gate-from-the-chain.md)
