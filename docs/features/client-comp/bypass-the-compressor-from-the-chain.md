# Omitir el Compresor de la Cadena

Active o desactive el Aetherial Compressor (TX) o el Aetherial AGC-C (RX) sin modificar ninguna de sus configuraciones. Omitirlo le permite comparar el audio procesado y sin procesar, o retirar temporalmente el compresor de la ruta de la señal.

## Antes de comenzar

- El widget CHAIN debe estar visible en el contenedor principal Aetherial Audio (TXDSP).
- Identifique qué lado desea omitir: el compresor TX (etapa COMP en la cadena TX) o el compresor RX (etapa COMP en la cadena RX).

## Pasos

1. Localice el widget CHAIN del lado que desea afectar (TX o RX).
2. Haga clic una vez en la etapa **COMP** del widget CHAIN.
   - Un clic cambia el estado de omisión de esa etapa.
   - Cuando está omitida, la etapa queda inactiva y el panel del subcontenedor Aetherial Compressor (TX) o Aetherial AGC-C (RX) se oculta.
   - Cuando está habilitada (omisión desactivada), el panel se vuelve visible y el compresor procesa el audio.
3. Para volver a habilitarla, haga clic una vez más en la etapa **COMP**.

## Qué hace cada control

| Control | Qué hace | Clave de configuración |
|---|---|---|
| Etapa COMP (TX, un clic) | Activa o desactiva el compresor TX en la cadena de señal. El estado habilitado se conserva. | `ClientCompTxEnabled` |
| Etapa COMP (RX, un clic) | Activa o desactiva el compresor RX en la cadena de señal. El estado habilitado se conserva. | `ClientCompRxEnabled` |

## Consejos

- Omitir la etapa no restablece los valores de los mandos. Thresh, Ratio, Attack, Release y Makeup permanecen en sus últimas posiciones cuando vuelve a habilitar la etapa.
- Hacer doble clic en la etapa **COMP** abre el editor completo del compresor en lugar de alternar la omisión. Use un solo clic únicamente para omitir.
- La barra de reducción de ganancia en el panel del applet indica cero cuando está omitido, ya que no se realiza ningún procesamiento. Úselo como confirmación rápida de que la omisión está activa.

## Relacionado

- [Descripción general de Aetherial Compressor (TX) / Aetherial AGC-C (RX)](overview.md)
- [Abrir el editor completo del compresor para los controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Ver la reducción de ganancia en tiempo real mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
