# Visión general de Aetherial TX Gate / Aetherial AGC-G (RX)

AetherSDR incluye un expansor descendente y compuerta de ruido del lado del cliente que funciona de forma independiente tanto en la ruta de audio de transmisión como en la de recepción. Úselo para suprimir el ruido de fondo entre palabras en TX, o para reducir el ruido de banda por debajo de un umbral elegido en RX.

## Antes de comenzar

- La etapa Gate debe estar habilitada a través del widget CHAIN o el editor flotante en el lado correspondiente antes de que el applet sea visible.
- AetherSDR no necesita estar conectado a una radio para ajustar los controles de la compuerta, pero el audio debe estar funcionando para que los indicadores en vivo tengan sentido.

## Cómo funciona

AetherSDR crea dos copias completamente independientes del applet de compuerta:

- **Aetherial TX Gate** — actúa sobre el audio de transmisión saliente. Se encuentra en el contenedor principal Aetherial Audio (TXDSP).
- **Aetherial AGC-G** — actúa sobre el audio de recepción entrante. Se encuentra en el mismo contenedor principal como un subcontenedor separado.

Ambas copias comparten controles e indicadores idénticos. La configuración de cada lado se almacena de forma independiente. Los cambios realizados en el mosaico del applet acoplado y los cambios realizados en el editor flotante se mantienen sincronizados; el applet consulta el motor aproximadamente cada 33 ms y actualiza las posiciones de las perillas y la barra de reducción de ganancia para reflejar el lado que está activo.

### Flujo de señal

La compuerta es un **expansor descendente**. Cuando el nivel de entrada cae por debajo del punto Thresh, la compuerta atenúa la señal. La cantidad de atenuación depende de Ratio, y el corte más profundo permitido lo establece Floor. Return establece una banda muerta de histéresis: la compuerta se abre cuando la señal supera Thresh y no se cierra de nuevo hasta que la señal cae por debajo de Thresh − Return. Release controla la rapidez con la que se cierra la compuerta una vez que la señal cae por debajo de ese límite inferior.

Establecer Ratio en un valor bajo (cerca de 1.0:1) produce un efecto de expansor suave que reduce gradualmente el nivel. Establecer Ratio en un valor alto (cerca de 10.0:1) produce una compuerta dura que corta agresivamente.

### Atenuación por bypass

Cuando la etapa de compuerta está en bypass, todo el mosaico del applet se renderiza con opacidad reducida (aproximadamente el 55 % del brillo completo). Esto coincide con el efecto de atenuación utilizado en la curva de EQ y proporciona una indicación clara de un vistazo de que la etapa no está procesando audio. El mosaico vuelve a la opacidad completa tan pronto como se vuelve a habilitar la etapa.

### Abrir el applet

Haga doble clic en la etapa GATE en el widget CHAIN en el lado TX o RX para abrir el editor flotante correspondiente, titulado **Aetherial Gate — TX** o **Aetherial Gate — RX**. Las barras de título del subcontenedor acoplado para **Aetherial TX Gate** y **Aetherial AGC-G** se pueden hacer clic con el botón derecho para flotar, sacar u ocultar el mosaico.

## Qué hace cada control

Los controles listados a continuación aparecen de forma idéntica tanto en los applets de TX como de RX. Las claves de configuración mostradas se aplican al lado TX; el lado RX utiliza las claves equivalentes `ClientGateRx*`.

