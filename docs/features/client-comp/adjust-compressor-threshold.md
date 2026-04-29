# Ajustar el umbral del compresor

Establezca el nivel en el que el compresor de TX comienza a actuar sobre su señal. Bajar el umbral hace que la compresión se active antes y con mayor frecuencia; subirlo reserva la compresión solo para los picos más altos.

## Antes de comenzar

- La etapa Compressor debe estar habilitada (no omitida) en el widget CHAIN. Si el bloque COMPRESSOR está oculto, habilite primero la etapa desde allí — consulte [Omitir el compresor desde la cadena](bypass-the-compressor-from-the-chain.md).
- El subcontenedor COMPRESSOR debe estar visible dentro del contenedor principal PooDoo Audio (TXDSP).

## Pasos

1. Localice el subcontenedor COMPRESSOR en el panel de applets.
2. Encuentre el control **Thresh** — el mando más a la izquierda en la fila de cinco mandos que aparece debajo de la curva de transferencia.
3. Haga clic y arrastre el mando **Thresh** para establecer el nivel de umbral. Arrastre hacia arriba para subir el umbral; arrastre hacia abajo para bajarlo. La etiqueta del mando se actualiza en tiempo real y muestra el valor en dB (por ejemplo, `-18.0 dB`).
4. Observe la barra de reducción de ganancia mientras habla. La franja ámbar debe llenarse desde la derecha cuando su señal supera el umbral. Una cantidad de reducción de ganancia típica en funcionamiento se sitúa cerca de la marca `-6 dB`.
5. Suelte el mando. El nuevo valor se guarda automáticamente en `ClientCompTxThresholdDb`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Descripción |
|---|---|---|---|---|
| Thresh | -18.0 dB | -60.0 a 0.0 dB | `ClientCompTxThresholdDb` | Nivel a partir del cual comienza la compresión. Mapeo lineal. |
| Ratio | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` | Cuánto se limitan los picos una vez superado el umbral. Mapeo logarítmico. La etiqueta se muestra como `X.XX:1`. |
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` | Con qué rapidez actúa el compresor tras superar el umbral. Mapeo exponencial. |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` | Con qué rapidez se recupera la ganancia cuando la señal vuelve a caer por debajo del umbral. Mapeo exponencial. |
| Makeup | 0.0 dB | -12.0 a 24.0 dB | `ClientCompTxMakeupDb` | Recupera la ganancia perdida por la compresión. Los valores positivos se muestran con signo `+` explícito. |
| Curva de transferencia | — | — | — | Solo visualización. Dibuja la curva estática de entrada/salida más una bola animada que muestra el nivel de envolvente actual. |
| Barra de reducción de ganancia | — | 0 a 20 dB GR | — | Franja ámbar horizontal, rellena desde la derecha. La marca en -6 dB indica una cantidad típica de trabajo. Se actualiza aproximadamente a 30 Hz. |

## Consejos

- Comience con el umbral predeterminado de `-18.0 dB` y bájelo gradualmente mientras habla a su nivel de voz normal, hasta que la barra de reducción de ganancia muestre una actividad constante pero moderada.
- La bola animada sobre la curva de transferencia rastrea su envolvente actual frente a la curva estática. Úsela para ver exactamente dónde se sitúa su nivel de voz respecto a la rodilla del umbral.
- Si la compresión se activa pero el nivel general suena más bajo, aumente el mando **Makeup** para compensar — consulte [Aplicar ganancia de compensación después de la compresión](apply-make-up-gain-after-compression.md).
- Para los ajustes de rodilla y limitador que el applet no expone, abra el editor completo — consulte [Abrir el editor completo del compresor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).

## Solución de problemas

- **La barra de reducción de ganancia no muestra actividad al transmitir** — Es posible que la etapa Compressor esté omitida, o que su nivel de entrada no esté alcanzando el umbral. Verifique que la etapa esté activa en el widget CHAIN y luego baje el mando **Thresh** hasta que la barra comience a mostrar relleno ámbar.
- **La barra de reducción de ganancia alcanza el máximo (20 dB) de inmediato** — El umbral está demasiado bajo para su nivel de entrada. Suba el mando **Thresh** hacia 0 dB hasta que la barra muestre una cantidad moderada.
- **El mando regresa a un valor diferente al que usted estableció** — Otra fuente (el editor flotante o la carga de un perfil) puede haber escrito un valor en conflicto en `ClientCompTxThresholdDb`. Consulte el editor flotante para ver el valor actual.

## Temas relacionados

- [Descripción general del compresor](overview.md)
- [Ajustar la relación de compresión para voz](set-compression-ratio-for-voice.md)
- [Ajustar el ataque y la liberación para un sonido de compresión natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de compensación después de la compresión](apply-make-up-gain-after-compression.md)
- [Observar la reducción de ganancia en tiempo real mientras habla](watch-live-gain-reduction-while-speaking.md)
- [Abrir el editor completo del compresor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Omitir el compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
