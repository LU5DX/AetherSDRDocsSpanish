# Resumen del Procesador de Voz TX Aetherial / Aetherial RX Poodoo™

El applet Aetherial Poodoo es la etapa de realce armónico central de la cadena de audio Aetherial. Funciona como dos instancias completamente independientes — una en la ruta de TX ("Procesador de Voz TX Aetherial") y otra en la ruta de RX ("Aetherial RX Poodoo™") — permitiéndole moldear el peso de las frecuencias graves y la "aire" de las frecuencias agudas por separado para el audio de transmisión y recepción.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en el widget CHAIN del lado TX o RX correspondiente antes de que el applet sea visible.
- El contenedor principal Aetherial Audio (TXDSP) debe estar abierto en el panel de applets.

## Cómo funciona

Cada instancia de Poodoo procesa el audio en dos bandas paralelas, denominadas **Poo** (bajas frecuencias) y **Doo** (altas frecuencias). El carácter del procesamiento lo define el modo que seleccione:

- **Modo Even** utiliza modelado asimétrico de linaje Aphex — predominantemente armónicos pares, de carácter más cálido, con saturación Big Bottom en bajas frecuencias.
- **Modo Odd** utiliza modelado simétrico tanh de linaje Behringer — armónicos impares puros, de carácter más brillante, con un compresor de graves feed-forward.

Ambas bandas producen una señal procesada (wet) que se mezcla con la señal seca (dry) mediante sus respectivos controles Mix. El logotipo animado de PooDoo parpadea al ritmo del valor RMS de la señal procesada (wet), ofreciendo una indicación visual de cuánto realce está activo.

Las instancias de TX y RX se abren haciendo doble clic en la etapa PUDU del widget CHAIN en el lado correspondiente. El editor flotante se titula "Aetherial Poodoo™ — TX" o "Aetherial Poodoo™ — RX". También puede hacer clic derecho en la barra de título del subcontenedor "Aetherial TX Poodoo" o "Aetherial RX Poodoo" para flotarlo, sacarlo u ocultarlo. El bypass se controla directamente desde el widget CHAIN; no hay un botón Enable independiente dentro del applet. Cuando la etapa está en bypass, todo el mosaico del applet se atenúa con una opacidad reducida para indicar que el DSP está inactivo.

Todos los ajustes se conservan de forma independiente para los lados TX y RX.

## Función de cada control

### Grupo Body (procesador de bajas frecuencias)

Los tres mandos bajo la etiqueta del grupo **Body** moldean las frecuencias graves.

| Control | Valor predeterminado | Rango | Comportamiento | Clave de ajuste TX | Clave de ajuste RX |
|---|---|---|---|---|---|
| Drive | 6,0 dB | 0,0 – 24,0 dB | Excita con más fuerza el saturador o compresor de bajas frecuencias. Mapeo lineal. Se muestra como "X,X dB". | `ClientPuduTxPooDriveDb` | `ClientPuduRxPooDriveDb` |
| Tune | 100 Hz | 50 – 160 Hz | Centra la banda de enfoque de bajas frecuencias. Mapeo lineal. Se muestra como "X Hz". | `ClientPuduTxPooTuneHz` | `ClientPuduRxPooTuneHz` |
| Mix | 30 % | 0 – 100 % | Mezcla la banda grave realzada con la señal seca. Mapeo lineal. Se muestra como porcentaje. | `ClientPuduTxPooMix` | `ClientPuduRxPooMix` |

### Grupo Clarity (procesador de altas frecuencias)

Los tres mandos bajo la etiqueta del grupo **Clarity** añaden presencia y "aire".

