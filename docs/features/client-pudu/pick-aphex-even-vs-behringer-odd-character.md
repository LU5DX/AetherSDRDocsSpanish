# Elegir el carácter Aphex (par) frente a Behringer (impar)

Elija entre dos algoritmos de realce armónico en el excitador PUDU: el modo Even (línea Aphex) para un carácter más cálido y asimétrico, o el modo Odd (línea Behringer) para un sonido más brillante y simétrico. La selección se aplica de forma independiente a las cadenas TX y RX.

## Antes de comenzar

- La etapa PUDU debe estar visible en la cadena Aetherial Audio. Si el applet está oculto, habilite la etapa PUDU a través del widget CHAIN en el lado TX o RX, o haga doble clic en la etapa PUDU en el widget CHAIN para abrir el editor flotante.
- Decida si está ajustando la ruta de transmisión ("Aetherial TX Voice Processor — TX") o la ruta de recepción ("Aetherial RX Poodoo™ — RX"). Los dos lados son completamente independientes.
- En TX, el panel se abre con el título "Aetherial Poodoo™ — TX". En RX, el panel se abre con el título "Aetherial Poodoo™ — RX". Utilice el panel correcto para la cadena que desea ajustar.

## Pasos

1. Abra el panel del excitador PUDU: haga doble clic en la etapa PUDU en el widget CHAIN del lado TX o RX. Aparece el editor flotante con el título correcto para esa cadena.
2. Encuentre los dos botones de modo directamente debajo del logotipo de AetherVoice: `Even` y `Odd`.
3. Haga clic en `Even` para seleccionar el modelado asimétrico de la línea Aphex: armónicos predominantemente pares, más cálidos y con saturación LF Big Bottom. El botón se resalta en ámbar cuando está activo.
4. Haga clic en `Odd` para seleccionar el modelado tanh simétrico de la línea Behringer: armónicos impares puros, más brillantes, con un compresor de graves feed-forward.
5. Cierre el panel. Para ajustar la otra cadena, haga doble clic en su etapa PUDU en el widget CHAIN para abrir su panel independiente.

La selección se guarda inmediatamente en `ClientPuduTxMode` (TX) o `ClientPuduRxMode` (RX).

## Descripción de cada control

| Control         | Comportamiento                                                                                      | Valor predeterminado                     |
|-----------------|-----------------------------------------------------------------------------------------------------|------------------------------------------|
| `Even`          | Selecciona el modelado asimétrico de la línea Aphex. Exclusivo con `Odd`.                           | —                                        |
| `Odd`           | Selecciona el modelado tanh simétrico de la línea Behringer. Exclusivo con `Even`.                  | —                                        |
| Logo AetherVoice | Logotipo animado que pulsa con el RMS de la señal procesada. Muestra la marca 'AetherVoice™'. | Widget PooDooLogo — 40 px de altura mínima. |

Solo uno de los modos `Even` u `Odd` puede estar activo a la vez. Seleccionar uno deselecciona el otro.

## Controles de perilla

El excitador PUDU proporciona seis perillas organizadas en dos grupos:

### Grupo Body (procesador de baja frecuencia)

| Control    | Predeterminado | Rango            | Clave de ajuste            | Comportamiento                                                                |
|------------|----------------|------------------|----------------------------|-------------------------------------------------------------------------------|
| Drive      | 6.0 dB         | 0.0 a 24.0 dB    | `ClientPuduTxPooDriveDb`   | Mapeo lineal. Excita más el saturador/compresor de baja frecuencia.          |
| Tune       | 100 Hz         | 50 a 160 Hz      | `ClientPuduTxPooTuneHz`    | Mapeo lineal. Centra la banda de enfoque de baja frecuencia.                  |
| Mix        | 30 %           | 0.0 a 100.0 %    | `ClientPuduTxPooMix`       | Mapeo lineal. Mezcla la banda baja realzada con la señal seca.               |

### Grupo Clarity (procesador de alta frecuencia)

| Control    | Predeterminado | Rango              | Clave de ajuste               | Comportamiento                                                                 |
|------------|----------------|--------------------|-------------------------------|--------------------------------------------------------------------------------|
| Tune       | 5000 Hz        | 1000 a 10000 Hz    | `ClientPuduTxDooTuneHz`       | Mapeo logarítmico. Centra la banda de excitación de alta frecuencia.           |
| Air        | 6.0 dB         | 0.0 a 24.0 dB      | `ClientPuduTxDooHarmonicsDb`  | Mapeo lineal. Cantidad de armónicos / 'aire' añadidos en la banda alta.        |
| Mix        | 30 %           | 0.0 a 100.0 %      | `ClientPuduTxDooMix`          | Mapeo lineal. Mezcla las altas frecuencias excitadas con la señal seca.        |

## Edición de valor en línea

Cada perilla admite la entrada numérica directa:

1. Haga clic en el texto del valor que se muestra debajo de la perilla. Aparece un pequeño editor de texto con un borde cian.
2. Escriba un nuevo valor. Puede incluir unidades o caracteres adicionales; el editor elimina automáticamente el contenido no numérico.
3. Presione `Enter` o haga clic en otro lugar para aplicar el valor. El valor se limita al rango válido de la perilla.
4. Presione `Escape` para cancelar la edición y volver al valor anterior.

El editor en línea está siempre disponible y utiliza el mismo formato de visualización que la etiqueta de la perilla (por ejemplo, "6.0 dB", "100 Hz", "30 %").

## Etiquetas de grupo

La etiqueta del grupo "Body" agrupa las tres perillas de baja frecuencia (Drive, Tune, Mix). La etiqueta del grupo "Clarity" agrupa las tres perillas de alta frecuencia (Tune, Air, Mix).

## Consejos

- El modo Even es adecuado para señales de voz donde se busca calidez y cuerpo en las frecuencias graves. El modo Odd es adecuado para situaciones donde se prefiere una mayor presencia y brillo.
- El logotipo de AetherVoice pulsa con el RMS de la señal procesada, por lo que puede ver la reacción del excitador al cambiar de modo sin necesidad de monitorear el audio.
- Cuando la etapa PUDU está en bypass, todo el mosaico del applet se atenúa aproximadamente al 55% de opacidad, coincidiendo con el efecto de atenuación aplicado a la curva EQ. Esto es solo un indicador visual y no afecta su configuración.
- Las seis perillas de los grupos Body y Clarity permanecen activas independientemente del modo seleccionado; su efecto en la señal cambia de carácter según el modo elegido.

## Relacionados

- [Descripción general de Aetherial TX Voice Processor / Aetherial RX Poodoo](overview.md)
- [Ajuste Poo Drive para grosor LF](dial-poo-drive-for-lf-thickness.md)
- [Añada aire con Doo Air](add-air-with-doo-harmonics.md)
- [Ponga PUDU en bypass desde cualquier cadena](bypass-pudu-from-either-chain.md)
