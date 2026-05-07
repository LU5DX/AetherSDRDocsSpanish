# Omitir la Puerta de la Cadena

El widget CHAIN controla si la etapa de Puerta está activa en la cadena de procesamiento de audio. Omitirla le permite desactivar completamente la puerta de TX o RX sin cambiar ninguno de sus mandos de ajuste, de modo que pueda comparar el audio con y sin puerta o silenciar temporalmente la etapa.

## Antes de comenzar

- Abra el contenedor principal Aetherial Audio (TXDSP) en el Panel de Applets. Los subcontenedores "Aetherial TX Gate" (TX) y "Aetherial AGC-T" (RX) están ocultos hasta que la etapa de Puerta se habilite mediante el widget CHAIN.
- Sepa qué lado desea omitir: TX (afecta su audio transmitido) o RX (afecta el audio recibido).

## Pasos

1. Localice el widget CHAIN para el lado que desea cambiar — TX o RX — dentro del contenedor principal Aetherial Audio (TXDSP) en el Panel de Applets.
2. Haga clic una vez en la etapa GATE del widget CHAIN para alternar la omisión de la puerta en ese lado.
   - Cuando la etapa está habilitada, el subcontenedor "Aetherial TX Gate" o "Aetherial AGC-T" se vuelve visible con opacidad completa y la puerta está activa en la cadena.
   - Cuando la etapa está omitida, el subcontenedor se atenúa a una opacidad reducida (aproximadamente el 55 % del brillo total) y no se aplica ninguna reducción de ganancia.
3. Para volver a habilitar la etapa, haga clic una vez en la etapa GATE del widget CHAIN nuevamente. El subcontenedor vuelve a su opacidad completa.

El estado de omisión se conserva como `ClientGateTxEnabled` (lado TX) o `ClientGateRxEnabled` (lado RX) y se restaura en el próximo inicio de la aplicación.

## Consejos

- El efecto de atenuación al omitir la etapa coincide con el tratamiento visual aplicado a la curva de EQ cuando su etapa está omitida, proporcionando una señal visual coherente en todas las etapas de DSP.
- Omitir desde el widget CHAIN no restablece ninguno de los cinco mandos de ajuste: los valores de Thresh, Ratio, Return, Release y Floor se conservan.
- Para abrir el editor de puerta flotante para un ajuste detallado sin omitirla, haga doble clic en la etapa GATE del widget CHAIN en lugar de un solo clic.

## Relacionados

- [Descripción general de Aetherial TX Gate / Aetherial AGC-T (RX)](overview.md)
- [Establecer el umbral de TX justo por encima del piso de ruido de la sala](set-tx-threshold-just-above-room-noise-floor.md)
- [Observar la GR en vivo mientras no habla](watch-live-gr-while-not-speaking.md)
