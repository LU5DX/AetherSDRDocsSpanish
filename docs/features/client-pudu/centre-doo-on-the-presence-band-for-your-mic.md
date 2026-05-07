# Centrar el Doo en la banda de presencia de su micrófono

La perilla **Doo / Tune** establece la frecuencia central del procesador de altas frecuencias del excitador PUDU. Colocarla en el pico de presencia natural de su micrófono permite que la etapa Doo agregue armónicos y aire donde tienen el mayor efecto en la inteligibilidad y el brillo percibido.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en la cadena de audio PooDoo. Si está oculta, actívela a través del widget CHAIN o haga doble clic en la etapa PUDU (Enh) para abrir el editor flotante.
- El subcontenedor PUDU debe estar visible dentro del contenedor principal PooDoo Audio (TXDSP).

## Pasos

1. Localice el grupo **Doo** en el applet de PUDU. La etiqueta del soporte dice "Doo" y se encuentra sobre las tres perillas más a la derecha.
2. Encuentre la primera perilla debajo del soporte Doo, etiquetada como **Tune**.
3. Gire **Doo / Tune** a la frecuencia donde se encuentra el pico de presencia de su micrófono. El valor predeterminado es 5.0 kHz; el rango válido es de 1000 a 10000 Hz.
4. Hable al micrófono a su nivel de operación normal y ajuste **Doo / Tune** mientras observa el logotipo animado de PooDoo; su brillo sigue la señal procesada. Escuche el punto donde la claridad y la presencia aumentan sin aspereza.
5. La configuración se guarda automáticamente cuando suelta la perilla.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Doo / Tune** | 5.0 kHz | 1000 a 10000 Hz | `ClientPuduTxDooTuneHz` | Establece la frecuencia central de la banda de excitación de altas frecuencias. Utiliza mapeo logarítmico. Se muestra como "X.X kHz" en o por encima de 1 kHz. |
| **Doo / Air** | 6.0 dB | 0.0 a 24.0 dB | `ClientPuduTxDooHarmonicsDb` | Controla la cantidad de armónicos añadidos en la frecuencia sintonizada. |
| **Doo / Mix** | 30 % | 0.0 a 1.0 | `ClientPuduTxDooMix` | Mezcla la banda alta excitada de vuelta con la señal seca. Se muestra como un porcentaje. |

## Consejos

- La perilla **Doo / Tune** utiliza una escala logarítmica, por lo que los movimientos pequeños cerca del extremo inferior del rango (1 kHz) producen cambios de frecuencia mayores que el mismo movimiento cerca de 10 kHz. Realice pasos más pequeños cuando trabaje por debajo de 2 kHz.
- Ajuste **Doo / Tune** antes de aumentar **Doo / Air**. Configurar primero la frecuencia central le permite escuchar el carácter de la banda antes de añadir armónicos.
- Si está usando el modo Even, la etapa Doo interactúa con la saturación LF de Big Bottom del grupo Poo. Ajuste Doo / Tune lo suficientemente alto (típicamente 3 kHz o más para voz) para mantener las dos bandas sin superponerse.

## Solución de problemas

- **Doo / Tune no tiene efecto audible** — Verifique que **Doo / Mix** esté por encima del 0 % y que **Doo / Air** esté por encima de 0.0 dB. Con cualquiera de ellos al mínimo, el procesador Doo no produce salida independientemente de la configuración de Tune.
- **El applet PUDU no es visible** — El subcontenedor está oculto hasta que se habilita la etapa PUDU. Actívelo desde el widget CHAIN o haciendo doble clic en la etapa PUDU (Enh).

## Relacionado

- [Resumen del excitador PUDU](overview.md)
- [Añada aire con Doo Harmonics](add-air-with-doo-harmonics.md)
- [Mezcle la excitación Doo con Mix](blend-the-doo-excitement-with-mix.md)
- [Seleccione el carácter Aphex (Even) vs Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- [Ajuste Poo a la fundamental de su voz](tune-poo-to-the-fundamental-of-your-voice.md)
