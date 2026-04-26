# Combinar el realce Poo con Mix

El control "Poo / Mix" determina qué proporción de la señal de baja frecuencia procesada se mezcla de vuelta con el audio seco. Úselo para ajustar la cantidad de realce Poo sin saturar la señal original.

## Antes de comenzar

- PUDU debe estar habilitado en el lado que desea ajustar. Si el grupo Poo no es visible, la etapa PUDU puede estar en bypass — consulte [Omitir PUDU desde cualquiera de las cadenas](bypass-pudu-from-either-chain.md).
- Abra el applet correspondiente: "Aetherial TX Poodoo™" para transmisión, o "Aetherial RX Poodoo™" para recepción. Haga doble clic en la etapa PUDU del widget CHAIN en el lado correspondiente para abrir el editor sin marco si el applet no está visible aún.

## Pasos

1. Localice el corchete del grupo **Poo** en el applet. Contiene tres controles: **Drive**, **Tune** y **Mix**.
2. Gire el control **Mix** bajo el corchete **Poo** hasta el nivel de mezcla deseado.
   - Girar hacia 0 % deja pasar la señal seca sin ningún realce de baja frecuencia.
   - Girar hacia 100 % incorpora la señal procesada completa a la mezcla.
3. El valor se guarda automáticamente. No se requiere ninguna confirmación adicional.

## Qué hace cada control

| Control | Valor por defecto | Rango válido | Ajuste persistente |
|---|---|---|---|
| **Poo / Mix** (TX) | 30 % | 0 % a 100 % (almacenado como 0.0 a 1.0) | `ClientPuduTxPooMix` |
| **Poo / Mix** (RX) | 30 % | 0 % a 100 % (almacenado como 0.0 a 1.0) | `ClientPuduRxPooMix` |

El control muestra el valor como un porcentaje en número entero (por ejemplo, "30 %"). Internamente, el valor se almacena como una fracción lineal entre 0.0 y 1.0.

## Consejos

- Los lados TX y RX tienen valores de Mix completamente independientes. Ajustar uno no afecta al otro.
- Observe el logotipo de PooDoo: su brillo pulsa con el RMS de la señal húmeda (procesada). Un aumento notorio en la intensidad del pulso al elevar Mix confirma que el procesamiento de baja frecuencia es audible en la mezcla.
- Comience con el valor por defecto de 30 % y auméntelo de forma gradual. Valores altos de Mix pueden engrosar las frecuencias bajas hasta el punto de enturbiarse el sonido, especialmente si **Poo / Drive** también es alto.

## Relacionados

- [Ajustar Poo Drive para el grosor de baja frecuencia](dial-poo-drive-for-lf-thickness.md)
- [Sintonizar Poo al fundamental de su voz (TX) o para realzar los graves del programa en RX](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md)
- [Combinar el realce Doo con Mix](blend-the-doo-excitement-with-mix.md)
- [Descripción general de Aetherial TX Poodoo / Aetherial RX Poodoo](overview.md)
