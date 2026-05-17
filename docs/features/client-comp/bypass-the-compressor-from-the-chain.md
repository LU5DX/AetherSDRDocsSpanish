# Omitir el Compresor de la Cadena

Active o desactive el Compresor Aetherial (TX) o el AGC-C Aetherial (RX) sin cambiar ninguno de sus ajustes. Omitirlo le permite comparar el audio procesado y sin procesar, o sacar temporalmente el compresor de la ruta de la señal.

## Antes de empezar

- El widget CHAIN debe estar visible en el contenedor principal de Aetherial Audio (TXDSP).
- Identifique qué lado desea omitir: el compresor TX (etapa COMP en la cadena TX) o el compresor RX (etapa COMP en la cadena RX).

## Pasos

1. Localice el widget CHAIN para el lado que desea modificar (TX o RX).
2. Haga un solo clic en la etapa **COMP** del widget CHAIN.
   - Un solo clic alterna el estado de omisión para esa etapa.
   - Cuando está omitida, la etapa está inactiva y el mosaico de la aplicación Compresor Aetherial (TX) o AGC-C Aetherial (RX) se atenúa a una opacidad reducida (aproximadamente el 55% del brillo normal), coincidiendo con el efecto de atenuación utilizado por la curva EQ cuando su etapa está omitida.
   - Cuando está habilitada (omisión desactivada), el mosaico vuelve a la opacidad completa y el compresor procesa el audio.
3. Para reactivar, haga un solo clic en la etapa **COMP** nuevamente.

## Qué hace cada control

| Control | Qué hace | Clave de ajuste |
|---|---|---|
| Etapa COMP (TX, un solo clic) | Activa o desactiva el compresor TX en la cadena de señal. El estado habilitado se conserva. | `ClientCompTxEnabled` |
| Etapa COMP (RX, un solo clic) | Activa o desactiva el compresor RX en la cadena de señal. El estado habilitado se conserva. | `ClientCompRxEnabled` |

## Controles del mosaico de la aplicación

Los mosaicos de la aplicación Compresor Aetherial (TX) y AGC-C Aetherial (RX) ofrecen una vista compacta del estado del compresor con retroalimentación en vivo y cinco perillas de ajuste.

| Control | Qué hace | Clave de ajuste |
|---|---|---|
| Curva de transferencia | Visualización solo de lectura de la curva de transferencia entrada/salida con un punto en vivo que muestra el nivel de envolvente actual. Editable en el editor de Compresor flotante. | N/A |
| Barra de reducción de ganancia | Barra horizontal de color ámbar que muestra de 0 a 20 dB de reducción de ganancia rellenada hacia la derecha. Una marca en -6 dB señala una cantidad de trabajo típica. Se actualiza a ~30 Hz. | N/A |
| Perilla Thresh | Establece el nivel por encima del cual comienza la compresión. Rango de -60.0 a 0.0 dB, valor predeterminado -18.0 dB. | `ClientCompTxThresholdDb` o `ClientCompRxThresholdDb` |
| Perilla Ratio | Establece la intensidad con la que se contienen los picos una vez superado el umbral. Rango de 1.0 a 20.0, valor predeterminado 3.0. La etiqueta se formatea como "X.XX:1". | `ClientCompTxRatio` o `ClientCompRxRatio` |
| Perilla Attack | Establece la rapidez con la que el compresor se activa tras superar el umbral. Rango de 0.1 a 300.0 ms, valor predeterminado 20.0 ms. | `ClientCompTxAttackMs` o `ClientCompRxAttackMs` |
| Perilla Release | Establece la rapidez con la que la ganancia retorna tras caer la entrada por debajo del umbral. Rango de 5 a 2000 ms, valor predeterminado 200 ms. | `ClientCompTxReleaseMs` o `ClientCompRxReleaseMs` |
| Perilla Makeup | Añade la ganancia perdida por la compresión. Rango de -12.0 a 24.0 dB, valor predeterminado 0.0 dB. Los valores positivos muestran un signo "+". | `ClientCompTxMakeupDb` o `ClientCompRxMakeupDb` |

## Edición de valor en línea

Las perillas del mosaico de la aplicación admiten la edición de valor en línea para un ajuste preciso:

1. Haga clic en la etiqueta del valor actual de una perilla. La etiqueta se transforma en un campo de texto editable con un fondo oscuro sutil y un borde cian.
2. Escriba un nuevo valor. El análisis de configuración regional admite separadores decimales de punto y coma.
3. Presione **Enter** para confirmar el valor, o haga clic en otro lugar de la interfaz. La posición de la perilla se actualiza para coincidir con el valor ingresado.
4. Presione **Escape** para cancelar la edición y revertir al valor anterior.
5. Mientras el editor en línea esté activo, los eventos de la rueda del ratón aún ajustan la perilla con normalidad.

## Consejos

- Omitir no restablece ningún valor de perilla. Thresh, Ratio, Attack, Release y Makeup permanecen en sus últimas posiciones cuando reactive la etapa.
- Hacer doble clic en la etapa **COMP** abre el editor completo del Compresor en lugar de alternar la omisión. Use un solo clic únicamente para omitir.
- La barra de reducción de ganancia en el mosaico de la aplicación marca cero cuando está omitida, ya que no se está procesando. La apariencia atenuada del mosaico proporciona una confirmación adicional de un vistazo de que la omisión está activa.
- Las instancias del compresor TX y RX tienen ajustes completamente independientes. Cambiar las perillas en una no afecta a la otra.

## Relacionado

- [Resumen del Compresor Aetherial (TX) / AGC-C Aetherial (RX)](overview.md)
- [Abra el editor completo del Compresor para controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Observe la reducción de ganancia en vivo mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
