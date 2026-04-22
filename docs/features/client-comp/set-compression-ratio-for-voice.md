# Establecer la relación de compresión para voz

El control Ratio determina con qué intensidad el compresor limita los picos una vez que la señal supera el umbral. Aumentar la relación produce un nivel más agresivo y uniforme; reducirla genera una compresión más suave y natural. Ajuste este control según su voz y estilo de operación.

## Antes de comenzar

- El compresor debe estar habilitado (bypass desactivado). Si el tile COMPRESSOR está oculto, habilite la etapa Comp a través del widget CHAIN primero. Consulte [Omitir el compresor desde la cadena](bypass-the-compressor-from-the-chain.md).
- El subcontenedor COMPRESSOR debe estar visible dentro del contenedor padre PooDoo Audio (TXDSP) en el panel de applets.

## Pasos

1. Localice el tile COMPRESSOR en el panel de applets.
2. Encuentre el control **Ratio** — el segundo control en la fila de cinco, etiquetado como "Ratio".
3. Haga clic y arrastre el control para establecer la relación deseada. La etiqueta debajo del control se actualiza con el formato `X.XX:1` mientras lo gira.
4. Suelte el control. El nuevo valor se guarda automáticamente en `ClientCompTxRatio`.
5. Observe cómo la curva de transferencia sobre la fila de controles y la barra de reducción de ganancia se actualizan para reflejar la nueva relación. La bola de envolvente se desplaza a lo largo del segmento de curva más pronunciado o más suave en tiempo real mientras habla.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistente |
|---|---|---|---|
| **Ratio** | 3.0 | 1.0 a 20.0 (mostrado como `X.XX:1`) | `ClientCompTxRatio` |

El control utiliza una escala logarítmica, por lo que giros pequeños en el extremo inferior ofrecen un control fino sobre relaciones suaves (p. ej., 1.5:1 a 4:1 para voz natural), mientras que los giros en el extremo superior avanzan rápidamente hacia el territorio de limitación (10:1 y superior).

## Consejos

- Una relación entre 2:1 y 4:1 es típica para voz en SSB. Las relaciones más altas (8:1 y superior) se aproximan al comportamiento de limitador y pueden causar un efecto de bombeo si el ataque y la liberación no están ajustados cuidadosamente.
- Observe la barra de reducción de ganancia mientras habla. El relleno ámbar debe alcanzar aproximadamente la marca de -6 dB para una compresión moderada. Si la barra siempre está vacía, es posible que el umbral esté configurado demasiado alto para que la relación actual lo active. Consulte [Ajustar el umbral del compresor](adjust-compressor-threshold.md).
- Tras aumentar la relación, probablemente necesite añadir ganancia de compensación para restaurar el nivel de salida promedio. Consulte [Aplicar ganancia de compensación tras la compresión](apply-make-up-gain-after-compression.md).
- Para los ajustes de rodilla y limitador avanzado (`ClientCompTxKneeDb`, `ClientCompTxLimEnabled`, `ClientCompTxLimCeilingDb`) que no están disponibles en el applet, abra el editor completo. Consulte [Abrir el editor completo del compresor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).

## Solución de problemas

- **El control Ratio no tiene efecto en el audio** — Es posible que la etapa del compresor esté en bypass. Verifique que la etapa Comp esté activa en el widget CHAIN. Consulte [Omitir el compresor desde la cadena](bypass-the-compressor-from-the-chain.md).
- **La barra de reducción de ganancia permanece vacía con relaciones altas** — La señal de entrada no está superando el umbral. Reduzca el control Thresh (`ClientCompTxThresholdDb`) o aumente la ganancia del micrófono hasta que la bola de envolvente se desplace por encima de la línea de umbral en la curva de transferencia.
- **La curva de transferencia no se actualiza tras girar el control** — Es posible que el tile COMPRESSOR aún no esté vinculado al motor de audio. Verifique que la radio esté conectada y que la cadena TX DSP esté activa.

## Temas relacionados

- [Ajustar el umbral del compresor](adjust-compressor-threshold.md)
- [Aplicar ganancia de compensación tras la compresión](apply-make-up-gain-after-compression.md)
- [Ajustar el ataque y la liberación para una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Observar la reducción de ganancia en vivo mientras habla](watch-live-gain-reduction-while-speaking.md)
- [Abrir el editor completo del compresor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Omitir el compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
