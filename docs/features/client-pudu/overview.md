# Descripción general de Aetherial TX Poodoo / Aetherial RX Poodoo

El applet Aetherial Poodoo es la etapa de mejora armónica en el centro de la cadena Aetherial Audio. Se ejecuta como dos instancias completamente independientes — una en la ruta TX ("Aetherial TX Poodoo") y otra en la ruta RX ("Aetherial RX Poodoo") — lo que permite modelar el peso de las frecuencias bajas y el aire de las frecuencias altas de forma separada para el audio de transmisión y recepción.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en el widget CHAIN en el lado TX o RX correspondiente antes de que el applet sea visible.
- El contenedor principal Aetherial Audio (TXDSP) debe estar abierto en el panel de applets.

## Cómo funciona

Cada instancia de Poodoo procesa el audio en dos bandas paralelas, denominadas **Poo** (baja frecuencia) y **Doo** (alta frecuencia). El carácter del procesamiento lo determina el modo que se seleccione:

- El modo **Even** utiliza modelado asimétrico de linaje Aphex — predominantemente armónicos pares, de carácter más cálido, con saturación de graves Big Bottom.
- El modo **Odd** utiliza modelado simétrico tanh de linaje Behringer — armónicos impares puros, de carácter más brillante, con un compresor de graves de retroalimentación directa.

Ambas bandas producen una señal procesada (wet) que se mezcla con la señal seca (dry) mediante sus respectivos controles Mix. El logotipo animado de PooDoo pulsa con el brillo del nivel RMS de la señal procesada, ofreciendo una indicación visual de cuánta mejora está activa.

Las instancias TX y RX se abren haciendo doble clic en la etapa PUDU en el widget CHAIN del lado correspondiente. El editor flotante se titula "Aetherial Poodoo — TX" o "Aetherial Poodoo — RX". También puede hacer clic derecho en la barra de título del subcontenedor "Aetherial TX Poodoo" o "Aetherial RX Poodoo" para hacerlo flotante, extraerlo u ocultarlo. El bypass se gestiona directamente desde el widget CHAIN; no hay un botón Enable separado dentro del applet.

Todos los ajustes se guardan de forma independiente para los lados TX y RX.

## Qué hace cada control

### Mode

| Control | Comportamiento | Ajuste guardado |
|---|---|---|
| Even | Selecciona el modelado asimétrico de linaje Aphex. Se ilumina en ámbar cuando está activo. Exclusivo con Odd. | `ClientPuduTxMode` / `ClientPuduRxMode` |
| Odd | Selecciona el modelado simétrico tanh de linaje Behringer. Exclusivo con Even. | `ClientPuduTxMode` / `ClientPuduRxMode` |

### Grupo Poo (procesador de baja frecuencia)

| Control | Predeterminado | Rango | Comportamiento | Clave de ajuste TX | Clave de ajuste RX |
|---|---|---|---|---|---|
| Poo / Drive | 6.0 dB | 0.0 – 24.0 dB | Aumenta la intensidad del saturador o compresor de baja frecuencia. Mapeo lineal. | `ClientPuduTxPooDriveDb` | `ClientPuduRxPooDriveDb` |
| Poo / Tune | 100 Hz | 50 – 160 Hz | Centra la banda de enfoque de baja frecuencia. Mapeo lineal. | `ClientPuduTxPooTuneHz` | `ClientPuduRxPooTuneHz` |
| Poo / Mix | 30 % | 0 – 100 % | Mezcla la banda baja mejorada con la señal seca. Mapeo lineal. | `ClientPuduTxPooMix` | `ClientPuduRxPooMix` |

### Grupo Doo (procesador de alta frecuencia)

| Control | Predeterminado | Rango | Comportamiento | Clave de ajuste TX | Clave de ajuste RX |
|---|---|---|---|---|---|
| Doo / Tune | 5000 Hz | 1000 – 10000 Hz | Centra la banda de excitación de alta frecuencia. Mapeo logarítmico. | `ClientPuduTxDooTuneHz` | `ClientPuduRxDooTuneHz` |
| Doo / Air | 6.0 dB | 0.0 – 24.0 dB | Cantidad de armónicos y aire añadidos en la banda alta. Mapeo lineal. | `ClientPuduTxDooHarmonicsDb` | `ClientPuduRxDooHarmonicsDb` |
| Doo / Mix | 30 % | 0 – 100 % | Mezcla los agudos excitados con la señal seca. Mapeo lineal. | `ClientPuduTxDooMix` | `ClientPuduRxDooMix` |

### Indicador

| Indicador | Comportamiento |
|---|---|
| Logotipo PooDoo | Logotipo animado. El brillo pulsa con el nivel RMS de la señal procesada (wet). |

## Consejos

- Mantenga los valores de Mix moderados — tanto Poo / Mix como Doo / Mix tienen un valor predeterminado del 30 %, que integra el efecto sin saturar la señal seca.
- Poo / Tune utiliza un mapeo lineal entre 50 – 160 Hz. Para una voz masculina típica en TX, ajuste hacia el extremo inferior de ese rango; para material de programa en RX, ajuste al gusto por el oído.
- Doo / Tune utiliza un mapeo logarítmico, por lo que el control ofrece mayor resolución en las frecuencias más bajas dentro del rango de 1 – 10 kHz.
- Las instancias TX y RX son completamente independientes. Puede usar Even en TX y Odd en RX, o diferentes valores de Drive y Air en cada lado.

## Temas relacionados

- [Elegir el carácter Aphex (Even) o Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- [Ajustar Poo Drive para mayor densidad en bajas frecuencias](dial-poo-drive-for-lf-thickness.md)
- [Sintonizar Poo a la frecuencia fundamental de su voz (TX) o para realzar los graves en RX](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md)
- [Mezclar la mejora de Poo con Mix](blend-the-poo-enhancement-with-mix.md)
- [Centrar Doo en la banda de presencia de su micrófono (TX) o para mejorar la inteligibilidad en RX](centre-doo-on-the-presence-band-for-your-mic-tx-or-for-rx-intelligibility.md)
- [Añadir aire con Doo Harmonics](add-air-with-doo-harmonics.md)
- [Mezclar la excitación de Doo con Mix](blend-the-doo-excitement-with-mix.md)
- [Activar el bypass de PUDU desde cualquier cadena](bypass-pudu-from-either-chain.md)
