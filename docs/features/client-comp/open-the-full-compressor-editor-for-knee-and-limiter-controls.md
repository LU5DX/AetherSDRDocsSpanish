# Abrir el editor completo del compresor para los controles de knee y limitador

El applet COMPRESSOR expone cinco perillas para ajustes habituales, pero los controles de knee (`ClientCompTxKneeDb`) y limitador (`ClientCompTxLimEnabled`, `ClientCompTxLimCeilingDb`) solo están disponibles en el editor flotante del compresor. Abra el editor cuando necesite dar forma a la zona de transición o agregar un techo fijo al audio de TX.

## Antes de comenzar

- El subcontenedor COMPRESSOR debe estar visible dentro del contenedor principal PooDoo Audio (TXDSP).
- La etapa del compresor debe estar habilitada (bypass desactivado) mediante el widget CHAIN; el panel COMPRESSOR permanece oculto mientras está en bypass.

## Pasos

1. Localice el widget CHAIN dentro del contenedor PooDoo Audio (TXDSP).
2. Haga doble clic en la etapa **Comp** del widget CHAIN. El editor flotante del compresor se abre.

Alternativamente:

2. Haga clic derecho en la barra de título del subcontenedor **COMPRESSOR** y elija la opción de flotar o desprender del menú contextual. Esto muestra el editor completo en una ventana separada.

## Qué hace cada control

El editor flotante agrega los siguientes controles que no están presentes en el applet:

| Control | Predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|
| Knee | — | — | `ClientCompTxKneeDb` |
| Habilitación del limitador | — | On / Off | `ClientCompTxLimEnabled` |
| Techo del limitador | — | — | `ClientCompTxLimCeilingDb` |

El editor también replica las cinco perillas disponibles en el applet:

| Control | Predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|
| Thresh | −18.0 dB | −60.0 a 0.0 dB | `ClientCompTxThresholdDb` |
| Ratio | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` |
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` |
| Makeup | 0.0 dB | −12.0 a 24.0 dB | `ClientCompTxMakeupDb` |

Los cambios realizados en el editor y en las perillas del applet se mantienen sincronizados.

## Consejos

- La curva de transferencia en el applet es de solo lectura. El editor flotante proporciona la versión interactiva de la misma curva, donde los ajustes de knee se reflejan visualmente en tiempo real.
- Un solo clic en el widget CHAIN pone el compresor en bypass; el doble clic abre el editor. No haga un solo clic cuando su intención sea abrir el editor.

## Relacionados

- [Descripción general del compresor](overview.md)
- [Poner el compresor en bypass desde la cadena](bypass-the-compressor-from-the-chain.md)
- [Ajustar el umbral del compresor](adjust-compressor-threshold.md)
- [Establecer la relación de compresión para voz](set-compression-ratio-for-voice.md)
- [Ajustar ataque y release para una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de compensación tras la compresión](apply-make-up-gain-after-compression.md)
- [Monitorear la reducción de ganancia en tiempo real mientras habla](watch-live-gain-reduction-while-speaking.md)
