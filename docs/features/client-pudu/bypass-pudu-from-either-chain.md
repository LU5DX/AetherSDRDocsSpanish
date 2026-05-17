# Bypass PUDU desde cualquiera de las cadenas

El widget CHAIN le permite omitir la etapa PUDU en la cadena TX, la cadena RX o ambas, sin abrir el editor PUDU. Úselo cuando desee comparar el efecto A/B o eliminarlo temporalmente de la ruta de la señal.

## Antes de comenzar

- AetherSDR debe estar ejecutándose con el contenedor principal Aetherial Audio (TXDSP) visible en el panel de applets.
- La etapa PUDU ya debe estar presente en la cadena correspondiente (TX o RX).

## Pasos

1. Localice el widget CHAIN en el panel de applets para el lado que desea omitir: TX o RX.
2. Haga un solo clic en el bloque de la etapa PUDU en el widget CHAIN para activar o desactivar la omisión en ese lado.
   - Una etapa omitida se muestra visualmente inactiva; el audio pasa sin procesar.
   - Haga clic nuevamente en el mismo bloque para volver a activar PUDU.
3. Repita el procedimiento en el widget CHAIN de la otra cadena si desea omitir tanto TX como RX de forma independiente.

El estado de omisión se conserva: `ClientPuduTxEnabled` para la cadena TX y `ClientPuduRxEnabled` para la cadena RX.

## Consejos

- Un solo clic en el widget CHAIN omite la etapa. Un doble clic abre el editor PUDU sin marco ("Aetherial Voice Processor — TX" o "Aetherial RX Poodoo — RX") sin cambiar el estado de omisión.
- Cuando la etapa está omitida, todo el mosaico PUDU se atenúa a una opacidad reducida (aproximadamente 55 %), coincidiendo con el efecto de atenuación utilizado en la visualización de la curva EQ. Esta señal visual es consistente tanto si omite desde el widget CHAIN como si lo hace desde el editor.
- El logotipo de PooDoo dentro del editor pulsa con el RMS de la señal procesada solo cuando la etapa está activada. Si el logotipo está estático, la etapa está omitida.
- Los estados de omisión de TX y RX son completamente independientes. Puede omitir el PUDU de TX mientras deja activo el PUDU de RX.

## Abrir el editor PUDU

El editor PUDU se puede abrir por separado para las cadenas TX y RX. Cada uno abre una ventana flotante sin marco con su propio estado independiente.

1. En el widget CHAIN para la cadena TX o RX, haga doble clic en el bloque de la etapa PUDU.
   - El editor TX se abre con el título de ventana "Aetherial Poodoo — TX".
   - El editor RX se abre con el título de ventana "Aetherial Poodoo — RX".
2. El editor muestra seis perillas en dos grupos, un selector de modo (Even/Odd) y el logotipo de AetherVoice.
3. Use el botón Cerrar en la parte superior de la ventana del editor para descartarlo.

## Grupos de perillas

El editor PUDU organiza sus seis perillas bajo dos etiquetas de grupo.

| Grupo            | Perillas                                                                                     | Rango de frecuencia                |
|------------------|----------------------------------------------------------------------------------------------|-------------------------------------|
| **Body**         | Drive, Tune, Mix                                                                             | 50 – 160 Hz                         |
| **Clarity**      | Tune, Air, Mix                                                                               | 1000 – 10000 Hz                     |
| Logotipo AetherVoice | Logotipo animado de marca que pulsa con el RMS de la señal procesada. Muestra la marca 'AetherVoice™'. | Widget PooDooLogo — altura mínima 40 px. |

## Controles de perilla

Cada perilla admite edición de valor en línea. Haga clic en el texto del valor de una perilla (el número debajo del arco de la perilla) para activar un campo de entrada de texto. Escriba un nuevo valor y presione Enter o haga clic en cualquier otro lugar para confirmar. El valor se limita al rango válido de la perilla. Presione Escape para cancelar la edición y revertir al valor anterior.

| Control               | Valor predeterminado | Rango         | Clave de ajuste            | Comportamiento                                                              |
|-----------------------|----------------------|---------------|----------------------------|-----------------------------------------------------------------------------|
| Even                  | —                    | —             | `ClientPuduTxMode`         | Selecciona el modelado asimétrico de la herencia Aphex (armónicos pares). Ámbar cuando está marcado. Exclusivo con Odd. |
| Odd                   | —                    | —             | `ClientPuduTxMode`         | Selecciona el modelado tanh simétrico de la herencia Behringer (armónicos impares). Exclusivo con Even. |
| Body / Drive          | 6.0 dB               | 0.0 – 24.0 dB | `ClientPuduTxPooDriveDb`  | Excita más el saturador/compresor de baja frecuencia.                       |
| Body / Tune           | 100 Hz               | 50 – 160 Hz   | `ClientPuduTxPooTuneHz`   | Centra la banda de enfoque de baja frecuencia.                              |
| Body / Mix            | 30 %                 | 0.0 – 1.0     | `ClientPuduTxPooMix`      | Mezcla la banda baja mejorada con la señal seca.                            |
| Clarity / Tune        | 5000 Hz              | 1000 – 10000 Hz | `ClientPuduTxDooTuneHz`  | Centra la banda de excitación de alta frecuencia. Mapeo logarítmico.        |
| Clarity / Air         | 6.0 dB               | 0.0 – 24.0 dB | `ClientPuduTxDooHarmonicsDb` | Cantidad de armónicos/'aire' en la banda alta.                           |
| Clarity / Mix         | 30 %                 | 0.0 – 1.0     | `ClientPuduTxDooMix`      | Mezcla los agudos excitados con la señal seca.                              |

## Selección de modo

- **Even**: Color PooDoo ámbar cuando está marcado. Modelado asimétrico de la herencia Aphex — predominantemente armónicos pares, más cálido, con saturación LF Big Bottom.
- **Odd**: Modelado tanh simétrico de la herencia Behringer — armónicos impares puros, más brillante, con un compresor de graves feed-forward.

Los dos botones de opción son mutuamente excluyentes.

## Edición de valor en línea

Cada perilla en el editor admite entrada numérica directa:

1. Haga clic en el texto del valor debajo de cualquier perilla. Aparece un campo de entrada de texto con el valor actual.
2. Escriba el valor deseado. Puede incluir unidades (dB, Hz, %), pero se ignoran. Se aceptan separadores decimales según la configuración regional (coma o punto).
3. Presione Enter o haga clic en cualquier otro lugar para confirmar el valor. La perilla se actualiza inmediatamente.
4. Presione Escape para cancelar la edición. La perilla vuelve a su valor anterior.

El campo del editor muestra un borde cian sutil y un fondo oscuro mientras está activo, y es transparente (coincidiendo con la apariencia normal de la etiqueta) cuando no tiene el foco.

## Relacionados

- [Descripción general del Aetherial TX Voice Processor / Aetherial RX Poodoo](overview.md)
- [Seleccionar el carácter Aphex (Even) vs Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- [Ajustar Body Drive para espesor LF](dial-poo-drive-for-lf-thickness.md)
