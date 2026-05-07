# Use AGC-G en RX para suprimir el ruido de banda por debajo de un piso seleccionado

El AGC-G Aetherial del lado RX (expansor descendente del lado del cliente) atenúa el audio recibido que cae por debajo de un umbral que usted establece, lo que le permite silenciar el ruido de fondo de banda o la estática entre señales, manteniendo el audio deseado intacto.

## Antes de comenzar

- Debe estar conectado a una radio FLEX-8600.
- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el Panel de Applets.
- La etapa Gate del lado RX debe estar habilitada a través del widget CHAIN (haga doble clic en la etapa GATE del lado RX para abrir su editor, o un clic para alternar el bypass).

## Pasos

1. En el Panel de Applets, localice el subcontenedor **Aetherial AGC-G (RX)** dentro del contenedor principal Aetherial Audio (TXDSP). Si está oculto, haga doble clic en la etapa GATE del widget CHAIN en el lado RX para abrir el editor flotante (titulado "Aetherial Gate — RX").

2. Ajuste **Thresh** (valor predeterminado: -40.0 dB) hacia abajo hasta que el ruido de banda que desea suprimir quede por debajo del umbral. Observe la bola de entrada en vivo en la visualización de la curva de transferencia — cuando la bola esté por debajo de la línea de umbral, la compuerta está cerrada y se aplica atenuación.

3. Establezca **Floor** (valor predeterminado: -15.0 dB) en la atenuación máxima que desea aplicar al ruido de fondo. Un ajuste típico es de -15 a -20 dB — suficiente para silenciar el ruido sin que los espacios entre palabras suenen artificialmente silenciosos.

4. Ajuste **Ratio** (valor predeterminado: 2.0) para controlar la agresividad con la que corta la compuerta:
   - Ratios bajos (1.0–3.0) actúan como un expansor descendente suave — el ruido de fondo se desvanece gradualmente.
   - Ratios altos (5.0–10.0) crean una sensación de compuerta más dura y tradicional.

5. Establezca **Return** (valor predeterminado: 2.0 dB) para evitar aperturas y cierres rápidos cerca del umbral. Aparece una banda de histéresis cian en la curva de transferencia entre (Thresh − Return) y Thresh — la compuerta permanece abierta dentro de esta zona hasta que la entrada cae por debajo de ella, luego debe superar Thresh para reabrirse.

6. Ajuste **Release** (valor predeterminado: 100 ms) para controlar la rapidez con la que se cierra la compuerta después de que la entrada cae por debajo de Thresh − Return. Valores más largos (500–2000 ms) proporcionan un desvanecimiento más natural; valores más cortos (5–50 ms) pueden sonar abruptos.

## Qué hace cada control

| Control | Predeterminado | Rango | Clave de ajuste | Comportamiento |
|---------|---------------|-------|-----------------|----------------|
| Thresh | -40.0 dB | -80.0 a 0.0 dB | `ClientGateRxThresholdDb` | Nivel por debajo del cual la compuerta comienza a atenuar. Mapeo lineal. |
| Ratio | 2.0 | 1.0 a 10.0 | `ClientGateRxRatio` | Ratios más altos producen un corte más duro, similar a una compuerta; ratios más bajos actúan como un expansor descendente suave. Se muestra como "X.X:1". |
| Return | 2.0 dB | 0.0 a 20.0 dB | `ClientGateRxReturnDb` | Banda muerta de histéresis: la compuerta se abre por encima de Thresh y permanece abierta hasta que la entrada cae por debajo de Thresh − Return. Se muestra como "X.XX dB". |
| Release | 100 ms | 5 a 2000 ms | `ClientGateRxReleaseMs` | Rapidez con la que la compuerta se cierra después de que la entrada cae por debajo de Thresh − Return. Mapeo exponencial. |
| Floor | -15.0 dB | -80.0 a 0.0 dB | `ClientGateRxFloorDb` | Atenuación máxima que la compuerta puede aplicar. Mapeo lineal. |
| Barra de reducción de ganancia | — | 0 a 40 dB GR | — | Franja horizontal ámbar, rellena desde la derecha. Una marca a -15 dB indica el Floor predeterminado. |
| Curva de transferencia | — | — | — | Traza la curva de transferencia estática del expansor con una bola de entrada en vivo. La banda cian muestra la zona de histéresis. |

## Consejos

- Comience con Thresh justo por encima del nivel más alto de ruido de fondo que desea suprimir. Ajuste mientras escucha una señal débil — la compuerta debe abrirse limpiamente cuando la señal se eleve por encima del ruido.
- La barra de reducción de ganancia muestra la profundidad de atenuación en vivo. Cuando no hay señal presente, debe mostrar una GR constante igual a su ajuste de Floor. Si nunca alcanza Floor, es posible que Thresh esté configurado demasiado bajo o que el ruido de banda sea demasiado fuerte.
- Las perillas de ajuste aquí y en el editor flotante se mantienen sincronizadas — los cambios en cualquier lugar actualizan el otro en vivo.

## Relacionados

- [Establezca el umbral de TX justo por encima del piso de ruido de la sala](set-tx-threshold-just-above-room-noise-floor.md)
- [Elija el comportamiento de compuerta vs. expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Establezca Return para evitar el traqueteo de la compuerta cerca del umbral](set-return-to-prevent-gate-chatter-near-threshold.md)
- [Ajuste Release para un cierre natural de la compuerta](tune-release-for-natural-gate-close.md)
- [Establezca Floor para evitar el silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Bypasse la compuerta desde la cadena](bypass-the-gate-from-the-chain.md)
- [Observe la GR en vivo mientras no habla](watch-live-gr-while-not-speaking.md)
