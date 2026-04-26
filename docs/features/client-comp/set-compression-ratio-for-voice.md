# Establecer la relación de compresión para voz

El control **Ratio** determina con qué intensidad el compresor limita los picos de señal una vez que superan el umbral. Una relación más alta produce una compresión agresiva al estilo broadcast; una relación más baja ofrece un resultado más suave y transparente.

## Antes de comenzar

- La etapa Compressor debe estar habilitada (bypass desactivado). Si el subcontenedor COMPRESSOR está oculto, habilite la etapa desde el widget CHAIN primero. Consulte [Desactivar el compresor desde la cadena](bypass-the-compressor-from-the-chain.md).
- El subcontenedor COMPRESSOR debe estar visible dentro del contenedor principal PooDoo Audio (TXDSP) en el panel de applets.

## Pasos

1. Localice el subcontenedor COMPRESSOR en el panel de applets.
2. Encuentre el control **Ratio** en la fila de cinco controles en la parte inferior del applet.
3. Gire el control **Ratio** en sentido horario para aumentar la relación, o en sentido antihorario para disminuirla. La etiqueta debajo del control se actualiza en tiempo real y muestra el valor actual como `X.XX:1`.
4. Observe la barra de reducción de ganancia situada encima de la fila de controles mientras habla al micrófono. Un relleno ámbar que se desplaza hacia la marca de -6 dB indica que el compresor está trabajando activamente con la relación establecida.
5. Ajuste **Thresh** y **Makeup** según sea necesario para compensar los cambios de nivel provocados por la nueva relación.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Ratio | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` |
| Thresh | -18.0 dB | -60.0 a 0.0 dB | `ClientCompTxThresholdDb` |
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` |
| Makeup | 0.0 dB | -12.0 a 24.0 dB | `ClientCompTxMakeupDb` |

El control **Ratio** utiliza una escala logarítmica. Los movimientos pequeños cerca del extremo inferior del rango ofrecen un control preciso en torno a las relaciones típicas para voz (2:1 a 4:1). Los movimientos amplios cerca del extremo superior se aproximan al comportamiento de limitador (20:1).

La barra de reducción de ganancia alcanza un máximo de 20 dB de reducción. Una marca en -6 dB indica una cantidad de reducción de ganancia habitual para voz.

Los ajustes de rodilla y limitador (`ClientCompTxKneeDb`, `ClientCompTxLimEnabled`, `ClientCompTxLimCeilingDb`) no están disponibles en el applet. Consulte [Abrir el editor completo del Compressor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).

## Consejos

- Para voz en SSB, las relaciones entre 2:1 y 4:1 son un punto de partida habitual. El valor predeterminado de 3.0:1 es adecuado para la mayoría de las combinaciones de micrófono y voz.
- Si la barra de reducción de ganancia permanece fija completamente a la derecha durante el habla normal, es posible que la relación sea demasiado alta o el umbral demasiado bajo. Reduzca la relación o eleve el umbral y compruebe el resultado de nuevo con **Makeup**.
- La curva de transferencia en el applet muestra la relación estática entre entrada y salida. La bola de envolvente se desplaza a lo largo de la curva en tiempo real mientras habla, lo que le proporciona una referencia visual de dónde se sitúa su voz respecto al umbral y la relación establecidos.

## Relacionados

- [Ajustar el umbral del compresor](adjust-compressor-threshold.md)
- [Aplicar ganancia de compensación tras la compresión](apply-make-up-gain-after-compression.md)
- [Ajustar el ataque y la liberación para una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Ver la reducción de ganancia en vivo mientras habla](watch-live-gain-reduction-while-speaking.md)
- [Abrir el editor completo del Compressor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Desactivar el compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
