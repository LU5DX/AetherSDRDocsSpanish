# Combine la emoción de Doo con Mix

Use el control Doo / Mix para definir cuánta excitación de alta frecuencia de Doo se mezcla con la señal seca. Un valor de Mix demasiado alto puede introducir aspereza; si es demasiado bajo, el procesamiento Doo tendrá poco efecto audible.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en el widget CHAIN para el lado correspondiente (TX o RX). Consulte [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md).
- Abra el editor de Poodoo haciendo doble clic en la etapa PUDU en el widget CHAIN. El editor se titula "Aetherial Poodoo™ — TX" o "Aetherial Poodoo™ — RX", según el lado en el que esté trabajando.
- Cuando la etapa PUDU está desviada, todo el tile del applet se atenúa aproximadamente al 55 % de opacidad. Esto es solo un indicador visual: la configuración de los controles se conserva. Vuelva a habilitar la etapa para restaurar la opacidad total y el procesamiento activo.

## Pasos

1. Localice el grupo **Clarity** — los tres controles en el lado derecho de la fila de controles, bajo la etiqueta del grupo "Clarity".
2. Identifique el tercer control del grupo Clarity, etiquetado como **Mix**.
3. Gire el control **Mix** para mezclar la señal excitada de alta frecuencia con la señal seca. El valor se muestra como un porcentaje directamente en el control.
4. Para escribir un valor preciso en lugar de girar el control, haga clic en el texto del valor del control. Aparece un pequeño editor de texto en lugar de la visualización del valor. Escriba el número deseado y presione **Enter** o haga clic en otro lugar para confirmar el valor. El control se ajusta automáticamente y se limita al rango válido. Presione **Escape** durante la edición para cancelar y revertir al valor anterior.

   *Nota: El editor en línea acepta formatos de número según la configuración regional (por ejemplo, "12,5" en locales con coma decimal) y elimina automáticamente los caracteres no numéricos si el análisis falla.*

5. Suelte el control o confirme el valor escrito. La configuración se guarda automáticamente.

## Función de cada control

| Control          | Valor predeterminado                                                                         | Rango válido                              |
|------------------|----------------------------------------------------------------------------------------------|-------------------------------------------|
| Doo / Mix (TX)   | 30 %                                                                                         | 0 % a 100 %                               |
| Doo / Mix (RX)   | 30 %                                                                                         | 0 % a 100 %                               |
| Logo AetherVoice | Logotipo animado con marca registrada que pulsa con el RMS de la señal procesada. Muestra la marca 'AetherVoice™'. | Widget PooDooLogo — altura mínima de 40 px. |

El control tiene una asignación lineal. Al 0 %, el procesador Doo se elimina por completo de la mezcla y no tiene efecto sobre la señal. Al 100 %, solo pasa la señal procesada — no se mezcla señal seca. Los lados TX y RX mantienen valores de Mix completamente independientes.

## Consejos

- Comience con el valor predeterminado del 30 % y aumente gradualmente mientras escucha el efecto en la presencia o la inteligibilidad.
- El logotipo de PooDoo pulsa con el RMS de la señal procesada. Un pulso más rápido y fuerte a medida que aumenta Mix confirma que la etapa Doo está contribuyendo a la salida.
- Si aún no ha posicionado la banda Doo en la frecuencia correcta, ajuste Mix temporalmente al 0 % mientras ajusta Doo / Tune, luego vuelva a subir Mix. Consulte [Centre Doo on the presence band for your mic (TX) or for RX intelligibility](centre-doo-on-the-presence-band-for-your-mic-tx-or-for-rx-intelligibility.md).
- Para ingresar un porcentaje específico con precisión, haga clic en la visualización del valor del control para abrir el editor en línea, escriba el número (por ejemplo, "42" para 42 %) y presione Enter. El control se ajusta a ese valor.

## Relacionados

- [Add air with Doo Harmonics](add-air-with-doo-harmonics.md)
- [Centre Doo on the presence band for your mic (TX) or for RX intelligibility](centre-doo-on-the-presence-band-for-your-mic-tx-or-for-rx-intelligibility.md)
- [Blend the Poo enhancement with Mix](blend-the-poo-enhancement-with-mix.md)
- [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md)
- [Aetherial TX Voice Processor / Aetherial RX Poodoo overview](overview.md)
