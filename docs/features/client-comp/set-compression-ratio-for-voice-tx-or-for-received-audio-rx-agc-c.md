# Establecer la relación de compresión para Voz (TX) o Audio Recibido (RX AGC-C)

El mando Ratio controla la intensidad con la que el compresor limita los picos una vez que la señal supera el umbral. Una relación más alta produce una compresión más agresiva sobre los picos fuertes de voz (en el lado TX) o del audio recibido (en el lado RX AGC-C).

## Antes de comenzar

- La etapa del compresor debe estar habilitada (sin bypass) en el lado que desee ajustar. Cuando la etapa está en bypass, el mosaico completo del applet se atenúa aproximadamente al 55% de opacidad para indicar que está inactiva. Consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md).
- Abra el contenedor principal "Aetherial Audio (TXDSP)" y expanda el subcontenedor correspondiente: "Aetherial Compressor" para TX, o "Aetherial AGC-C" para RX.

## Pasos

1. Localice la fila de cinco mandos en la parte inferior del mosaico del applet. Los mandos están etiquetados como Thresh, Ratio, Attack, Release y Makeup, de izquierda a derecha.
2. Gire el mando **Ratio** para establecer la relación de compresión.
   - Para la compresión de voz en TX, este mando persiste en `ClientCompTxRatio`.
   - Para RX AGC-C, este mando persiste en `ClientCompRxRatio`.
3. Lea el valor actual en la etiqueta debajo del mando. Tiene el formato `X.XX:1` (por ejemplo, `3.00:1`).
4. Observe la barra de reducción de ganancia y la bola de envolvente en la curva de transferencia mientras habla (TX) o mientras se reproduce audio (RX) para confirmar que la relación está produciendo la cantidad deseada de reducción de ganancia.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Configuración persistida (TX / RX) |
|---|---|---|---|
| Ratio | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` / `ClientCompRxRatio` |
| Thresh | -18.0 dB | -60.0 a 0.0 dB | `ClientCompTxThresholdDb` / `ClientCompRxThresholdDb` |
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` / `ClientCompRxAttackMs` |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` / `ClientCompRxReleaseMs` |
| Makeup | 0.0 dB | -12.0 a 24.0 dB | `ClientCompTxMakeupDb` / `ClientCompRxMakeupDb` |

El mando Ratio utiliza un mapeo logarítmico (`1 × 20^n`) para que las relaciones bajas (compresión suave, 1.0–4.0:1) ocupen la mayor parte del recorrido del mando y las relaciones altas (limitación dura, hasta 20.0:1) se concentren en el extremo superior.

## Visualización de la curva de transferencia

El ClientCompCurveWidget en modo compacto dibuja la curva estática de transferencia entrada/salida con una "bola" en vivo que muestra el nivel de envolvente actual. Las etiquetas de los ejes se renderizan usando objetos QStaticText en caché que se reconstruyen automáticamente cuando el applet cambia entre las vistas compacta y expandida. En el applet, la curva es solo de visualización; para editar los parámetros Knee y limiter ceiling, abra el ClientCompEditor flotante haciendo doble clic en la etapa COMP en el widget CHAIN.

## Medidor de reducción de ganancia

La barra horizontal de color ámbar se llena de derecha a izquierda, mostrando hasta 20 dB de reducción de ganancia. Una marca en -6 dB indica una cantidad de reducción de trabajo típica. El medidor se actualiza a aproximadamente 30 Hz utilizando la balística de MeterSmoother aplicada al valor `ClientComp::gainReductionDb()`.

## Consejos

- Una relación entre 2.0:1 y 4.0:1 es típica para la compresión de voz en TX. Los valores superiores a 10.0:1 se aproximan a un comportamiento de limitación.
- La barra de reducción de ganancia muestra hasta 20 dB de reducción. Una marca en -6 dB indica una cantidad de reducción de ganancia de trabajo típica. Si la barra rara vez alcanza esa marca, es posible que el umbral esté demasiado alto para que la relación actual tenga mucho efecto.
- Aumentar la relación mientras se reduce el Makeup mantiene estable el nivel de salida promedio mientras se ajusta el rango dinámico.
- Para acceder a los controles Knee y limiter ceiling, que dan forma adicional a cómo se aplica la relación, abra el editor completo haciendo doble clic en la etapa COMP en el widget CHAIN.

## Solución de problemas

- **El mando Ratio no tiene efecto audible** — Es posible que la etapa aún esté en bypass. Confirme que el compresor esté habilitado en el lado correcto (TX o RX) a través del widget CHAIN. Cuando la etapa está en bypass, el mosaico del applet se atenúa aproximadamente al 55% de opacidad; restaure la opacidad completa habilitando la etapa.
- **La barra de reducción de ganancia está fijada al máximo** — Es probable que el umbral esté demasiado bajo en relación con el nivel de la señal entrante. Reduzca la relación o suba el mando Thresh hasta que la barra muestre una reducción moderada e intermitente.

## Relacionados

- [Adjust compressor threshold (TX or RX side)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Tune attack / release for a natural-sounding squeeze](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
- [Watch live gain reduction while speaking or listening](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md)
