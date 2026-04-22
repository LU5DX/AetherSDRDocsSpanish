# Omitir el tubo de la cadena

Use esta página para retirar el Tube Saturator de la ruta de señal TX sin modificar ninguno de sus ajustes. Omitirlo le permite comparar su señal con y sin saturación, o simplemente deshabilitar la etapa cuando no sea necesaria.

## Antes de comenzar

- La etapa Tube Saturator debe estar ya presente en el widget CHAIN dentro del contenedor PooDoo Audio (TXDSP).
- El subcontenedor TUBE debe ser visible, o bien debe tener acceso al widget CHAIN.

## Pasos

1. Localice la etapa Tube en el widget CHAIN dentro del contenedor PooDoo Audio (TXDSP).
2. Haga clic una vez sobre la etapa Tube en el widget CHAIN para activar o desactivar el bypass.

Cuando la etapa está en bypass, la curva de transferencia del tubo y los mandos del subcontenedor TUBE permanecen en sus últimos valores. El ajuste `ClientTubeTxEnabled` se actualiza y se guarda automáticamente.

## Consejos

- Para reactivar el tubo, haga clic una vez más sobre la etapa Tube en el widget CHAIN.
- Usar el bypass desde el widget CHAIN no restablece Drive, Tone, Bias, Output ni Mix — todos los valores se conservan para cuando vuelva a habilitar la etapa.
- Para abrir el editor flotante completo en lugar de activar el bypass, haga doble clic sobre la etapa Tube en el widget CHAIN.

## Relacionado

- [Descripción general del Tube Saturator](overview.md)
- [Ajuste Drive hasta que la curva comience a curvarse](dial-drive-until-the-curve-starts-to-bend.md)
- [Saturación con mezcla en paralelo usando Mix](parallel-blend-saturation-with-mix.md)
