# Excitador PUDU Aetherial

El widget CHAIN le permite omitir la etapa PUDU en la cadena TX, la cadena RX, o ambas, sin abrir el editor PUDU. Úselo cuando desee comparar el efecto A/B o eliminarlo temporalmente de la ruta de la señal.

## Antes de comenzar

- AetherSDR debe estar ejecutándose con el contenedor principal Aetherial Audio (TXDSP) visible en el panel de applets.
- La etapa PUDU ya debe estar presente en la cadena correspondiente (TX o RX).

## Pasos

1. Localice el widget CHAIN en el panel de applets para el lado que desea omitir: TX o RX.
2. Haga clic una vez en el bloque de la etapa PUDU en el widget CHAIN para activar o desactivar la omisión en ese lado.
   - Una etapa omitida se muestra visualmente inactiva; el audio pasa sin procesar.
   - Haga clic en el mismo bloque nuevamente para volver a activar PUDU.
3. Repita el proceso en el widget CHAIN de la otra cadena si desea omitir tanto TX como RX de forma independiente.

El estado de omisión se conserva: `ClientPuduTxEnabled` para la cadena TX y `ClientPuduRxEnabled` para la cadena RX.

## Consejos

- Un solo clic en el widget CHAIN omite la etapa. Un doble clic abre el editor PUDU sin marco ("Aetherial Voice Processor — TX" o "Aetherial RX Poodoo — RX") sin cambiar el estado de omisión.
- Cuando la etapa está omitida, todo el mosaico PUDU se atenúa con una opacidad reducida (aproximadamente 55 %), igual que el efecto de atenuación utilizado en la visualización de la curva EQ. Esta señal visual es consistente, ya sea que omita desde el widget CHAIN o desde el editor.
- El logotipo AetherVoice dentro del editor pulsa con el RMS de la señal procesada solo cuando la etapa está activada. Si el logotipo está estático, la etapa está omitida.
- Los estados de omisión de TX y RX son completamente independientes. Puede omitir el PUDU de TX mientras deja activo el PUDU de RX.

## Abrir el editor PUDU

El editor PUDU se puede abrir por separado para las cadenas TX y RX. Cada uno abre una ventana flotante sin marco con su propio estado independiente.

1. En el widget CHAIN de la cadena TX o RX, haga doble clic en el bloque de la etapa PUDU.
   - El editor TX se abre con el título de ventana "Aetherial Poodoo — TX".
   - El editor RX se abre con el título de ventana "Aetherial Poodoo — RX".
2. El editor muestra seis perillas en dos grupos, un selector de modo (Even/Odd) y el logotipo AetherVoice.
3. Use el botón Cerrar en la parte superior de la ventana del editor para descartarlo.

## Grupos de perillas

El editor PUDU organiza sus seis perillas bajo dos etiquetas de corchetes.

| Corchete        | Perillas                                                                                 | Rango de frecuencia                     |
|-----------------|------------------------------------------------------------------------------------------|-----------------------------------------|
| **Body**        | Drive, Tune, Mix                                                                         | 50 – 160 Hz                             |
| **Clarity**     | Tune, Air, Mix                                                                           | 1000 – 10000 Hz                         |
| Logotipo AetherVoice | Logotipo animado de marca que pulsa con el RMS de la señal procesada. Muestra la marca registrada 'AetherVoice™'. | Widget PooDooLogo — altura mínima de 40 px. |

## Controles de perillas

El editor etiqueta la primera perilla del grupo Body como "Poo / Drive", la etiqueta del grupo Clarity es "Clarity" (no "Doo"), y la etiqueta de la perilla Air es "Air". Las claves de configuración subyacentes permanecen sin cambios.

Cada perilla admite la edición de valor en línea. Haga clic en el texto del valor de una perilla (el número debajo del arco de la perilla) para activar un campo de entrada de texto. Escriba un nuevo valor y presione Enter o haga clic en cualquier otro lugar para confirmar. El valor se limita al rango válido de la perilla. Presione Escape para cancelar la edición y revertir al valor anterior.

