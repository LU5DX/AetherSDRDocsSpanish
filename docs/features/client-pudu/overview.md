# Descripción general del Aetherial TX Voice Processor / Aetherial RX Poodoo™

El applet Aetherial Poodoo es la etapa de realce armónico en el centro de la cadena Aetherial Audio. Se ejecuta como dos instancias completamente independientes — una en la ruta de TX ("Aetherial TX Voice Processor") y otra en la ruta de RX ("Aetherial RX Poodoo™") — permitiéndole modelar el peso de las frecuencias bajas y el aire de las altas frecuencias por separado para el audio de transmisión y recepción.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en el widget CHAIN en el lado TX o RX correspondiente antes de que el applet sea visible.
- El contenedor principal Aetherial Audio (TXDSP) debe estar abierto en el panel de applets.

## Cómo funciona

Cada instancia de Poodoo procesa audio en dos bandas paralelas, denominadas **Poo** (baja frecuencia) y **Doo** (alta frecuencia). El carácter del procesamiento se define por el modo que elija:

- El modo **Even** usa modelado asimétrico de la línea Aphex — armónicos predominantemente pares, de carácter más cálido, con saturación Big Bottom de baja frecuencia.
- El modo **Odd** usa modelado tanh simétrico de la línea Behringer — armónicos impares puros, de carácter más brillante, con un compresor de graves feed-forward.

Ambas bandas producen una señal procesada (wet) que se mezcla con la señal seca (dry) usando sus respectivos mandos Mix. El logotipo animado de PooDoo palpita con el brillo de la señal procesada (wet) RMS, dando una indicación visual de cuánto realce está activo.

Las instancias TX y RX se abren haciendo doble clic en la etapa PUDU en el widget CHAIN del lado correspondiente. El editor flotante se titula "Aetherial Poodoo™ — TX" o "Aetherial Poodoo™ — RX". También puede hacer clic derecho en la barra de título del subcontenedor "Aetherial TX Poodoo" o "Aetherial RX Poodoo" para flotarlo, sacarlo u ocultarlo. El bypass se maneja directamente desde el widget CHAIN; no hay un botón de Enable independiente dentro del applet. Cuando la etapa está en bypass, todo el mosaico del applet se atenúa con opacidad reducida para indicar que el DSP está inactivo.

Toda la configuración se conserva de forma independiente para los lados TX y RX.

## Qué hace cada control

### Grupo Body (procesador de baja frecuencia)

Los tres mandos bajo la etiqueta del grupo **Body** modelan las frecuencias bajas.

| Control | Valor predeterminado | Rango | Comportamiento | Clave de configuración TX | Clave de configuración RX |
|---|---|---|---|---|---|
| Drive | 6.0 dB | 0.0 – 24.0 dB | Excita con más fuerza el saturador o compresor de baja frecuencia. Mapeo lineal. Se muestra como "X.X dB". | `ClientPuduTxPooDriveDb` | `ClientPuduRxPooDriveDb` |
| Tune | 100 Hz | 50 – 160 Hz | Centra la banda de enfoque de baja frecuencia. Mapeo lineal. Se muestra como "X Hz". | `ClientPuduTxPooTuneHz` | `ClientPuduRxPooTuneHz` |
| Mix | 30 % | 0 – 100 % | Mezcla la banda baja realzada con la señal seca. Mapeo lineal. Se muestra como porcentaje. | `ClientPuduTxPooMix` | `ClientPuduRxPooMix` |

### Grupo Clarity (procesador de alta frecuencia)

Los tres mandos bajo la etiqueta del grupo **Clarity** añaden presencia y aire.

| Control | Valor predeterminado | Rango | Comportamiento | Clave de configuración TX | Clave de configuración RX |
|---|---|---|---|---|---|
| Tune | 5000 Hz | 1000 – 10000 Hz | Centra la banda de excitación de alta frecuencia. Mapeo logarítmico (1000 * 10^n). Se muestra como "5.0 kHz" por encima de 1 kHz, "X Hz" por debajo. | `ClientPuduTxDooTuneHz` | `ClientPuduRxDooTuneHz` |
| Air | 6.0 dB | 0.0 – 24.0 dB | Cantidad de armónicos y aire añadidos en la banda alta. Mapeo lineal. Se muestra como "X.X dB". | `ClientPuduTxDooHarmonicsDb` | `ClientPuduRxDooHarmonicsDb` |
| Mix | 30 % | 0 – 100 % | Mezcla los agudos excitados con la señal seca. Mapeo lineal. Se muestra como porcentaje. | `ClientPuduTxDooMix` | `ClientPuduRxDooMix` |

