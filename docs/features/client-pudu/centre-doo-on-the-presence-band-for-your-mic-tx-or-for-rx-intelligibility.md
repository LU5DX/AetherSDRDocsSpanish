# Centre Doo en la banda de presencia para su micrófono (TX) o para la inteligibilidad en RX

El mando **Doo / Tune** establece la frecuencia central de la banda de excitación de alta frecuencia. Desplazarlo permite apuntar a la región de presencia o inteligibilidad que más importa: el mordiente de rango medio-alto de su micrófono en TX, o la banda de claridad de voz en RX.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en el widget CHAIN para el lado que desea ajustar (TX o RX). Consulte [Omitir PUDU desde cualquiera de las cadenas](bypass-pudu-from-either-chain.md).
- Abra el applet correspondiente: **Aetherial TX Poodoo™** para transmisión, **Aetherial RX Poodoo™** para recepción. Ambos se encuentran dentro del contenedor principal Aetherial Audio (TXDSP). También puede hacer doble clic en la etapa PUDU en el widget CHAIN para abrir el editor sin marco correspondiente (titulado **Aetherial Poodoo™ — TX** o **Aetherial Poodoo™ — RX**).

## Pasos

1. Localice el grupo **Doo** — el corchete derecho de la fila de seis mandos.
2. Encuentre el primer mando bajo el corchete **Doo**, etiquetado como **Tune**.
3. Gire **Doo / Tune** hasta la frecuencia que cubra el rango de presencia que desea realzar.
   - Para un pico de presencia típico de micrófono en TX, pruebe el rango de 3 kHz – 6 kHz.
   - Para inteligibilidad de voz en RX, pruebe entre 2 kHz – 4 kHz.
   - El mando muestra su valor como **X.X kHz** a partir de 1000 Hz.
4. Observe el logotipo de PooDoo — su brillo pulsante refleja el nivel de la señal húmeda procesada e indica en tiempo real que la sección Doo está activa.
5. Ajuste **Doo / Air** y **Doo / Mix** según su preferencia tras establecer la frecuencia central. Consulte [Añadir aire con los armónicos Doo](add-air-with-doo-harmonics.md) y [Mezclar la excitación Doo con Mix](blend-the-doo-excitement-with-mix.md).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistido | Comportamiento |
|---|---|---|---|---|
| **Doo / Tune** (TX) | 5000 Hz | 1000 – 10000 Hz | `ClientPuduTxDooTuneHz` | Mapeo logarítmico. Centra la banda de excitación de alta frecuencia en TX. Se muestra como X.X kHz por encima de 1 kHz. |
| **Doo / Tune** (RX) | 5000 Hz | 1000 – 10000 Hz | `ClientPuduRxDooTuneHz` | Mapeo logarítmico. Centra la banda de excitación de alta frecuencia en RX. |
| **Doo / Air** (TX) | 6.0 dB | 0.0 – 24.0 dB | `ClientPuduTxDooHarmonicsDb` | Cantidad de armónicos añadidos en la banda Doo. |
| **Doo / Air** (RX) | 6.0 dB | 0.0 – 24.0 dB | `ClientPuduRxDooHarmonicsDb` | Cantidad de armónicos añadidos en la banda Doo. |
| **Doo / Mix** (TX) | 30 % | 0 – 100 % | `ClientPuduTxDooMix` | Mezcla la banda alta excitada con la señal seca. |
| **Doo / Mix** (RX) | 30 % | 0 – 100 % | `ClientPuduRxDooMix` | Mezcla la banda alta excitada con la señal seca. |

## Consejos

- **Doo / Tune** utiliza mapeo logarítmico, por lo que la mitad superior del recorrido del mando abarca un rango de frecuencias más amplio que la mitad inferior. Realice ajustes pequeños cuando trabaje por encima de 5 kHz.
- Las instancias de TX y RX son completamente independientes. Establecer una frecuencia Doo en TX no tiene efecto sobre RX.
- El modo **Even** (linaje Aphex) añade armónicos asimétricos en la banda Doo — carácter más cálido. El modo **Odd** (linaje Behringer) añade armónicos impares simétricos — más brillante y directo. El punto óptimo de **Doo / Tune** puede variar entre modos. Consulte [Elegir el carácter Aphex (Even) o Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md).

## Relacionados

- [Descripción general de Aetherial TX Poodoo / Aetherial RX Poodoo](overview.md)
- [Añadir aire con los armónicos Doo](add-air-with-doo-harmonics.md)
- [Mezclar la excitación Doo con Mix](blend-the-doo-excitement-with-mix.md)
- [Elegir el carácter Aphex (Even) o Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- [Omitir PUDU desde cualquiera de las cadenas](bypass-pudu-from-either-chain.md)
