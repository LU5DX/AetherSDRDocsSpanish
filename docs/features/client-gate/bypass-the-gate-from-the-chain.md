# Omitir el Gate de la cadena

El widget CHAIN controla si la etapa Gate está activa en la cadena de procesamiento de audio. Omitirla le permite deshabilitar el gate de TX o RX por completo sin modificar ninguno de sus controles de ajuste, para que pueda comparar el audio con y sin gate, o silenciar la etapa temporalmente.

## Antes de comenzar

- Abra el contenedor principal Aetherial Audio (TXDSP) en el Applet Panel. Los subcontenedores "Aetherial TX Gate" (TX) y "Aetherial AGC-T" (RX) permanecen ocultos hasta que la etapa Gate se habilite mediante el widget CHAIN.
- Identifique qué lado desea omitir: TX (afecta el audio transmitido) o RX (afecta el audio recibido).

## Pasos

1. Localice el widget CHAIN del lado que desea modificar —TX o RX— dentro del contenedor principal Aetherial Audio (TXDSP) en el Applet Panel.
2. Haga clic una vez en la etapa GATE del widget CHAIN para activar o desactivar el bypass del gate en ese lado.
   - Cuando la etapa está habilitada, el subcontenedor "Aetherial TX Gate" o "Aetherial AGC-T" se vuelve visible y el gate está activo en la cadena.
   - Cuando la etapa está omitida, el subcontenedor se oculta y no se aplica ninguna reducción de ganancia.
3. Para volver a habilitar la etapa, haga clic una vez más en la etapa GATE del widget CHAIN.

El estado de bypass se guarda como `ClientGateTxEnabled` (lado TX) o `ClientGateRxEnabled` (lado RX) y se restaura en el siguiente inicio de la aplicación.

## Consejos

- Omitir la etapa desde el widget CHAIN no restablece ninguno de los cinco controles de ajuste: los valores de Thresh, Ratio, Return, Release y Floor se conservan.
- Para abrir el editor flotante del gate y realizar ajustes detallados sin omitir la etapa, haga doble clic en la etapa GATE del widget CHAIN en lugar de un solo clic.

## Relacionados

- [Descripción general de Aetherial TX Gate / Aetherial AGC-T (RX)](overview.md)
- [Ajustar el umbral de TX justo por encima del nivel de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md)
- [Monitorear la reducción de ganancia en tiempo real mientras no habla](watch-live-gr-while-not-speaking.md)
