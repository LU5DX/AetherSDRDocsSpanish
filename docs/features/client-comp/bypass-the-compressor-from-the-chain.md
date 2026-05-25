# Omitir el Compresor de la Cadena

Active o desactive el Aetherial Compressor (TX) o el Aetherial AGC-C (RX) sin cambiar ninguna de sus configuraciones. La omisión le permite comparar el audio procesado y sin procesar, o sacar temporalmente el compresor de la ruta de la señal.

## Antes de comenzar

- El widget CHAIN debe estar visible en el contenedor principal de Aetherial Audio (TXDSP).
- Identifique qué lado desea omitir: el compresor de TX (etapa COMP en la cadena de TX) o el compresor de RX (etapa COMP en la cadena de RX).

## Pasos

1. Localice el widget CHAIN para el lado que desea afectar (TX o RX).
2. Haga clic una vez en la etapa **COMP** en el widget CHAIN.
   - Un clic alterna el estado de omisión de esa etapa.
   - Cuando está omitida, la etapa está inactiva y el mosaico del applet Aetherial Compressor (TX) o Aetherial AGC-C (RX) se atenúa a una opacidad reducida (aproximadamente el 55 % del brillo normal), coincidiendo con el efecto de atenuación utilizado por la curva EQ cuando su etapa está omitida.
   - Cuando está habilitada (omisión desactivada), el mosaico vuelve a su opacidad total y el compresor procesa el audio.
3. Para volver a habilitar, haga clic una vez en la etapa **COMP** nuevamente.

## Función de cada control

| Control                       | Función                                                                                                                                                                                                                                   | Clave de configuración                                                                                                                                                         |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Etapa COMP (TX, un clic)      | Alterna la inclusión del compresor de TX en la cadena de señal. El estado habilitado se conserva.                                                                                                                                         | `ClientCompTxEnabled`                                                                                                                                                          |
| Etapa COMP (RX, un clic)      | Alterna la inclusión del compresor de RX en la cadena de señal. El estado habilitado se conserva.                                                                                                                                         | `ClientCompRxEnabled`                                                                                                                                                          |
| Drive                         | Aumento de ganancia previo a la compresión. Empuja más señal por encima del umbral para que el compresor actúe con más fuerza, elevando la potencia media. Combínelo con Phase para mantener los picos limpios.                            | Se muestra solo en el panel flotante StripCompPanel (columna derecha). La etiqueta se muestra como '+X.X dB'. La información sobre herramientas explica la combinación para reducción de PAPR #2887. |
| Phase                         | Número de secciones de paso total en cascada (0 = desactivado). Cada etapa añade 12 dB/octava de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más opcionalmente 1000/2000 Hz). Simetriza los picos asimétricos de voz antes de la compresión para reducir la PAPR. | Se muestra solo en el panel flotante StripCompPanel (columna derecha). Etiqueta 'Off' cuando es 0, 'N stg' cuando está activo. Información sobre herramientas: 'Rotador de fase previo a compresión (#2887). 0=off, 4=valor predeterminado de radiodifusión.' |
## Controles del mosaico del applet

Los mosaicos del applet Aetherial Compressor (TX) y Aetherial AGC-C (RX) proporcionan una vista compacta del estado del compresor con retroalimentación en vivo y cinco perillas de ajuste.

| Control | Función | Clave de configuración |
|---|---|---|
| Curva de transferencia | Visualización solo de lectura de la curva de transferencia entrada/salida con un punto móvil que muestra el nivel de envolvente actual. Editable en el editor flotante del compresor. | N/A |
| Barra de reducción de ganancia | Barra horizontal de color ámbar que muestra de 0 a 20 dB de reducción de ganancia, rellenada de derecha a izquierda. Una marca en -6 dB indica una cantidad de trabajo típica. Se actualiza a ~30 Hz. | N/A |
| Perilla Thresh | Establece el nivel por encima del cual comienza la compresión. Rango -60.0 a 0.0 dB, valor predeterminado -18.0 dB. | `ClientCompTxThresholdDb` o `ClientCompRxThresholdDb` |
| Perilla Ratio | Establece la intensidad con la que se sujetan los picos una vez superado el umbral. Rango 1.0 a 20.0, valor predeterminado 3.0. La etiqueta tiene el formato "X.XX:1". | `ClientCompTxRatio` o `ClientCompRxRatio` |
| Perilla Attack | Establece la rapidez con la que el compresor actúa después de superar el umbral. Rango 0.1 a 300.0 ms, valor predeterminado 20.0 ms. | `ClientCompTxAttackMs` o `ClientCompRxAttackMs` |
| Perilla Release | Establece la rapidez con la que la ganancia regresa después de que la señal de entrada cae por debajo del umbral. Rango 5 a 2000 ms, valor predeterminado 200 ms. | `ClientCompTxReleaseMs` o `ClientCompRxReleaseMs` |
| Perilla Makeup | Añade la ganancia perdida por la compresión. Rango -12.0 a 24.0 dB, valor predeterminado 0.0 dB. Los valores positivos muestran un signo "+". | `ClientCompTxMakeupDb` o `ClientCompRxMakeupDb` |

## Edición de valor en línea

Las perillas en el mosaico del applet admiten la edición de valor en línea para un ajuste preciso:

1. Haga clic en la etiqueta del valor actual de una perilla. La etiqueta se transforma en un campo de texto editable con un fondo oscuro sutil y un borde cian.
2. Escriba un nuevo valor. El análisis sensible a la configuración regional admite separadores decimales de punto y coma.
3. Presione **Enter** para confirmar el valor, o haga clic en otro lugar de la interfaz. La posición de la perilla se actualiza para coincidir con el valor ingresado.
4. Presione **Escape** para cancelar la edición y revertir al valor anterior.
5. Mientras el editor en línea está activo, los eventos de la rueda del ratón siguen ajustando la perilla normalmente.

## Consejos

- Omitir no restablece ningún valor de perilla. Thresh, Ratio, Attack, Release y Makeup permanecen en sus últimas posiciones cuando vuelve a habilitar la etapa.
- Haga doble clic en la etapa **COMP** para abrir el editor completo del compresor en lugar de alternar la omisión. Utilice un solo clic solo para omitir.
- La barra de reducción de ganancia en el mosaico del applet marca cero cuando está omitida, ya que no se está realizando ningún procesamiento. La apariencia atenuada del mosaico proporciona una confirmación adicional de un vistazo de que la omisión está activa.
- Las instancias del compresor de TX y RX tienen configuraciones totalmente independientes. Cambiar las perillas en una no afecta a la otra.

## Relacionados

- [Resumen de Aetherial Compressor (TX) / Aetherial AGC-C (RX)](overview.md)
- [Abra el editor completo del compresor para controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Observe la reducción de ganancia en vivo mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
