# Omitir el Gate de la Cadena

Omitir el gate lo elimina de la cadena de procesamiento de audio TX sin modificar ninguna de sus configuraciones. Use esta función cuando desee deshabilitar temporalmente el noise gate — por ejemplo, durante un check-in de red — y restaurarlo más adelante con la misma configuración.

## Antes de comenzar

- La etapa GATE ya debe estar presente en el widget CHAIN dentro del contenedor PooDoo Audio (TXDSP).
- El applet del subcontenedor GATE solo es visible cuando la etapa Gate está habilitada en el widget CHAIN; el bypass se realiza desde el propio widget CHAIN.

## Pasos

1. Localice el widget CHAIN dentro del contenedor PooDoo Audio (TXDSP) en el panel de applets.
2. Haga clic una vez en el bloque de la etapa Gate en el widget CHAIN para alternar su estado de bypass.

La etapa Gate está en bypass cuando el bloque aparece inactivo en el widget CHAIN. El subcontenedor GATE permanece visible, pero el gate no aplica ninguna atenuación — la barra de reducción de ganancia mostrará 0 dB y la bola de la curva de transferencia seguirá el nivel de entrada sin activar ninguna reducción de ganancia.

3. Para volver a habilitar el gate, haga clic una vez más en el bloque de la etapa Gate.

El estado de bypass se guarda en `ClientGateTxEnabled`. Todos los valores de los controles (`ClientGateTxThresholdDb`, `ClientGateTxRatio`, `ClientGateTxAttackMs`, `ClientGateTxReleaseMs`, `ClientGateTxFloorDb`) permanecen sin cambios al activar el bypass.

## Consejos

- Activar el bypass desde el widget CHAIN es no destructivo. Los cinco controles de ajuste (Thresh, Ratio, Attack, Release, Floor) conservan sus valores y surten efecto de inmediato al volver a habilitar la etapa.
- Para abrir el editor flotante del Gate y realizar ajustes detallados sin activar el bypass, haga doble clic en la etapa Gate en el widget CHAIN.

## Relacionados

- [Descripción general del Noise Gate / Expansor](overview.md)
- [Ajustar el umbral justo por encima del nivel de ruido ambiental](set-threshold-just-above-room-noise-floor.md)
- [Ver la reducción de ganancia en tiempo real sin hablar](watch-live-gr-while-not-speaking.md)
