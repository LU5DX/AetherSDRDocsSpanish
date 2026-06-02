# Selección del carácter Aphex (Par) frente a Behringer (Impar)

Elija entre dos algoritmos de realce armónico en el excitador PUDU: el modo Par (linaje Aphex) para un carácter más cálido y asimétrico, o el modo Impar (linaje Behringer) para un sonido más brillante y simétrico. La selección se aplica de forma independiente a las cadenas de TX y RX.

## Antes de comenzar

- La etapa PUDU debe estar visible en la cadena Aetherial Audio. Si el applet está oculto, active la etapa PUDU a través del widget CHAIN en el lado TX o RX, o haga doble clic en la etapa PUDU en el widget CHAIN para abrir el editor flotante.
- Decida si está ajustando la ruta de transmisión ("Aetherial TX Voice Processor — TX") o la ruta de recepción ("Aetherial RX Poodoo™ — RX"). Ambos lados son completamente independientes.
- En TX, el panel se abre con el título "Aetherial Poodoo™ — TX". En RX, el panel se abre con el título "Aetherial Poodoo™ — RX". Utilice el panel correcto para la cadena que desea ajustar.

## Pasos

1. Abra el panel del excitador PUDU: haga doble clic en la etapa PUDU en el widget CHAIN del lado TX o RX. El editor flotante aparece con el título correcto para esa cadena.
2. Localice los dos botones de modo directamente debajo del logotipo AetherVoice: `Even` e `Odd`.
3. Haga clic en `Even` para seleccionar el modelado asimétrico de linaje Aphex — armónicos predominantemente pares, más cálidos, con saturación de graves Big Bottom. El botón se ilumina en ámbar cuando está activo.
4. Haga clic en `Odd` para seleccionar el modelado tanh simétrico de linaje Behringer — armónicos puramente impares, más brillantes, con un compresor de graves feed-forward.
5. Cierre el panel. Para ajustar la otra cadena, haga doble clic en su etapa PUDU en el widget CHAIN para abrir su panel independiente.

La selección se guarda inmediatamente en `ClientPuduTxMode` (TX) o `ClientPuduRxMode` (RX).

## Función de cada control

| Control         | Comportamiento                                                                               | Valor predeterminado                       |
|-----------------|----------------------------------------------------------------------------------------------|--------------------------------------------|
| `Even`          | Selecciona el modelado asimétrico de linaje Aphex. Excluyente con `Odd`.                     | —                                          |
| `Odd`           | Selecciona el modelado tanh simétrico de linaje Behringer. Excluyente con `Even`.             | —                                          |
| Logo AetherVoice | Logotipo animado de marca que pulsa con el RMS de la señal procesada. Muestra la marca 'AetherVoice™'. | Widget PooDooLogo — altura mínima 40 px.  |

Solo uno de los modos `Even` u `Odd` puede estar activo a la vez. Seleccionar uno deselecciona el otro.

## Controles de perilla

El excitador PUDU proporciona seis perillas organizadas en dos grupos:

### Grupo Body (procesador de baja frecuencia)

| Control     | Valor predeterminado | Rango           | Clave de ajuste             | Comportamiento                                                           |
|-------------|----------------------|-----------------|------------------------------|--------------------------------------------------------------------------|
| Drive       | 6,0 dB               | 0,0 a 24,0 dB   | `ClientPuduTxPooDriveDb`     | Mapeo lineal. Exige más al saturador/compresor de baja frecuencia.      |
| Tune        | 100 Hz               | 50 a 160 Hz     | `ClientPuduTxPooTuneHz`      | Mapeo lineal. Centra la banda de enfoque de baja frecuencia.             |
| Mix         | 30 %                 | 0,0 a 100,0 %   | `ClientPuduTxPooMix`         | Mapeo lineal. Mezcla la banda baja realzada con la señal seca.          |

### Grupo Clarity (procesador de alta frecuencia)

| Control     | Valor predeterminado | Rango             | Clave de ajuste                | Comportamiento                                                                         |
|-------------|----------------------|-------------------|--------------------------------|----------------------------------------------------------------------------------------|
| Tune        | 5000 Hz              | 1000 a 10000 Hz   | `ClientPuduTxDooTuneHz`        | Mapeo logarítmico. Centra la banda de excitación de alta frecuencia.                   |
| Air         | 6,0 dB               | 0,0 a 24,0 dB     | `ClientPuduTxDooHarmonicsDb`   | Mapeo lineal. Cantidad de armónicos / 'aire' añadido en la banda alta.                 |
| Mix         | 30 %                 | 0,0 a 100,0 %     | `ClientPuduTxDooMix`           | Mapeo lineal. Mezcla los agudos excitados con la señal seca.                          |

## Edición de valor en línea

Cada perilla admite entrada numérica directa:

1. Haga clic en el texto del valor que se muestra debajo de la perilla. Aparece un pequeño editor de texto con un borde cian.
2. Escriba un nuevo valor. Puede incluir unidades o caracteres adicionales — el editor elimina automáticamente el contenido no numérico.
3. Pulse `Enter` o haga clic en otro lugar para aplicar el valor. El valor se limita al rango válido de la perilla.
4. Pulse `Escape` para cancelar la edición y volver al valor anterior.

El editor en línea está siempre disponible y utiliza el mismo formato de visualización que la etiqueta de la perilla (por ejemplo, "6,0 dB", "100 Hz", "30 %").

## Etiquetas de grupo

La etiqueta del grupo "Body" agrupa las tres perillas de baja frecuencia (Drive, Tune, Mix). La etiqueta del grupo "Clarity" agrupa las tres perillas de alta frecuencia (Tune, Air, Mix).

## Consejos

- El modo Par es adecuado para señales de voz donde se busca calidez y cuerpo en las bajas frecuencias. El modo Impar es adecuado para situaciones donde se prefiere una mayor presencia y brillantez.
- El logotipo AetherVoice pulsa con el RMS de la señal procesada (húmeda), por lo que puede ver la reacción del excitador al cambiar de modo sin necesidad de monitorizar el audio.
- Cuando la etapa PUDU está puenteada, todo el mosaico del applet se atenúa aproximadamente al 55 % de opacidad, coincidiendo con el efecto de atenuación aplicado a la curva EQ. Esto es solo un indicador visual y no afecta a su configuración.
- Las seis perillas de Body y Clarity permanecen activas independientemente del modo seleccionado; su efecto en la señal cambia de carácter según el modo elegido.
- Los componentes de la perilla (anillo de fondo, arco, indicador de la manija) ahora utilizan los colores del tema del espacio de nombres `color.knob.*`. Los grupos Body y Clarity leen los colores del texto de `color.text.*`. Las anulaciones por contenedor de applet (por ejemplo, el color ámbar PooDoo en el botón Even) son compatibles a través del sistema de contenedores de temas (`applet/pudu`).

## Relacionados

- [Descripción general de Aetherial TX Voice Processor / Aetherial RX Poodoo](overview.md)
- [Ajuste de Poo Drive para grosor de baja frecuencia](dial-poo-drive-for-lf-thickness.md)
- [Añada aire con Doo Air](add-air-with-doo-harmonics.md)
- [Puenteo de PUDU desde cualquier cadena](bypass-pudu-from-either-chain.md)
