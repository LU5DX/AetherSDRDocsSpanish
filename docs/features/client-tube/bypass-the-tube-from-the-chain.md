# Omitir el módulo de la cadena

Cuando desee escuchar su señal de TX sin saturación del módulo, para comparación o solución de problemas, puede omitir la etapa Tube sin cambiar ninguna de sus configuraciones. Omitirla deja todas las posiciones de las perillas intactas para que pueda volver a habilitar la etapa exactamente como la dejó.

## Antes de comenzar

- La cadena de procesamiento TXDSP (PooDoo Audio) debe estar visible en el panel de applets.
- La etapa Tube ya debe estar presente en el widget CHAIN. Si no está en la cadena, no hay nada que omitir.

## Pasos

1. Localice el widget CHAIN dentro del contenedor PooDoo Audio (TXDSP) en el panel de applets.
2. Haga un solo clic en la etapa Tube en el widget CHAIN para alternar su estado de omisión.

   - Cuando está omitida, la etapa se elimina de la ruta de señal activa. El subcontenedor TUBE, si está visible, sigue mostrando la curva de transferencia y las posiciones de las perillas, pero el modelo del módulo no se aplica a la señal de TX.
   - Haga un solo clic nuevamente para volver a habilitar la etapa.

El estado de omisión se conserva en `ClientTubeTxEnabled`.

## Consejos

- Para abrir el editor flotante de Tube sin alternar la omisión, haga doble clic en la etapa Tube en el widget CHAIN en lugar de un solo clic.
- La curva de transferencia y la bola de entrada en vivo en el subcontenedor TUBE continúan actualizándose visualmente independientemente del estado de omisión. Observe la curva para confirmar sus ajustes de Drive, Bias y Tone antes de volver a activar la etapa.
- Si desea una mezcla parcial en lugar de una omisión completa, reduzca la perilla Mix hacia 0 %. Esto mantiene la etapa activa pero se desvanece hacia la señal seca. Consulte [Saturación en mezcla paralela con Mix](parallel-blend-saturation-with-mix.md).

## Relacionados

- [Descripción general del saturador Tube](overview.md)
- [Saturación en mezcla paralela con Mix](parallel-blend-saturation-with-mix.md)
- [Ajuste Drive hasta que la curva comience a doblarse](dial-drive-until-the-curve-starts-to-bend.md)
