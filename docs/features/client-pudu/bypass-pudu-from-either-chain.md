# Omitir PUDU desde cualquiera de las cadenas

El widget CHAIN permite omitir la etapa PUDU en la cadena TX, en la cadena RX o en ambas, sin necesidad de abrir el editor PUDU. Use esta función cuando desee comparar el efecto (A/B) o eliminarlo temporalmente de la ruta de la señal.

## Antes de comenzar

- AetherSDR debe estar en ejecución con el contenedor principal Aetherial Audio (TXDSP) visible en el panel de applets.
- La etapa PUDU ya debe estar presente en la cadena correspondiente (TX o RX).

## Pasos

1. Localice el widget CHAIN en el panel de applets correspondiente al lado que desea omitir: TX o RX.
2. Haga clic una sola vez en el bloque de la etapa PUDU dentro del widget CHAIN para activar o desactivar el bypass en ese lado.
   - Una etapa en bypass aparece visualmente inactiva; el audio pasa sin procesamiento.
   - Haga clic nuevamente en el mismo bloque para reactivar PUDU.
3. Repita el procedimiento en el widget CHAIN de la otra cadena si desea omitir TX y RX de forma independiente.

El estado del bypass se conserva: `ClientPuduTxEnabled` para la cadena TX y `ClientPuduRxEnabled` para la cadena RX.

## Sugerencias

- Un clic simple en el widget CHAIN omite la etapa. Un doble clic abre el editor PUDU sin bordes ("Aetherial Poodoo™ — TX" o "— RX") sin modificar el estado del bypass.
- El logotipo de PooDoo dentro del editor pulsa al ritmo del RMS de la señal húmeda únicamente cuando la etapa está habilitada. Si el logotipo permanece estático, la etapa está en bypass.
- Los estados de bypass de TX y RX son completamente independientes. Puede omitir el PUDU de TX mientras el PUDU de RX permanece activo.

## Temas relacionados

- [Descripción general de Aetherial TX Poodoo / Aetherial RX Poodoo](overview.md)
- [Elegir el carácter Aphex (par) o Behringer (impar)](pick-aphex-even-vs-behringer-odd-character.md)
- [Ajustar Poo Drive para mayor grosor en bajas frecuencias](dial-poo-drive-for-lf-thickness.md)
