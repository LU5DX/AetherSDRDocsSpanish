# Descripción general del excitador PUDU

El excitador PUDU es la pieza central de la cadena de TX de PooDoo Audio. Añade realce armónico y modelado tonal al audio transmitido en dos regiones de frecuencia: cuerpo de bajos ("Poo") y presencia y aire en alta frecuencia ("Doo").

## Antes de comenzar

- La etapa PUDU debe estar habilitada en el widget CHAIN antes de que el applet PUDU sea visible. El subcontenedor permanece oculto hasta que la etapa esté activa.
- El contenedor principal de PooDoo Audio (TXDSP) debe estar abierto en el panel de applets.

## Cómo funciona

PUDU procesa el audio en dos bandas independientes, cada una controlada por un grupo de tres mandos.

**Selección de modo** — Los botones de opción Even y Odd en la parte superior del applet seleccionan el carácter del modelado armónico aplicado en ambas bandas. El modo Even utiliza saturación asimétrica de linaje Aphex, produciendo predominantemente armónicos pares con un carácter más cálido y saturación de bajos frecuentes Big Bottom. El modo Odd utiliza modelado simétrico tanh de linaje Behringer, produciendo armónicos impares puros con un carácter más brillante y un compresor de graves de alimentación directa. Los dos botones son mutuamente excluyentes; la selección activa se muestra en ámbar.

**Grupo Poo** — Los tres mandos bajo el indicador "Poo" actúan sobre la banda de baja frecuencia. Drive empuja con más fuerza el saturador o compresor. Tune centra la banda de frecuencia en el fundamental objetivo. Mix mezcla la banda de bajos procesada con la señal sin procesar.

**Grupo Doo** — Los tres mandos bajo el indicador "Doo" actúan sobre la banda de alta frecuencia. Tune centra la banda de excitación en la región de presencia o aire. Air controla la cantidad de armónicos añadidos en esa banda. Mix mezcla los agudos excitados con la señal sin procesar.

El logotipo animado de PooDoo pulsa en brillo con el RMS de la señal procesada (húmeda), proporcionando una indicación visual continua de que la etapa está activa y transmitiendo audio.

Para abrir el editor flotante, haga doble clic en la etapa PUDU (Enh) en el widget CHAIN. Para hacer flotar, separar u ocultar el subcontenedor, haga clic derecho en la barra de título del subcontenedor PUDU.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistido |
|---|---|---|---|
| Even | — | — | `ClientPuduTxMode` |
| Odd | — | — | `ClientPuduTxMode` |
| Poo / Drive | 6.0 dB | 0.0 – 24.0 dB | `ClientPuduTxPooDriveDb` |
| Poo / Tune | 100 Hz | 50 – 160 Hz | `ClientPuduTxPooTuneHz` |
| Poo / Mix | 30 % | 0 – 100 % | `ClientPuduTxPooMix` |
| Doo / Tune | 5000 Hz | 1000 – 10000 Hz | `ClientPuduTxDooTuneHz` |
| Doo / Air | 6.0 dB | 0.0 – 24.0 dB | `ClientPuduTxDooHarmonicsDb` |
| Doo / Mix | 30 % | 0 – 100 % | `ClientPuduTxDooMix` |

El ajuste `ClientPuduTxEnabled` guarda si la etapa PUDU está activa en la cadena.

## Consejos

- Poo / Tune responde a un mapeo de frecuencia lineal, por lo que los ajustes pequeños cerca de 50 Hz y cerca de 160 Hz desplazan la banda en la misma cantidad absoluta. Ajuste Tune cerca del fundamental de su voz antes de aumentar Drive o Mix.
- Doo / Tune utiliza un mapeo logarítmico, por lo que el mando cubre más octavas hacia el extremo superior de su recorrido. Un valor de 5.0 kHz es la etiqueta mostrada en la posición predeterminada; los valores por debajo de 1000 Hz se muestran en Hz.
- Mantenga Poo / Mix y Doo / Mix en valores conservadores — ambos tienen un valor predeterminado de 30 %. Valores de mezcla elevados con ajustes altos de Drive pueden incrementar la potencia media de forma significativa.

## Relacionados

- [Elegir el carácter Aphex (Even) o Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- [Ajustar Poo Drive para obtener grosor en bajas frecuencias](dial-poo-drive-for-lf-thickness.md)
- [Sintonizar Poo al fundamental de su voz](tune-poo-to-the-fundamental-of-your-voice.md)
- [Mezclar el realce Poo con Mix](blend-the-poo-enhancement-with-mix.md)
- [Centrar Doo en la banda de presencia para su micrófono](centre-doo-on-the-presence-band-for-your-mic.md)
- [Añadir aire con los armónicos Doo](add-air-with-doo-harmonics.md)
- [Mezclar la excitación Doo con Mix](blend-the-doo-excitement-with-mix.md)
- [Omitir PUDU desde la cadena](bypass-pudu-from-the-chain.md)
