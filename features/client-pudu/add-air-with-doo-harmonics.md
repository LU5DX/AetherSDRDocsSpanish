# Agregar aire con Doo Harmonics

El control **Doo / Air** determina cuánto contenido armónico de alta frecuencia agrega el excitador PUDU en la banda Doo. Al aumentarlo, se añade presencia y "aire" al audio transmitido sin modificar el nivel de señal subyacente.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en la cadena PooDoo Audio. Consulte [Omitir PUDU de la cadena](bypass-pudu-from-the-chain.md) si el subcontenedor PUDU no es visible.
- Abra el applet PUDU: localice el subcontenedor **PUDU** dentro del contenedor padre PooDoo Audio (TXDSP) en el panel de applets, o haga doble clic en la etapa PUDU (Enh) en el widget CHAIN para abrir el editor flotante.

## Pasos

1. En el grupo **Doo**, localice el control **Air** (el knob central bajo el corchete Doo).
2. Gire **Air** en sentido horario para aumentar la cantidad de excitación armónica añadida en la banda alta. El valor se muestra en dB debajo del knob.
3. Observe el logotipo de PooDoo — su brillo pulsa con el nivel de señal procesada, proporcionando retroalimentación visual mientras realiza los ajustes.
4. Si los armónicos añadidos resultan demasiado prominentes en la mezcla final, reduzca **Doo / Mix** para mezclar la señal excitada de vuelta hacia la señal seca. Consulte [Mezclar la excitación Doo con Mix](blend-the-doo-excitement-with-mix.md).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| **Air** | 6.0 dB | 0.0 a 24.0 dB | `ClientPuduTxDooHarmonicsDb` |
| **Doo / Tune** | 5000 Hz (5.0 kHz) | 1000 a 10000 Hz | `ClientPuduTxDooTuneHz` |
| **Doo / Mix** | 30 % | 0 a 100 % | `ClientPuduTxDooMix` |

**Air** — Establece el nivel de armónicos generados en la banda alta, en dB. Los valores más altos añaden más presencia y aire. Los valores más bajos reducen el efecto hasta el nivel de bypass.

**Doo / Tune** — Establece la frecuencia central de la banda de excitación de alta frecuencia. El knob utiliza una escala logarítmica; los valores en 1 kHz o superiores se muestran en kHz (p. ej., "5.0 kHz"). Ajuste esta frecuencia a la región de presencia de su micrófono antes de aumentar Air. Consulte [Centrar Doo en la banda de presencia de su micrófono](centre-doo-on-the-presence-band-for-your-mic.md).

**Doo / Mix** — Mezcla la banda alta procesada con la señal seca. Al 0 % la sección Doo queda efectivamente silenciada, independientemente del ajuste de Air. Al 100 % se utiliza la señal procesada completa.

## Consejos

- Ajuste **Doo / Tune** primero para que la excitación esté centrada en la banda de frecuencia correcta antes de aumentar **Air**. Un valor alto de **Air** en la frecuencia incorrecta puede añadir aspereza en lugar de claridad.
- El modo Even (linaje Aphex) y el modo Odd (linaje Behringer) cambian el carácter armónico de lo que genera Air. Even produce armónicos más cálidos; Odd produce un resultado más brillante y agresivo. Consulte [Elegir el carácter Aphex (Even) vs Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md).
- Use **Doo / Mix** para mantener el efecto Air sutil — pequeñas cantidades de excitación armónica suelen ser más efectivas en el aire que las cantidades grandes.

## Solución de problemas

- **El knob Air no produce ningún efecto audible** — Verifique que la etapa PUDU esté habilitada en el widget CHAIN y que `ClientPuduTxEnabled` esté activo. Confirme también que **Doo / Mix** esté por encima de 0 %; un Mix de 0 % silencia toda la sección Doo independientemente del ajuste de Air.
- **Los armónicos añadidos suenan ásperos** — La frecuencia central de Doo / Tune puede ser demasiado alta, o Air está configurado muy por encima del rango útil para su micrófono. Reduzca **Air**, luego reajuste **Doo / Tune** a una frecuencia más baja antes de volver a aumentar **Air**.

## Relacionados

- [Centrar Doo en la banda de presencia de su micrófono](centre-doo-on-the-presence-band-for-your-mic.md)
- [Mezclar la excitación Doo con Mix](blend-the-doo-excitement-with-mix.md)
- [Elegir el carácter Aphex (Even) vs Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- [Descripción general del excitador PUDU](overview.md)