| Control | Tipo | Predeterminado | Rango Válido | Clave de Configuración | Comportamiento |
|---|---|---|---|---|---|
| Curva de transferencia | Indicador | — | — | — | ClientGateCurveWidget en modo compacto. Traza la curva de transferencia estática del expansor y una bola en vivo en el nivel de entrada actual. |
| Barra de reducción de ganancia | Medidor | — | 0 a 40 dB GR | — | Franja horizontal ámbar, relleno desde la derecha. La escala máxima es de 40 dB (las compuertas pueden cortar muy profundo); una marca en -15 dB señala el piso predeterminado del expansor suave. |
| Thresh | Perilla | −40.0 dB | −80.0 a 0.0 dB | `ClientGateTxThresholdDb` | Mapeo lineal. Nivel por debajo del cual la compuerta comienza a atenuar. |
| Ratio | Perilla | 2.0:1 | 1.0 a 10.0 | `ClientGateTxRatio` | Mapeo lineal. Ratios más altos proporcionan un corte más duro, similar a una compuerta; ratios más bajos actúan como un expansor descendente suave. La etiqueta se muestra como 'X.X:1'. |
| Return | Perilla | 2.0 dB | 0.0 a 20.0 dB | `ClientGateTxReturnDb` | Mapeo lineal (n * 20). Establece la banda muerta de histéresis: la compuerta se abre por encima de Thresh y no se cierra de nuevo hasta que la entrada cae por debajo de Thresh − Return, evitando el chattering rápido cerca del umbral. La etiqueta se muestra como 'X.XX dB'. El widget de la curva dibuja una banda vertical cian suave entre (Thresh − Return) y Thresh para hacer visible la zona de histéresis. |
| Release | Perilla | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` | Mapeo exponencial (5 * 400^n). Establece la rapidez con la que se cierra la compuerta después de que la entrada cae por debajo de Thresh − Return. La etiqueta muestra 'X.X ms' por debajo de 100, 'X ms' por encima. |
| Floor | Perilla | −15.0 dB | −80.0 a 0.0 dB | `ClientGateTxFloorDb` | Mapeo lineal. Atenuación máxima que la compuerta puede aplicar. |

El estado de habilitación/bypass para cada lado se conserva bajo `ClientGateTxEnabled` (TX) y `ClientGateRxEnabled` (RX).

## Edición de valor en línea

Las perillas en el mosaico del applet admiten la entrada numérica directa. Haga clic en el texto del valor debajo de una perilla para activar un editor en línea que se ve idéntico a la etiqueta de valor pintada. Escriba un número y presione Enter o haga clic en otro lugar para confirmar el valor. El valor se limita al rango válido de la perilla. Presione Escape para cancelar la edición y volver al valor anterior.

El editor en línea está disponible en todos los controles de perilla tanto en los mosaicos de los applets de TX como de RX.

## Indicadores visuales

| Indicador | Estados | Significado |
|---|---|---|
| Bola de entrada | Por debajo del umbral / por encima del umbral | Muestra si la compuerta está actualmente abierta o cerrada. |
| Banda de histéresis | Ausente (Return = 0) / banda vertical cian suave | Visualiza la banda muerta de Return en el eje de entrada de la curva de transferencia — la zona de histéresis de la compuerta entre (Thresh − Return) y Thresh. |
| Franja de reducción de ganancia | Vacía / relleno ámbar / marca de −15 dB | Profundidad de atenuación mientras la compuerta está cerrada. La escala máxima es de 40 dB; una marca en −15 dB señala el piso predeterminado del expansor suave. |
| Opacidad del mosaico del applet | Opacidad completa (habilitado) / ~55 % de opacidad (bypass) | Indica de un vistazo si la etapa de compuerta está procesando audio actualmente. |

## Colores de perilla adaptados al tema

Los componentes de las perillas ahora leen del sistema de colores del tema en lugar de usar colores fijos. Los siguientes roles de color controlan la apariencia de la perilla:

- **`color.knob.background`** — Color del anillo de fondo.
- **`color.knob.foreground`** — Color del arco de valor.
- **`color.knob.handle`** — Color del puntero/indicador.
- **`color.text.secondary`** — Color del texto de la etiqueta de la perilla.
- **`color.text.primary`** — Color del texto del valor de la perilla.

El contenedor del applet de compuerta está registrado bajo la ruta de tema `applet/gate`, lo que permite anulaciones de tema por applet. Esto permite que el color de primer plano de la perilla ámbar utilizado en la curva de transferencia y la barra de reducción de ganancia de la compuerta se estilice de forma independiente de las perillas en otros applets.

## Optimizaciones de animación (v26.7.4)

El temporizador de suavizado del medidor ahora activa un repintado en cada tic, incluso cuando el valor de reducción de ganancia se ha estabilizado. Esto garantiza que la bola de entrada en vivo y la barra de reducción de ganancia sigan siendo receptivas y muestren la información de nivel de audio más actualizada sin interrupciones.

## Consejos

- Observe la barra de reducción de ganancia mientras no habla (TX) o durante un momento de solo ruido de banda (RX). Si la barra no se llena, Thresh está configurado por debajo del piso de ruido y la compuerta no se está activando. Consulte [Ver GR en vivo mientras no habla](watch-live-gr-while-not-speaking.md).
- La marca de −15 dB en la barra de reducción de ganancia señala el valor predeterminado de Floor. Si la barra se llena completamente más allá de esa marca, Floor está configurado más profundo que −15 dB o Ratio es lo suficientemente alto como para llevar la reducción más allá de ese punto.
- Use la banda de histéresis cian en la curva de transferencia para juzgar si el valor de Return es lo suficientemente amplio para evitar el chattering sin hacer que la compuerta sea lenta para cerrarse.
- Cuando el mosaico aparece atenuado, la etapa de compuerta está en bypass. Vuelva a habilitarla a través del widget CHAIN o el editor flotante antes de esperar cualquier atenuación.
- Los cambios en cualquier perilla surten efecto de inmediato y se guardan automáticamente. No se necesita ningún botón Apply.
- Para ingresar un valor numérico preciso, haga clic en el texto del valor debajo de cualquier perilla y escriba el número directamente.

## Solución de problemas

- **El applet no es visible** — La etapa Gate no se ha habilitado en ese lado. Habilítela a través del widget CHAIN o el editor flotante para el lado TX o RX.
- **El mosaico del applet aparece atenuado** — La etapa de compuerta está en bypass. El mosaico se renderiza con opacidad reducida cuando el bypass está activo. Habilite la etapa a través del widget CHAIN o el editor flotante para restaurar el procesamiento completo y el brillo completo del mosaico.
- **La compuerta no está atenuando el ruido entre palabras** — Thresh puede estar configurado demasiado bajo, por debajo del piso de ruido ambiente. Suba Thresh hasta que la barra de reducción de ganancia muestre movimiento durante el silencio. Consulte [Establecer el umbral TX justo por encima del piso de ruido ambiente](set-tx-threshold-just-above-room-noise-floor.md).
- **La compuerta chacharea rápidamente cerca del umbral** — Return está configurado demasiado bajo. Aumente Return para que la compuerta no se vuelva a abrir hasta que la señal esté claramente por encima de Thresh, ampliando la banda muerta mostrada por la banda cian en la curva de transferencia.
- **Silencio antinatural entre palabras** — Floor está configurado demasiado profundo. Suba Floor hacia 0 dB para que pase algo de audio residual durante los períodos cerrados. Consulte [Establecer Floor para evitar silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md).
- **Las posiciones de las perillas en el mosaico no coinciden con el editor flotante** — El mosaico se sincroniza cada ~33 ms. Si parecen no coincidir inmediatamente después de abrir el editor, espere un ciclo de actualización o mueva una perilla para forzar una sincronización.
- **Recorte o vibración de las etiquetas de los ejes en la curva de transferencia** — Este problema se ha resuelto en v26.5.1. La curva ahora utiliza texto estático en caché para las etiquetas de los ejes, mejorando el rendimiento de renderizado y evitando el movimiento de las etiquetas durante las transiciones de modo compacto.

## Relacionado

- [Establecer el umbral TX justo por encima del piso de ruido ambiente](set-tx-threshold-just-above-room-noise-floor.md)
- [Usar AGC-G en RX para suprimir el ruido de banda por debajo de un umbral elegido](use-agc-g-on-rx-to-suppress-band-noise-below-a-chosen-floor.md)
- [Elegir comportamiento de compuerta vs expansor suave mediante ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Establecer Floor para evitar silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Ver GR en vivo mientras no habla](watch-live-gr-while-not-speaking.md)
- [Poner en bypass la compuerta desde la cadena](bypass-the-gate-from-the-chain.md)
