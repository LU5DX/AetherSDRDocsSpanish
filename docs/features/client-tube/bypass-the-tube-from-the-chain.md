# Omitir el tubo de la cadena

Cuando desee escuchar su señal de TX sin la saturación del tubo — para comparación o diagnóstico — puede omitir la etapa Tube sin modificar ninguno de sus ajustes. Al omitirla, todas las posiciones de los controles se conservan, de modo que puede reactivar la etapa exactamente como la dejó.

## Antes de comenzar

- La cadena de procesamiento TXDSP (PooDoo Audio) debe estar visible en el panel de applets.
- La etapa Tube debe estar ya presente en el widget CHAIN. Si no se encuentra en la cadena, no hay nada que omitir.

## Pasos

1. Localice el widget CHAIN dentro del contenedor PooDoo Audio (TXDSP) en el panel de applets.
2. Haga clic una vez en la etapa Tube en el widget CHAIN para alternar su estado de omisión.

   - Cuando está omitida, la etapa se elimina de la ruta de señal activa. El subcontenedor TUBE, si está visible, continúa mostrando la curva de transferencia y las posiciones de los controles, pero el modelo de tubo no se aplica a la señal de TX.
   - Haga clic de nuevo para reactivar la etapa.

El estado de omisión se conserva en `ClientTubeTxEnabled`.

## Consejos

- Para abrir el editor flotante Tube sin alternar la omisión, haga doble clic en la etapa Tube en el widget CHAIN en lugar de un solo clic.
- La curva de transferencia y el indicador de entrada en tiempo real en el subcontenedor TUBE continúan actualizándose visualmente independientemente del estado de omisión. Observe la curva para confirmar los ajustes de Drive, Bias y Tone antes de reactivar la etapa.
- Si prefiere una mezcla parcial en lugar de una omisión total, reduzca el control Mix hacia 0 % en su lugar. Esto mantiene la etapa activa pero desvanece la señal hacia el camino seco (dry). Consulte [Saturación con mezcla en paralelo mediante Mix](parallel-blend-saturation-with-mix.md).

## Relacionados

- [Descripción general del saturador Tube](overview.md)
- [Saturación con mezcla en paralelo mediante Mix](parallel-blend-saturation-with-mix.md)
- [Ajuste de Drive hasta que la curva comience a curvarse](dial-drive-until-the-curve-starts-to-bend.md)
