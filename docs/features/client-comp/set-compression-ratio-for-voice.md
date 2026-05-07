# Establecer la relación de compresión para la voz

El control **Ratio** determina con qué intensidad el compresor atenúa los picos de la señal una vez que cruzan el umbral. Una relación más alta produce una compresión más agresiva, similar a la de una emisora de radio; una relación más baja ofrece un resultado más suave y transparente.

## Antes de comenzar

- La etapa Compressor debe estar habilitada (bypass desactivado). Si el subcontenedor COMPRESSOR está oculto, active primero la etapa a través del widget CHAIN. Consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md).
- El subcontenedor COMPRESSOR debe estar visible dentro del contenedor principal PooDoo Audio (TXDSP) en el panel del applet.

## Pasos

1. Localice el subcontenedor COMPRESSOR en el panel del applet.
2. Encuentre el control **Ratio** en la fila de cinco controles en la parte inferior del applet.
3. Gire el control **Ratio** en el sentido de las agujas del reloj para aumentar la relación o en sentido contrario para disminuirla. La etiqueta debajo del control se actualiza en tiempo real y muestra el valor actual como `X.XX:1`.
4. Observe la barra de reducción de ganancia sobre la fila de controles mientras habla por el micrófono. Un relleno de color ámbar que se mueve hacia la marca de -6 dB indica que el compresor está trabajando activamente con la relación que ha establecido.
5. Ajuste **Thresh** y **Makeup** según sea necesario para compensar los cambios de nivel causados por la nueva relación.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Ratio | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` |
| Thresh | -18.0 dB | -60.0 a 0.0 dB | `ClientCompTxThresholdDb` |
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` |
| Makeup | 0.0 dB | -12.0 a 24.0 dB | `ClientCompTxMakeupDb` |

El control **Ratio** utiliza una escala logarítmica. Los movimientos pequeños cerca del extremo inferior del rango proporcionan un control preciso para las relaciones de voz típicas (2:1 a 4:1). Los movimientos grandes cerca del extremo superior se aproximan al comportamiento de un limitador (20:1).

La barra de reducción de ganancia tiene un máximo de 20 dB de reducción. Una marca en -6 dB indica una cantidad de trabajo típica de reducción de ganancia para voz.

Los ajustes de knee y limitador (`ClientCompTxKneeDb`, `ClientCompTxLimEnabled`, `ClientCompTxLimCeilingDb`) no están disponibles en el applet. Consulte [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).

## Consejos

- Para voz en SSB, las relaciones entre 2:1 y 4:1 son un punto de partida habitual. El valor predeterminado de 3.0:1 funciona bien con la mayoría de las combinaciones de micrófono y voz.
- Si la barra de reducción de ganancia se queda fija hacia la derecha durante el habla normal, la relación puede ser demasiado alta o el umbral demasiado bajo. Reduzca la relación o aumente el umbral, y luego vuelva a verificar con **Makeup**.
- La curva de transferencia en el applet muestra la relación estática entrada/salida. La bola del envolvente se mueve a lo largo de la curva en tiempo real mientras habla, proporcionándole una referencia visual de dónde se encuentra su voz en relación con el umbral y la relación que ha establecido.

## Relacionado

- [Adjust compressor threshold](adjust-compressor-threshold.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
- [Tune attack / release for a natural-sounding squeeze](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Watch live gain reduction while speaking](watch-live-gain-reduction-while-speaking.md)
- [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md)