### Modo

| Control | Comportamiento | Configuración persistida |
|---|---|---|
| Even | Selecciona el modelado asimétrico de la línea Aphex. Se ilumina en color ámbar PooDoo cuando está activo. Exclusivo con Odd. | `ClientPuduTxMode` / `ClientPuduRxMode` |
| Odd | Selecciona el modelado tanh simétrico de la línea Behringer. Exclusivo con Even. | `ClientPuduTxMode` / `ClientPuduRxMode` |

### Indicadores

| Indicador | Comportamiento |
|---|---|
| Logotipo AetherVoice | Logotipo animado de marca que palpita con el RMS de la señal procesada. Muestra la marca "AetherVoice™". Altura mínima de 40 px. |
| Corchete del grupo Body | Etiqueta de grupo — los tres mandos siguientes pertenecen al procesador de baja frecuencia (Drive, Tune, Mix). |
| Corchete del grupo Clarity | Etiqueta de grupo — los tres mandos siguientes pertenecen al procesador de alta frecuencia (Tune, Air, Mix). |

## Uso del editor de valores

Cada mando admite la edición en línea del valor. Haga clic en el texto del valor mostrado de un mando para activar el editor, escriba un número y luego presione Enter o haga clic en otro lugar para confirmar. El valor se limita al rango válido del mando. El editor acepta tanto formatos adaptados a la configuración regional (p. ej., "12,5" en configuraciones regionales con coma decimal) como entrada numérica sin formato. Presione Escape mientras edita para cancelar y revertir.

## Soporte de temas

Los colores de los mandos y del texto en todo el applet PUDU ahora se leen del sistema de temas en lugar de usar valores fijos. Los siguientes espacios de nombres del tema controlan la apariencia de PUDU:

- `color.knob.background` — la pista de fondo del anillo del mando
- `color.knob.foreground` — el arco del mando que representa el valor actual
- `color.knob.handle` — la línea indicadora del mando
- `color.text.primary` — el texto del valor que se muestra debajo de cada mando
- `color.text.secondary` — el texto de la etiqueta encima o al lado de cada mando

El contenedor del applet PUDU está registrado bajo `applet/pudu`, lo que permite anulaciones de tema por applet. Las anulaciones de tema permiten el color ámbar PooDoo en el botón de opción Even cuando está seleccionado.

Las etiquetas de corchete tanto en el panel del applet como en el editor flotante usan `{{color.text.primary}}` del tema para su color de texto, lo que garantiza una apariencia uniforme en diferentes temas.

## Consejos

- Mantenga los valores Mix moderados — ambos valores predeterminados de Mix son 30 %, lo que mezcla el efecto sin dominar la señal seca.
- Body Tune usa un mapeo lineal en el rango de 50 – 160 Hz. Para una voz masculina típica en TX, ajuste hacia el extremo inferior de ese rango; para material de programa en RX, ajuste al oído según su preferencia.
- Clarity Tune usa un mapeo logarítmico, por lo que el mando ofrece una resolución más fina en frecuencias más bajas dentro del rango de 1 – 10 kHz.
- Las instancias TX y RX son completamente independientes. Puede usar Even en TX y Odd en RX, o diferentes cantidades de Drive y Air en cada lado.
- Cuando la etapa PUDU está en bypass desde el widget CHAIN, el mosaico del applet se atenúa visualmente. Esto coincide con el comportamiento de atenuación en la curva EQ y confirma de un vistazo que no se está aplicando ningún DSP.

## Relacionados

- [Pick Aphex (Even) vs Behringer (Odd) character](pick-aphex-even-vs-behringer-odd-character.md)
- [Dial Drive for LF thickness](dial-poo-drive-for-lf-thickness.md)
- [Tune Body to the fundamental of your voice (TX) or to bring out RX program lows](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md)
- [Blend the low-frequency enhancement with Mix](blend-the-poo-enhancement-with-mix.md)
- [Centre Clarity Tune on the presence band for your mic (TX) or for RX intelligibility](centre-doo-on-the-presence-band-for-your-mic-tx-or-for-rx-intelligibility.md)
- [Add air with Clarity Air](add-air-with-doo-harmonics.md)
- [Blend the high-frequency excitement with Clarity Mix](blend-the-doo-excitement-with-mix.md)
- [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md)
