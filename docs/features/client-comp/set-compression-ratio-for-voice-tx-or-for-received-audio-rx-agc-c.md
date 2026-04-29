# Configurar la relación de compresión para voz (TX) o audio recibido (RX AGC-C)

El control Ratio determina con qué intensidad el compresor limita los picos una vez que la señal supera el umbral. Un valor más alto produce una compresión más agresiva sobre los picos de voz fuertes (en el lado TX) o sobre el audio recibido de alto nivel (en el lado RX AGC-C).

## Antes de comenzar

- La etapa de compresor debe estar habilitada (bypass desactivado) en el lado que desea ajustar. El mosaico del applet permanece oculto hasta que la etapa esté activa. Consulte [Omitir el compresor desde la cadena](bypass-the-compressor-from-the-chain.md).
- Abra el contenedor principal Aetherial Audio (TXDSP) y expanda el subcontenedor correspondiente: "Aetherial Compressor" para TX, o "Aetherial AGC-C" para RX.

## Pasos

1. Localice la fila de cinco controles en la parte inferior del mosaico del applet. Los controles están etiquetados como Thresh, Ratio, Attack, Release y Makeup, de izquierda a derecha.
2. Gire el control **Ratio** para establecer la relación de compresión.
   - Para la compresión de voz TX, este control se guarda en `ClientCompTxRatio`.
   - Para RX AGC-C, este control se guarda en `ClientCompRxRatio`.
3. Lea el valor actual en la etiqueta que aparece debajo del control. El formato es `X.XX:1` (por ejemplo, `3.00:1`).
4. Observe la barra de reducción de ganancia y la bola de envolvente en la curva de transferencia mientras habla (TX) o mientras se reproduce audio (RX) para confirmar que la relación produce la cantidad de reducción de ganancia deseada.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistente (TX / RX) |
|---|---|---|---|
| Ratio | 3.0 | 1.0 to 20.0 | `ClientCompTxRatio` / `ClientCompRxRatio` |
| Thresh | -18.0 dB | -60.0 to 0.0 dB | `ClientCompTxThresholdDb` / `ClientCompRxThresholdDb` |
| Attack | 20.0 ms | 0.1 to 300.0 ms | `ClientCompTxAttackMs` / `ClientCompRxAttackMs` |
| Release | 200 ms | 5 to 2000 ms | `ClientCompTxReleaseMs` / `ClientCompRxReleaseMs` |
| Makeup | 0.0 dB | -12.0 to 24.0 dB | `ClientCompTxMakeupDb` / `ClientCompRxMakeupDb` |

El control Ratio utiliza una escala logarítmica (`1 × 20^n`) de modo que los valores bajos (compresión suave, 1.0–4.0:1) ocupan la mayor parte del recorrido del control, mientras que los valores altos (limitación intensa, hasta 20.0:1) quedan comprimidos en el extremo superior.

## Consejos

- Una relación entre 2.0:1 y 4.0:1 es típica para la compresión de voz TX. Los valores superiores a 10.0:1 se aproximan al comportamiento de un limitador.
- La barra de reducción de ganancia muestra hasta 20 dB de reducción. Una marca en -6 dB indica una cantidad de reducción típica en uso normal. Si la barra rara vez alcanza esa marca, es posible que el umbral esté configurado demasiado alto para que la relación actual tenga un efecto significativo.
- Aumentar la relación mientras se reduce Makeup mantiene el nivel promedio de salida estable y estrecha el rango dinámico.
- Para acceder a los controles de Knee y al techo del limitador, que definen con mayor precisión cómo se aplica la relación, abra el editor completo haciendo doble clic en la etapa COMP del widget CHAIN.

## Resolución de problemas

- **El control Ratio no produce ningún efecto audible** — Es posible que la etapa siga en bypass. Confirme que el compresor esté habilitado en el lado correcto (TX o RX) mediante el widget CHAIN. El mosaico del applet permanece oculto mientras la etapa está en bypass.
- **La barra de reducción de ganancia está fijada al máximo** — Es probable que el umbral sea demasiado bajo en relación con el nivel de la señal entrante. Reduzca la relación o aumente el control Thresh hasta que la barra muestre una reducción moderada e intermitente.

## Temas relacionados

- [Ajustar el umbral del compresor (lado TX o RX)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Ajustar el ataque y la liberación para una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de compensación después de la compresión](apply-make-up-gain-after-compression.md)
- [Ver la reducción de ganancia en tiempo real mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Abrir el editor completo del compresor para los controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Omitir el compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
