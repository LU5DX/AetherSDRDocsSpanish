# Descripción general de Aetherial TX Gate / Aetherial AGC-T (RX)

AetherSDR incluye un expansor descendente y puerta de ruido del lado del cliente que funciona de forma independiente tanto en las rutas de audio de transmisión como de recepción. Úselo para suprimir el ruido de fondo entre palabras en TX, o para reducir el ruido de banda por debajo de un piso seleccionado en RX.

## Antes de comenzar

- La etapa de puerta debe estar habilitada a través del widget CHAIN o el editor flotante en el lado correspondiente antes de que el applet sea visible.
- AetherSDR no necesita estar conectado a una radio para que los controles de la puerta se puedan ajustar, pero el audio debe estar funcionando para que los indicadores en vivo tengan sentido.

## Cómo funciona

AetherSDR crea dos copias completamente independientes del applet de puerta:

- **Aetherial TX Gate** — actúa sobre el audio de transmisión saliente. Se encuentra en el contenedor principal Aetherial Audio (TXDSP).
- **Aetherial AGC-T** — actúa sobre el audio de recepción entrante. Se encuentra en el mismo contenedor principal como un subcontenedor separado.

Ambas copias comparten controles e indicadores idénticos. La configuración de cada lado se almacena de forma independiente. Los cambios realizados en el mosaico del applet acoplado y los cambios realizados en el editor flotante se mantienen sincronizados; el applet consulta el motor aproximadamente cada 33 ms y actualiza las posiciones de las perillas y la barra de reducción de ganancia para reflejar el lado que esté activo.

### Flujo de señal

La puerta es un **expansor descendente**. Cuando el nivel de entrada cae por debajo del punto de Umbral, la puerta atenúa la señal. La cantidad de atenuación depende de la Relación, y el corte máximo permitido lo establece el Piso. La Vuelta establece una banda muerta de histéresis: la puerta se abre cuando la señal supera el Umbral y no se cierra hasta que la señal cae por debajo de Umbral − Vuelta. La Liberación controla la rapidez con la que se cierra la puerta una vez que la señal cae por debajo de ese límite inferior.

Establecer la Relación en un valor bajo (cerca de 1.0:1) produce un efecto suave de expansor suave que reduce gradualmente el nivel. Establecer la Relación en un valor alto (cerca de 10.0:1) produce una puerta dura que corta de forma agresiva.

### Atenuación por bypass

Cuando la etapa de puerta está en bypass, todo el mosaico del applet se renderiza con opacidad reducida (aproximadamente el 55 % del brillo total). Esto coincide con el efecto de atenuación utilizado en la curva de EQ y proporciona una indicación clara de un vistazo de que la etapa no está procesando audio. El mosaico vuelve a la opacidad total tan pronto como se vuelve a habilitar la etapa.

### Abrir el applet

Haga doble clic en la etapa GATE en el widget CHAIN en el lado TX o RX para abrir el editor sin marco correspondiente, titulado **Aetherial Gate — TX** o **Aetherial Gate — RX**. Se puede hacer clic derecho en las barras de título del subcontenedor acoplado para **Aetherial TX Gate** y **Aetherial AGC-T** para flotar, desacoplar u ocultar el mosaico.

## Qué hace cada control

Los controles que se enumeran a continuación aparecen de forma idéntica tanto en los applets de TX como de RX. Las claves de configuración que se muestran se aplican al lado TX; el lado RX utiliza las claves `ClientGateRx*` equivalentes.

| Control | Tipo | Valor predeterminado |
|---|---|---|
| Curva de transferencia | Indicador | — |
| Barra de reducción de ganancia | Medidor | — |
| Umbral | Perilla | −40.0 dB |
| Relación | Perilla | 2.0:1 |
| Vuelta | Perilla | 2.0 dB |
| Liberación | Perilla | 100 ms |
| Piso | Perilla | −15.0 dB |
| Alternar (Expansor / Puerta) | Desmarcado = expansor descendente (suave, basado en relación). Marcado = Puerta (corte duro). Ajusta la relación y el piso a pares predefinidos al alternar; las otras perillas permanecen en su lugar. La etiqueta se actualiza en vivo entre 'Expander' y 'Gate'. | Control solo del editor (ClientGateEditor flotante). Color: desmarcado = verde (Expander), marcado = ámbar (Gate). Tooltip: 'Alterna entre modos Expander descendente (suave) y Gate (duro). Ajusta la relación + el piso a pares predefinidos; las otras perillas se quedan donde las dejaste.' |
| Avance (lookahead) | Establece un retardo de lectura previa para que la puerta pueda abrirse una fracción antes de que llegue un transitorio, evitando bordes de ataque recortados. 'Off' deshabilita completamente la línea de retardo. | Control solo del editor. Valores más altos aumentan la latencia en la ruta TX. 1 y 1.5 ms coinciden con las opciones predefinidas de Ableton; se agregaron 3 y 5 ms para transitorios muy rápidos. |
| Ataque | Mapeo exponencial (0.1 * 1000^n). Establece la rapidez con la que se abre la puerta después de que la entrada supera el Umbral. | Control solo del editor. Etiqueta 'X.XX ms' por debajo de 10 ms, 'X.X ms' por encima. |
| Mantención | Mapeo lineal (n * 500). Después de que la entrada cae por debajo de Umbral − Vuelta, la puerta permanece abierta durante este tiempo antes de comenzar a cerrarse, evitando el aleteo en material rítmico. | Control solo del editor. Etiqueta 'X.X ms'. |

