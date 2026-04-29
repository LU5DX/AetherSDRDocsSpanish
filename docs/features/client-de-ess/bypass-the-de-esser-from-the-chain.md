# Omitir el de-esser de la cadena

Elimine el Aetherial De-Esser de su ruta de audio TX sin modificar ninguno de sus ajustes. Omitirlo es útil cuando desea comparar el audio procesado con el sin procesar, o cuando necesita desactivar temporalmente el de-essing para una sesión determinada.

## Antes de comenzar

- AetherSDR debe estar abierto y la cadena de procesamiento Aetherial Audio (TXDSP) debe estar visible.
- La etapa DESS debe existir ya en el widget CHAIN. Si el de-esser nunca ha sido habilitado, es posible que la etapa DESS no esté presente — consulte [Descripción general del Aetherial De-Esser](overview.md).

## Pasos

1. Localice el widget CHAIN en el contenedor Aetherial Audio (TXDSP).
2. Encuentre la etapa **DESS** en la cadena.
3. Haga clic una vez en la etapa **DESS** para activar o desactivar el bypass.

Cuando está omitida, la etapa se marca visualmente como inactiva y el de-esser queda fuera de la ruta de audio TX. Un clic adicional la reactiva. El ajuste `ClientDeEssTxEnabled` se actualiza de inmediato.

## Consejos

- Omitir la etapa no restablece los valores de los controles. Freq, Q, Thresh y Amount conservan sus ajustes actuales al reactivar la etapa.
- Para abrir el editor completo y realizar ajustes detallados, haga doble clic en la etapa **DESS** en lugar de un solo clic.

## Relacionados

- [Descripción general del Aetherial De-Esser](overview.md)
- [Barrer Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Establecer el umbral justo por debajo de los picos más fuertes de 'S'](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
