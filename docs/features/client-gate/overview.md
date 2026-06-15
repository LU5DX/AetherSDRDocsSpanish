# Aetherial TX Gate / Aetherial AGC-G (RX) — Resumen general

AetherSDR incluye un expansor descendente y un puerta de ruido del lado del cliente que funciona de forma independiente en las rutas de audio de transmisión y recepción. Úselo para suprimir el ruido de fondo entre palabras en TX, o para reducir el ruido de banda por debajo de un piso seleccionado en RX.

## Antes de comenzar

- La etapa Gate debe habilitarse a través del widget CHAIN o el editor flotante en el lado correspondiente antes de que el applet sea visible.
- AetherSDR no necesita estar conectado a una radio para ajustar los controles de la puerta, pero el audio debe estar funcionando para que los indicadores en vivo tengan sentido.

## Cómo funciona

AetherSDR crea dos copias completamente independientes del applet de puerta:

- **Aetherial TX Gate** — actúa sobre el audio de transmisión saliente. Se encuentra en el contenedor principal Aetherial Audio (TXDSP).
- **Aetherial AGC-G** — actúa sobre el audio de recepción entrante. Se encuentra en el mismo contenedor principal como un subcontenedor separado.

Ambas copias comparten controles e indicadores idénticos. La configuración de cada lado se almacena de forma independiente. Los cambios realizados en el mosaico del applet acoplado y los cambios realizados en el editor flotante se mantienen sincronizados; el applet consulta el motor aproximadamente cada 33 ms y actualiza las posiciones de las perillas y la barra de reducción de ganancia para reflejar el lado activo.

### Flujo de señal

La puerta es un **expansor descendente**. Cuando el nivel de entrada cae por debajo del punto Thresh, la puerta atenúa la señal. La cantidad de atenuación depende de Ratio, y el corte máximo permitido se establece mediante Floor. Return establece una banda muerta de histéresis: la puerta se abre cuando la señal supera Thresh y no se cierra de nuevo hasta que la señal cae por debajo de Thresh − Return. Release controla la rapidez con la que se cierra la puerta una vez que la señal cae por debajo de ese límite inferior.

Configurar Ratio en un valor bajo (cerca de 1.0:1) produce un efecto suave de expansor descendente que reduce gradualmente el nivel. Configurar Ratio en un valor alto (cerca de 10.0:1) produce una puerta fuerte que corta de forma agresiva.

### Atenuación por bypass

Cuando la etapa de puerta está en bypass, todo el mosaico del applet se renderiza con opacidad reducida (aproximadamente el 55 % del brillo total). Esto coincide con el efecto de atenuación utilizado en la curva EQ y ofrece una indicación clara de un vistazo de que la etapa no está procesando audio. El mosaico vuelve a la opacidad total tan pronto como se vuelve a habilitar la etapa.

### Abrir el applet

Haga doble clic en la etapa GATE en el widget CHAIN en el lado TX o RX para abrir el editor flotante correspondiente, titulado **Aetherial Gate — TX** o **Aetherial Gate — RX**. Las barras de título de los subcontenedores acoplados para **Aetherial TX Gate** y **Aetherial AGC-G** se pueden hacer clic derecho para flotar, extraer u ocultar el mosaico.

## Qué hace cada control

Los controles listados a continuación aparecen de forma idéntica tanto en los applets TX como RX. Las claves de configuración mostradas corresponden al lado TX; el lado RX usa las claves equivalentes `ClientGateRx*`.