El estado de habilitación/bypass para cada lado se conserva bajo `ClientGateTxEnabled` (TX) y `ClientGateRxEnabled` (RX).

## Indicadores visuales

| Indicador | Estados | Significado |
|---|---|---|
| Bola de entrada | Por debajo del umbral / por encima del umbral | Muestra si la puerta está actualmente abierta o cerrada. |
| Banda de histéresis | Ausente (Vuelta = 0) / banda vertical cian suave | Visualiza la banda muerta de Vuelta en el eje de entrada de la curva de transferencia: la zona de fijación de la puerta entre (Umbral − Vuelta) y Umbral. |
| Barra de reducción de ganancia | Vacía / relleno ámbar / marca de −15 dB | Profundidad de atenuación mientras la puerta está cerrada. La escala máxima es 40 dB; una marca en −15 dB señala el piso predeterminado del expansor suave. |
| Opacidad del mosaico del applet | Opacidad total (habilitado) / ~55 % de opacidad (en bypass) | Indica de un vistazo si la etapa de puerta está procesando audio actualmente. |

## Consejos

- Observe la barra de reducción de ganancia mientras no habla (TX) o durante un momento de solo ruido de banda (RX). Si la barra no se llena, el Umbral está configurado por debajo del piso de ruido y la puerta no se activa. Consulte [Observe la GR en vivo mientras no habla](watch-live-gr-while-not-speaking.md).
- La marca de −15 dB en la barra de reducción de ganancia señala el valor predeterminado del Piso. Si la barra se llena completamente más allá de esa marca, el Piso está configurado más profundo que −15 dB o la Relación es lo suficientemente alta como para llevar la reducción más allá de ese punto.
- Use la banda de histéresis cian en la curva de transferencia para evaluar si el valor de Vuelta es lo suficientemente amplio para evitar el aleteo sin que la puerta sea lenta para cerrarse.
- Cuando el mosaico aparece atenuado, la etapa de puerta está en bypass. Vuelva a habilitarla a través del widget CHAIN o el editor flotante antes de esperar cualquier atenuación.
- Los cambios en cualquier perilla surten efecto de inmediato y se guardan automáticamente. No se necesita ningún botón Apply.

## Solución de problemas

- **El applet no es visible** — La etapa de puerta no se ha habilitado en ese lado. Habilítela a través del widget CHAIN o el editor flotante para el lado TX o RX.
- **El mosaico del applet aparece atenuado** — La etapa de puerta está en bypass. El mosaico se renderiza con opacidad reducida cuando el bypass está activo. Habilite la etapa a través del widget CHAIN o el editor flotante para restaurar el procesamiento completo y el brillo total del mosaico.
- **La puerta no atenúa el ruido entre palabras** — El Umbral puede estar configurado demasiado bajo, por debajo del piso de ruido ambiental. Suba el Umbral hasta que la barra de reducción de ganancia muestre movimiento durante el silencio. Consulte [Establezca el umbral TX justo por encima del piso de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md).
- **La puerta aletea rápidamente cerca del umbral** — La Vuelta está configurada demasiado baja. Aumente la Vuelta para que la puerta no se vuelva a abrir hasta que la señal esté claramente por encima del Umbral, ampliando la banda muerta mostrada por la banda cian en la curva de transferencia.
- **Silencio antinatural entre palabras** — El Piso está configurado demasiado profundo. Suba el Piso hacia 0 dB para que pase algo de audio residual durante los períodos cerrados. Consulte [Establezca el Piso para evitar el silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md).
- **Las posiciones de las perillas en el mosaico no coinciden con el editor flotante** — El mosaico se sincroniza cada ~33 ms. Si parecen no coincidir inmediatamente después de abrir el editor, espere un ciclo de actualización o mueva una perilla para forzar una sincronización.
- **Recorte o vibración de las etiquetas de los ejes en la curva de transferencia** — Este problema se ha resuelto en v26.5.1. La curva ahora utiliza texto estático en caché para las etiquetas de los ejes, mejorando el rendimiento de renderizado y evitando el movimiento de las etiquetas durante las transiciones de modo compacto.

## Relacionados

- [Establezca el umbral TX justo por encima del piso de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md)
- [Use AGC-T en RX para suprimir el ruido de banda por debajo de un piso seleccionado](use-agc-t-on-rx-to-suppress-band-noise-below-a-chosen-floor.md)
- [Elija el comportamiento de puerta vs. expansor suave mediante la relación](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Establezca el Piso para evitar el silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Observe la GR en vivo mientras no habla](watch-live-gr-while-not-speaking.md)
- [Ponga en bypass la puerta desde la cadena](bypass-the-gate-from-the-chain.md)
