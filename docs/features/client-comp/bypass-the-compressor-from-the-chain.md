# Omitir el Compresor de la Cadena

Active o desactive el Compresor Aetherial (TX) o el AGC-C Aetherial (RX) sin cambiar ninguna de sus configuraciones. La omisión le permite comparar el audio procesado y sin procesar, o eliminar temporalmente el compresor de la ruta de la señal.

## Antes de empezar

- El widget CADENA debe estar visible en el contenedor principal de Audio Aetherial (TXDSP).
- Identifique qué lado desea omitir: el compresor de TX (etapa COMP en la cadena de TX) o el compresor de RX (etapa COMP en la cadena de RX).

## Pasos

1. Localice el widget CADENA para el lado que desea modificar (TX o RX).
2. Haga un solo clic en la etapa **COMP** en el widget CADENA.
   - Un clic alterna el estado de omisión para esa etapa.
   - Cuando está omitida, la etapa está inactiva y el mosaico de la aplicación Compresor Aetherial (TX) o AGC-C Aetherial (RX) se atenúa a una opacidad reducida (aproximadamente el 55% del brillo normal), coincidiendo con el efecto de atenuación utilizado por la curva EQ cuando su etapa está omitida.
   - Cuando está activada (sin omisión), el mosaico vuelve a la opacidad total y el compresor procesa el audio.
3. Para reactivar, haga un solo clic en la etapa **COMP** nuevamente.

## Qué hace cada control

| Control                           | Qué hace                                                                                                                                                                                                                                                                                                                                                                   | Clave de configuración                                                                                                                                                        |
|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Etapa COMP (TX, un clic)          | Alterna el compresor de TX dentro o fuera de la cadena de señal. El estado activado se conserva.                                                                                                                                                                                                                                                                           | `ClientCompTxEnabled`                                                                                                                                                         |
| Etapa COMP (RX, un clic)          | Alterna el compresor de RX dentro o fuera de la cadena de señal. El estado activado se conserva.                                                                                                                                                                                                                                                                           | `ClientCompRxEnabled`                                                                                                                                                         |
| Drive                             | Aumento de ganancia previo a la compresión con auto-makeup vinculado. Empuja más señal por encima del umbral para que el compresor actúe con más fuerza, y simultáneamente añade la misma ganancia en la salida para que el RMS promedio se eleve junto con los picos en lugar de caer. Rango de 0.0 a 18.0 dB, valor predeterminado 0.0 dB. Combínelo con Phase para mantener los picos limpios. | Se muestra solo en el StripCompPanel flotante (columna derecha). La etiqueta se muestra como '+X.X dB'. Clave de configuración: `ClientCompTxDriveDb` o `ClientCompRxDriveDb`. El tooltip explica la reducción de PAPR #2887. El auto-makeup coincide con el modelo broadcast-Optimod. |
| Phase                             | Número de secciones de paso total en cascada (0 = desactivado). Cada etapa añade 12 dB/oct de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más opcionalmente 1000/2000 Hz). Simetriza los picos de voz asimétricos antes de la compresión para reducir la PAPR. Rango de 0 a 6 etapas, valor predeterminado 0 etapas. Etiqueta 'Off' cuando es 0, 'N stg' cuando está activo. | Se muestra solo en el StripCompPanel flotante (columna derecha). Clave de configuración: `ClientCompTxPhaseRotatorStages` o `ClientCompRxPhaseRotatorStages`. Tooltip: 'Rotador de fase pre-comp (#2887). 0=off, 4=valor predeterminado broadcast.' Los centros predeterminados (300/700/1500/2500 Hz con 1000/2000 Hz opcional) cubren el rango de formantes del habla sin agruparse. |
## Controles del mosaico de la aplicación

Los mosaicos de la aplicación Compresor Aetherial (TX) y AGC-C Aetherial (RX) proporcionan una vista compacta del estado del compresor con retroalimentación en vivo y cinco perillas de sintonización.

