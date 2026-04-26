# Omitir el compresor de la cadena

Active o desactive el Aetherial Compressor (TX) o el Aetherial AGC-C (RX) sin modificar ninguno de sus ajustes. La función de omisión (bypass) le permite comparar el audio procesado y sin procesar, o retirar temporalmente el compresor de la ruta de señal.

## Antes de comenzar

- El widget CHAIN debe estar visible en el contenedor principal Aetherial Audio (TXDSP).
- Identifique qué lado desea omitir: el compresor TX (etapa COMP en la cadena TX) o el compresor RX (etapa COMP en la cadena RX).

## Pasos

1. Localice el widget CHAIN del lado que desea afectar (TX o RX).
2. Haga clic una vez en la etapa **COMP** del widget CHAIN.
   - Un clic cambia el estado de omisión de esa etapa.
   - Cuando está omitida, la etapa queda inactiva y el panel del subcontenedor Aetherial Compressor (TX) o Aetherial AGC-C (RX) se oculta automáticamente.
   - Cuando está habilitada (omisión desactivada), el panel se vuelve visible y el compresor procesa el audio.
3. Para volver a habilitarla, haga clic una vez en la etapa **COMP** nuevamente.

## Qué hace cada control

| Control | Función | Clave de ajuste |
|---|---|---|
| Etapa COMP (TX, un clic) | Activa o desactiva el compresor TX en la cadena de señal. El estado habilitado se conserva. | `ClientCompTxEnabled` |
| Etapa COMP (RX, un clic) | Activa o desactiva el compresor RX en la cadena de señal. El estado habilitado se conserva. | `ClientCompRxEnabled` |

## Consejos

- La omisión no restablece ningún valor de los controles. Thresh, Ratio, Attack, Release y Makeup permanecen en sus últimas posiciones cuando se vuelve a habilitar la etapa.
- Hacer doble clic en la etapa **COMP** abre el editor completo del compresor en lugar de alternar la omisión. Use un solo clic únicamente para omitir.
- La barra de reducción de ganancia en el panel del applet muestra cero cuando está omitido, ya que no se está realizando ningún procesamiento. Use esto como confirmación rápida de que la omisión está activa.

## Relacionados

- [Descripción general de Aetherial Compressor (TX) / Aetherial AGC-C (RX)](overview.md)
- [Abrir el editor completo del compresor para los controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Observar la reducción de ganancia en tiempo real mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
