# Enfoque de Claridad en la banda de presencia para su micrófono (TX) o para inteligibilidad en RX

El mando **Doo / Tune** establece la frecuencia central de la banda de excitación de altas frecuencias. Al moverlo, puede apuntar a la región específica de presencia o inteligibilidad que más le interese: el toque de medios altos de su micrófono en TX, o la banda de claridad del habla en RX.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en el widget CHAIN para el lado que desea ajustar (TX o RX). Consulte [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md). Cuando la etapa está en bypass, todo el mosaico del applet se atenúa aproximadamente al 55 % de opacidad como recordatorio visual de que el DSP está inactivo.
- Abra el applet correspondiente: **Aetherial TX Voice Processor** para transmisión, **Aetherial RX Poodoo™** para recepción. Ambos se encuentran dentro del contenedor principal Aetherial Audio (TXDSP). También puede hacer doble clic en la etapa PUDU en el widget CHAIN para abrir el editor sin marco correspondiente (titulado **Aetherial Poodoo™ — TX** o **Aetherial Poodoo™ — RX**).

## Pasos

1. Localice el grupo **Clarity**: el corchete derecho de la fila de seis mandos.
2. Encuentre el primer mando debajo del corchete **Clarity**, etiquetado **Tune**.
3. Gire **Doo / Tune** a la frecuencia que cubra el rango de presencia que desea potenciar.
   - Para un pico típico de presencia en el micrófono en TX, pruebe el rango de 3 kHz – 6 kHz.
   - Para inteligibilidad del habla en RX, pruebe 2 kHz – 4 kHz.
   - El mando muestra su valor como **X.X kHz** a partir de 1000 Hz.
4. Supervise el logotipo AetherVoice: el brillo de su pulso refleja el nivel de la señal procesada (wet) y proporciona una indicación en tiempo real de que la sección Clarity está activa.
5. Opcionalmente, haga clic en el texto del valor de cualquier mando para introducir un valor preciso mediante el editor en línea. Escriba el número deseado y presione Intro, o haga clic en otro lugar para confirmar. El valor se limita automáticamente al rango válido.
6. Ajuste **Doo / Air** y **Doo / Mix** a su gusto después de establecer la frecuencia central. Consulte [Add air with Doo Harmonics](add-air-with-doo-harmonics.md) y [Blend the Doo excitement with Mix](blend-the-doo-excitement-with-mix.md).

## Función de cada control

| Control             | Valor predeterminado                                                                        | Rango válido                            |
|---------------------|---------------------------------------------------------------------------------------------|-----------------------------------------|
| **Doo / Tune** (TX) | 5000 Hz                                                                                     | 1000 – 10000 Hz                         |
| **Doo / Tune** (RX) | 5000 Hz                                                                                     | 1000 – 10000 Hz                         |
| **Doo / Air** (TX)  | 6.0 dB                                                                                      | 0.0 – 24.0 dB                           |
| **Doo / Air** (RX)  | 6.0 dB                                                                                      | 0.0 – 24.0 dB                           |
| **Doo / Mix** (TX)  | 30 %                                                                                        | 0 – 100 %                               |
| **Doo / Mix** (RX)  | 30 %                                                                                        | 0 – 100 %                               |
| Logotipo AetherVoice| Logotipo animado que pulsa con el RMS de la señal wet. Muestra la marca 'AetherVoice™'.     | Widget PooDooLogo — altura mínima 40 px.|
| Etiqueta grupo Clarity| Etiqueta del corchete para los tres mandos del procesador de altas frecuencias (Tune, Air, Mix).| —                                       |

## Consejos

- **Doo / Tune** utiliza una asignación logarítmica, por lo que la mitad superior del recorrido del mando cubre un rango de frecuencia más amplio que la mitad inferior. Realice ajustes pequeños cuando trabaje por encima de 5 kHz.
- Las instancias de TX y RX son completamente independientes. Ajustar una frecuencia Doo en TX no tiene efecto en RX.
- El modo **Even** (herencia Aphex) añade armónicos asimétricos en la banda de claridad — carácter más cálido. El modo **Odd** (herencia Behringer) añade armónicos impares simétricos — más brillante y adelantado. El mejor punto de Doo / Tune puede diferir entre modos. Consulte [Pick Aphex (Even) vs Behringer (Odd) character](pick-aphex-even-vs-behringer-odd-character.md).
- Si el mosaico del applet aparece atenuado, la etapa PUDU está en bypass. Vuelva a habilitarla en el widget CHAIN antes de realizar ajustes.
- Use el editor en línea para escribir frecuencias exactas. Haga clic en el valor mostrado para activar el editor, escriba un número y presione Intro. El análisis acepta separadores decimales de punto y coma según la configuración regional. Los valores no válidos se revierten silenciosamente al valor anterior.

## Relacionados

- [Aetherial TX Voice Processor / Aetherial RX Poodoo overview](overview.md)
- [Add air with Doo Harmonics](add-air-with-doo-harmonics.md)
- [Blend the Doo excitement with Mix](blend-the-doo-excitement-with-mix.md)
- [Pick Aphex (Even) vs Behringer (Odd) character](pick-aphex-even-vs-behringer-odd-character.md)
- [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md)
