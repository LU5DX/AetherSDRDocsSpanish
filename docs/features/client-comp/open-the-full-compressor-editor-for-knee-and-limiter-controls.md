# Abrir el editor completo del compresor para los controles de rodilla y limitador

El applet COMPRESSOR expone cinco mandos para ajustes cotidianos. Dos controles — el ancho de la rodilla suave (`ClientCompTxKneeDb`) y el limitador de salida (`ClientCompTxLimEnabled`, `ClientCompTxLimCeilingDb`) — solo están disponibles en el editor flotante del compresor. Abra el editor cuando necesite dar forma a la curva de compresión en el umbral o agregar un techo fijo a su señal de TX.

## Antes de comenzar

- La etapa Compressor debe estar presente en la cadena PooDoo Audio (TXDSP). Si aún no la ha agregado, consulte [Omitir el compresor de la cadena](bypass-the-compressor-from-the-chain.md).
- El subcontenedor COMPRESSOR debe estar visible en el panel de applets. Permanece oculto mientras la etapa Compressor está en modo bypass.

## Pasos

1. Localice el widget CHAIN dentro del contenedor PooDoo Audio (TXDSP).
2. Haga doble clic en la etapa **Comp** en el widget CHAIN. El editor flotante del compresor se abre.

Alternativamente:

1. Haga clic derecho en la barra de título del subcontenedor **COMPRESSOR**.
2. Seleccione la opción para abrir o hacer flotar el editor desde el menú contextual.

## Qué hace cada control

El editor flotante del compresor expone todos los parámetros del compresor, incluidos los dos que no están disponibles en el applet.

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Thresh | −18.0 dB | −60.0 a 0.0 dB | `ClientCompTxThresholdDb` |
| Ratio | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` |
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` |
| Makeup | 0.0 dB | −12.0 a 24.0 dB | `ClientCompTxMakeupDb` |
| Knee | — | — | `ClientCompTxKneeDb` |
| Limiter enabled | — | activado / desactivado | `ClientCompTxLimEnabled` |
| Limiter ceiling | — | — | `ClientCompTxLimCeilingDb` |

El widget de curva de transferencia en el editor es interactivo, a diferencia de la versión de solo visualización del applet. Los cambios en la rodilla, el umbral y la relación se reflejan en la curva de inmediato.

## Consejos

- Los cambios en los mandos y en la curva realizados en el editor flotante se reflejan en tiempo real en la curva de transferencia y la barra de reducción de ganancia del applet, de modo que puede observar las mediciones en el applet mientras edita los parámetros en la ventana flotante.
- Los cinco mandos del applet COMPRESSOR (Thresh, Ratio, Attack, Release, Makeup) se mantienen sincronizados con el editor. Ajustar cualquiera de las dos ubicaciones actualiza la otra.

## Relacionados

- [Descripción general del compresor](overview.md)
- [Ajustar el umbral del compresor](adjust-compressor-threshold.md)
- [Establecer la relación de compresión para voz](set-compression-ratio-for-voice.md)
- [Ajustar ataque y liberación para una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de compensación después de la compresión](apply-make-up-gain-after-compression.md)
- [Observar la reducción de ganancia en vivo mientras habla](watch-live-gain-reduction-while-speaking.md)
- [Omitir el compresor de la cadena](bypass-the-compressor-from-the-chain.md)
