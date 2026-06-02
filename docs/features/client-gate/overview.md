# Descripción general de Aetherial TX Gate / Aetherial AGC-T (RX)

AetherSDR incluye un expansor descendente y una compuerta de ruido del lado del cliente que se ejecuta de forma independiente tanto en la ruta de audio de transmisión como en la de recepción. Úselo para suprimir el ruido de fondo entre palabras en TX, o para reducir el ruido de banda por debajo de un umbral elegido en RX.

## Antes de comenzar

- La etapa Gate debe habilitarse a través del widget CHAIN o del editor flotante en el lado correspondiente antes de que el applet se vuelva visible.
- AetherSDR no necesita estar conectado a una radio para ajustar los controles de la compuerta, pero el audio debe estar en ejecución para que los indicadores en vivo tengan sentido.

## Cómo funciona

AetherSDR crea dos copias completamente independientes del applet de compuerta:

- **Aetherial TX Gate**: actúa sobre el audio de transmisión saliente. Se encuentra en el contenedor principal Aetherial Audio (TXDSP).
- **Aetherial AGC-T**: actúa sobre el audio de recepción entrante. Se encuentra en el mismo contenedor principal como un subcontenedor separado.

Ambas copias comparten controles e indicadores idénticos. La configuración de cada lado se almacena de forma independiente. Los cambios realizados en el mosaico del applet acoplado y los cambios realizados en el editor flotante se mantienen sincronizados; el applet consulta el motor aproximadamente cada 33 ms y actualiza las posiciones de las perillas y la barra de reducción de ganancia para reflejar el lado que esté activo.

### Flujo de señal

La compuerta es un **expansor descendente**. Cuando el nivel de entrada cae por debajo del punto Thresh, la compuerta atenúa la señal. La cantidad de atenuación depende de Ratio, y el corte más profundo permitido está definido por Floor. Return establece una banda muerta de histéresis: la compuerta se abre cuando la señal supera Thresh y no se vuelve a cerrar hasta que la señal cae por debajo de Thresh − Return. Release controla la rapidez con la que se cierra la compuerta una vez que la señal cae por debajo de ese límite inferior.

Establecer Ratio en un valor bajo (cerca de 1.0:1) produce un efecto suave de expansor que reduce gradualmente el nivel. Establecer Ratio en un valor alto (cerca de 10.0:1) produce una compuerta fuerte que corta de forma agresiva.

### Atenuación por derivación

Cuando la etapa de compuerta está derivada, todo el mosaico del applet se renderiza con opacidad reducida (aproximadamente el 55 % del brillo completo). Esto coincide con el efecto de atenuación utilizado en la curva EQ y proporciona una indicación clara de un vistazo de que la etapa no está procesando audio. El mosaico vuelve a la opacidad completa tan pronto como se vuelve a habilitar la etapa.

### Abrir el applet

Haga doble clic en la etapa GATE en el widget CHAIN del lado TX o RX para abrir el editor flotante correspondiente, titulado **Aetherial Gate — TX** o **Aetherial Gate — RX**. Las barras de título del subcontenedor acoplado para **Aetherial TX Gate** y **Aetherial AGC-T** se pueden hacer clic derecho para flotar, desacoplar u ocultar el mosaico.

## Qué hace cada control

Los controles que se enumeran a continuación aparecen de forma idéntica tanto en los applets de TX como de RX. Las claves de configuración mostradas se aplican al lado TX; el lado RX utiliza las claves equivalentes `ClientGateRx*`.

| Control | Tipo | Valor predeterminado |
|---|---|---|
| Transfer curve | Indicador | — |
| Gain-reduction bar | Medidor | — |
| Thresh | Perilla | −40.0 dB |
| Ratio | Perilla | 2.0:1 |
| Return | Perilla | 2.0 dB |
| Release | Perilla | 100 ms |
| Floor | Perilla | −15.0 dB |
| Flip (Expander / Gate) | Sin marcar = expansor descendente (suave, basado en ratio). Marcado = Gate (corte fuerte). Ajusta ratio y floor a pares predefinidos al alternar; las otras perillas permanecen en su lugar. La etiqueta se actualiza en vivo entre 'Expander' y 'Gate'. | Control solo del editor (ClientGateEditor flotante). Color: sin marcar = verde (Expander), marcado = ámbar (Gate). Información sobre herramientas: 'Cambiar entre modos Expander descendente (suave) y Gate (fuerte). Ajusta ratio + floor a pares predefinidos; las otras perillas se quedan donde las dejó.' |
| Peek (lookahead) | Establece un retardo de prelectura para que la compuerta pueda abrirse fraccionalmente antes de que llegue un transitorio, evitando bordes de ataque recortados. 'Off' desactiva por completo la línea de retardo. | Control solo del editor. Los valores más altos aumentan la latencia en la ruta TX. 1 y 1.5 ms coinciden con las opciones predefinidas de Ableton; se agregaron 3 y 5 ms para transitorios muy rápidos. |
| Attack | Mapeo exponencial (0.1 * 1000^n). Establece la rapidez con la que se abre la compuerta después de que la entrada supera Thresh. | Control solo del editor. Etiqueta 'X.XX ms' por debajo de 10 ms, 'X.X ms' por encima. |
| Hold | Mapeo lineal (n * 500). Después de que la entrada cae por debajo de Thresh − Return, la compuerta permanece abierta durante este tiempo antes de comenzar a cerrarse, evitando vibraciones en material rítmico. | Control solo del editor. Etiqueta 'X.X ms'. |

El estado de habilitación/derivación de cada lado se conserva bajo `ClientGateTxEnabled` (TX) y `ClientGateRxEnabled` (RX).

