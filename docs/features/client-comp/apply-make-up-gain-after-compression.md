# Aplicar ganancia de compensación (makeup gain) después de la compresión

Use el control **Makeup** para restaurar la sonoridad perdida por la compresión, de modo que su señal transmitida alcance un nivel consistente sin necesidad de reajustar manualmente la ganancia de excitación.

## Antes de comenzar

- La etapa Compressor debe estar habilitada (bypass desactivado). Consulte [Omitir el compresor desde la cadena](bypass-the-compressor-from-the-chain.md).
- El subcontenedor COMPRESSOR debe estar visible dentro del contenedor principal PooDoo Audio (TXDSP).

## Pasos

1. Localice la fila de cinco controles en la parte inferior del applet COMPRESSOR.
2. Encuentre el control más a la derecha, etiquetado como **Makeup**.
3. Gire el control **Makeup** en sentido horario para aumentar la ganancia, o en sentido antihorario para reducirla.
4. Observe la barra de reducción de ganancia mientras habla. Intente compensar la cantidad típica de reducción de ganancia que se muestra — la marca de −6 dB en la franja ámbar es un punto de referencia útil.
5. Suelte el control. El valor se guarda inmediatamente en `ClientCompTxMakeupDb`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistido |
|---|---|---|---|
| Makeup | 0.0 dB | −12.0 to +24.0 dB | `ClientCompTxMakeupDb` |

La etiqueta del control muestra un signo `+` explícito para valores positivos (por ejemplo, `+3.0 dB`) y ningún signo para valores negativos (por ejemplo, `-2.0 dB`). La ganancia de compensación se aplica después de la compresión y después de la etapa limitadora.

## Consejos

- Comience con **Makeup** en `0.0 dB` y auméntelo en pasos pequeños mientras observa la barra de reducción de ganancia. Si el compresor está reduciendo aproximadamente 6 dB en los picos típicos de voz, agregar +6 dB de makeup devuelve la salida promedio al nivel sin comprimir.
- Si necesita agregar más de 12–15 dB de makeup, es posible que el umbral o la razón de compresión estén configurados de forma demasiado agresiva. Consulte [Ajustar el umbral del compresor](adjust-compressor-threshold.md) y [Establecer la razón de compresión para voz](set-compression-ratio-for-voice.md).
- La curva de transferencia en el applet no refleja visualmente la ganancia de compensación. Abra el editor completo para ver cómo interactúa el makeup con la rodilla (knee) y el techo del limitador. Consulte [Abrir el editor completo del Compressor para los controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).

## Solución de problemas

- **El control Makeup no tiene efecto** — Confirme que la etapa Compressor esté activa. Si la etapa está en bypass, se omite toda la cadena DSP del compresor, incluida la ganancia de compensación.
- **La salida presenta saturación (clipping) después de agregar makeup** — Es posible que el techo del limitador (`ClientCompTxLimCeilingDb`) necesite ajuste. Abra el editor completo del Compressor para habilitar o ajustar el limitador. Consulte [Abrir el editor completo del Compressor para los controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).

## Temas relacionados

- [Observar la reducción de ganancia en tiempo real mientras habla](watch-live-gain-reduction-while-speaking.md)
- [Ajustar el umbral del compresor](adjust-compressor-threshold.md)
- [Establecer la razón de compresión para voz](set-compression-ratio-for-voice.md)
- [Abrir el editor completo del Compressor para los controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
