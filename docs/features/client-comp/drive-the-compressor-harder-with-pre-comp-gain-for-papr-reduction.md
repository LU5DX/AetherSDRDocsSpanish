# Aumente la fuerza del compresor con la ganancia previa a la compresión para reducir la PAPR

La ganancia previa a la compresión (Drive) introduce más señal en el compresor para que actúe con mayor intensidad, elevando la potencia promedio sin aumentar la potencia pico. Combínela con el Rotador de Fase para mantener los picos limpios y reducir la relación entre potencia pico y potencia promedio (PAPR) de su señal transmitida.

## Antes de comenzar

- Abra el editor completo del Compresor: haga doble clic en el mosaico COMP en el widget CHAIN del lado de TX. El editor flotante tiene el título "Aetherial Compressor — TX".
- El compresor debe estar habilitado (sin bypass) para que Drive surta efecto.

## Pasos

1. En el editor flotante del Compresor, localice el control **Drive** en la columna derecha.
2. Haga clic y arrastre hacia arriba sobre el control Drive para agregar ganancia. El valor predeterminado es 0.0 dB; el rango válido es de 0.0 a 18.0 dB.
3. Mientras habla por el micrófono, observe la barra de reducción de ganancia en el mosaico del applet de TX. A medida que aumenta Drive, el relleno ámbar debería mostrar más reducción, indicando un trabajo más intenso del compresor.
4. Ajuste el control **Phase** (0 a 6 etapas) para rotar la simetría de fase de la voz. Comience con 4 etapas (el valor predeterminado de transmisión) y escuche buscando picos más limpios.
5. Observe la "bola" en vivo sobre la curva de transferencia: debería moverse más hacia la región de compresión a medida que aumenta Drive.

## Función de cada control

| Control | Etiqueta | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|----------|----------------------|-------|------------------------|----------------|
| Ganancia previa a la compresión | Drive | 0.0 dB | 0.0 a 18.0 dB | `ClientCompTxDriveDb` | Aumenta el nivel de audio antes del compresor. Los valores más altos introducen más señal por encima del umbral, incrementando la potencia promedio. |
| Rotación de fase | Phase | 0 etapas | 0 a 6 etapas | `ClientCompTxPhaseRotatorStages` | Número de secciones de paso total en cascada. Cada etapa agrega 12 dB/octava de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más 1000/2000 Hz opcionales). Simetriza los picos asimétricos de la voz para reducir la PAPR. 0 = desactivado; 4 = valor predeterminado de transmisión. |

## Consejos

- Drive solo está disponible en el editor flotante StripCompPanel (columna derecha), no en el mosaico compacto del applet. Para abrirlo, haga doble clic en el mosaico COMP en el widget CHAIN.
- La etiqueta muestra un signo más para valores positivos (p. ej., "+6.0 dB").
- Si aumenta Drive significativamente, es posible que deba ajustar el umbral (Threshold) o la ganancia de compensación (Makeup gain) para mantener el nivel de audio deseado.

## Relacionados

- [Open the full Compressor editor for knee, limiter, Drive, and Phase controls](open-the-full-compressor-editor-for-knee-limiter-drive-and-phase-controls.md)
- [Rotate voice phase symmetry with the Phase rotator (0–6 stages)](rotate-voice-phase-symmetry-with-the-phase-rotator-0-6-stages.md)
- [Adjust compressor threshold (TX or RX side)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
