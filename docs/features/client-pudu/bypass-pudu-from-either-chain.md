# Omitir PUDU desde cualquier cadena

El widget CHAIN permite omitir la etapa PUDU en la cadena TX, en la cadena RX o en ambas, sin necesidad de abrir el editor PUDU. Utilice esta función cuando desee comparar el efecto (A/B) o retirarlo temporalmente de la ruta de señal.

## Antes de comenzar

- AetherSDR debe estar en ejecución con el contenedor principal Aetherial Audio (TXDSP) visible en el panel de applets.
- La etapa PUDU debe estar ya presente en la cadena correspondiente (TX o RX).

## Pasos

1. Localice el widget CHAIN en el panel de applets correspondiente al lado que desea omitir: TX o RX.
2. Haga clic una vez en el bloque de etapa PUDU dentro del widget CHAIN para activar o desactivar el bypass en ese lado.
   - Una etapa omitida aparece visualmente inactiva; el audio pasa sin procesamiento.
   - Haga clic en el mismo bloque nuevamente para reactivar PUDU.
3. Repita el procedimiento en el widget CHAIN de la otra cadena si desea omitir tanto TX como RX de forma independiente.

El estado de bypass se conserva: `ClientPuduTxEnabled` para la cadena TX y `ClientPuduRxEnabled` para la cadena RX.

## Consejos

- Un clic simple en el widget CHAIN omite la etapa. Un doble clic abre el editor PUDU sin marco ("Aetherial Poodoo™ — TX" o "— RX") sin modificar el estado de bypass.
- El logotipo de PooDoo dentro del editor pulsa con el RMS de la señal procesada (wet) únicamente cuando la etapa está habilitada. Si el logotipo permanece estático, la etapa está omitida.
- Los estados de bypass de TX y RX son completamente independientes. Es posible omitir el PUDU de TX mientras el PUDU de RX permanece activo.

## Relacionados

- [Descripción general de Aetherial TX Poodoo / Aetherial RX Poodoo](overview.md)
- [Seleccionar el carácter Aphex (par) o Behringer (impar)](pick-aphex-even-vs-behringer-odd-character.md)
- [Ajustar Poo Drive para espesor en bajas frecuencias](dial-poo-drive-for-lf-thickness.md)