| Control                        | Qué hace                                                                                                                                                                                                                                                                                                     | Clave de configuración                                                                                                                                 |
|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| Curva de transferencia         | Visualización de solo lectura de la curva de transferencia de entrada/salida con una bola en vivo que muestra el nivel de envolvente actual. Editable en el editor Compressor flotante. Los colores se adaptan al tema: fondo, cuadrícula, curva, línea identidad, etiquetas de ejes, resplandor de la bola y núcleo de la bola. | N/A |
| Barra de reducción de ganancia | Barra horizontal de color ámbar que muestra de 0 a 20 dB de reducción de ganancia rellenada hacia la derecha (relleno deslizante que se adapta al tema). Una marca en -6 dB indica una cantidad de trabajo típica. Se actualiza a ~30 Hz desde `ClientComp::gainReductionDb()` con balística `MeterSmoother`. | N/A |
| Perilla Thresh                  | Establece el nivel por encima del cual comienza la compresión. Rango de -60.0 a 0.0 dB, valor predeterminado -18.0 dB.                                                                                                                                                                                  | `ClientCompTxThresholdDb` o `ClientCompRxThresholdDb`                                                                                                  |
| Perilla Ratio                   | Establece la firmeza con la que se contienen los picos una vez que se supera el umbral. Rango de 1.0 a 20.0, valor predeterminado 3.0. La etiqueta se formatea como "X.XX:1".                                                                                                                              | `ClientCompTxRatio` o `ClientCompRxRatio`                                                                                                              |
| Perilla Attack                  | Establece la rapidez con la que el compresor actúa después de superar el umbral. Rango de 0.1 a 300.0 ms, valor predeterminado 20.0 ms.                                                                                                                                                                   | `ClientCompTxAttackMs` o `ClientCompRxAttackMs`                                                                                                        |
| Perilla Release                 | Establece la rapidez con la que la ganancia regresa después de que la entrada cae por debajo del umbral. Rango de 5 a 2000 ms, valor predeterminado 200 ms.                                                                                                                                                  | `ClientCompTxReleaseMs` o `ClientCompRxReleaseMs`                                                                                                      |
| Perilla Makeup                  | Añade de vuelta la ganancia perdida por la compresión. Rango de -12.0 a 24.0 dB, valor predeterminado 0.0 dB. Los valores positivos muestran un signo "+".                                                                                                                                                   | `ClientCompTxMakeupDb` o `ClientCompRxMakeupDb`                                                                                                        |

## Edición de valor en línea

Las perillas en el mosaico de la aplicación admiten la edición de valor en línea para un ajuste preciso:

1. Haga clic en la etiqueta del valor actual de una perilla. La etiqueta se transforma en un campo de texto editable con un fondo oscuro sutil y un borde cian.
2. Escriba un nuevo valor. El análisis sensible a la configuración regional admite separadores decimales tanto de punto como de coma.
3. Presione **Enter** para confirmar el valor, o haga clic en otro lugar de la interfaz. La posición de la perilla se actualiza para coincidir con el valor introducido.
4. Presione **Escape** para cancelar la edición y revertir al valor anterior.
5. Mientras el editor en línea está activo, los eventos de la rueda del ratón siguen ajustando la perilla normalmente.

## Consejos

- Omitir no restablece ningún valor de las perillas. Thresh, Ratio, Attack, Release y Makeup permanecen en sus últimas posiciones cuando vuelva a activar la etapa.
- Haga doble clic en la etapa **COMP** para abrir el editor Compressor completo en lugar de alternar la omisión. Use un solo clic solo para omitir.
- La barra de reducción de ganancia en el mosaico de la aplicación marca cero cuando está omitida, ya que no se está procesando. La apariencia atenuada del mosaico proporciona una confirmación adicional de un vistazo de que la omisión está activa.
- Las instancias del compresor de TX y RX tienen configuraciones completamente independientes. Cambiar las perillas en uno no afecta al otro.
- El widget de curva de transferencia y el deslizador de reducción de ganancia observan los colores del tema. Cuando cambie de tema, el fondo de la curva, las líneas de cuadrícula, las etiquetas de los ejes, la línea identidad, el color de la curva, el resplandor de la bola y el núcleo de la bola se actualizan automáticamente. El deslizador de reducción de ganancia usa el color `slider.foreground` del tema para la porción rellena.

## Relacionado

- [Descripción general del Compresor Aetherial (TX) / AGC-C Aetherial (RX)](overview.md)
- [Abra el editor Compressor completo para controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Observe la reducción de ganancia en vivo mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
