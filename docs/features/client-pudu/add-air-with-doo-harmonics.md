# Añadir aire con Doo Harmonics

Use el control Doo / Air para añadir excitación armónica y presencia en la banda de alta frecuencia. Esto eleva el "aire" percibido en TX para que su señal se destaque, o en RX para mejorar la inteligibilidad del audio entrante.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en la cadena de audio. Si no es visible, habilítela mediante el widget CHAIN en el lado TX o RX correspondiente.
- Abra el applet Aetherial TX Poodoo™ o Aetherial RX Poodoo™ en el Panel de Applets, o haga doble clic en la etapa PUDU en el widget CHAIN para abrir el editor flotante titulado "Aetherial Poodoo™ — TX" o "Aetherial Poodoo™ — RX".

## Pasos

1. Localice el grupo **Doo** — los tres controles en el lado derecho del applet, bajo la etiqueta de corchete "Doo".
2. Gire el control **Air** para establecer la cantidad de contenido armónico añadido en la banda de alta frecuencia. El valor se muestra en dB debajo del control.
3. Observe cómo aumenta el pulso del logotipo PooDoo a medida que sube el nivel de la señal procesada. Utilícelo como indicador aproximado de la cantidad de procesamiento aplicado.
4. Si el resultado es demasiado agresivo, reduzca **Air** o disminuya **Doo / Mix** para mezclar el efecto nuevamente con la señal seca.

Los ajustes se guardan automáticamente. El valor persiste en `ClientPuduTxDooHarmonicsDb` (TX) o `ClientPuduRxDooHarmonicsDb` (RX).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistente (TX / RX) | Comportamiento |
|---|---|---|---|---|
| Doo / Air | 6.0 dB | 0.0 a 24.0 dB | `ClientPuduTxDooHarmonicsDb` / `ClientPuduRxDooHarmonicsDb` | Establece la cantidad de armónicos añadidos en la banda de frecuencia Doo. Mapeo lineal. |
| Doo / Tune | 5000 Hz | 1000 a 10000 Hz | `ClientPuduTxDooTuneHz` / `ClientPuduRxDooTuneHz` | Centra la banda de excitación de alta frecuencia. Mapeo logarítmico. Se muestra como X.X kHz por encima de 1 kHz, X Hz por debajo. |
| Doo / Mix | 30 % | 0 a 100 % | `ClientPuduTxDooMix` / `ClientPuduRxDooMix` | Mezcla los agudos excitados con la señal seca. Mapeo lineal. |

## Consejos

- Comience con **Air** en 6.0 dB (valor predeterminado) y **Doo / Mix** en 30 % (valor predeterminado); luego aumente **Air** gradualmente mientras escucha el efecto sobre el material de programa.
- El control **Doo / Tune** centra la banda donde se añaden los armónicos. Ajústelo para que coincida con el pico de presencia de su micrófono en TX, o con el rango de inteligibilidad del audio entrante en RX. Consulte [Centrar Doo en la banda de presencia para su micrófono (TX) o para la inteligibilidad en RX](centre-doo-on-the-presence-band-for-your-mic-tx-or-for-rx-intelligibility.md) para conocer ese procedimiento.
- El modo Even (linaje Aphex) produce armónicos pares más cálidos; el modo Odd (linaje Behringer) produce armónicos impares más brillantes. El carácter de **Air** difiere entre ambos. Consulte [Elegir el carácter Aphex (Even) frente a Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md).

## Solución de problemas

- **El control Air no produce ningún efecto audible** — Es posible que la etapa PUDU esté omitida (bypassed). Verifique que la etapa esté habilitada en el widget CHAIN. Consulte [Omitir PUDU desde cualquier cadena](bypass-pudu-from-either-chain.md).
- **El efecto suena duro con valores moderados de Air** — Disminuya **Doo / Mix** para reducir la mezcla procesada en lugar de eliminar **Air** por completo. Consulte [Mezclar la excitación Doo con Mix](blend-the-doo-excitement-with-mix.md).

## Temas relacionados

- [Descripción general de Aetherial TX Poodoo / Aetherial RX Poodoo](overview.md)
- [Centrar Doo en la banda de presencia para su micrófono (TX) o para la inteligibilidad en RX](centre-doo-on-the-presence-band-for-your-mic-tx-or-for-rx-intelligibility.md)
- [Mezclar la excitación Doo con Mix](blend-the-doo-excitement-with-mix.md)
- [Elegir el carácter Aphex (Even) frente a Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- [Omitir PUDU desde cualquier cadena](bypass-pudu-from-either-chain.md)
