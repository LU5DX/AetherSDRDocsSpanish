# Agregar aire con Doo Harmonics

Use el control **Doo / Air** para ajustar cuánta excitación armónica agrega el procesador Doo en la banda de alta frecuencia. Al aumentarlo, se añade presencia y "aire" al audio transmitido.

## Antes de comenzar

- La etapa PUDU debe estar habilitada y visible. Permanece oculta hasta que se habilite mediante el widget CHAIN o el editor flotante. Consulte [Omitir PUDU desde la cadena](bypass-pudu-from-the-chain.md).
- AetherSDR debe estar conectado a su radio FLEX-8600 con el enrutamiento de audio activo.

## Pasos

1. Abra el applet PUDU Exciter. Aparece como el subcontenedor **PUDU** dentro del contenedor principal PooDoo Audio (TXDSP).
2. Localice el grupo **Doo** — el conjunto de tres controles en el lado derecho, marcado con la etiqueta de corchete "Doo".
3. Gire el control **Air** (el control central del grupo Doo) en sentido horario para aumentar la cantidad de armónicos añadidos en la banda de frecuencia Doo, o en sentido antihorario para reducirla.
4. Observe el logotipo de PooDoo — su brillo pulsa con el RMS de la señal procesada, lo que ofrece una indicación aproximada de cuánta señal wet se está produciendo.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Air | 6.0 dB | 0.0 a 24.0 dB | `ClientPuduTxDooHarmonicsDb` | Establece la cantidad de contenido armónico añadido en la banda de alta frecuencia Doo. Mapeo lineal. |
| Doo / Tune | 5000 Hz | 1000 a 10000 Hz | `ClientPuduTxDooTuneHz` | Centra la banda de frecuencia donde se aplica Air. Mapeo logarítmico. |
| Doo / Mix | 30 % | 0 a 100 % | `ClientPuduTxDooMix` | Mezcla la banda alta excitada con la señal dry. |

## Consejos

- El control **Air** y el control **Doo / Tune** funcionan en conjunto. Ajuste **Doo / Tune** a la frecuencia de presencia o aire de su micrófono antes de aumentar **Air**, de modo que los armónicos se añadan donde su micrófono ya tiene salida.
- Use **Doo / Mix** para contener el efecto general sin necesidad de reducir **Air**. Esto preserva el carácter armónico mientras controla el balance wet/dry.
- En el modo **Even**, la generación de armónicos sigue el modelado asimétrico de la línea Aphex — los armónicos añadidos son más cálidos. En el modo **Odd**, el modelado simétrico tanh de la línea Behringer produce armónicos más brillantes. El control **Air** se comporta igual en ambos modos, pero el carácter de lo que añade es diferente.

## Relacionados

- [Centrar Doo en la banda de presencia de su micrófono](centre-doo-on-the-presence-band-for-your-mic.md)
- [Mezclar la excitación Doo con Mix](blend-the-doo-excitement-with-mix.md)
- [Elegir el carácter Aphex (Even) vs Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- [Descripción general de PUDU Exciter](overview.md)
