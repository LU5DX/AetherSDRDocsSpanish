# Agregar aire con Doo Harmonics

Use el control Doo / Air para agregar excitación armónica y presencia en la banda de alta frecuencia. Esto eleva el "aire" percibido en TX para que su señal sobresalga, o en RX para mejorar la inteligibilidad del audio entrante.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en la cadena de audio. Si no es visible, habilítela mediante el widget CHAIN en el lado TX o RX correspondiente.
- Abra el applet Aetherial TX Poodoo™ o Aetherial RX Poodoo™ en el panel de applets, o haga doble clic en la etapa PUDU del widget CHAIN para abrir el editor flotante titulado "Aetherial Poodoo™ — TX" o "Aetherial Poodoo™ — RX".

## Pasos

1. Ubique el grupo **Doo** — los tres controles en el lado derecho del applet, bajo la etiqueta de corchete "Doo".
2. Gire el control **Air** para establecer la cantidad de contenido armónico que se agrega en la banda de alta frecuencia. El valor se muestra en dB debajo del control.
3. Observe cómo aumenta el pulso del logotipo de PooDoo a medida que sube el nivel de la señal procesada. Úselo como indicador aproximado de cuánto procesamiento se está aplicando.
4. Si el resultado es demasiado agresivo, reduzca **Air** o disminuya **Doo / Mix** para mezclar el efecto con la señal seca.

Los ajustes se guardan automáticamente. El valor persiste en `ClientPuduTxDooHarmonicsDb` (TX) o `ClientPuduRxDooHarmonicsDb` (RX).

## Qué hace cada control

| Control | Predeterminado | Rango válido | Ajuste persistente (TX / RX) | Comportamiento |
|---|---|---|---|---|
| Doo / Air | 6.0 dB | 0.0 a 24.0 dB | `ClientPuduTxDooHarmonicsDb` / `ClientPuduRxDooHarmonicsDb` | Establece la cantidad de armónicos agregados en la banda de frecuencia Doo. Mapeo lineal. |
| Doo / Tune | 5000 Hz | 1000 a 10000 Hz | `ClientPuduTxDooTuneHz` / `ClientPuduRxDooTuneHz` | Centra la banda de excitación de alta frecuencia. Mapeo logarítmico. Se muestra como X.X kHz por encima de 1 kHz, X Hz por debajo. |
| Doo / Mix | 30 % | 0 a 100 % | `ClientPuduTxDooMix` / `ClientPuduRxDooMix` | Mezcla los agudos excitados con la señal seca. Mapeo lineal. |

## Consejos

- Comience con **Air** en 6.0 dB (predeterminado) y **Doo / Mix** en 30 % (predeterminado); luego aumente **Air** de forma gradual mientras escucha el efecto sobre el material de programa.
- El control **Doo / Tune** centra la banda donde se agregan los armónicos. Ajústelo para que coincida con el pico de presencia de su micrófono en TX, o con el rango de inteligibilidad del audio entrante en RX. Consulte [Centrar Doo en la banda de presencia de su micrófono (TX) o para inteligibilidad en RX](centre-doo-on-the-presence-band-for-your-mic-tx-or-for-rx-intelligibility.md) para conocer ese procedimiento.
- El modo Even (linaje Aphex) produce armónicos pares más cálidos; el modo Odd (linaje Behringer) produce armónicos impares más brillantes. El carácter de **Air** difiere entre ambos. Consulte [Elegir el carácter Aphex (Even) vs Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md).

## Solución de problemas

- **El control Air no produce efecto audible** — La etapa PUDU puede estar omitida. Compruebe que la etapa esté habilitada en el widget CHAIN. Consulte [Omitir PUDU desde cualquiera de las cadenas](bypass-pudu-from-either-chain.md).
- **El efecto suena áspero con valores moderados de Air** — Reduzca **Doo / Mix** para disminuir la mezcla de señal procesada en lugar de eliminar **Air** por completo. Consulte [Mezclar la excitación de Doo con Mix](blend-the-doo-excitement-with-mix.md).

## Relacionados

- [Descripción general de Aetherial TX Poodoo / Aetherial RX Poodoo](overview.md)
- [Centrar Doo en la banda de presencia de su micrófono (TX) o para inteligibilidad en RX](centre-doo-on-the-presence-band-for-your-mic-tx-or-for-rx-intelligibility.md)
- [Mezclar la excitación de Doo con Mix](blend-the-doo-excitement-with-mix.md)
- [Elegir el carácter Aphex (Even) vs Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- [Omitir PUDU desde cualquiera de las cadenas](bypass-pudu-from-either-chain.md)
