# Aplicar ganancia de compensación después de la compresión

Después de que el compresor reduce los picos, el nivel general de la señal disminuye. El control **Makeup** recupera la ganancia perdida para que el audio transmitido alcance el nivel de volumen deseado.

## Antes de comenzar

- La etapa Compressor debe estar habilitada (bypass desactivado). Si está en bypass, la ganancia de compensación no tiene efecto. Consulte [Omitir el compresor de la cadena](bypass-the-compressor-from-the-chain.md).
- El subcontenedor COMPRESSOR debe estar visible dentro del contenedor principal PooDoo Audio (TXDSP).

## Pasos

1. Localice el subcontenedor COMPRESSOR en el panel de applets.
2. Encuentre el control **Makeup** — el control más a la derecha en la fila de cinco controles.
3. Gire o arrastre con clic el control **Makeup** para establecer la ganancia deseada.
   - Los valores positivos se muestran con un signo `+` explícito, por ejemplo `+6.0 dB`.
   - Observe la curva de transferencia y la barra de reducción de ganancia mientras habla para determinar cuánta ganancia restaurar.
4. Suelte el control. El valor se guarda automáticamente en `ClientCompTxMakeupDb`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistente |
|---|---|---|---|
| Makeup | `0.0 dB` | `-12.0 to 24.0 dB` | `ClientCompTxMakeupDb` |

El control **Makeup** utiliza un mapeo lineal. Añade una etapa de ganancia fija después del compresor. Aumentarlo compensa la reducción del nivel promedio causada por la reducción de ganancia; reducirlo por debajo de `0.0 dB` puede atenuar la señal posterior al compresor.

## Consejos

- Comience con el valor de **Makeup** aproximadamente igual a la lectura típica en la barra de reducción de ganancia. Si el compresor reduce en promedio 6 dB, pruebe `+6.0 dB` como punto de partida y luego ajuste a oído.
- La marca de referencia en la barra de reducción de ganancia se ubica en el punto de 6 dB y ofrece una referencia visual rápida para una cantidad de compresión típica de trabajo.
- Para una coincidencia más precisa, abra el editor completo donde también son accesibles el knee y el techo del limitador (`ClientCompTxLimCeilingDb`). Consulte [Abrir el editor completo del Compressor para los controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).

## Solución de problemas

- **El control Makeup no tiene efecto** — Es posible que la etapa Compressor esté en bypass. Habilítela mediante el widget CHAIN o el editor flotante y luego ajuste Makeup nuevamente.
- **La salida es demasiado alta después de añadir la ganancia de compensación** — Reduzca `ClientCompTxMakeupDb` o habilite el limitador y baje `ClientCompTxLimCeilingDb` para evitar el recorte (clipping). Consulte [Abrir el editor completo del Compressor para los controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).

## Relacionados

- [Observar la reducción de ganancia en vivo mientras habla](watch-live-gain-reduction-while-speaking.md)
- [Ajustar el umbral del compresor](adjust-compressor-threshold.md)
- [Abrir el editor completo del Compressor para los controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Establecer la relación de compresión para voz](set-compression-ratio-for-voice.md)
