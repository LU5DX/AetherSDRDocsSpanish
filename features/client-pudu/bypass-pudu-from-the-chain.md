# Omitir PUDU de la cadena

El excitador PUDU se activa y desactiva desde el widget CHAIN, no desde el interior del applet PUDU Exciter. Use esta página para quitar temporalmente PUDU de la cadena DSP de TX sin modificar ninguno de sus ajustes.

## Antes de comenzar

- El contenedor principal PooDoo Audio (TXDSP) debe ser visible en el panel de applets.
- La etapa PUDU (Enh) debe estar presente en el widget CHAIN.

## Pasos

1. Localice el widget CHAIN dentro del contenedor PooDoo Audio (TXDSP).
2. Encuentre el bloque de etapa **PUDU (Enh)** en la cadena.
3. Haga clic una vez en la etapa **PUDU (Enh)** para desactivarla. La etapa queda omitida y el audio pasa por la cadena sin el procesamiento de PUDU.
4. Haga clic una vez más en la etapa **PUDU (Enh)** para volver a activarla.

Cuando PUDU está omitido, el subcontenedor PUDU permanece oculto. El ajuste persistente `ClientPuduTxEnabled` se actualiza de inmediato. Todos los valores de los controles (`ClientPuduTxPooDriveDb`, `ClientPuduTxPooTuneHz`, `ClientPuduTxPooMix`, `ClientPuduTxDooTuneHz`, `ClientPuduTxDooHarmonicsDb`, `ClientPuduTxDooMix`) y el modo seleccionado (`ClientPuduTxMode`) se conservan.

## Consejos

- Omitir desde el widget CHAIN es una operación no destructiva. Al volver a activarlo, se restauran todas las posiciones de los controles exactamente como las dejó.
- Para abrir los controles de PUDU Exciter sin activar la etapa, haga doble clic en la etapa **PUDU (Enh)** en el widget CHAIN para abrir el editor flotante.

## Relacionado

- [Descripción general de PUDU Exciter](overview.md)
- [Elegir carácter Aphex (par) o Behringer (impar)](pick-aphex-even-vs-behringer-odd-character.md)
