# Omitir el tubo de la cadena

Cuando desea escuchar su señal de TX sin la saturación del tubo — para comparación o diagnóstico — puede omitir la etapa Tube sin cambiar ninguna de sus configuraciones. Al omitirla, todas las posiciones de los controles permanecen intactas para que pueda reactivar la etapa exactamente como la dejó.

## Antes de comenzar

- La cadena de procesamiento TXDSP (PooDoo Audio) debe estar visible en el panel de applets.
- La etapa Tube ya debe estar presente en el widget CHAIN. Si no está en la cadena, no hay nada que omitir.

## Pasos

1. Ubique el widget CHAIN dentro del contenedor PooDoo Audio (TXDSP) en el panel de applets.
2. Haga clic una vez sobre la etapa Tube en el widget CHAIN para alternar su estado de omisión.

   - Cuando está omitida, la etapa queda fuera de la ruta de señal activa. El subcontenedor TUBE, si está visible, continúa mostrando la curva de transferencia y las posiciones de los controles, pero el modelo de tubo no se aplica a la señal de TX.
   - Haga clic una vez más para reactivar la etapa.

El estado de omisión se guarda en `ClientTubeTxEnabled`.

## Consejos

- Para abrir el editor flotante de Tube sin alternar la omisión, haga doble clic sobre la etapa Tube en el widget CHAIN en lugar de un solo clic.
- La curva de transferencia y la bola de entrada en tiempo real en el subcontenedor TUBE continúan actualizándose visualmente independientemente del estado de omisión. Observe la curva para confirmar sus ajustes de Drive, Bias y Tone antes de reactivar la etapa.
- Si desea una mezcla parcial en lugar de una omisión total, reduzca el control Mix hacia 0 % en su lugar. Esto mantiene la etapa activa pero atenúa hacia la señal seca. Consulte [Saturación con mezcla paralela mediante Mix](parallel-blend-saturation-with-mix.md).

## Temas relacionados

- [Descripción general del Saturador de tubo](overview.md)
- [Saturación con mezcla paralela mediante Mix](parallel-blend-saturation-with-mix.md)
- [Ajuste el Drive hasta que la curva comience a curvarse](dial-drive-until-the-curve-starts-to-bend.md)
