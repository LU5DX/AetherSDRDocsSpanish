# Descripción general de Aetherial TX Voice Processor / Aetherial RX Poodoo™

El applet Aetherial Poodoo es la etapa de realce armónico en el centro de la cadena de audio Aetherial Audio. Funciona como dos instancias completamente independientes (una en la ruta de TX, "Aetherial TX Voice Processor", y otra en la ruta de RX, "Aetherial RX Poodoo™"), lo que le permite dar forma al peso de los graves y al aire de las frecuencias altas por separado para el audio de transmisión y recepción.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en el widget CHAIN en el lado correspondiente de TX o RX para que el applet sea visible.
- El contenedor principal Aetherial Audio (TXDSP) debe estar abierto en el panel de applets.

## Cómo funciona

Cada instancia de Poodoo procesa el audio en dos bandas paralelas, denominadas **Poo** (baja frecuencia) y **Doo** (alta frecuencia). El carácter del procesamiento se define por el modo que elija:

- El modo **Even** utiliza modelado asimétrico de la línea Aphex, con armónicos predominantemente pares, de carácter más cálido y con saturación Big Bottom de baja frecuencia.
- El modo **Odd** utiliza modelado tanh simétrico de la línea Behringer, con armónicos impares puros, de carácter más brillante y con un compresor de graves de avance (feed-forward).

Ambas bandas producen una señal procesada (wet) que se mezcla nuevamente con la señal seca (dry) usando sus respectivos controles Mix. El logotipo animado de PooDoo pulsa con la intensidad de la señal procesada (wet) RMS, proporcionando una indicación visual de cuánto realce está activo.

Las instancias de TX y RX se abren haciendo doble clic en la etapa PUDU en el widget CHAIN del lado correspondiente. El editor flotante se titula "Aetherial Poodoo™ — TX" o "Aetherial Poodoo™ — RX". También puede hacer clic derecho en la barra de título del subcontenedor "Aetherial TX Poodoo" o "Aetherial RX Poodoo" para flotarlo, sacarlo u ocultarlo. La desactivación (bypass) se maneja directamente desde el widget CHAIN; no hay un botón de habilitación independiente dentro del applet. Cuando la etapa está desactivada, el mosaico completo del applet se atenúa con una opacidad reducida para indicar que el DSP está inactivo.

Todas las configuraciones se conservan de forma independiente para los lados TX y RX.

## Qué hace cada control

### Modo

| Control | Comportamiento | Configuración persistente |
|---|---|---|
| Even | Selecciona el modelado asimétrico de la línea Aphex. Se ilumina en color ámbar PooDoo cuando está activo. Exclusivo con Odd. | `ClientPuduTxMode` / `ClientPuduRxMode` |
| Odd | Selecciona el modelado tanh simétrico de la línea Behringer. Exclusivo con Even. | `ClientPuduTxMode` / `ClientPuduRxMode` |

### Grupo Body (procesador de baja frecuencia)

Los tres controles bajo la etiqueta del grupo **Body** dan forma a los graves.

| Control | Valor predet. | Rango | Comportamiento | Clave de config. TX | Clave de config. RX |
|---|---|---|---|---|---|
| Drive | 6.0 dB | 0.0 – 24.0 dB | Impulsa con más fuerza el saturador o compresor de baja frecuencia. Mapeo lineal. Se muestra como "X.X dB". | `ClientPuduTxPooDriveDb` | `ClientPuduRxPooDriveDb` |
| Tune | 100 Hz | 50 – 160 Hz | Centra la banda de enfoque de baja frecuencia. Mapeo lineal. Se muestra como "X Hz". | `ClientPuduTxPooTuneHz` | `ClientPuduRxPooTuneHz` |
| Mix | 30 % | 0 – 100 % | Mezcla la banda de graves realzada nuevamente con la señal seca. Mapeo lineal. Se muestra como porcentaje. | `ClientPuduTxPooMix` | `ClientPuduRxPooMix` |

### Grupo Clarity (procesador de alta frecuencia)

Los tres controles bajo la etiqueta del grupo **Clarity** añaden presencia y aire.

