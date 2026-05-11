# Resumen del Compresor Aetherial (TX) / AGC-C Aetherial (RX)

AetherSDR incluye un compresor de rango dinámico del lado del cliente que se ejecuta en dos instancias independientes: **Compresor Aetherial** en la ruta de TX y **AGC-C Aetherial** en la ruta de RX. Use la instancia de TX para controlar los picos de voz antes de transmitir; use la instancia de RX para uniformar los niveles de audio recibido.

## Antes de comenzar

- Ambas instancias residen dentro del contenedor principal **Aetherial Audio (TXDSP)** en el panel de applets. Cada mosaico permanece oculto hasta que su etapa se habilita — desvíelo (bypass) mediante el widget CHAIN o el editor flotante en el lado correspondiente.
- No se requiere conexión de radio para configurar el compresor. Los ajustes se guardan localmente.

## Cómo funciona

Cada instancia procesa el audio de forma independiente. El compresor monitorea el nivel de la señal de entrada. Cuando el nivel supera el umbral, atenúa la salida según la relación de compresión que usted elija. Ataque y Liberación controlan la rapidez de su reacción. Maquillaje (Makeup) añade la ganancia perdida por la compresión. Un limitador opcional (configurado en el editor completo) establece un techo duro en la salida.

El mosaico del applet para cada instancia muestra:

- Una **curva de transferencia** — un gráfico estático de entrada/salida con una bola de envolvente en vivo que se desplaza a lo largo de la curva en tiempo real, mostrando el punto de operación actual.
- Una **barra de reducción de ganancia** — una franja horizontal de color ámbar que se llena desde la derecha. La escala va de 0 a 20 dB de reducción de ganancia. Una marca indica el punto de −6 dB como referencia de trabajo típica. La franja se actualiza a aproximadamente 30 Hz.

Cuando una etapa del compresor está desviada (bypassed), todo su mosaico del applet se atenúa hasta aproximadamente un 55 % de opacidad. El mosaico vuelve a la opacidad completa cuando la etapa se reactiva. Este estado visual coincide con el comportamiento de atenuación utilizado por el applet de la curva de EQ.

Para abrir el editor completo de cualquiera de las dos instancias — que añade controles de rodilla (knee) y limitador no disponibles en el applet — haga doble clic en la etapa COMP en el widget CHAIN del lado TX o RX. El editor se abre con el título **Aetherial Compressor — TX** o **Aetherial Compressor — RX** según corresponda.

## Qué hace cada control

Los cinco mandos aparecen en una fila en la parte inferior de cada mosaico del applet. Tanto la instancia de TX (Compresor Aetherial) como la de RX (AGC-C Aetherial) comparten la misma disposición de mandos con estado independiente.

| Mando | Valor predeterminado | Rango válido | Clave de ajuste TX | Clave de ajuste RX | Comportamiento |
|---|---|---|---|---|---|
| Thresh | −18.0 dB | −60.0 a 0.0 dB | `ClientCompTxThresholdDb` | `ClientCompRxThresholdDb` | Establece el nivel por encima del cual comienza la compresión. Mapeo lineal. La etiqueta muestra el valor como `-18.0 dB`. |
| Ratio | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` | `ClientCompRxRatio` | Establece la intensidad con que se controlan los picos una vez superado el umbral. Mapeo logarítmico. La etiqueta muestra el valor como `X.XX:1`. |
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` | `ClientCompRxAttackMs` | Establece la rapidez con que el compresor actúa tras superar el umbral. Mapeo exponencial. La etiqueta muestra `X.X ms` por debajo de 10, `X ms` por encima. |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` | `ClientCompRxReleaseMs` | Establece la rapidez con que la ganancia regresa después de que la entrada vuelve a caer por debajo del umbral. Mapeo exponencial. La etiqueta muestra `X ms`. |
| Makeup | 0.0 dB | −12.0 a 24.0 dB | `ClientCompTxMakeupDb` | `ClientCompRxMakeupDb` | Añade la ganancia perdida por la compresión. La etiqueta muestra un signo `+` explícito para valores positivos. |

Ajustes adicionales que se gestionan solo a través del editor completo:

| Clave de ajuste (TX) | Clave de ajuste (RX) | Descripción |
|---|---|---|
| `ClientCompTxEnabled` | `ClientCompRxEnabled` | Indica si la etapa del compresor está activa (bypass desactivado). |
| `ClientCompTxKneeDb` | `ClientCompRxKneeDb` | Anchura de la rodilla suave (soft knee) en dB. Ajustable en el editor flotante. |
| `ClientCompTxLimEnabled` | `ClientCompRxLimEnabled` | Indica si el limitador de salida está activo. |
| `ClientCompTxLimCeilingDb` | `ClientCompRxLimCeilingDb` | Techo duro aplicado por el limitador. |

## Consejos

- La bola de envolvente en la curva de transferencia proporciona una retroalimentación visual continua. Si la bola se sitúa muy por encima de la rodilla en reposo, el umbral está demasiado bajo — suba Thresh hasta que la bola solo cruce la rodilla en los picos.
- La marca de −6 dB en la barra de reducción de ganancia es un punto de referencia útil. Un llenado ámbar constante hasta ese punto o ligeramente más allá indica una compresión activa y moderada. Un llenado que alcanza el borde derecho de la barra significa que el compresor está trabajando con una reducción de 20 dB o más.
- Cuando una etapa está desviada (bypassed), el mosaico se atenúa notablemente. Si el mosaico parece atenuado y los controles no responden, verifique que la etapa COMP no esté desviada en el widget CHAIN.
- Las instancias de TX y RX son completamente independientes. Los cambios en el Compresor Aetherial (TX) no afectan al AGC-C Aetherial (RX) y viceversa.
- Los controles de rodilla y limitador no están disponibles en el mosaico del applet. Abra el editor completo para acceder a ellos.

## Relacionados

- [Ajustar el umbral del compresor (lado TX o RX)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Establecer la relación de compresión para voz (TX) o para audio recibido (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Ajustar ataque/liberación para una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de maquillaje después de la compresión](apply-make-up-gain-after-compression.md)
- [Observar la reducción de ganancia en vivo mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Desviar el compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
- [Abrir el editor completo del compresor para controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
