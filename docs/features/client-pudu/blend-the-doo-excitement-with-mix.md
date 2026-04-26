# Mezcle la excitación Doo con Mix

Use el control Doo / Mix para regular cuánto de la excitación de altas frecuencias de Doo se mezcla de vuelta en la señal seca. Un valor de Mix demasiado alto puede introducir aspereza; un valor demasiado bajo hace que el procesamiento Doo tenga poco efecto audible.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en el widget CHAIN para el lado correspondiente (TX o RX). Consulte [Omitir PUDU desde cualquiera de las cadenas](bypass-pudu-from-either-chain.md).
- Abra el editor Poodoo haciendo doble clic en la etapa PUDU dentro del widget CHAIN. El editor se titula "Aetherial Poodoo™ — TX" o "Aetherial Poodoo™ — RX" según el lado en el que esté trabajando.

## Pasos

1. Localice el grupo **Doo** — los tres controles a la derecha de la fila de mandos, bajo la etiqueta de corchete "Doo".
2. Identifique el tercer control del grupo Doo, denominado **Mix**.
3. Gire el mando **Mix** para mezclar la señal de altas frecuencias excitada con la señal seca. El valor se muestra como porcentaje directamente sobre el mando.
4. Suelte el mando. El ajuste se guarda automáticamente.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistido |
|---|---|---|---|
| Doo / Mix (TX) | 30 % | 0 % a 100 % | `ClientPuduTxDooMix` |
| Doo / Mix (RX) | 30 % | 0 % a 100 % | `ClientPuduRxDooMix` |

El mando tiene una respuesta lineal. Al 0 %, el procesador Doo queda completamente excluido de la mezcla y no tiene efecto sobre la señal. Al 100 %, solo la señal procesada pasa a la salida — no se mezcla señal seca. Los lados TX y RX mantienen valores de Mix completamente independientes.

## Consejos

- Comience con el valor predeterminado de 30 % y auméntelo gradualmente mientras escucha el efecto sobre la presencia o la inteligibilidad.
- El logotipo de PooDoo pulsa con el nivel RMS de la señal húmeda. Un pulso más rápido y pronunciado al subir Mix confirma que la etapa Doo está contribuyendo a la salida.
- Si aún no ha posicionado la banda Doo en la frecuencia correcta, ajuste Mix a 0 % temporalmente mientras regula Doo / Tune y, a continuación, vuelva a subir Mix. Consulte [Centrar Doo en la banda de presencia para su micrófono (TX) o para la inteligibilidad en RX](centre-doo-on-the-presence-band-for-your-mic-tx-or-for-rx-intelligibility.md).

## Relacionado

- [Añadir aire con Doo Harmonics](add-air-with-doo-harmonics.md)
- [Centrar Doo en la banda de presencia para su micrófono (TX) o para la inteligibilidad en RX](centre-doo-on-the-presence-band-for-your-mic-tx-or-for-rx-intelligibility.md)
- [Mezclar la mejora Poo con Mix](blend-the-poo-enhancement-with-mix.md)
- [Omitir PUDU desde cualquiera de las cadenas](bypass-pudu-from-either-chain.md)
- [Descripción general de Aetherial TX Poodoo / Aetherial RX Poodoo](overview.md)
