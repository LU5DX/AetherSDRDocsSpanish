# Combinar la mejora Poo con Mix

El mando "Poo / Mix" controla qué tanto de la señal de baja frecuencia procesada se mezcla de vuelta con el audio original (seco). Úselo para ajustar la cantidad de mejora Poo sin saturar la señal original.

## Antes de comenzar

- PUDU debe estar habilitado en el lado que desea ajustar. Si el grupo Poo no es visible, es posible que la etapa PUDU esté puenteada — consulte [Puentear PUDU desde cualquiera de las cadenas](bypass-pudu-from-either-chain.md).
- Abra el applet correspondiente: "Aetherial TX Poodoo™" para transmisión, o "Aetherial RX Poodoo™" para recepción. Haga doble clic en la etapa PUDU en el widget CHAIN del lado correspondiente para abrir el editor sin marco si el applet no está visible.

## Pasos

1. Localice el corchete del grupo **Poo** en el applet. Contiene tres mandos: **Drive**, **Tune** y **Mix**.
2. Gire el mando **Mix** bajo el corchete **Poo** hasta el nivel de mezcla deseado.
   - Girar hacia 0 % deja pasar la señal seca sin ninguna mejora de baja frecuencia.
   - Girar hacia 100 % incorpora por completo la señal procesada.
3. El valor se guarda automáticamente. No se requiere confirmación adicional.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Configuración persistida |
|---|---|---|---|
| **Poo / Mix** (TX) | 30 % | 0 % a 100 % (almacenado como 0.0 a 1.0) | `ClientPuduTxPooMix` |
| **Poo / Mix** (RX) | 30 % | 0 % a 100 % (almacenado como 0.0 a 1.0) | `ClientPuduRxPooMix` |

El mando muestra el valor como un porcentaje en número entero (por ejemplo, "30 %"). Internamente, el valor se almacena como una fracción lineal entre 0.0 y 1.0.

## Consejos

- Los lados TX y RX tienen valores de Mix completamente independientes. Ajustar uno no afecta al otro.
- Observe el logotipo de PooDoo: su brillo pulsa con el RMS de la señal húmeda (procesada). Un aumento notable en la intensidad del pulso al subir Mix confirma que el procesamiento de baja frecuencia es audible en la mezcla.
- Comience en el valor predeterminado de 30 % y auméntelo gradualmente. Valores altos de Mix pueden engrosar los bajos hasta el punto de enturbiarse, especialmente si **Poo / Drive** también es alto.

## Relacionados

- [Ajustar Poo Drive para el grosor de bajas frecuencias](dial-poo-drive-for-lf-thickness.md)
- [Sintonizar Poo al fundamental de su voz (TX) o para realzar los bajos del programa en RX](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md)
- [Combinar la emoción Doo con Mix](blend-the-doo-excitement-with-mix.md)
- [Descripción general de Aetherial TX Poodoo / Aetherial RX Poodoo](overview.md)
