# Mezcla del realce de Cuerpo con la combinación

El mando "Body / Mix" controla cuánta de la señal de baja frecuencia procesada se mezcla de vuelta con el audio seco. Úselo para ajustar la cantidad de realce de Cuerpo sin saturar la señal original.

## Antes de comenzar

- PUDU debe estar habilitado en el lado que desea ajustar. Si el grupo Body no está visible, la etapa PUDU puede estar omitida; consulte [Omitir PUDU desde cualquier cadena](bypass-pudu-from-either-chain.md).
- Abra el applet correspondiente: "Aetherial TX Voice Processor" para transmisión, o "Aetherial RX Poodoo™" para recepción. Haga doble clic en la etapa PUDU en el widget CHAIN del lado correspondiente para abrir el editor sin bordes si el applet aún no está visible.
- Cuando la etapa PUDU está omitida, todo el mosaico del applet se atenúa hasta aproximadamente un 55 % de opacidad. La opacidad total se restablece tan pronto como se vuelve a habilitar la etapa.

## Pasos

1. Localice el corchete del grupo **Poo** en el applet. Contiene tres mandos: **Drive**, **Tune** y **Mix**.
2. Gire el mando **Mix** debajo del corchete **Poo** al nivel de combinación deseado.
   - Girar hacia 0 % pasa la señal seca sin realce de baja frecuencia.
   - Girar hacia 100 % mezcla la señal procesada completa.
3. El valor se guarda automáticamente. No se necesita confirmación adicional.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistente |
|---|---|---|---|
| **Poo / Mix** (TX) | 30 % | 0 % a 100 % (almacenado como 0.0 a 1.0) | `ClientPuduTxPooMix` |
| **Poo / Mix** (RX) | 30 % | 0 % a 100 % (almacenado como 0.0 a 1.0) | `ClientPuduRxPooMix` |

La pantalla del mando muestra el valor como un porcentaje de número entero (por ejemplo, "30 %"). Internamente, el valor se almacena como una fracción lineal entre 0.0 y 1.0.

## Consejos

- Los lados TX y RX tienen valores de Mix completamente independientes. Ajustar uno no afecta al otro.
- Observe el logotipo de PooDoo: su brillo pulsa con la RMS de la señal húmeda (procesada). Un aumento notable en la intensidad del pulso a medida que sube Mix confirma que el procesamiento de baja frecuencia es audible en la combinación.
- Comience con el valor predeterminado del 30 % y aumente gradualmente. Los valores altos de Mix pueden espesar las frecuencias graves hasta el punto de volverlas embarradas, especialmente si **Poo / Drive** también está alto.

## Relacionados

- [Ajuste Poo / Drive para el grosor de LF](dial-poo-drive-for-lf-thickness.md)
- [Sintonice Poo con la fundamental de su voz (TX) o para resaltar los graves del programa RX](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md)
- [Mezcle la emoción de Doo con Mix](blend-the-doo-excitement-with-mix.md)
- [Descripción general de Aetherial TX Voice Processor / Aetherial RX Poodoo](overview.md)
