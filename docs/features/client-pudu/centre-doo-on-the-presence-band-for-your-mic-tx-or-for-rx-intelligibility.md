# Claridad del centro en la banda de presencia para su micrófono (TX) o para la inteligibilidad de RX

El mando **Doo / Tune** establece la frecuencia central de la banda de excitación de altas frecuencias. Moverlo le permite apuntar a la región específica de presencia o inteligibilidad que más le interese: el ataque de gama media-aguda de su micrófono en TX, o la banda de claridad del habla en RX.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en el widget CHAIN para el lado que desea ajustar (TX o RX). Consulte [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md). Cuando la etapa está desviada, todo el mosaico del applet se atenúa aproximadamente al 55 % de opacidad como recordatorio visual de que el DSP está inactivo.
- Abra el applet correspondiente: **Aetherial TX Voice Processor** para transmisión, **Aetherial RX Poodoo™** para recepción. Ambos se encuentran dentro del contenedor principal Aetherial Audio (TXDSP). También puede hacer doble clic en la etapa PUDU en el widget CHAIN para abrir el editor sin marco correspondiente (titulado **Aetherial Poodoo™ — TX** o **Aetherial Poodoo™ — RX**).

## Pasos

1. Localice el grupo **Clarity**: el corchete derecho de la fila de seis mandos.
2. Encuentre el primer mando bajo el corchete **Clarity**, etiquetado como **Tune**.
3. Gire **Doo / Tune** a la frecuencia que cubra el rango de presencia que desea realzar.
   - Para un pico de presencia típico de micrófono en TX, pruebe el rango de 3 kHz a 6 kHz.
   - Para inteligibilidad del habla en RX, pruebe de 2 kHz a 4 kHz.
   - El mando muestra su valor como **X.X kHz** a 1000 Hz y superiores.
4. Monitoree el logotipo de AetherVoice: el brillo de su pulso refleja el nivel de la señal húmeda procesada y proporciona una indicación en tiempo real de que la sección Clarity está activa.
5. Opcionalmente, haga clic en el texto del valor de cualquier mando para ingresar un valor preciso usando el editor incorporado. Escriba el número deseado y presione Enter, o haga clic en otro lugar para confirmar. El valor se ajusta automáticamente al rango válido.
6. Ajuste **Doo / Air** y **Doo / Mix** al gusto después de establecer la frecuencia central. Consulte [Add air with Doo Harmonics](add-air-with-doo-harmonics.md) y [Blend the Doo excitement with Mix](blend-the-doo-excitement-with-mix.md).

## Qué hace cada control

| Control              | Por defecto                                   | Rango válido                              |
|----------------------|-----------------------------------------------|-------------------------------------------|
| **Doo / Tune** (TX)  | 5000 Hz                                       | 1000 – 10000 Hz                           |
| **Doo / Tune** (RX)  | 5000 Hz                                       | 1000 – 10000 Hz                           |
| **Doo / Air** (TX)   | 6.0 dB                                        | 0.0 – 24.0 dB                             |
| **Doo / Air** (RX)   | 6.0 dB                                        | 0.0 – 24.0 dB                             |
| **Doo / Mix** (TX)   | 30 %                                          | 0 – 100 %                                 |
| **Doo / Mix** (RX)   | 30 %                                          | 0 – 100 %                                 |
| Logotipo AetherVoice | Logotipo animado de marca que pulsa con el RMS de la señal húmeda. Muestra la marca 'AetherVoice™'. | Widget PooDooLogo — altura mínima de 40 px. |
| Etiqueta grupo Clarity | Etiqueta de corchete para los tres mandos del procesador de alta frecuencia (Tune, Air, Mix). | —                                         |

## Consejos

- **Doo / Tune** utiliza una asignación logarítmica, por lo que la mitad superior del recorrido del mando cubre un rango de frecuencias más amplio que la mitad inferior. Realice ajustes pequeños cuando trabaje por encima de 5 kHz.
- Las instancias de TX y RX son completamente independientes. Establecer una frecuencia Doo en TX no tiene efecto en RX.
- El modo **Even** (linaje Aphex) añade armónicos asimétricos en la banda Clarity: carácter más cálido. El modo **Odd** (linaje Behringer) añade armónicos impares simétricos: más brillante y más frontal. El mejor punto de Doo / Tune puede diferir entre modos. Consulte [Pick Aphex (Even) vs Behringer (Odd) character](pick-aphex-even-vs-behringer-odd-character.md).
- Si el mosaico del applet aparece atenuado, la etapa PUDU está desviada. Vuelva a habilitarla en el widget CHAIN antes de realizar ajustes.
- Use el editor incorporado para escribir frecuencias exactas. Haga clic en el valor mostrado para activar el editor, escriba un número y presione Enter. El análisis, sensible a la configuración regional, acepta tanto el punto como la coma como separadores decimales. Los valores no válidos se revierten silenciosamente al valor anterior.
- Los colores de los mandos (anillo de fondo, arco de valor, puntero, texto de etiqueta y texto de valor) se obtienen del tema actual mediante los espacios de nombres `color.knob.*` y `color.text.*`. El applet PUDU se registra bajo el contenedor de tema `applet/pudu`, por lo que cualquier anulación de color por applet (por ejemplo, un color ámbar en el primer plano del mando) afecta a los mandos de PUDU sin afectar a los mandos de otros applets. Las etiquetas de corchete "Body" y "Clarity" también usan texto temático a través de `color.text.primary`.

## Relacionados

- [Aetherial TX Voice Processor / Aetherial RX Poodoo overview](overview.md)
- [Add air with Doo Harmonics](add-air-with-doo-harmonics.md)
- [Blend the Doo excitement with Mix](blend-the-doo-excitement-with-mix.md)
- [Pick Aphex (Even) vs Behringer (Odd) character](pick-aphex-even-vs-behringer-odd-character.md)
- [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md)