## Edición de valor en línea

Las perillas en el mosaico del applet admiten la entrada numérica directa. Haga clic en el texto del valor debajo de una perilla para activar un editor en línea que se ve idéntico a la etiqueta de valor pintada. Escriba un número y presione Enter o haga clic en otro lugar para confirmar el valor. El valor se limita al rango válido de la perilla. Presione Escape para cancelar la edición y volver al valor anterior.

El editor en línea está disponible en todos los controles de perilla tanto en los mosaicos del applet TX como RX.

## Indicadores visuales

| Indicador | Estados | Significado |
|---|---|---|
| Bola de entrada | Por debajo del umbral / por encima del umbral | Muestra si la compuerta está actualmente abierta o cerrada. |
| Banda de histéresis | Ausente (Return = 0) / banda vertical cian suave | Visualiza la banda muerta de Return en el eje de entrada de la curva de transferencia: la zona pegajosa de la compuerta entre (Thresh − Return) y Thresh. |
| Barra de reducción de ganancia | Vacía / relleno ámbar / marca de −15 dB | Profundidad de atenuación mientras la compuerta está cerrada. La escala máxima es de 40 dB; una marca en −15 dB señala el floor predeterminado del expansor suave. |
| Opacidad del mosaico del applet | Opacidad completa (habilitado) / ~55 % de opacidad (derivado) | Indica de un vistazo si la etapa de compuerta está procesando audio actualmente. |

## Colores de perilla sensibles al tema

Los componentes de las perillas ahora leen del sistema de colores del tema en lugar de usar colores fijos. Los siguientes roles de color controlan la apariencia de las perillas:

- **`color.knob.background`**: Color del anillo de fondo.
- **`color.knob.foreground`**: Color del arco de valor.
- **`color.knob.handle`**: Color del puntero/indicador.
- **`color.text.secondary`**: Color del texto de la etiqueta de la perilla.
- **`color.text.primary`**: Color del texto del valor de la perilla.

El contenedor del applet de compuerta está registrado bajo la ruta de tema `applet/gate`, lo que permite anulaciones de tema por applet. Esto permite que el color de primer plano ámbar de la perilla utilizado en la curva de transferencia y la barra de reducción de ganancia de la compuerta se estilice independientemente de las perillas en otros applets.

## Consejos

- Observe la barra de reducción de ganancia mientras no habla (TX) o durante un momento de solo ruido de banda (RX). Si la barra no se llena, Thresh está configurado por debajo del piso de ruido y la compuerta no se está activando. Consulte [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md).
- La marca de −15 dB en la barra de reducción de ganancia marca el Floor predeterminado. Si la barra se llena completamente más allá de esa marca, Floor está configurado más profundo que −15 dB o Ratio es lo suficientemente alto como para llevar la reducción más allá de ese punto.
- Use la banda de histéresis cian en la curva de transferencia para juzgar si el valor de Return es lo suficientemente amplio para evitar vibraciones sin hacer que la compuerta sea lenta para cerrarse.
- Cuando el mosaico aparece atenuado, la etapa de compuerta está derivada. Vuelva a habilitarla a través del widget CHAIN o del editor flotante antes de esperar cualquier atenuación.
- Los cambios en cualquier perilla surten efecto de inmediato y se guardan automáticamente. No se necesita ningún botón Apply.
- Para ingresar un valor numérico preciso, haga clic en el texto del valor debajo de cualquier perilla y escriba el número directamente.

## Solución de problemas

- **El applet no es visible**: la etapa Gate no se ha habilitado en ese lado. Habilítela a través del widget CHAIN o del editor flotante para el lado TX o RX.
- **El mosaico del applet aparece atenuado**: la etapa de compuerta está derivada. El mosaico se renderiza con opacidad reducida cuando la derivación está activa. Habilite la etapa a través del widget CHAIN o del editor flotante para restaurar el procesamiento completo y el brillo completo del mosaico.
- **La compuerta no atenúa el ruido entre palabras**: Thresh puede estar configurado demasiado bajo, por debajo del piso de ruido ambiental. Suba Thresh hasta que la barra de reducción de ganancia muestre movimiento durante el silencio. Consulte [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md).
- **La compuerta vibra rápidamente cerca del umbral**: Return está configurado demasiado bajo. Aumente Return para que la compuerta no se vuelva a abrir hasta que la señal esté claramente por encima de Thresh, ampliando la banda muerta mostrada por la banda cian en la curva de transferencia.
- **Silencio antinatural entre palabras**: Floor está configurado demasiado profundo. Suba Floor hacia 0 dB para que pase algo de audio residual durante los períodos cerrados. Consulte [Set Floor to avoid unnatural silence between words](set-floor-to-avoid-unnatural-silence-between-words.md).
- **Las posiciones de las perillas en el mosaico no coinciden con el editor flotante**: el mosaico se sincroniza cada ~33 ms. Si parecen desajustados inmediatamente después de abrir el editor, espere un ciclo de actualización o mueva una perilla para forzar una sincronización.
- **Recorte o vibración de la etiqueta del eje en la curva de transferencia**: este problema se ha resuelto en v26.5.1. La curva ahora utiliza texto estático en caché para las etiquetas de los ejes, lo que mejora el rendimiento de renderizado y evita el movimiento de las etiquetas durante las transiciones de modo compacto.

## Relacionados

- [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md)
- [Use AGC-T on RX to suppress band noise below a chosen floor](use-agc-t-on-rx-to-suppress-band-noise-below-a-chosen-floor.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Set Floor to avoid unnatural silence between words](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md)
- [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md)
