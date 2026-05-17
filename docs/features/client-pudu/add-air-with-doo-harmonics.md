# Añada aire con Doo Harmonics

Use el mando **Doo / Air** para agregar emoción armónica y presencia en la banda de altas frecuencias. Esto eleva la percepción de "aire" en TX para que su señal destaque, o en RX para mejorar la inteligibilidad del audio entrante.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en la cadena de audio. Si no es visible, actívala a través del widget CHAIN en el lado TX o RX correspondiente.
- Abra el applet Aetherial TX Voice Processor o Aetherial RX Poodoo™ en el Panel de applets, o haga doble clic en la etapa PUDU en el widget CHAIN para abrir el editor flotante titulado "Aetherial Poodoo™ — TX" o "Aetherial Poodoo™ — RX".

## Pasos

1. Localice el grupo **Clarity**: los tres mandos en el lado derecho del applet, bajo la etiqueta del grupo "Clarity".
2. Gire el mando **Air** para ajustar la cantidad de contenido armónico agregado en la banda de altas frecuencias. El valor se muestra en dB debajo del mando.
3. Observe cómo el pulso del logo AetherVoice aumenta a medida que sube el nivel de la señal procesada (wet). Úselo como un indicador aproximado de cuánto procesamiento se está aplicando.
4. Si el resultado es demasiado agresivo, reduzca **Air** o baje **Doo / Mix** para mezclar el efecto con la señal seca (dry).

Los ajustes se guardan automáticamente. El valor persiste en `ClientPuduTxDooHarmonicsDb` (TX) o `ClientPuduRxDooHarmonicsDb` (RX).

## Edición inline de valores

A partir de la versión 26.5.2, puede escribir un valor exacto directamente sobre el mando en lugar de arrastrarlo. Haga clic en el texto del valor debajo de cualquier mando para revelar un editor inline. Escriba un número y presione Enter o haga clic en otro lugar para confirmar. El valor se limita automáticamente al rango válido. Presione Escape para cancelar la edición y volver al valor anterior.

## Qué hace cada control

| Control          | Predeterminado                                                                            | Rango válido                              |
|------------------|-------------------------------------------------------------------------------------------|-------------------------------------------|
| Doo / Air        | 6.0 dB                                                                                    | 0.0 a 24.0 dB                             |
| Doo / Tune       | 5000 Hz                                                                                   | 1000 a 10000 Hz                           |
| Doo / Mix        | 30 %                                                                                      | 0 a 100 %                                 |
| Logo AetherVoice | Logotipo animado que pulsa con el RMS de la señal procesada. Muestra la marca 'AetherVoice™'. | Widget PooDooLogo — altura mínima 40 px.  |

## Consejos

- Comience con **Air** en 6.0 dB (predeterminado) y **Doo / Mix** en 30 % (predeterminado), luego aumente **Air** gradualmente mientras escucha el efecto en el material de programa.
- El mando **Doo / Tune** centra la banda donde se agregan los armónicos. Ajústelo para que coincida con el pico de presencia de su micrófono en TX, o con el rango de inteligibilidad del audio entrante en RX. Consulte [Centre Doo on the presence band for your mic (TX) or for RX intelligibility](centre-doo-on-the-presence-band-for-your-mic-tx-or-for-rx-intelligibility.md) para ese procedimiento.
- El modo Even (linaje Aphex) produce armónicos pares más cálidos; el modo Odd (linaje Behringer) produce armónicos impares más brillantes. El carácter de **Air** difiere entre ambos. Consulte [Pick Even vs Odd mode](pick-aphex-even-vs-behringer-odd-character.md).
- Use la edición inline para establecer rápidamente valores precisos: haga clic en el valor mostrado, escriba el número con unidades si lo desea y presione Enter.

## Solución de problemas

- **El mando Air no tiene efecto audible** — La etapa PUDU puede estar en bypass. Cuando la etapa está en bypass, todo el applet se atenúa con opacidad reducida. Verifique que la etapa esté habilitada en el widget CHAIN. Consulte [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md).
- **El efecto suena áspero con valores moderados de Air** — Baje **Doo / Mix** para reducir la mezcla procesada en lugar de eliminar **Air** por completo. Consulte [Blend the Doo excitement with Mix](blend-the-doo-excitement-with-mix.md).

## Relacionados

- [Aetherial TX Voice Processor / Aetherial RX Poodoo overview](overview.md)
- [Centre Doo on the presence band for your mic (TX) or for RX intelligibility](centre-doo-on-the-presence-band-for-your-mic-tx-or-for-rx-intelligibility.md)
- [Blend the Doo excitement with Mix](blend-the-doo-excitement-with-mix.md)
- [Pick Even vs Odd mode](pick-aphex-even-vs-behringer-odd-character.md)
- [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md)
