# Descripción general de Aetherial Compressor (TX) / Aetherial AGC-C (RX)

AetherSDR incluye un compresor de rango dinámico del lado del cliente que opera en dos instancias independientes: **Aetherial Compressor** en la ruta de TX y **Aetherial AGC-C** en la ruta de RX. Use la instancia de TX para controlar los picos de voz antes de transmitir; use la instancia de RX para igualar los niveles de audio recibido.

## Antes de comenzar

- Ambas instancias se encuentran dentro del contenedor principal **Aetherial Audio (TXDSP)** en el panel de applets. Cada mosaico permanece oculto hasta que su etapa esté habilitada — desactívela mediante el widget CHAIN o el editor flotante del lado correspondiente.
- No se requiere conexión a una radio para configurar el compresor. Los ajustes se guardan localmente.

## Cómo funciona

Cada instancia procesa el audio de forma independiente. El compresor monitorea el nivel de la señal de entrada. Cuando el nivel supera el umbral, atenúa la salida según la relación de compresión elegida. Attack y Release controlan la velocidad de reacción. Makeup recupera la ganancia perdida por la compresión. Un limitador opcional (configurado en el editor completo) establece un techo rígido en la salida.

El mosaico del applet para cada instancia muestra:

- Una **curva de transferencia** — un gráfico estático de entrada/salida con una bola de envolvente en tiempo real que se desplaza a lo largo de la curva, indicando el punto de operación actual.
- Una **barra de reducción de ganancia** — una franja horizontal ámbar que se llena desde la derecha. La escala va de 0 a 20 dB de reducción de ganancia. Una marca señala el punto de −6 dB como referencia de trabajo típica. La franja se actualiza a aproximadamente 30 Hz.

Para abrir el editor completo de cualquiera de las instancias — que agrega controles de knee y limitador no disponibles en el applet — haga doble clic en la etapa COMP del widget CHAIN en el lado TX o RX. El editor se abre con el título **Aetherial Compressor — TX** o **Aetherial Compressor — RX** según corresponda.

## Qué hace cada control

Los cinco mandos aparecen en fila en la parte inferior de cada mosaico del applet. Tanto la instancia de TX (Aetherial Compressor) como la de RX (Aetherial AGC-C) comparten el mismo diseño de mandos con estados independientes.

| Mando | Valor predeterminado | Rango válido | Clave de ajuste TX | Clave de ajuste RX | Comportamiento |
|---|---|---|---|---|---|
| Thresh | −18.0 dB | −60.0 a 0.0 dB | `ClientCompTxThresholdDb` | `ClientCompRxThresholdDb` | Establece el nivel a partir del cual comienza la compresión. Mapeado de forma lineal. La etiqueta muestra el valor como `-18.0 dB`. |
| Ratio | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` | `ClientCompRxRatio` | Establece con qué fuerza se controlan los picos una vez superado el umbral. Mapeado de forma logarítmica. La etiqueta muestra el valor como `X.XX:1`. |
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` | `ClientCompRxAttackMs` | Establece la rapidez con que el compresor actúa tras superar el umbral. Mapeado de forma exponencial. La etiqueta muestra `X.X ms` por debajo de 10, `X ms` por encima. |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` | `ClientCompRxReleaseMs` | Establece la rapidez con que la ganancia se recupera cuando la entrada cae por debajo del umbral. Mapeado de forma exponencial. La etiqueta muestra `X ms`. |
| Makeup | 0.0 dB | −12.0 a 24.0 dB | `ClientCompTxMakeupDb` | `ClientCompRxMakeupDb` | Recupera la ganancia perdida por la compresión. La etiqueta muestra un signo `+` explícito para valores positivos. |

Ajustes adicionales gestionados únicamente desde el editor completo:

| Clave de ajuste (TX) | Clave de ajuste (RX) | Descripción |
|---|---|---|
| `ClientCompTxEnabled` | `ClientCompRxEnabled` | Indica si la etapa del compresor está activa (bypass desactivado). |
| `ClientCompTxKneeDb` | `ClientCompRxKneeDb` | Ancho del knee suave en dB. Ajustable en el editor flotante. |
| `ClientCompTxLimEnabled` | `ClientCompRxLimEnabled` | Indica si el limitador de salida está activo. |
| `ClientCompTxLimCeilingDb` | `ClientCompRxLimCeilingDb` | Techo rígido aplicado por el limitador. |

## Consejos

- La bola de envolvente en la curva de transferencia ofrece retroalimentación visual continua. Si la bola permanece bien por encima del knee en reposo, el umbral está demasiado bajo — suba Thresh hasta que la bola solo cruce el knee en los picos.
- La marca de −6 dB en la barra de reducción de ganancia es un punto de referencia útil. Un relleno ámbar constante hasta esa marca, o ligeramente más allá, indica una compresión activa y moderada. Si el relleno alcanza el borde derecho de la barra, el compresor está trabajando a 20 dB de reducción o más.
- Las instancias de TX y RX son completamente independientes. Los cambios en Aetherial Compressor (TX) no afectan a Aetherial AGC-C (RX) y viceversa.
- Los controles de knee y limitador no están disponibles en el mosaico del applet. Abra el editor completo para acceder a ellos.

## Temas relacionados

- [Ajustar el umbral del compresor (lado TX o RX)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Establecer la relación de compresión para voz (TX) o para audio recibido (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Ajustar attack y release para un sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de makeup tras la compresión](apply-make-up-gain-after-compression.md)
- [Observar la reducción de ganancia en tiempo real al hablar o escuchar](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Poner en bypass el compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
- [Abrir el editor completo del compresor para los controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