| Control | Valor predet. | Rango | Comportamiento | Clave de config. TX | Clave de config. RX |
|---|---|---|---|---|---|
| Tune | 5000 Hz | 1000 – 10000 Hz | Centra la banda de excitación de alta frecuencia. Mapeo logarítmico (1000 * 10^n). Se muestra como "5.0 kHz" por encima de 1 kHz, "X Hz" por debajo. | `ClientPuduTxDooTuneHz` | `ClientPuduRxDooTuneHz` |
| Air | 6.0 dB | 0.0 – 24.0 dB | Cantidad de armónicos y aire añadidos en la banda alta. Mapeo lineal. Se muestra como "X.X dB". | `ClientPuduTxDooHarmonicsDb` | `ClientPuduRxDooHarmonicsDb` |
| Mix | 30 % | 0 – 100 % | Mezcla los agudos excitados nuevamente con la señal seca. Mapeo lineal. Se muestra como porcentaje. | `ClientPuduTxDooMix` | `ClientPuduRxDooMix` |

### Indicadores

| Indicador | Comportamiento |
|---|---|
| Logotipo AetherVoice | Logotipo animado de marca que pulsa con la señal RMS procesada (wet). Muestra la marca "AetherVoice™". Altura mínima de 40 px. |
| Corchete del grupo Body | Etiqueta de grupo: los tres controles debajo pertenecen al procesador de baja frecuencia (Drive, Tune, Mix). |
| Corchete del grupo Clarity | Etiqueta de grupo: los tres controles debajo pertenecen al procesador de alta frecuencia (Tune, Air, Mix). |

## Uso del editor de valores

Cada control admite la edición de valores en línea. Haga clic en el texto del valor mostrado de un control para activar el editor, escriba un número y luego presione Enter o haga clic en otro lugar para confirmar. El valor se limita al rango válido del control. El editor acepta tanto formatos adaptados a la configuración regional (por ejemplo, "12,5" en configuraciones regionales con coma decimal) como entrada numérica simple. Presione Escape mientras edita para cancelar y revertir.

## Soporte de temas

Los colores de los controles y del texto en todo el applet PUDU ahora se leen del sistema de temas en lugar de usar valores fijos. Los siguientes espacios de nombres del tema controlan la apariencia de PUDU:

- `color.knob.background` — la pista de fondo del anillo del control
- `color.knob.foreground` — el arco del control que representa el valor actual
- `color.knob.handle` — la línea del puntero del control
- `color.text.primary` — el texto del valor que se muestra debajo de cada control
- `color.text.secondary` — el texto de la etiqueta arriba o al lado de cada control

El contenedor del applet PUDU está registrado bajo `applet/pudu`, lo que permite anulaciones de tema por applet. Las anulaciones de tema permiten el color ámbar PooDoo en el botón de opción Even cuando está seleccionado.

Las etiquetas de corchete tanto en el panel del applet como en el editor flotante usan `{{color.text.primary}}` del tema para su color de texto, lo que garantiza una apariencia consistente en diferentes temas.

## Consejos

- Mantenga los valores de Mix moderados; ambos valores predeterminados de Mix son 30 %, lo que combina el efecto sin abrumar la señal seca.
- Body Tune utiliza un mapeo lineal en el rango de 50 a 160 Hz. Para una voz masculina típica en TX, ajuste hacia el extremo inferior de ese rango; para el material de programa en RX, ajuste al oído según su gusto.
- Clarity Tune utiliza un mapeo logarítmico, por lo que el control ofrece una resolución más fina en frecuencias más bajas dentro del rango de 1 a 10 kHz.
- Las instancias de TX y RX son completamente independientes. Puede usar Even en TX y Odd en RX, o diferentes cantidades de Drive y Air en cada lado.
- Cuando la etapa PUDU está desactivada desde el widget CHAIN, el mosaico del applet se atenúa visualmente. Esto coincide con el comportamiento de atenuación en la curva EQ y confirma de un vistazo que no se está aplicando DSP.

## Relacionados

- [Elegir el carácter Aphex (Even) vs Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- [Ajustar Drive para el grosor de baja frecuencia](dial-poo-drive-for-lf-thickness.md)
- [Ajustar Body a la frecuencia fundamental de su voz (TX) o para resaltar los graves del programa de RX](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md)
- [Mezclar el realce de baja frecuencia con Mix](blend-the-poo-enhancement-with-mix.md)
- [Centrar Clarity Tune en la banda de presencia para su micrófono (TX) o para la inteligibilidad de RX](centre-doo-on-the-presence-band-for-your-mic-tx-or-for-rx-intelligibility.md)
- [Añadir aire con Clarity Air](add-air-with-doo-harmonics.md)
- [Mezclar la excitación de alta frecuencia con Clarity Mix](blend-the-doo-excitement-with-mix.md)
- [Desactivar PUDU desde cualquiera de las cadenas](bypass-pudu-from-either-chain.md)
