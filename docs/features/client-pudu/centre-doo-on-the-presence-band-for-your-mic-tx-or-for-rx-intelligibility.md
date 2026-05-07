# Enfoque de la Claridad en la banda de presencia para su micrófono (TX) o para la inteligibilidad de RX

El mando **Doo / Tune** establece la frecuencia central de la banda de realce de alta frecuencia. Ajustarlo le permite enfocar la región de presencia o inteligibilidad que más le interese — el "bite" de medios agudos de su micrófono en TX, o la banda de claridad del habla en RX.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en el widget CHAIN para el lado que desea ajustar (TX o RX). Consulte [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md). Cuando la etapa está en bypass, el panel completo del applet se oscurece a aproximadamente un 55 % de opacidad como recordatorio visual de que el DSP está inactivo.
- Abra el applet correspondiente: **Aetherial TX Voice Processor** para transmisión, **Aetherial RX Poodoo™** para recepción. Ambos se encuentran dentro del contenedor principal Aetherial Audio (TXDSP). También puede hacer doble clic en la etapa PUDU del widget CHAIN para abrir el editor frameless correspondiente (titulado **Aetherial Poodoo™ — TX** o **Aetherial Poodoo™ — RX**).

## Pasos

1. Localice el grupo **Doo** — el soporte derecho de la fila de seis mandos.
2. Encuentre el primer mando bajo el soporte **Doo**, etiquetado como **Tune**.
3. Gire **Doo / Tune** hasta la frecuencia que cubra el rango de presencia que desea realzar.
   - Para un pico típico de presencia en micrófono TX, pruebe el rango de 3 kHz – 6 kHz.
   - Para inteligibilidad del habla en RX, pruebe de 2 kHz – 4 kHz.
   - El mando muestra su valor como **X.X kHz** desde 1000 Hz en adelante.
4. Supervise el logotipo de PooDoo — su brillo de pulso refleja el nivel de la señal procesada (húmeda) y proporciona una indicación en tiempo real de que la sección Clarity está activa.
5. Ajuste **Doo / Air** y **Doo / Mix** según su gusto después de establecer la frecuencia central. Consulte [Add air with Doo Harmonics](add-air-with-doo-harmonics.md) y [Blend the Doo excitement with Mix](blend-the-doo-excitement-with-mix.md).

## Función de cada control

| Control | Valor predeterminado | Rango válido | Configuración persistente | Comportamiento |
|---|---|---|---|---|
| **Doo / Tune** (TX) | 5000 Hz | 1000 – 10000 Hz | `ClientPuduTxDooTuneHz` | Mapeo logarítmico. Centra la banda de realce de alta frecuencia en TX. Se muestra como X.X kHz por encima de 1 kHz. |
| **Doo / Tune** (RX) | 5000 Hz | 1000 – 10000 Hz | `ClientPuduRxDooTuneHz` | Mapeo logarítmico. Centra la banda de realce de alta frecuencia en RX. |
| **Doo / Air** (TX) | 6,0 dB | 0,0 – 24,0 dB | `ClientPuduTxDooHarmonicsDb` | Cantidad de armónicos añadidos en la banda Clarity. |
| **Doo / Air** (RX) | 6,0 dB | 0,0 – 24,0 dB | `ClientPuduRxDooHarmonicsDb` | Cantidad de armónicos añadidos en la banda Clarity. |
| **Doo / Mix** (TX) | 30 % | 0 – 100 % | `ClientPuduTxDooMix` | Mezcla la banda alta realzada con la señal seca. |
| **Doo / Mix** (RX) | 30 % | 0 – 100 % | `ClientPuduRxDooMix` | Mezcla la banda alta realzada con la señal seca. |

## Consejos

- **Doo / Tune** utiliza un mapeo logarítmico, por lo que la mitad superior del recorrido del mando cubre un intervalo de frecuencias más amplio que la mitad inferior. Realice pequeños ajustes cuando trabaje por encima de 5 kHz.
- Las instancias de TX y RX son completamente independientes. Ajustar una frecuencia Doo en TX no tiene efecto en RX.
- El modo **Even** (linaje Aphex) añade armónicos asimétricos en la banda Clarity — un carácter más cálido. El modo **Odd** (linaje Behringer) añade armónicos impares simétricos — más brillante y adelantado. El mejor punto de Doo / Tune puede diferir entre modos. Consulte [Pick Aphex (Even) vs Behringer (Odd) character](pick-aphex-even-vs-behringer-odd-character.md).
- Si el panel del applet aparece atenuado, la etapa PUDU está en bypass. Vuelva a habilitarla en el widget CHAIN antes de realizar ajustes.

## Relacionados

- [Aetherial TX Voice Processor / Aetherial RX Poodoo overview](overview.md)
- [Add air with Doo Harmonics](add-air-with-doo-harmonics.md)
- [Blend the Doo excitement with Mix](blend-the-doo-excitement-with-mix.md)
- [Pick Aphex (Even) vs Behringer (Odd) character](pick-aphex-even-vs-behringer-odd-character.md)
- [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md)