| Control                | Valor predeterminado | Rango           | Clave de configuración    | Comportamiento                                                                                         |
|------------------------|----------------------|-----------------|----------------------------|--------------------------------------------------------------------------------------------------------|
| Even                   | —                    | —               | `ClientPuduTxMode`         | Selecciona el modelado asimétrico de la línea Aphex (armónicos pares). Ámbar cuando está marcado. Exclusivo con Odd. |
| Odd                    | —                    | —               | `ClientPuduTxMode`         | Selecciona el modelado tanh simétrico de la línea Behringer (armónicos impares). Exclusivo con Even.   |
| Body / Drive           | 6.0 dB               | 0.0 – 24.0 dB   | `ClientPuduTxPooDriveDb`  | Impulsa con más fuerza el saturación/compresor de baja frecuencia. Etiqueta "Poo / Drive".             |
| Body / Tune            | 100 Hz               | 50 – 160 Hz     | `ClientPuduTxPooTuneHz`   | Centra la banda de enfoque de baja frecuencia.                                                         |
| Body / Mix             | 30 %                 | 0.0 – 1.0       | `ClientPuduTxPooMix`      | Mezcla la banda baja realzada con la señal seca.                                                       |
| Clarity / Tune         | 5000 Hz              | 1000 – 10000 Hz | `ClientPuduTxDooTuneHz`  | Centra la banda de excitación de alta frecuencia. Mapeo logarítmico.                                   |
| Clarity / Air          | 6.0 dB               | 0.0 – 24.0 dB   | `ClientPuduTxDooHarmonicsDb` | Cantidad de armónicos/'aire' en la banda alta. Etiqueta "Air".                                      |
| Clarity / Mix          | 30 %                 | 0.0 – 1.0       | `ClientPuduTxDooMix`      | Mezcla las altas frecuencias excitadas con la señal seca.                                              |

## Selección de modo

- **Even**: Color PooDoo ámbar cuando está marcado. Modelado asimétrico de la línea Aphex: predominan los armónicos pares, más cálido, con saturación LF de Big Bottom.
- **Odd**: Modelado tanh simétrico de la línea Behringer: armónicos impares puros, más brillante, con un compresor de graves feed-forward.

Los dos botones de radio son mutuamente excluyentes.

## Integración de temas

Los colores de las perillas (anillo de fondo, arco de primer plano, indicador de puntero, texto de etiqueta, texto de valor) ahora se obtienen del espacio de nombres de tema `color.knob.*`, con el contenedor de applet PUDU `applet/pudu` proporcionando una anulación de color de perilla ámbar en primer plano. El color del texto de la etiqueta del corchete sigue `color.text.primary` del tema activo.

## Edición de valor en línea

Cada perilla en el editor admite la entrada numérica directa:

1. Haga clic en el texto del valor debajo de cualquier perilla. Aparece un campo de entrada de texto con el valor actual.
2. Escriba el valor deseado. Puede incluir unidades (dB, Hz, %), pero se ignoran. Se aceptan separadores decimales (coma o punto) según la configuración regional.
3. Presione Enter o haga clic en cualquier otro lugar para confirmar el valor. La perilla se actualiza inmediatamente.
4. Presione Escape para cancelar la edición. La perilla vuelve a su valor anterior.

El campo del editor muestra un borde cian sutil y un fondo oscuro mientras está activo, y es transparente (coincidiendo con la apariencia normal de la etiqueta) cuando no está enfocado.

## Relacionados

- [Descripción general del Aetherial TX Voice Processor / Aetherial RX Poodoo](overview.md)
- [Seleccionar el carácter Aphex (Even) vs Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- [Ajustar Body Drive para grosor LF](dial-poo-drive-for-lf-thickness.md)
