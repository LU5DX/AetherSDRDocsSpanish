# Impulse el compresor con más fuerza mediante la ganancia previa a la compresión para reducir la PAPR

La ganancia previa a la compresión (Drive) introduce más señal en el compresor para que actúe con más intensidad, elevando la potencia media sin aumentar la potencia pico. Combínela con el Rotador de Fase para mantener los picos limpios y reducir la relación potencia pico a potencia media (PAPR) de su señal transmitida.

## Antes de comenzar

- Abra el editor completo del compresor: haga doble clic en el mosaico COMP del widget CHAIN en el lado de TX. El editor flotante se titula "Aetherial Compressor — TX".
- El compresor debe estar habilitado (sin bypass) para que Drive surta efecto.

## Pasos

1. En el editor flotante del compresor, localice el mando **Drive** en la columna derecha.
2. Haga clic y arrastre hacia arriba en el mando Drive para añadir ganancia. El valor predeterminado es 0,0 dB; el rango válido es de 0,0 a 18,0 dB.
3. Mientras habla por su micrófono, observe la barra de reducción de ganancia en el mosaico del applet de TX. Al aumentar Drive, el relleno ámbar debería mostrar más reducción a medida que el compresor trabaja con más intensidad.
4. Ajuste el mando **Phase** (0–6 etapas) para rotar la simetría de fase de la voz. Comience con 4 etapas (el valor predeterminado de radiodifusión) y escuche si los picos se ven más limpios.
5. Observe la "bola" en vivo sobre la curva de transferencia; debería desplazarse más hacia la región de compresión a medida que aumenta Drive.

## Función de cada control

| Control                 | Etiqueta                                                                                                                                                                                                                                                                                                                             | Valor predeterminado                                                                                                                                                                                                                                                                                                                                                              |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Ganancia previa a la compresión | Drive                                                                                                                                                                                                                                                                                                                                | 0,0 dB                                                                                                                                                                                                                                                                                                                                                                            |
| Rotación de fase        | Phase                                                                                                                                                                                                                                                                                                                                | 0 etapas                                                                                                                                                                                                                                                                                                                                                                          |
| Drive                   | Aumento de ganancia previa a la compresión con ecualización automática vinculada. Introduce más señal por encima del umbral para que el compresor actúe con más intensidad y, simultáneamente, añade la misma ganancia en la salida, de modo que el RMS promedio se eleva junto con los picos en lugar de descender. Combínelo con Phase para mantener los picos limpios. | Se muestra únicamente en el StripCompPanel flotante (columna derecha). La etiqueta aparece como '+X.X dB'. La información sobre herramientas explica la combinación para reducir la PAPR. La ecualización automática sigue el modelo broadcast-Optimod: Drive introduce más material en la curva Y añade la misma ganancia de vuelta, de modo que el mando Makeup fijado por el usuario sigue siendo un control de recorte posterior limpio. |
| Phase                   | Número de secciones de paso total en cascada (0 = desactivado). Cada etapa añade 12 dB/octava de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más opcionalmente 1000/2000 Hz). Simetriza los picos asimétricos de la voz antes de la compresión para reducir la PAPR.                                          | Se muestra únicamente en el StripCompPanel flotante (columna derecha). La etiqueta muestra 'Off' cuando es 0, 'N stg' cuando está activo. Información sobre herramientas: 'Rotador de fase previo a la compresión. Cascada de paso total que simetriza los picos asimétricos de la voz antes de la compresión. 0 = desactivado, 4 = valor predeterminado de radiodifusión.' Los centros predeterminados (300/700/1500/2500 Hz con opcional 1000/2000 Hz) cubren el rango de formantes del habla sin agruparse. |

## Consejos

- El mosaico del applet ahora utiliza colores adaptados al tema para el widget de la curva de compresión. El fondo, la cuadrícula, las etiquetas de los ejes, la curva y la bola siguen el tema de color activo. La barra de reducción de ganancia se rellena con el color de acento del deslizador definido por el tema.
- Drive solo está disponible en el editor flotante StripCompPanel (columna derecha), no en el mosaico compacto del applet. Haga doble clic en el mosaico COMP del widget CHAIN para abrirlo.
- La etiqueta muestra un signo más para valores positivos (p. ej., "+6.0 dB").
- Si aumenta Drive de forma significativa, es posible que deba ajustar el umbral (Threshold) o la ganancia de ecualización (Makeup) para mantener el nivel de audio deseado.

## Relacionados

- [Abra el editor completo del compresor para los controles de rodilla, limitador, Drive y Phase](open-the-full-compressor-editor-for-knee-limiter-drive-and-phase-controls.md)
- [Rote la simetría de fase de la voz con el rotador de fase (0–6 etapas)](rotate-voice-phase-symmetry-with-the-phase-rotator-0-6-stages.md)
- [Ajuste el umbral del compresor (lado TX o RX)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Aplique ganancia de ecualización después de la compresión](apply-make-up-gain-after-compression.md)
