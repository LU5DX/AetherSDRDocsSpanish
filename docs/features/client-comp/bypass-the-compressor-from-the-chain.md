# Omitir el Compresor de la Cadena

Active o desactive el Compresor Aetherial (TX) o el AGC-C Aetherial (RX) sin cambiar ninguno de sus parámetros. La omisión le permite comparar el audio procesado y sin procesar, o eliminar temporalmente el compresor de la ruta de la señal.

## Antes de comenzar

- El widget CHAIN debe estar visible en el contenedor principal Audio Aetherial (TXDSP).
- Identifique qué lado desea omitir: el compresor de TX (etapa COMP en la cadena de TX) o el compresor de RX (etapa COMP en la cadena de RX).

## Pasos

1. Localice el widget CHAIN para el lado que desea afectar (TX o RX).
2. Haga un solo clic en la etapa **COMP** en el widget CHAIN.
   - Un clic alterna el estado de omisión de esa etapa.
   - Cuando está omitida, la etapa está inactiva y el mosaico del applet Compresor Aetherial (TX) o AGC-C Aetherial (RX) se atenúa hasta una opacidad reducida (aproximadamente el 55 % del brillo normal), coincidiendo con el efecto de atenuación utilizado por la curva EQ cuando su etapa está omitida.
   - Cuando está habilitada (omisión desactivada), el mosaico vuelve a la opacidad total y el compresor procesa el audio.
3. Para re-habilitar, haga un solo clic en la etapa **COMP** nuevamente.

## Qué hace cada control

| Control | Qué hace | Clave de configuración |
|---|---|---|
| Etapa COMP (TX, un clic) | Activa o desactiva el compresor de TX en la cadena de señal. El estado habilitado se conserva. | `ClientCompTxEnabled` |
| Etapa COMP (RX, un clic) | Activa o desactiva el compresor de RX en la cadena de señal. El estado habilitado se conserva. | `ClientCompRxEnabled` |

## Consejos

- La omisión no restablece ningún valor de perilla. Thresh, Ratio, Attack, Release y Makeup permanecen en sus últimas posiciones cuando rehabilita la etapa.
- Hacer doble clic en la etapa **COMP** abre el editor completo del compresor en lugar de alternar la omisión. Use un solo clic solo para omitir.
- La barra de reducción de ganancia en el mosaico del applet marca cero cuando está omitido, ya que no se está realizando ningún procesamiento. La apariencia atenuada del mosaico proporciona una confirmación adicional de un vistazo de que la omisión está activa.

## Relacionado

- [Descripción general del Compresor Aetherial (TX) / AGC-C Aetherial (RX)](overview.md)
- [Abra el editor completo del compresor para controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Observe la reducción de ganancia en vivo mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
