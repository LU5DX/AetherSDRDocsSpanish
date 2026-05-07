# Ajustar el umbral del compresor

Establezca el nivel en el que el compresor de TX comienza a actuar sobre su señal. Bajar el umbral hace que la compresión se active antes y con más frecuencia; subirlo reserva la compresión solo para los picos más fuertes.

## Antes de empezar

- La etapa Compressor debe estar habilitada (no en bypass) en el widget CHAIN. Si el mosaico COMPRESSOR está oculto, habilite la etapa allí primero; consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md).
- El subcontenedor COMPRESSOR debe estar visible dentro del contenedor principal PooDoo Audio (TXDSP).

## Pasos

1. Localice el subcontenedor COMPRESSOR en el panel del applet.
2. Busque el mando **Thresh** — el mando más a la izquierda en la fila de cinco mandos debajo de la curva de transferencia.
3. Haga clic y arrastre el mando **Thresh** para establecer el nivel de umbral. Arrastre hacia arriba para subir el umbral; arrastre hacia abajo para bajarlo. La etiqueta del mando se actualiza en tiempo real y muestra el valor en dB (por ejemplo, `-18.0 dB`).
4. Observe la barra de reducción de ganancia mientras habla. La barra ámbar debe llenarse desde la derecha cuando su señal supere el umbral. Una cantidad de trabajo típica de reducción de ganancia se sitúa cerca de la marca `-6 dB`.
5. Suelte el mando. El nuevo valor se guarda automáticamente en `ClientCompTxThresholdDb`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Descripción |
|---|---|---|---|---|
| Thresh | -18.0 dB | -60.0 a 0.0 dB | `ClientCompTxThresholdDb` | Nivel a partir del cual comienza la compresión. Mapeo lineal. |
| Ratio | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` | Cuán firmemente se contienen los picos una vez que se supera el umbral. Mapeo logarítmico. La etiqueta se muestra como `X.XX:1`. |
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` | Qué tan rápido el compresor reduce la ganancia después de superar el umbral. Mapeo exponencial. |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` | Qué tan rápido la ganancia vuelve a la normalidad después de que la señal cae por debajo del umbral. Mapeo exponencial. |
| Makeup | 0.0 dB | -12.0 a 24.0 dB | `ClientCompTxMakeupDb` | Añade ganancia para compensar la pérdida por compresión. Los valores positivos se muestran con un signo `+` explícito. |
| Curva de transferencia | — | — | — | Solo visualización. Dibuja la curva estática de entrada/salida más una bola en vivo que muestra el nivel actual de la envolvente. |
| Barra de reducción de ganancia | — | 0 a 20 dB GR | — | Barra horizontal ámbar que se llena desde la derecha. Una marca en -6 dB señala una cantidad de trabajo típica. Se actualiza a aproximadamente 30 Hz. |

## Consejos

- Comience con el umbral predeterminado de `-18.0 dB` y bájelo gradualmente mientras habla a su nivel de voz normal hasta que la barra de reducción de ganancia muestre actividad constante pero moderada.
- La bola en vivo en la curva de transferencia rastrea su envolvente actual en relación con la curva estática. Úsela para ver exactamente dónde se sitúa su nivel de voz con respecto a la rodilla del umbral.
- Si la compresión se activa pero el nivel general suena más bajo, aumente el mando **Makeup** para compensarlo; consulte [Apply make-up gain after compression](apply-make-up-gain-after-compression.md).
- Para los ajustes de rodilla (knee) y limitador que el applet no expone, abra el editor completo; consulte [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).

## Solución de problemas

- **La barra de reducción de ganancia no muestra actividad mientras transmite** — La etapa Compressor puede estar en bypass, o su nivel de entrada no alcanza el umbral. Verifique que la etapa esté activa en el widget CHAIN, luego baje el mando **Thresh** hasta que la barra comience a mostrar relleno ámbar.
- **La barra de reducción de ganancia se fija al máximo (20 dB) inmediatamente** — El umbral está demasiado bajo para su nivel de entrada. Suba el mando **Thresh** hacia 0 dB hasta que la barra indique una cantidad moderada.
- **El mando vuelve a un valor diferente al que usted configuró** — Otra fuente (el editor flotante o una carga de perfil) puede haber escrito un valor conflictivo en `ClientCompTxThresholdDb`. Revise el editor flotante para ver el valor actual.

## Relacionados

- [Compressor overview](overview.md)
- [Set compression ratio for voice](set-compression-ratio-for-voice.md)
- [Tune attack / release for a natural-sounding squeeze](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
- [Watch live gain reduction while speaking](watch-live-gain-reduction-while-speaking.md)
- [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md)
