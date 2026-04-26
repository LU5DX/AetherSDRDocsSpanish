# Centrar Doo en la banda de presencia de su micrófono

El control **Doo / Tune** establece la frecuencia central del procesador de alta frecuencia del excitador PUDU. Posicionarlo en el pico de presencia natural de su micrófono permite que la etapa Doo añada armónicos y aire donde tienen mayor efecto sobre la inteligibilidad y el brillo percibido.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en la cadena PooDoo Audio. Si está oculta, habilítela mediante el widget CHAIN o haga doble clic en la etapa PUDU (Enh) para abrir el editor flotante.
- El subcontenedor PUDU debe ser visible dentro del contenedor principal PooDoo Audio (TXDSP).

## Pasos

1. Localice el grupo **Doo** en el applet PUDU. La etiqueta del corchete indica "Doo" y se encuentra sobre los tres controles más a la derecha.
2. Encuentre el primer control bajo el corchete Doo, etiquetado **Tune**.
3. Gire **Doo / Tune** hasta la frecuencia donde se encuentra el pico de presencia de su micrófono. El valor predeterminado es 5.0 kHz; el rango válido es de 1000 a 10000 Hz.
4. Hable al micrófono en su nivel operativo habitual y ajuste **Doo / Tune** mientras observa el logotipo animado de PooDoo — su brillo sigue la señal procesada. Escuche el punto donde la claridad y la presencia aumentan sin aspereza.
5. La configuración se guarda automáticamente al soltar el control.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Doo / Tune** | 5.0 kHz | 1000 a 10000 Hz | `ClientPuduTxDooTuneHz` | Establece la frecuencia central de la banda de excitación de alta frecuencia. Usa mapeo logarítmico. Se muestra como "X.X kHz" a partir de 1 kHz. |
| **Doo / Air** | 6.0 dB | 0.0 a 24.0 dB | `ClientPuduTxDooHarmonicsDb` | Controla la cantidad de armónicos añadidos en la frecuencia sintonizada. |
| **Doo / Mix** | 30 % | 0.0 a 1.0 | `ClientPuduTxDooMix` | Mezcla la banda alta excitada con la señal seca. Se muestra como porcentaje. |

## Consejos

- El control **Doo / Tune** usa una escala logarítmica, por lo que los movimientos pequeños cerca del extremo inferior del rango (1 kHz) producen cambios de frecuencia mayores que el mismo movimiento cerca de 10 kHz. Dé pasos más pequeños al trabajar por debajo de 2 kHz.
- Ajuste **Doo / Tune** antes de aumentar **Doo / Air**. Establecer primero la frecuencia central le permite escuchar el carácter de la banda antes de añadir armónicos.
- Si está usando el modo Even, la etapa Doo interactúa con la saturación de baja frecuencia Big Bottom del grupo Poo. Ajuste Doo / Tune lo suficientemente alto (generalmente 3 kHz o más para voz) para evitar que las dos bandas se superpongan.

## Solución de problemas

- **Doo / Tune no tiene efecto audible** — Verifique que **Doo / Mix** esté por encima de 0 % y que **Doo / Air** esté por encima de 0.0 dB. Si cualquiera de los dos está en el mínimo, el procesador Doo no produce salida independientemente del ajuste de Tune.
- **El applet PUDU no es visible** — El subcontenedor está oculto hasta que la etapa PUDU esté habilitada. Habilítela desde el widget CHAIN o haciendo doble clic en la etapa PUDU (Enh).

## Relacionado

- [Descripción general del excitador PUDU](overview.md)
- [Añadir aire con los armónicos Doo](add-air-with-doo-harmonics.md)
- [Mezclar la excitación Doo con Mix](blend-the-doo-excitement-with-mix.md)
- [Elegir el carácter Aphex (Even) o Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- [Sintonizar Poo al fundamental de su voz](tune-poo-to-the-fundamental-of-your-voice.md)
