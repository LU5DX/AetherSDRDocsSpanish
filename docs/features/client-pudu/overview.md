# Procesador de Voz de TX Aetherial / Aetherial RX Poodoo™ — Descripción general

El applet Aetherial Poodoo es la etapa de realce armónico en el centro de la cadena de audio Aetherial. Funciona como dos instancias completamente independientes — una en la ruta de TX ("Procesador de Voz de TX Aetherial") y otra en la ruta de RX ("Aetherial RX Poodoo™") — lo que le permite moldear el peso de las frecuencias graves y la presencia de las frecuencias agudas por separado para el audio de transmisión y recepción.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en el widget CHAIN del lado TX o RX correspondiente antes de que el applet sea visible.
- El contenedor principal Aetherial Audio (TXDSP) debe estar abierto en el panel de applets.

## Cómo funciona

Cada instancia de Poodoo procesa el audio en dos bandas paralelas, denominadas **Poo** (frecuencias bajas) y **Doo** (frecuencias altas). El carácter del procesamiento se define mediante el modo que seleccione:

- El modo **Even** utiliza conformación asimétrica de la línea Aphex — armónicos predominantemente pares, de carácter más cálido, con saturación Big Bottom en frecuencias bajas.
- El modo **Odd** utiliza conformación simétrica tanh de la línea Behringer — armónicos impares puros, de carácter más brillante, con un compresor de graves feed-forward.

Ambas bandas producen una señal procesada que se mezcla con la señal seca usando sus respectivos controles Mix. El logotipo animado de PooDoo pulsa con la amplitud RMS de la señal procesada (húmeda), ofreciendo una indicación visual de cuánto realce está activo.

Las instancias de TX y RX se abren haciendo doble clic en la etapa PUDU en el widget CHAIN del lado correspondiente. El editor flotante se titula "Aetherial Voice Processor — TX" o "Aetherial Voice Processor — RX". También puede hacer clic derecho en la barra de título del subcontenedor "Aetherial TX Poodoo" o "Aetherial RX Poodoo" para flotarlo, sacarlo u ocultarlo. La bypass se gestiona directamente desde el widget CHAIN; no hay un botón Enable separado dentro del applet. Cuando la etapa está en bypass, todo el mosaico del applet se atenúa con opacidad reducida para indicar que el DSP está inactivo.

Toda la configuración se guarda de forma independiente para los lados TX y RX.

## Qué hace cada control

### Modo

| Control | Comportamiento | Configuración persistente |
|---|---|---|
| Even | Selecciona la conformación asimétrica de la línea Aphex. Se ilumina en color ámbar PooDoo cuando está activo. Exclusivo con Odd. | `ClientPuduTxMode` / `ClientPuduRxMode` |
| Odd | Selecciona la conformación simétrica tanh de la línea Behringer. Exclusivo con Even. | `ClientPuduTxMode` / `ClientPuduRxMode` |

### Grupo Poo (procesador de frecuencias bajas)

| Control | Valor predet. | Rango | Comportamiento | Clave de config. TX | Clave de config. RX |
|---|---|---|---|---|---|
| Poo / Drive | 6.0 dB | 0.0 – 24.0 dB | Excita con más intensidad el saturador o compresor de frecuencias bajas. Mapeo lineal. Se muestra como "X.X dB". | `ClientPuduTxPooDriveDb` | `ClientPuduRxPooDriveDb` |
| Poo / Tune | 100 Hz | 50 – 160 Hz | Centra la banda de enfoque de frecuencias bajas. Mapeo lineal. Se muestra como "X Hz". | `ClientPuduTxPooTuneHz` | `ClientPuduRxPooTuneHz` |
| Poo / Mix | 30 % | 0 – 100 % | Mezcla la banda baja realzada con la señal seca. Mapeo lineal. Se muestra como porcentaje. | `ClientPuduTxPooMix` | `ClientPuduRxPooMix` |

### Grupo Doo (procesador de frecuencias altas)

| Control | Valor predet. | Rango | Comportamiento | Clave de config. TX | Clave de config. RX |
|---|---|---|---|---|---|
| Doo / Tune | 5000 Hz | 1000 – 10000 Hz | Centra la banda de excitación de frecuencias altas. Mapeo logarítmico (1000 * 10^n). Se muestra como "5.0 kHz" por encima de 1 kHz, "X Hz" por debajo. | `ClientPuduTxDooTuneHz` | `ClientPuduRxDooTuneHz` |
| Doo / Air | 6.0 dB | 0.0 – 24.0 dB | Cantidad de armónicos y aire añadidos en la banda alta. Mapeo lineal. Se muestra como "X.X dB". | `ClientPuduTxDooHarmonicsDb` | `ClientPuduRxDooHarmonicsDb` |
| Doo / Mix | 30 % | 0 – 100 % | Mezcla las frecuencias altas excitadas con la señal seca. Mapeo lineal. Se muestra como porcentaje. | `ClientPuduTxDooMix` | `ClientPuduRxDooMix` |

### Indicadores

| Indicador | Comportamiento |
|---|---|
| Pulso del logotipo PooDoo | Logotipo animado de marca. El brillo pulsa con la amplitud RMS de la señal procesada (húmeda). Altura mínima de 40 px. |
| Corchete del grupo Poo | Etiqueta de grupo: los tres controles debajo pertenecen al procesador de frecuencias bajas. |
| Corchete del grupo Doo | Etiqueta de grupo: los tres controles debajo pertenecen al procesador de frecuencias altas. |

## Consejos

- Mantenga los valores de Mix moderados: tanto Poo / Mix como Doo / Mix tienen un valor predeterminado de 30 %, lo que mezcla el efecto sin abrumar la señal seca.
- Poo / Tune utiliza un mapeo lineal en el rango de 50 – 160 Hz. Para una voz masculina típica en TX, ajuste hacia el extremo inferior de ese rango; para material de programa en RX, ajuste al oído según prefiera.
- Doo / Tune utiliza un mapeo logarítmico, por lo que el control ofrece una resolución más fina en frecuencias más bajas dentro del rango de 1 – 10 kHz.
- Las instancias de TX y RX son completamente independientes. Puede usar Even en TX y Odd en RX, o diferentes cantidades de Drive y Air en cada lado.
- Cuando la etapa PUDU está en bypass desde el widget CHAIN, el mosaico del applet se atenúa visualmente. Esto coincide con el comportamiento de atenuación en la curva EQ y confirma de un vistazo que no se está aplicando ningún DSP.

## Relacionado

- [Seleccionar el carácter Aphex (Even) vs Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- [Ajustar Poo Drive para grosor en LF](dial-poo-drive-for-lf-thickness.md)
- [Ajustar Poo a la frecuencia fundamental de su voz (TX) o para resaltar graves del programa RX](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md)
- [Mezclar el realce Poo con Mix](blend-the-poo-enhancement-with-mix.md)
- [Centrar Doo en la banda de presencia de su micrófono (TX) o para inteligibilidad RX](centre-doo-on-the-presence-band-for-your-mic-tx-or-for-rx-intelligibility.md)
- [Añadir aire con Doo Harmonics](add-air-with-doo-harmonics.md)
- [Mezclar la excitación Doo con Mix](blend-the-doo-excitement-with-mix.md)
- [Activar bypass de PUDU desde cualquier cadena](bypass-pudu-from-either-chain.md)
