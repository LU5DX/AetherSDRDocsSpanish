# Descripción general del excitador PUDU

El excitador PUDU es la pieza central de la cadena DSP de transmisión de PooDoo Audio. Añade cuerpo en bajas frecuencias ("Poo") y presencia o aire en altas frecuencias ("Doo") al audio transmitido, mediante dos procesadores paralelos independientes, cada uno con su propio carácter, sintonía y mezcla húmedo/seco.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en el widget CHAIN antes de que el applet sea visible. El subcontenedor permanece oculto hasta que la etapa esté activa.
- No se requiere conexión a ningún radio para ajustar la configuración de PUDU.

## Cómo funciona

PUDU procesa el audio de transmisión en dos bandas paralelas.

**Mode** selecciona el carácter general de ambos procesadores. Haga clic en **Even** para obtener el modelado asimétrico de linaje Aphex — predominantemente armónicos pares, más cálido, con saturación de bajas frecuencias tipo Big Bottom. Haga clic en **Odd** para obtener el modelado simétrico tanh de linaje Behringer — armónicos impares puros, más brillante, con un compresor de graves de alimentación hacia adelante. Los dos botones son mutuamente excluyentes; el modo seleccionado se guarda en `ClientPuduTxMode`.

**Grupo Poo** — los tres controles bajo la etiqueta "Poo" dan forma a la banda de bajas frecuencias:

- **Drive** establece con qué intensidad se lleva el saturador o compresor de bajas frecuencias. Valores más altos añaden mayor densidad y grosor en las bajas.
- **Tune** centra la banda de enfoque de bajas frecuencias en una frecuencia específica.
- **Mix** mezcla la banda baja procesada con la señal seca. Al 0 % el procesador Poo queda completamente puenteado; al 100 % es completamente húmedo.

**Grupo Doo** — los tres controles bajo la etiqueta "Doo" añaden presencia y aire en la banda de altas frecuencias:

- **Tune** centra la banda de excitación de altas frecuencias en una frecuencia específica. El mapeo es logarítmico, por lo que el control avanza más lentamente en frecuencias más altas.
- **Air** establece la cantidad de armónicos añadidos en la banda Doo.
- **Mix** mezcla las altas frecuencias excitadas con la señal seca.

El **logotipo de PooDoo** en la parte superior del applet pulsa en brillo con el nivel RMS de la señal procesada (húmeda), ofreciendo una indicación visual de que el excitador está activo y recibiendo audio.

El puenteo y la habilitación se gestionan desde el widget CHAIN, no mediante controles dentro del applet. Para abrir el editor flotante de PUDU, haga doble clic en la etapa PUDU (Enh) en el widget CHAIN.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistente |
|---|---|---|---|
| Even / Odd | — | Una u otra | `ClientPuduTxMode` |
| Poo / Drive | 6.0 dB | 0.0 – 24.0 dB | `ClientPuduTxPooDriveDb` |
| Poo / Tune | 100 Hz | 50 – 160 Hz | `ClientPuduTxPooTuneHz` |
| Poo / Mix | 30 % | 0 – 100 % | `ClientPuduTxPooMix` |
| Doo / Tune | 5000 Hz | 1000 – 10000 Hz | `ClientPuduTxDooTuneHz` |
| Doo / Air | 6.0 dB | 0.0 – 24.0 dB | `ClientPuduTxDooHarmonicsDb` |
| Doo / Mix | 30 % | 0 – 100 % | `ClientPuduTxDooMix` |

El estado de habilitación/deshabilitación se guarda por separado como `ClientPuduTxEnabled` y se controla desde el widget CHAIN.

## Consejos

- El pulso del logotipo de PooDoo es una comprobación rápida de que el audio fluye por la ruta húmeda. Si el logotipo no pulsa durante la transmisión, verifique que la etapa PUDU esté habilitada en el widget CHAIN.
- Poo / Tune responde de forma lineal; por lo tanto, ajústelo cerca de la frecuencia fundamental de su voz para obtener el realce de bajas más focalizado.
- Doo / Tune utiliza una escala logarítmica. Un pequeño movimiento físico cerca del extremo superior del rango abarca un amplio intervalo de frecuencias; use giros lentos y deliberados al apuntar a un pico de presencia específico.
- Mantenga Poo / Mix y Doo / Mix en valores moderados (20–40 %) como punto de partida. El procesamiento paralelo con niveles de mezcla altos puede hacer que la señal suene excesivamente procesada en el extremo receptor.

## Relacionados

- [Elegir el carácter Aphex (Even) o Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- [Ajustar Poo Drive para grosor en bajas frecuencias](dial-poo-drive-for-lf-thickness.md)
- [Sintonizar Poo a la frecuencia fundamental de su voz](tune-poo-to-the-fundamental-of-your-voice.md)
- [Mezclar el realce de Poo con Mix](blend-the-poo-enhancement-with-mix.md)
- [Centrar Doo en la banda de presencia de su micrófono](centre-doo-on-the-presence-band-for-your-mic.md)
- [Añadir aire con los armónicos de Doo](add-air-with-doo-harmonics.md)
- [Mezclar la excitación de Doo con Mix](blend-the-doo-excitement-with-mix.md)
- [Puentear PUDU desde la cadena](bypass-pudu-from-the-chain.md)
