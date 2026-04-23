# Descripción general del Tube Saturator

El Tube Saturator es un procesador del lado de transmisión (TX) que moldea la señal transmitida mediante un modelo de válvula con barrido de polarización, añadiendo riqueza armónica antes de que la señal llegue al radio. Úselo para agregar calidez o carácter a SSB y otros modos de voz sin modificar nada en el radio Flex.

## Antes de comenzar

- El Tube Saturator opera sobre la cadena de audio de transmisión. No tiene efecto sobre las señales recibidas.
- La etapa TUBE debe habilitarse mediante el widget CHAIN o el editor flotante antes de que el applet sea visible en el contenedor PooDoo Audio (TXDSP).

## Cómo funciona

El Tube Saturator inserta una función de transferencia no lineal —un modelo de válvula— en la cadena de audio TX. Drive empuja la señal más profundamente hacia la región no lineal de la curva. Bias desplaza el punto de operación sobre esa curva, modificando la proporción entre armónicos pares e impares. Tone aplica una inclinación espectral posterior a la saturación para aclarar u oscurecer el resultado. Output ajusta el nivel después de la saturación para que pueda compensar cualquier cambio de ganancia. Mix mezcla la señal saturada con la señal seca, lo que permite saturación en paralelo.

La pantalla de la curva de transferencia muestra la forma actual del modelo de válvula en tiempo real. Una bola indicadora de entrada en vivo se desplaza a lo largo de la curva según el nivel de entrada real, mostrando qué parte de la curva excita la señal en cada momento. Cuando Drive es bajo y la curva es casi recta, la saturación es mínima. A medida que Drive aumenta, la curva se dobla y la bola entra en la región no lineal.

Los cambios realizados en el editor flotante (que se abre haciendo doble clic en la etapa Tube en el widget CHAIN) se reflejan en los mandos del applet en aproximadamente 33 ms, y viceversa.

Para abrir el applet: habilite la etapa Tube en el widget CHAIN. El subcontenedor TUBE aparece dentro del contenedor principal PooDoo Audio (TXDSP). Haga doble clic en la etapa Tube en el widget CHAIN para abrir el editor flotante. Haga clic derecho en la barra de título del subcontenedor TUBE para flotarlo, sacarlo o ocultarlo.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Transfer curve | Dibuja la curva de transferencia de válvula activa. La bola indicadora de entrada en vivo se mueve a lo largo de la curva según el nivel de entrada actual. Indicador de solo lectura. | — | — | — |
| Drive | Empuja más señal hacia la etapa de válvula, aumentando la saturación. | 0.0 dB | 0.0 a 24.0 dB | `ClientTubeTxDriveDb` |
| Tone | Inclina el balance de frecuencias de la señal saturada. Los valores negativos oscurecen; los positivos aclaran. | 0.00 | -1.0 a 1.0 | `ClientTubeTxTone` |
| Bias | Desplaza el punto de operación sobre la curva de transferencia, cambiando la mezcla de armónicos entre órdenes pares e impares. | 0 % | 0 % a 100 % | `ClientTubeTxBiasAmount` |
| Output | Ganancia de compensación o recorte posterior a la válvula. Úselo para compensar los cambios de nivel introducidos por la saturación. | 0.0 dB | -24.0 a 12.0 dB | `ClientTubeTxOutputGainDb` |
| Mix | Mezcla las señales seca (sin procesar) y saturada. El 100 % pasa la señal completamente saturada; el 0 % pasa la señal seca sin cambios. | 100 % | 0 % a 100 % | `ClientTubeTxDryWet` |

El estado habilitado/deshabilitado de la etapa Tube se almacena como `ClientTubeTxEnabled`. El bypass se controla desde el widget CHAIN, no desde el applet en sí.

## Consejos

- Comience con Drive en un valor bajo y observe la curva de transferencia. La bola indica qué porción de la curva utiliza su señal — trate de mantener los picos en la región levemente curvada, en lugar de presionarlos contra los límites.
- Después de aumentar Drive, use Output para devolver el nivel a su punto original, de modo que el procesamiento posterior y el nivel de audio TX se mantengan consistentes.
- Ajustar Mix por debajo del 100 % le permite mezclar solo una parte de la saturación, lo cual puede ser útil cuando desea una mejora armónica sutil sin un cambio tonal pronunciado.

## Relacionados

- [Ajuste Drive hasta que la curva comience a doblarse](dial-drive-until-the-curve-starts-to-bend.md)
- [Desplace Bias para ajustar el balance de armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Aclare u oscurezca la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compense los cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Mezcle la saturación en paralelo con Mix](parallel-blend-saturation-with-mix.md)
- [Omita la válvula desde la cadena](bypass-the-tube-from-the-chain.md)
