# Ajustar la relación de compresión para voz (TX) o audio recibido (RX AGC-C)

El mando Ratio controla con qué fuerza el compresor limita los picos una vez que la señal supera el umbral. Un valor más alto produce una compresión más agresiva de los picos de voz en transmisión (lado TX) o del audio recibido en recepción (lado RX AGC-C).

## Antes de comenzar

- La etapa de compresión debe estar habilitada (bypass desactivado) en el lado que desea ajustar. El mosaico del applet permanece oculto hasta que la etapa esté activa. Consulte [Desactivar el compresor en la cadena](bypass-the-compressor-from-the-chain.md).
- Abra el contenedor principal Aetherial Audio (TXDSP) y expanda el subcontenedor correspondiente: "Aetherial Compressor" para TX, o "Aetherial AGC-C" para RX.

## Pasos

1. Localice la fila de cinco mandos en la parte inferior del mosaico del applet. Los mandos están etiquetados de izquierda a derecha como Thresh, Ratio, Attack, Release y Makeup.
2. Gire el mando **Ratio** para establecer la relación de compresión.
   - Para compresión de voz en TX, este mando se almacena en `ClientCompTxRatio`.
   - Para RX AGC-C, este mando se almacena en `ClientCompRxRatio`.
3. Lea el valor actual en la etiqueta debajo del mando. El formato es `X.XX:1` (por ejemplo, `3.00:1`).
4. Observe la barra de reducción de ganancia y la bola de envolvente en la curva de transferencia mientras habla (TX) o mientras se reproduce audio (RX) para confirmar que la relación produce la cantidad de reducción de ganancia deseada.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Ajuste almacenado (TX / RX) |
|---|---|---|---|
| Ratio | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` / `ClientCompRxRatio` |
| Thresh | -18.0 dB | -60.0 a 0.0 dB | `ClientCompTxThresholdDb` / `ClientCompRxThresholdDb` |
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` / `ClientCompRxAttackMs` |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` / `ClientCompRxReleaseMs` |
| Makeup | 0.0 dB | -12.0 a 24.0 dB | `ClientCompTxMakeupDb` / `ClientCompRxMakeupDb` |

El mando Ratio utiliza una escala logarítmica (`1 × 20^n`) de modo que los valores bajos (compresión suave, 1.0–4.0:1) ocupan la mayor parte del recorrido del mando, mientras que los valores altos (limitación fuerte, hasta 20.0:1) se concentran en el extremo superior.

## Consejos

- Una relación entre 2.0:1 y 4.0:1 es habitual para la compresión de voz en TX. Los valores superiores a 10.0:1 se aproximan al comportamiento de un limitador.
- La barra de reducción de ganancia muestra hasta 20 dB de reducción. Una marca en -6 dB indica una cantidad de reducción de ganancia típica en operación normal. Si la barra raramente alcanza esa marca, el umbral puede estar demasiado alto para que la relación actual tenga un efecto apreciable.
- Aumentar la relación mientras se reduce el Makeup mantiene el nivel de salida promedio estable a la vez que estrecha el rango dinámico.
- Para acceder a los controles de Knee y techo del limitador, que definen con mayor detalle cómo se aplica la relación, abra el editor completo haciendo doble clic en la etapa COMP en el widget CHAIN.

## Solución de problemas

- **El mando Ratio no produce ningún efecto audible** — Es posible que la etapa siga en bypass. Confirme que el compresor está habilitado en el lado correcto (TX o RX) mediante el widget CHAIN. El mosaico del applet permanece oculto mientras la etapa está en bypass.
- **La barra de reducción de ganancia está fijada al máximo** — El umbral probablemente está demasiado bajo en relación con el nivel de la señal entrante. Reduzca la relación o suba el mando Thresh hasta que la barra muestre una reducción moderada e intermitente.

## Temas relacionados

- [Ajustar el umbral del compresor (lado TX o RX)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Ajustar el ataque y la liberación para una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de compensación después de la compresión](apply-make-up-gain-after-compression.md)
- [Observar la reducción de ganancia en tiempo real mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Abrir el editor completo del compresor para los controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Desactivar el compresor en la cadena](bypass-the-compressor-from-the-chain.md)
