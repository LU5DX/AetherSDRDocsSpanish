# Mezcla del refuerzo de frecuencias graves con Mix

El mando "Body / Mix" controla cuánto de la señal procesada de baja frecuencia se mezcla con el audio seco. Úselo para ajustar la cantidad de refuerzo de graves sin saturar la señal original.

## Antes de comenzar

- PUDU debe estar habilitado en el lado que desea ajustar. Si el grupo Body no está visible, la etapa PUDU puede estar desactivada (bypassed); consulte [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md).
- Abra el applet correspondiente: "Aetherial TX Voice Processor" para transmisión, o "Aetherial RX Poodoo™" para recepción. Haga doble clic en la etapa PUDU en el widget CHAIN del lado correspondiente para abrir el editor sin marco si el applet no está visible.
- Cuando la etapa PUDU está desactivada, todo el mosaico del applet se atenúa aproximadamente al 55 % de opacidad. La opacidad total se restablece en cuanto la etapa se vuelve a activar.

## Pasos

1. Localice el grupo **Body** en el applet. Contiene tres mandos: **Drive**, **Tune** y **Mix**.
2. Gire el mando **Mix** dentro del grupo **Body** hasta el nivel de mezcla deseado.
   - Girando hacia 0 % pasa la señal seca sin refuerzo de baja frecuencia.
   - Girando hacia 100 % mezcla la señal procesada completa.
3. El valor se guarda automáticamente. No se necesita confirmación adicional.

## Edición inline de valores

v26.5.2.1 añade entrada directa por teclado para los valores de los mandos.

1. Haga clic en el texto del valor debajo de un mando para activar el editor inline. El área de texto obtiene un borde fino color cian para indicar el modo de edición.
2. Escriba un nuevo valor. El editor acepta:
   - Números simples (ej., `30`, `8500`)
   - Valores decimales (ej., `15.5`)
   - Formato con separador local (ej., `12,5` en regiones que usan coma decimal)
   - Números con texto de unidad al final (ej., `30 %`, `5.0 kHz`, `100 Hz`)
3. Presione **Enter** o haga clic fuera del editor para confirmar el valor. El mando se actualiza al nuevo ajuste, limitado a su rango válido.
4. Presione **Escape** para cancelar la edición sin cambiar el valor.
5. Mientras el editor está activo, la rueda del ratón ajusta el mando como de costumbre; los eventos de la rueda se redirigen al mando.

El editor inline usa el mismo formato que la visualización normal del mando (por ejemplo, los valores porcentuales aparecen como `30 %`, los valores de frecuencia como `100 Hz` o `5.0 kHz`).

## Qué hace cada control

| Control              | Valor predeterminado                                                                                 | Rango válido                              |
|----------------------|------------------------------------------------------------------------------------------------------|-------------------------------------------|
| **Poo / Drive** (TX) | 6.0 dB                                                                                               | 0.0 a 24.0 dB                             |
| **Poo / Tune** (TX)  | 100 Hz                                                                                               | 50 a 160 Hz                               |
| **Poo / Mix** (TX)   | 30 %                                                                                                 | 0 % a 100 % (almacenado como 0.0 a 1.0)   |
| **Poo / Drive** (RX) | 6.0 dB                                                                                               | 0.0 a 24.0 dB                             |
| **Poo / Tune** (RX)  | 100 Hz                                                                                               | 50 a 160 Hz                               |
| **Poo / Mix** (RX)   | 30 %                                                                                                 | 0 % a 100 % (almacenado como 0.0 a 1.0)   |
| Logotipo AetherVoice | Logotipo animado que pulsa con el RMS de la señal procesada. Muestra la marca 'AetherVoice™'. | Widget PooDooLogo: altura mínima de 40 px. |

La visualización del mando muestra el valor como un porcentaje entero (por ejemplo, "30 %"). Internamente el valor se almacena como una fracción lineal entre 0.0 y 1.0.

## Consejos

- Los lados TX y RX tienen valores Mix completamente independientes. Ajustar uno no afecta al otro.
- Observe el logotipo PooDoo: su brillo pulsa con el RMS de la señal procesada (wet). Un aumento notable en la intensidad del pulso al subir Mix confirma que el procesamiento de baja frecuencia es audible en la mezcla.
- Empiece en el valor predeterminado de 30 % y aumente gradualmente. Valores Mix altos pueden espesar las frecuencias graves hasta el punto de sonar embarrados, especialmente si **Poo / Drive** también es alto.
- Use la función de edición inline para escribir valores exactos en lugar de ajustar con la rueda del ratón; por ejemplo, escriba `45` para establecer exactamente 45 % de Mix.

## Relacionados

- [Dial Poo / Drive for LF thickness](dial-poo-drive-for-lf-thickness.md)
- [Tune Poo to the fundamental of your voice (TX) or to bring out RX program lows](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md)
- [Blend the Clarity excitement with Mix](blend-the-clarity-excitement-with-mix.md)
- [Aetherial TX Voice Processor / Aetherial RX Poodoo overview](overview.md)