| Control | Tipo | Predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|---|
| Curva de transferencia | Indicador | — | — | — | ClientGateCurveWidget en modo compacto. Grafica la curva de transferencia estática del expansor y una bola en vivo en el nivel de entrada actual. |
| Barra de reducción de ganancia | Medidor | — | 0 a 40 dB GR | — | Barra horizontal ámbar, relleno desde la derecha. La escala máxima es de 40 dB (las puertas pueden cortar muy profundo); una marca en -15 dB señala el piso predeterminado del expansor suave. |
| Thresh | Perilla | −40.0 dB | −80.0 a 0.0 dB | `ClientGateTxThresholdDb` | Mapeo lineal. Nivel por debajo del cual la puerta comienza a atenuar. |
| Ratio | Perilla | 2.0:1 | 1.0 a 10.0 | `ClientGateTxRatio` | Mapeo lineal. Las relaciones más altas producen un corte más fuerte, similar a una puerta; las relaciones más bajas actúan como un expansor descendente suave. La etiqueta se muestra como 'X.X:1'. |
| Return | Perilla | 2.0 dB | 0.0 a 20.0 dB | `ClientGateTxReturnDb` | Mapeo lineal (n * 20). Establece la banda muerta de histéresis: la puerta se abre por encima de Thresh y no se vuelve a cerrar hasta que la entrada cae por debajo de Thresh − Return, evitando el aleteo rápido cerca del umbral. La etiqueta se muestra como 'X.XX dB'. El widget de curva dibuja una banda vertical cian claro entre (Thresh − Return) y Thresh para hacer visible la zona de adherencia. |
| Release | Perilla | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` | Mapeo exponencial (5 * 400^n). Establece la rapidez con la que se cierra la puerta después de que la entrada cae por debajo de Thresh − Return. La etiqueta muestra 'X.X ms' por debajo de 100, 'X ms' por encima. |
| Floor | Perilla | −15.0 dB | −80.0 a 0.0 dB | `ClientGateTxFloorDb` | Mapeo lineal. Atenuación máxima que la puerta puede aplicar. |
| Flip (Expander / Gate) | Alternar | Desmarcado (Expander) | — | — | Control solo en editor (ClientGateEditor flotante). Desmarcado = expansor descendente (suave, basado en ratio). Marcado = Gate (corte fuerte). Ajusta Ratio y Floor a pares predefinidos al alternar; las otras perillas permanecen en su lugar. La etiqueta se actualiza en vivo entre 'Expander' y 'Gate'. Color: desmarcado = verde (Expander), marcado = ámbar (Gate). Tooltip: 'Alternar entre modos Expansor descendente (suave) y Puerta (fuerte). Ajusta ratio + floor a pares predefinidos; las otras perillas permanecen donde las dejó.' |
| Peek (lookahead) | Desplegable | Off | Off, 1 ms, 1.5 ms, 3 ms, 5 ms | — | Control solo en editor. Establece un retardo de prelectura para que la puerta pueda abrirse fraccionalmente antes de que llegue un transitorio, evitando bordes de ataque recortados. 'Off' deshabilita completamente la línea de retardo. Los valores más altos aumentan la latencia en la ruta TX. 1 y 1.5 ms coinciden con las opciones predefinidas de Ableton; se agregaron 3 y 5 ms para transitorios muy rápidos. |
| Attack | Perilla | 0.50 ms | 0.1 a 100 ms | `ClientGateTxAttackMs` | Control solo en editor. Mapeo exponencial (0.1 * 1000^n). Establece la rapidez con la que se abre la puerta después de que la entrada supera Thresh. La etiqueta muestra 'X.XX ms' por debajo de 10 ms, 'X.X ms' por encima. |
| Hold | Perilla | 0.0 ms | 0.0 a 500 ms | `ClientGateTxHoldMs` | Control solo en editor. Mapeo lineal (n * 500). Después de que la entrada cae por debajo de Thresh − Return, la puerta permanece abierta durante este tiempo antes de comenzar a cerrarse, evitando el aleteo en material rítmico. La etiqueta muestra 'X.X ms'. |

El estado de habilitación/bypass de cada lado se conserva bajo `ClientGateTxEnabled` (TX) y `ClientGateRxEnabled` (RX).

## Edición de valor en línea

Las perillas en el mosaico del applet admiten la entrada numérica directa. Haga clic en el texto del valor debajo de una perilla para activar un editor en línea que se ve idéntico a la etiqueta de valor pintada. Escriba un número y presione Enter o haga clic en otro lugar para confirmar el valor. El valor se ajusta al rango válido de la perilla. Presione Escape para cancelar la edición y revertir al valor anterior.

El editor en línea está disponible en todos los controles de perilla tanto en los mosaicos TX como RX.

## Indicadores visuales

| Indicador | Estados | Significado |
|---|---|---|
| Bola de entrada | Debajo del umbral / sobre el umbral | Muestra si la puerta está actualmente abierta o cerrada. |
| Banda de histéresis | Ausente (Return = 0) / banda vertical cian claro | Visualiza la banda muerta de Return en el eje de entrada de la curva de transferencia — la zona de adherencia de la puerta entre (Thresh − Return) y Thresh. |
| Barra de reducción de ganancia | Vacía / relleno ámbar / marca de -15 dB | Profundidad de atenuación mientras la puerta está cerrada. La escala máxima es de 40 dB; una marca en -15 dB señala el piso predeterminado del expansor suave. |
| Opacidad del mosaico del applet | Opacidad completa (habilitado) / ~55 % de opacidad (en bypass) | Indica de un vistazo si la etapa de puerta está procesando audio actualmente. |

## Colores de perillas adaptables al tema

Los componentes de las perillas ahora leen del sistema de colores del tema en lugar de usar colores fijos. Los siguientes roles de color controlan la apariencia de las perillas:

- **`color.knob.background`** — Color del anillo de fondo.
- **`color.knob.foreground`** — Color del arco de valor.
- **`color.knob.handle`** — Color del puntero/indicador.
- **`color.text.secondary`** — Color del texto de la etiqueta de la perilla.
- **`color.text.primary`** — Color del texto del valor de la perilla.

El contenedor del applet de puerta está registrado bajo la ruta de tema `applet/gate`, lo que permite anulaciones de tema por applet. Esto permite que el color de primer plano ámbar de la perilla utilizado en la curva de transferencia y la barra de reducción de ganancia de la puerta se estilice independientemente de las perillas en otros applets.

## Optimizaciones de animación (v26.6.3)

El temporizador de suavizado del medidor ahora se detiene cuando el valor de reducción de ganancia se ha estabilizado, y solo activa un repintado cuando es necesario. Esto reduce el uso de CPU cuando la puerta no está atenuando audio activamente. La bola de entrada en vivo y la barra de reducción de ganancia continúan actualizándose normalmente durante la compuerta activa.

## Consejos

- Observe la barra de reducción de ganancia mientras no habla (TX) o durante un momento de solo ruido de banda (RX). Si la barra no se llena, Thresh está configurado por debajo del piso de ruido y la puerta no se está activando. Consulte [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md).
- La marca de -15 dB en la barra de reducción de ganancia señala el Floor predeterminado. Si la barra se llena completamente más allá de esa marca, Floor está configurado más profundo que -15 dB o Ratio es lo suficientemente alto como para empujar la reducción más allá de él.
- Use la banda de histéresis cian en la curva de transferencia para juzgar si el valor de Return es lo suficientemente amplio para evitar el aleteo sin hacer que la puerta sea lenta para cerrarse.
- Cuando el mosaico aparece atenuado, la etapa de puerta está en bypass. Vuelva a habilitarla a través del widget CHAIN o el editor flotante antes de esperar cualquier atenuación.
- Los cambios en cualquier perilla surten efecto de inmediato y se guardan automáticamente. No se necesita un botón Apply.
- Para ingresar un valor numérico preciso, haga clic en el texto del valor debajo de cualquier perilla y escriba el número directamente.

## Solución de problemas

- **El applet no es visible** — La etapa Gate no se ha habilitado en ese lado. Habilítela a través del widget CHAIN o el editor flotante para el lado TX o RX.
- **El mosaico del applet aparece atenuado** — La etapa de puerta está en bypass. El mosaico se renderiza con opacidad reducida cuando el bypass está activo. Habilite la etapa a través del widget CHAIN o el editor flotante para restaurar el procesamiento completo y el brillo total del mosaico.
- **La puerta no está atenuando el ruido entre palabras** — Thresh puede estar configurado demasiado bajo, por debajo del piso de ruido ambiente. Suba Thresh hasta que la barra de reducción de ganancia muestre movimiento durante el silencio. Consulte [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md).
- **La puerta aletea rápidamente cerca del umbral** — Return está configurado demasiado bajo. Aumente Return para que la puerta no se vuelva a abrir hasta que la señal esté claramente por encima de Thresh, ampliando la banda muerta mostrada por la banda cian en la curva de transferencia.
- **Silencio antinatural entre palabras** — Floor está configurado demasiado profundo. Suba Floor hacia 0 dB para que pase algo de audio residual durante los períodos de cierre. Consulte [Set Floor to avoid unnatural silence between words](set-floor-to-avoid-unnatural-silence-between-words.md).
- **Las posiciones de las perillas en el mosaico no coinciden con el editor flotante** — El mosaico se sincroniza cada ~33 ms. Si parecen no coincidir inmediatamente después de abrir el editor, espere un ciclo de actualización o mueva una perilla para forzar una sincronización.
- **Recorte o vibración de la etiqueta del eje en la curva de transferencia** — Este problema se ha resuelto en v26.5.1. La curva ahora usa texto estático en caché para las etiquetas de los ejes, mejorando el rendimiento de renderizado y evitando el movimiento de las etiquetas durante las transiciones de modo compacto.

## Relacionados

- [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md)
- [Use AGC-G on RX to suppress band noise below a chosen floor](use-agc-g-on-rx-to-suppress-band-noise-below-a-chosen-floor.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Set Floor to avoid unnatural silence between words](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md)
- [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md)
