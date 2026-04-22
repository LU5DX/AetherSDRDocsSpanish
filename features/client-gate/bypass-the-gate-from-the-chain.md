# Omitir la Puerta de la Cadena

Esta página explica cómo omitir la puerta de ruido TX sin eliminar su configuración. Use la omisión cuando desee deshabilitar temporalmente la puerta — por ejemplo, para comparar el audio procesado con el no procesado — manteniendo intactos todos los parámetros ajustados.

## Antes de comenzar

- La etapa Gate debe estar habilitada en el widget CHAIN antes de poder omitirla. Si el subcontenedor GATE no es visible en el contenedor principal PooDoo Audio (TXDSP), la puerta aún no ha sido añadida a la cadena.
- No se requiere una conexión de radio para omitir la puerta; la configuración es local en AetherSDR.

## Pasos

1. Localice el widget **CHAIN** dentro del contenedor principal PooDoo Audio (TXDSP) en el panel de applets.
2. Haga clic una vez en la etapa **Gate** en el widget CHAIN para activar o desactivar la omisión.
   - Cuando está omitida, la puerta no aplica ninguna atenuación y la curva de transferencia y la barra de reducción de ganancia en el subcontenedor GATE reflejan el estado inactivo.
   - Hacer clic de nuevo una vez reactiva la puerta; los valores de Thresh, Ratio, Attack, Release y Floor establecidos anteriormente se restauran de inmediato.

El estado de omisión se persiste en `ClientGateTxEnabled`. Todos los demás parámetros de la puerta (`ClientGateTxThresholdDb`, `ClientGateTxRatio`, `ClientGateTxAttackMs`, `ClientGateTxReleaseMs`, `ClientGateTxFloorDb`) no se ven afectados por la omisión.

## Consejos

- Para abrir el editor flotante de Gate en lugar de alternar la omisión, haga doble clic en la etapa Gate en el widget CHAIN.
- La barra de reducción de ganancia en el tile GATE se oscurece (sin relleno ámbar) mientras la puerta está omitida, lo que permite confirmar fácilmente a simple vista que la omisión está activa.

## Relacionados

- [Descripción general de la puerta de ruido / expansor](overview.md)
- [Ver la reducción de ganancia en tiempo real sin hablar](watch-live-gr-while-not-speaking.md)
- [Establecer el umbral justo por encima del piso de ruido ambiental](set-threshold-just-above-room-noise-floor.md)
