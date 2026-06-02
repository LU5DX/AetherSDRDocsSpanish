# Mezcla del refuerzo de graves con el control Mix

El control "Body / Mix" determina cuánto de la señal procesada de baja frecuencia se mezcla con el audio seco. Úselo para ajustar la cantidad de refuerzo de graves sin saturar la señal original.

## Antes de comenzar

- PUDU debe estar habilitado en el lado que desea ajustar. Si el grupo Body no está visible, es posible que la etapa PUDU esté en bypass; consulte [Bypass PUDU desde cualquier cadena](bypass-pudu-from-either-chain.md).
- Abra el applet correspondiente: "Aetherial TX Voice Processor" para transmisión, o "Aetherial RX Poodoo™" para recepción. Haga doble clic en la etapa PUDU en el widget CHAIN del lado correspondiente para abrir el editor sin bordes si el applet aún no está visible.
- Cuando la etapa PUDU está en bypass, todo el mosaico del applet se atenúa aproximadamente al 55 % de opacidad. La opacidad total se restaura en cuanto la etapa se vuelve a habilitar.

## Pasos

1. Localice el corchete del grupo **Body** en el applet. Contiene tres perillas: **Drive**, **Tune** y **Mix**.
2. Gire la perilla **Mix** debajo del corchete **Body** al nivel de mezcla deseado.
   - Girando hacia 0 % pasa la señal seca sin refuerzo de baja frecuencia.
   - Girando hacia 100 % mezcla la señal procesada completa.
3. El valor se guarda automáticamente. No se necesita confirmación adicional.

## Edición de valor en línea

v26.5.2.1 añade entrada directa por teclado para los valores de las perillas.

1. Haga clic en el texto del valor debajo de una perilla para activar el editor en línea. El área de texto adquiere un borde cian delgado para indicar el modo de edición.
2. Escriba un nuevo valor. El editor acepta:
   - Números simples (p. ej., `30`, `8500`)
   - Valores decimales (p. ej., `15.5`)
   - Formato con separador decimal regional (p. ej., `12,5` en regiones que usan coma)
   - Números con texto de unidad al final (p. ej., `30 %`, `5.0 kHz`, `100 Hz`)
3. Presione **Enter** o haga clic fuera del editor para confirmar el valor. La perilla se actualiza al nuevo ajuste, limitado a su rango válido.
4. Presione **Escape** para cancelar la edición sin cambiar el valor.
5. Mientras el editor está activo, la rueda del ratón ajusta la perilla como de costumbre: los eventos de la rueda se reenvían a la perilla.

El editor en línea usa el mismo formato que la visualización normal de la perilla (por ejemplo, los valores porcentuales aparecen como `30 %`, los valores de frecuencia como `100 Hz` o `5.0 kHz`).

## Función de cada control

| Control            | Valor predeterminado                                                                         | Rango válido                               |
|--------------------|----------------------------------------------------------------------------------------------|--------------------------------------------|
| **Even**           | No seleccionado por defecto                                                                  | N/A (botón de opción exclusivo con Odd)    |
| **Odd**            | No seleccionado por defecto                                                                  | N/A (botón de opción exclusivo con Even)   |
| **Poo / Drive** (TX) | 6.0 dB                                                                                     | 0.0 a 24.0 dB                             |
| **Poo / Tune** (TX)  | 100 Hz                                                                                      | 50 a 160 Hz                               |
| **Poo / Mix** (TX)   | 30 %                                                                                        | 0 % a 100 % (almacenado como 0.0 a 1.0)   |
| **Poo / Drive** (RX) | 6.0 dB                                                                                     | 0.0 a 24.0 dB                             |
| **Poo / Tune** (RX)  | 100 Hz                                                                                      | 50 a 160 Hz                               |
| **Poo / Mix** (RX)   | 30 %                                                                                        | 0 % a 100 % (almacenado como 0.0 a 1.0)   |
| Logotipo AetherVoice   | Logotipo animado que pulsa con el RMS de la señal procesada. Muestra la marca 'AetherVoice™'. | Widget PooDooLogo — 40 px de altura mínima. |

La pantalla de la perilla muestra el valor como un porcentaje de número entero (por ejemplo, "30 %"). Internamente el valor se almacena como una fracción lineal entre 0.0 y 1.0.

## Consejos

- Los lados TX y RX tienen valores Mix completamente independientes. Ajustar uno no afecta al otro.
- Observe el logotipo PooDoo: su brillo pulsa con el RMS de la señal procesada. Un aumento notable en la intensidad del pulso al subir Mix confirma que el procesamiento de baja frecuencia es audible en la mezcla.
- Comience con el valor predeterminado del 30 % y aumente gradualmente. Valores Mix altos pueden espesar las frecuencias graves hasta el punto de sonar embarrados, especialmente si **Poo / Drive** también está alto.
- Use la función de edición en línea para escribir valores exactos en lugar de ajustar con la rueda del ratón; por ejemplo, escriba `45` para establecer exactamente 45 % de Mix.
- Los botones de opción **Even** y **Odd** seleccionan el modo de procesamiento. El modo Even usa conformación asimétrica estilo Aphex con saturación LF Big Bottom. El modo Odd usa conformación simétrica tanh estilo Behringer con un compresor de graves feed-forward.

## Relacionados

- [Ajuste Poo / Drive para espesor LF](dial-poo-drive-for-lf-thickness.md)
- [Ajuste Poo a la frecuencia fundamental de su voz (TX) o para resaltar los graves del programa en RX](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md)
- Mezcle la excitación Clarity con Mix
- [Descripción general de Aetherial TX Voice Processor / Aetherial RX Poodoo](overview.md)