| Control | Valor predeterminado | Rango | Comportamiento | Clave de ajuste TX | Clave de ajuste RX |
|---|---|---|---|---|---|
| Tune | 5000 Hz | 1000 – 10000 Hz | Centra la banda de excitación de altas frecuencias. Mapeo logarítmico (1000 * 10^n). Se muestra como "5,0 kHz" por encima de 1 kHz, "X Hz" por debajo. | `ClientPuduTxDooTuneHz` | `ClientPuduRxDooTuneHz` |
| Air | 6,0 dB | 0,0 – 24,0 dB | Cantidad de armónicos y "aire" añadidos en la banda aguda. Mapeo lineal. Se muestra como "X,X dB". | `ClientPuduTxDooHarmonicsDb` | `ClientPuduRxDooHarmonicsDb` |
| Mix | 30 % | 0 – 100 % | Mezcla las frecuencias agudas excitadas con la señal seca. Mapeo lineal. Se muestra como porcentaje. | `ClientPuduTxDooMix` | `ClientPuduRxDooMix` |

### Modo

| Control | Comportamiento | Ajuste persistido |
|---|---|---|
| Even | Selecciona el modelado asimétrico de linaje Aphex. Se ilumina en color ámbar PooDoo cuando está activo. Excluye a Odd. | `ClientPuduTxMode` / `ClientPuduRxMode` |
| Odd | Selecciona el modelado simétrico tanh de linaje Behringer. Excluye a Even. | `ClientPuduTxMode` / `ClientPuduRxMode` |

### Indicadores

| Indicador | Comportamiento |
|---|---|
| Logotipo AetherVoice | Logotipo animado de marca que parpadea al ritmo del RMS de la señal procesada (wet). Muestra la marca "AetherVoice™". Altura mínima de 40 píxeles. |
| Corchete del grupo Body | Etiqueta de grupo: los tres mandos siguientes pertenecen al procesador de bajas frecuencias (Drive, Tune, Mix). |
| Corchete del grupo Clarity | Etiqueta de grupo: los tres mandos siguientes pertenecen al procesador de altas frecuencias (Tune, Air, Mix). |

## Uso del editor de valores

Cada mando admite la edición inline de valores. Haga clic en el texto del valor mostrado de un mando para activar el editor, escriba un número y luego presione Enter o haga clic en otro lugar para confirmar. El valor se limita al rango válido del mando. El editor acepta tanto formatos adaptados a la configuración regional (p. ej., "12,5" en regiones que usan coma decimal) como entrada numérica directa. Presione Escape mientras edita para cancelar y revertir.

## Consejos

- Mantenga los valores Mix moderados: el valor predeterminado de ambos Mix es 30 %, lo que mezcla el efecto sin abrumar la señal seca.
- Body Tune utiliza un mapeo lineal en el rango de 50 – 160 Hz. Para una voz masculina típica en TX, ajuste hacia el extremo inferior de ese rango; para material de programa en RX, ajuste al oído.
- Clarity Tune utiliza un mapeo logarítmico, por lo que el mando ofrece una resolución más fina en las frecuencias más bajas dentro del rango de 1 – 10 kHz.
- Las instancias TX y RX son completamente independientes. Puede usar Even en TX y Odd en RX, o diferentes cantidades de Drive y Air en cada lado.
- Cuando la etapa PUDU está en bypass desde el widget CHAIN, el mosaico del applet se atenúa visualmente. Esto coincide con el comportamiento de atenuación en la curva EQ y confirma de un vistazo que no se está aplicando DSP.

## Relacionados

- [Pick Aphex (Even) vs Behringer (Odd) character](pick-aphex-even-vs-behringer-odd-character.md)
- [Dial Drive for LF thickness](dial-poo-drive-for-lf-thickness.md)
- [Tune Body to the fundamental of your voice (TX) or to bring out RX program lows](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md)
- [Blend the low-frequency enhancement with Mix](blend-the-poo-enhancement-with-mix.md)
- [Centre Clarity Tune on the presence band for your mic (TX) or for RX intelligibility](centre-doo-on-the-presence-band-for-your-mic-tx-or-for-rx-intelligibility.md)
- [Add air with Clarity Air](add-air-with-doo-harmonics.md)
- [Blend the high-frequency excitement with Clarity Mix](blend-the-doo-excitement-with-mix.md)
- [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md)
