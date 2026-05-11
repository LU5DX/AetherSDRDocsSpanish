# Use AGC-G en RX para suprimir el ruido de banda por debajo de un piso seleccionado

El AGC-G Aetherial del lado RX (expansor descendente del lado cliente) atenúa el audio recibido que cae por debajo de un umbral que usted establece, permitiéndole silenciar el ruido de fondo de banda o estática entre señales, manteniendo intacto el audio deseado.

## Antes de comenzar

- Debe estar conectado a una radio FLEX-8600.
- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el Panel de Applets.
- La etapa Gate del lado RX debe estar habilitada a través del widget CHAIN (haga doble clic en la etapa GATE del lado RX para abrir su editor, o un clic para alternar bypass).

## Pasos

1. En el Panel de Applets, localice el subcontenedor **Aetherial AGC-G (RX)** dentro del contenedor principal Aetherial Audio (TXDSP). Si está oculto, haga doble clic en la etapa GATE del widget CHAIN en el lado RX para abrir el editor flotante (titulado "Aetherial Gate — RX").

2. Ajuste **Thresh** (predeterminado: -40.0 dB) hacia abajo hasta que el ruido de banda que desea suprimir quede por debajo del umbral. Observe la bola de entrada en vivo en la visualización de la curva de transferencia — cuando la bola está debajo de la línea de umbral, la compuerta está cerrada y se aplica atenuación.

3. Establezca **Floor** (predeterminado: -15.0 dB) en la atenuación máxima que desea aplicar al ruido de fondo. Un valor típico es de -15 a -20 dB — suficiente para silenciar el ruido sin que los espacios entre palabras suenen anormalmente silenciosos.

4. Ajuste **Ratio** (predeterminado: 2.0) para controlar la agresividad del corte de la compuerta:
   - Ratios más bajos (1.0–3.0) actúan como un expansor descendente suave — el ruido de fondo se desvanece de forma gradual.
   - Ratios más altos (5.0–10.0) crean una sensación de compuerta más dura y tradicional.

5. Establezca **Return** (predeterminado: 2.0 dB) para evitar aperturas y cierres rápidos cerca del umbral. Aparece una banda de histéresis cian en la curva de transferencia entre (Thresh − Return) y Thresh — la compuerta permanece abierta dentro de esta zona hasta que la entrada cae por debajo de ella, luego debe subir por encima de Thresh para reabrirse.

6. Ajuste **Release** (predeterminado: 100 ms) para controlar la rapidez con que se cierra la compuerta después de que la entrada caiga por debajo de Thresh − Return. Valores más largos (500–2000 ms) proporcionan un desvanecimiento más natural; valores más cortos (5–50 ms) pueden sonar abruptos.

## Qué hace cada control

| Control | Predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------------|-------|------------------------|----------------|
| Thresh | -40.0 dB | -80.0 a 0.0 dB | `ClientGateRxThresholdDb` | Nivel por debajo del cual la compuerta comienza a atenuar. Mapeo lineal. |
| Ratio | 2.0 | 1.0 a 10.0 | `ClientGateRxRatio` | Ratios más altos dan un corte más duro, similar a una compuerta; ratios más bajos actúan como un expansor descendente suave. Se muestra como "X.X:1". |
| Return | 2.0 dB | 0.0 a 20.0 dB | `ClientGateRxReturnDb` | Banda muerta de histéresis: la compuerta se abre por encima de Thresh y permanece abierta hasta que la entrada cae por debajo de Thresh − Return. Se muestra como "X.XX dB". El widget de curva de transferencia dibuja una banda vertical cian suave entre (Thresh − Return) y Thresh para hacer visible la zona de retención. |
| Release | 100 ms | 5 a 2000 ms | `ClientGateRxReleaseMs` | Qué tan rápido se cierra la compuerta después de que la entrada cae por debajo de Thresh − Return. Mapeo exponencial. Se muestra como "X.X ms" por debajo de 100 ms, "X ms" por encima. |
| Floor | -15.0 dB | -80.0 a 0.0 dB | `ClientGateRxFloorDb` | Atenuación máxima que la compuerta puede aplicar. Mapeo lineal. |
| Barra de reducción de ganancia | — | 0 a 40 dB GR | — | Franja horizontal ámbar, rellena hacia la derecha. La escala máxima es 40 dB; una marca en -15 dB señala el Floor predeterminado. |
| Curva de transferencia | — | — | — | Traza la curva de transferencia estática del expansor y una bola en vivo en el nivel de entrada actual. En modo compacto (cuando se usa el editor flotante), las etiquetas de los ejes se almacenan en caché como texto estático y se renderizan con tamaño de fuente de 7 píxeles para mejorar el rendimiento. |

## Consejos

- Comience con Thresh justo por encima del nivel más alto de ruido de fondo que desea suprimir. Ajuste mientras escucha una señal débil — la compuerta debe abrirse limpiamente cuando la señal supere el ruido.
- La barra de reducción de ganancia muestra la profundidad de atenuación en vivo. Cuando no hay señal presente, debe mostrar una GR constante igual a su configuración de Floor. Si nunca alcanza Floor, Thresh puede estar configurado demasiado bajo o el ruido de banda es demasiado alto.
- Los mandos aquí y en el editor flotante se mantienen sincronizados — los cambios en cualquier lugar actualizan el otro en vivo.
- La visualización de la curva de transferencia almacena en caché las etiquetas de los ejes para un renderizado eficiente. Al cambiar entre el modo compacto (editor flotante) y el modo de tamaño completo, las etiquetas se actualizan automáticamente al tamaño de fuente apropiado.

## Relacionado

- [Establezca el umbral de TX justo por encima del piso de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md)
- [Elija comportamiento de compuerta vs. expansor suave mediante ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Establezca Return para evitar vibraciones de la compuerta cerca del umbral](set-return-to-prevent-gate-chatter-near-threshold.md)
- [Ajuste Release para un cierre natural de la compuerta](tune-release-for-natural-gate-close.md)
- [Establezca Floor para evitar silencios antinaturales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Ignore la compuerta desde la cadena](bypass-the-gate-from-the-chain.md)
- [Observe la GR en vivo mientras no habla](watch-live-gr-while-not-speaking.md)
