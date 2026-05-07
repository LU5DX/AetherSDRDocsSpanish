# Combine la emoción del Doo con el Mix

Use el mando **Doo / Mix** para controlar cuánta excitación de alta frecuencia del Doo se mezcla de nuevo con la señal seca. Si ajusta Mix demasiado alto, puede introducir aspereza; si lo ajusta demasiado bajo, el procesamiento Doo tendrá poco efecto audible.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en el widget CHAIN para el lado correspondiente (TX o RX). Consulte [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md).
- Abra el editor Poodoo haciendo doble clic en la etapa PUDU en el widget CHAIN. El editor se titula "Aetherial Voice Processor — TX" o "Aetherial Voice Processor — RX", según el lado en el que esté trabajando.
- Cuando la etapa PUDU está desviada, todo el mosaico del applet se atenúa hasta aproximadamente un 55 % de opacidad. Esto es solo un indicador visual: la configuración de sus mandos se conserva. Vuelva a habilitar la etapa para restaurar la opacidad completa y el procesamiento activo.

## Pasos

1. Localice el grupo **Doo**: los tres mandos en el lado derecho de la fila de mandos, bajo la etiqueta del soporte "Doo".
2. Identifique el tercer mando del grupo Doo, etiquetado como **Mix**.
3. Gire el mando **Mix** para mezclar la señal excitada de alta frecuencia con la señal seca. El valor se muestra como un porcentaje directamente en el mando.
4. Suelte el mando. El ajuste se guarda automáticamente.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Ajuste persistido |
|---|---|---|---|
| Doo / Mix (TX) | 30 % | 0 % a 100 % | `ClientPuduTxDooMix` |
| Doo / Mix (RX) | 30 % | 0 % a 100 % | `ClientPuduRxDooMix` |

El mando tiene una asignación lineal. Al 0 %, el procesador Doo se mezcla completamente y no tiene efecto sobre la señal. Al 100 %, solo pasa la señal procesada; no se mezcla señal seca. Los lados TX y RX mantienen valores Mix completamente independientes.

## Consejos

- Comience con el valor predeterminado del 30 % y auméntelo gradualmente mientras escucha el efecto en la presencia o la inteligibilidad.
- El logotipo de PooDoo parpadea con el RMS de la señal húmeda. Un pulso más rápido y fuerte al aumentar Mix confirma que la etapa Doo está contribuyendo a la salida.
- Si aún no ha posicionado la banda Doo en la frecuencia correcta, ajuste Mix al 0 % temporalmente mientras ajusta Doo / Tune, luego vuelva a subir Mix. Consulte [Centre Doo on the presence band for your mic (TX) or for RX intelligibility](centre-doo-on-the-presence-band-for-your-mic-tx-or-for-rx-intelligibility.md).

## Relacionado

- [Add air with Doo Harmonics](add-air-with-doo-harmonics.md)
- [Centre Doo on the presence band for your mic (TX) or for RX intelligibility](centre-doo-on-the-presence-band-for-your-mic-tx-or-for-rx-intelligibility.md)
- [Blend the Poo enhancement with Mix](blend-the-poo-enhancement-with-mix.md)
- [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md)
- [Aetherial TX Voice Processor / Aetherial RX Poodoo overview](overview.md)
