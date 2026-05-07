# Ajustar la Relación de Compresión para Voz (TX) o Audio Recibido (RX AGC-C)

El control Ratio determina la intensidad con la que el compresor limita los picos una vez que la señal supera el umbral. Una relación más alta comprime de forma más agresiva los picos de voz fuertes (en el lado TX) o el audio recibido intenso (en el lado RX AGC-C).

## Antes de comenzar

- La etapa del compresor debe estar habilitada (sin bypass) en el lado que desea ajustar. Cuando la etapa está en bypass, todo el mosaico del applet se atenúa aproximadamente al 55 % de opacidad para indicar que está inactivo. Consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md).
- Abra el contenedor principal "Aetherial Audio (TXDSP)" y expanda el subcontenedor correspondiente: "Aetherial Compressor" para TX, o "Aetherial AGC-C" para RX.

## Pasos

1.  Localice la fila de cinco mandos en la parte inferior del mosaico del applet. Los mandos están etiquetados como Thresh, Ratio, Attack, Release y Makeup, de izquierda a derecha.
2.  Gire el mando **Ratio** para ajustar la relación de compresión.
    - Para la compresión de voz en TX, este mando persiste en `ClientCompTxRatio`.
    - Para RX AGC-C, este mando persiste en `ClientCompRxRatio`.
3.  Lea el valor actual en la etiqueta debajo del mando. Tiene el formato `X.XX:1` (por ejemplo, `3.00:1`).
4.  Observe la barra de reducción de ganancia y la bola de la envolvente en la curva de transferencia mientras habla (TX) o mientras se reproduce audio (RX) para confirmar que la relación está produciendo la cantidad de reducción de ganancia deseada.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistido (TX / RX) |
|---|---|---|---|
| Ratio | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` / `ClientCompRxRatio` |
| Thresh | -18.0 dB | -60.0 a 0.0 dB | `ClientCompTxThresholdDb` / `ClientCompRxThresholdDb` |
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` / `ClientCompRxAttackMs` |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` / `ClientCompRxReleaseMs` |
| Makeup | 0.0 dB | -12.0 a 24.0 dB | `ClientCompTxMakeupDb` / `ClientCompRxMakeupDb` |

El mando Ratio utiliza una asignación logarítmica (`1 × 20^n`) para que las relaciones bajas (compresión suave, 1.0–4.0:1) ocupen la mayor parte del recorrido del mando y las relaciones altas (limitación dura, hasta 20.0:1) se concentren en el extremo superior.

## Consejos

- Una relación entre 2.0:1 y 4.0:1 es típica para la compresión de voz en TX. Los valores superiores a 10.0:1 se aproximan a un comportamiento de limitación.
- La barra de reducción de ganancia muestra hasta 20 dB de reducción. Una marca en -6 dB indica una cantidad de trabajo típica. Si la barra rara vez alcanza esa marca, es posible que el umbral esté demasiado alto para que la relación actual tenga un efecto significativo.
- Aumentar la relación mientras se reduce Makeup mantiene el nivel de salida promedio estable al tiempo que reduce el rango dinámico.
- Para acceder a los controles de Knee y techo del limitador, que definen aún más cómo se aplica la relación, abra el editor completo haciendo doble clic en la etapa COMP en el widget CHAIN.

## Solución de problemas

- **El mando Ratio no tiene un efecto audible** — Es posible que la etapa aún esté en bypass. Confirme que el compresor esté habilitado en el lado correcto (TX o RX) a través del widget CHAIN. Cuando la etapa está en bypass, el mosaico del applet se atenúa aproximadamente al 55 % de opacidad; restaure la opacidad total habilitando la etapa.
- **La barra de reducción de ganancia está fijada al máximo** — Es probable que el umbral sea demasiado bajo en relación con el nivel de la señal entrante. Reduzca la relación o suba el mando Thresh hasta que la barra muestre una reducción moderada e intermitente.

## Relacionados

- [Adjust compressor threshold (TX or RX side)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Tune attack / release for a natural-sounding squeeze](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
- [Watch live gain reduction while speaking or listening](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md)
