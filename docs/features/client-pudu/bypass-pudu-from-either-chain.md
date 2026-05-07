# Omitir PUDU desde cualquiera de las cadenas

El widget CHAIN le permite omitir la etapa PUDU en la cadena de TX, la cadena de RX, o ambas, sin abrir el editor de PUDU. Úselo cuando desee comparar el efecto A/B o eliminarlo temporalmente de la ruta de la señal.

## Antes de comenzar

- AetherSDR debe estar ejecutándose con el contenedor principal Aetherial Audio (TXDSP) visible en el panel de applets.
- La etapa PUDU ya debe estar presente en la cadena correspondiente (TX o RX).

## Pasos

1. Localice el widget CHAIN en el panel de applets del lado que desea omitir: TX o RX.
2. Haga un solo clic en el bloque de la etapa PUDU en el widget CHAIN para activar la omisión en ese lado.
   - Una etapa omitida se muestra visualmente inactiva; el audio pasa sin procesar.
   - Haga clic en el mismo bloque nuevamente para volver a activar PUDU.
3. Repita en el widget CHAIN de la otra cadena si desea omitir TX y RX de forma independiente.

El estado de omisión se conserva: `ClientPuduTxEnabled` para la cadena TX y `ClientPuduRxEnabled` para la cadena RX.

## Consejos

- Un solo clic en el widget CHAIN omite la etapa. Un doble clic abre el editor PUDU sin marco ("Aetherial Voice Processor — TX" o "Aetherial Voice Processor — RX") sin cambiar el estado de omisión.
- Cuando la etapa está omitida, todo el mosaico PUDU se atenúa con una opacidad reducida (aproximadamente 55 %), igual que el efecto de atenuación usado en la visualización de la curva EQ. Esta señal visual es coherente tanto si omite desde el widget CHAIN como desde el editor.
- El logotipo de PooDoo dentro del editor pulsa con el RMS de la señal húmeda solo cuando la etapa está activada. Si el logotipo está estático, la etapa está omitida.
- Los estados de omisión de TX y RX son completamente independientes. Puede omitir PUDU de TX mientras deja activo PUDU de RX.

## Abrir el editor de PUDU

El editor de PUDU se puede abrir por separado para las cadenas TX y RX. Cada uno abre una ventana flotante sin marco con su propio estado independiente.

1. En el widget CHAIN de la cadena TX o RX, haga doble clic en el bloque de la etapa PUDU.
   - El editor TX se abre con el título de ventana "Aetherial Voice Processor — TX".
   - El editor RX se abre con el título de ventana "Aetherial Voice Processor — RX".
2. El editor muestra seis perillas en dos grupos, un selector de modo (Even/Odd) y el logotipo de PooDoo.
3. Use el botón Cerrar en la parte superior de la ventana del editor para descartarla.

## Grupos de perillas

El editor de PUDU organiza sus seis perillas bajo dos etiquetas de corchete.

| Corchete | Perillas | Rango de frecuencia | Propósito |
|----------|----------|---------------------|-----------|
| **Body** | Drive, Tune, Mix | 50 – 160 Hz | Saturator/compresor de baja frecuencia |
| **Clarity** | Tune, Air, Mix | 1000 – 10 000 Hz | Excitación de alta frecuencia y armónicos |

En versiones anteriores, estos grupos se etiquetaban como **Poo** y **Doo** respectivamente. Cualquier referencia a esos nombres en otras partes del manual se refiere a los mismos controles ahora etiquetados como **Body** y **Clarity**.

## Relacionados

- [Resumen de Aetherial TX Poodoo / Aetherial RX Poodoo](overview.md)
- [Seleccionar carácter Aphex (Even) vs Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- [Ajustar Body Drive para grosor de baja frecuencia](dial-poo-drive-for-lf-thickness.md)
