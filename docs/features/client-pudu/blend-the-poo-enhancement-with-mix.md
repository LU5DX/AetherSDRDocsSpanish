# Mezcla de la mejora de cuerpo con Mix

El control "Body / Mix" determina cuánto de la señal procesada de baja frecuencia se mezcla con el audio seco. Úselo para ajustar la cantidad de mejora de cuerpo sin saturar la señal original.

## Antes de comenzar

- PUDU debe estar habilitado en el lado que desea ajustar. Si el grupo Body no es visible, la etapa PUDU puede estar desviada — consulte [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md).
- Abra el applet correspondiente: "Aetherial TX Voice Processor" para transmisión o "Aetherial RX Poodoo™" para recepción. Haga doble clic en la etapa PUDU en el widget CHAIN del lado correspondiente para abrir el editor sin marco si el applet aún no es visible.
- Cuando la etapa PUDU está desviada, todo el mosaico del applet se atenúa aproximadamente al 55 % de opacidad. La opacidad total se restablece al reactivar la etapa.

## Pasos

1. Localice el grupo **Body** en el applet. Contiene tres perillas: **Drive**, **Tune** y **Mix**.
2. Gire la perilla **Mix** dentro del grupo **Body** al nivel de mezcla deseado.
   - Girar hacia 0 % pasa la señal seca sin mejora de baja frecuencia.
   - Girar hacia 100 % mezcla la señal procesada completa.
3. El valor se guarda automáticamente. No se necesita confirmación adicional.

## Edición inline de valores

v26.5.2.1 agrega entrada directa por teclado para valores de perilla.

1. Haga clic en el texto del valor debajo de una perilla para activar el editor inline. El área de texto adquiere un borde cian fino para indicar el modo de edición.
2. Escriba un nuevo valor. El editor acepta:
   - Números simples (ej., `30`, `8500`)
   - Valores decimales (ej., `15.5`)
   - Formato sensible a la configuración regional (ej., `12,5` en regiones con coma decimal)
   - Números con texto de unidad al final (ej., `30 %`, `5.0 kHz`, `100 Hz`)
3. Presione **Enter** o haga clic fuera del editor para confirmar el valor. La perilla se actualiza al nuevo ajuste, limitado a su rango válido.
4. Presione **Escape** para cancelar la edición sin cambiar el valor.
5. Mientras el editor está activo, la rueda del ratón ajusta la perilla como de costumbre — los eventos de rueda se reenvían a la perilla.

El editor inline usa el mismo formato que la pantalla normal de la perilla (por ejemplo, los valores de porcentaje aparecen como `30 %`, los valores de frecuencia como `100 Hz` o `5.0 kHz`).

## Función de cada control

| Control            | Valor predeterminado                                                                         | Rango válido                               |
|--------------------|----------------------------------------------------------------------------------------------|--------------------------------------------|
| **Even**           | No seleccionado por defecto                                                                  | N/A (botón de opción exclusivo con Odd)    |
| **Odd**            | No seleccionado por defecto                                                                  | N/A (botón de opción exclusivo con Even)   |
| **Poo / Drive** (TX) | 6.0 dB                                                                                     | 0.0 a 24.0 dB                              |
| **Poo / Tune** (TX)  | 100 Hz                                                                                      | 50 a 160 Hz                                |
| **Poo / Mix** (TX)   | 30 %                                                                                        | 0 % a 100 % (almacenado como 0.0 a 1.0)    |
| **Poo / Drive** (RX) | 6.0 dB                                                                                     | 0.0 a 24.0 dB                              |
| **Poo / Tune** (RX)  | 100 Hz                                                                                      | 50 a 160 Hz                                |
| **Poo / Mix** (RX)   | 30 %                                                                                        | 0 % a 100 % (almacenado como 0.0 a 1.0)    |
| **Doo / Tune** (TX)  | 5000 Hz                                                                                     | 1000 a 10000 Hz                            |
| **Doo / Air** (TX)   | 6.0 dB                                                                                     | 0.0 a 24.0 dB                              |
| **Doo / Mix** (TX)   | 30 %                                                                                        | 0 % a 100 % (almacenado como 0.0 a 1.0)    |
| **Doo / Tune** (RX)  | 5000 Hz                                                                                     | 1000 a 10000 Hz                            |
| **Doo / Air** (RX)   | 6.0 dB                                                                                     | 0.0 a 24.0 dB                              |
| **Doo / Mix** (RX)   | 30 %                                                                                        | 0 % a 100 % (almacenado como 0.0 a 1.0)    |
| Logo AetherVoice   | Logotipo animado de marca que pulsa con el RMS de la señal procesada. Muestra la marca 'AetherVoice™'. | Widget PooDooLogo — altura mínima de 40 px. |

La pantalla de la perilla muestra el valor como un porcentaje de número entero (por ejemplo, "30 %"). Internamente, el valor se almacena como una fracción lineal entre 0.0 y 1.0.

## Consejos

- Los lados TX y RX tienen valores Mix completamente independientes. Ajustar uno no afecta al otro.
- Observe el logotipo de PooDoo: su brillo pulsa con el RMS de la señal procesada. Un aumento notable en la intensidad del pulso al aumentar Mix confirma que el procesamiento de baja frecuencia es audible en la mezcla.
- Comience con el valor predeterminado del 30 % y aumente gradualmente. Los valores altos de Mix pueden espesar los graves hasta el punto de opacidad, especialmente si **Poo / Drive** también es alto.
- Use la función de edición inline para escribir valores exactos en lugar de ajustar con la rueda del ratón — por ejemplo, escriba `45` para establecer exactamente 45 % de Mix.
- Los botones de opción **Even** y **Odd** seleccionan el modo de procesamiento. El modo Even usa modelado asimétrico estilo Aphex con saturación LF Big Bottom. El modo Odd usa modelado simétrico tanh estilo Behringer con un compresor de graves de alimentación directa.
- El grupo **Body** contiene los controles del procesador de baja frecuencia: **Drive**, **Tune** y **Mix**.
- El grupo **Clarity** contiene los controles del procesador de alta frecuencia: **Tune**, **Air** y **Mix**.

## Relacionados

- [Dial Poo / Drive for LF thickness](dial-poo-drive-for-lf-thickness.md)
- [Tune Poo to the fundamental of your voice (TX) or to bring out RX program lows](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md)
- Blend the Clarity excitement with Mix
- [Aetherial TX Voice Processor / Aetherial RX Poodoo overview](overview.md)
