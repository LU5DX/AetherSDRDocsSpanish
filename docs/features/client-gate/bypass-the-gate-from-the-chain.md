# Omitir la etapa Gate desde el CHAIN

El widget CHAIN controla si la etapa Gate está activa en la cadena de procesamiento de audio. Omitirla le permite desactivar completamente el gate de TX o RX sin modificar ninguno de sus controles de ajuste, de modo que puede comparar el audio con y sin gate, o silenciar la etapa temporalmente.

## Antes de comenzar

- Abra el contenedor principal Aetherial Audio (TXDSP) en el Applet Panel. Los subcontenedores "Aetherial TX Gate" (TX) y "Aetherial AGC-T" (RX) permanecen ocultos hasta que la etapa Gate se habilite mediante el widget CHAIN.
- Identifique qué lado desea omitir: TX (afecta el audio que transmite) o RX (afecta el audio recibido).

## Pasos

1. Ubique el widget CHAIN correspondiente al lado que desea modificar —TX o RX— dentro del contenedor principal Aetherial Audio (TXDSP) en el Applet Panel.
2. Haga clic una vez sobre la etapa GATE en el widget CHAIN para activar o desactivar el bypass del gate en ese lado.
   - Cuando la etapa está habilitada, el subcontenedor "Aetherial TX Gate" o "Aetherial AGC-T" se vuelve visible y el gate está activo en la cadena.
   - Cuando la etapa está en bypass, el subcontenedor se oculta y no se aplica ninguna reducción de ganancia.
3. Para volver a habilitar la etapa, haga clic una vez más sobre la etapa GATE en el widget CHAIN.

El estado del bypass se guarda como `ClientGateTxEnabled` (lado TX) o `ClientGateRxEnabled` (lado RX) y se restaura en el próximo inicio de la aplicación.

## Consejos

- Omitir la etapa desde el widget CHAIN no restablece ninguno de los cinco controles de ajuste: los valores de Thresh, Ratio, Attack, Release y Floor se conservan.
- Para abrir el editor flotante del gate y realizar ajustes detallados sin activar el bypass, haga doble clic sobre la etapa GATE en el widget CHAIN en lugar de un solo clic.

## Relacionado

- [Descripción general de Aetherial TX Gate / Aetherial AGC-T (RX)](overview.md)
- [Ajustar el umbral de TX justo por encima del nivel de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md)
- [Monitorear la reducción de ganancia en tiempo real sin hablar](watch-live-gr-while-not-speaking.md)
