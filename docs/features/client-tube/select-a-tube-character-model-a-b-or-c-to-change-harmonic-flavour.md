# Seleccionar un carácter de tubo (Modelo A, B o C) para cambiar el matiz armónico

El selector de carácter de tubo elige entre tres curvas de saturación distintas que utiliza la etapa de tubo, moldeando directamente el contenido armónico que se añade a su audio de TX o RX. Cambie de modelo para comparar matices sin modificar ningún otro parámetro.

## Antes de comenzar

- La etapa de tubo debe estar habilitada en el lado que desea ajustar (TX o RX). Si la etapa está puenteada, la selección del modelo se mantiene, pero no notará ninguna diferencia hasta que la habilite. Cuando la etapa está puenteada, el mosaico completo de la aplicación acoplada se atenúa aproximadamente al 55 % de opacidad como indicador visual; vuelve a la opacidad completa cuando la etapa se rehabilita.
- Abra el editor flotante del lado correspondiente: haga doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX para abrir el editor "Aetherial Tube — TX" o "Aetherial Tube — RX". El selector de modelo solo está disponible en el editor flotante, no en el mosaico de la aplicación acoplada.

## Pasos

1. Haga doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX. Se abrirá el editor sin bordes titulado "Aetherial Tube — TX" o "Aetherial Tube — RX".
2. Localice los tres botones de alternancia etiquetados **A**, **B** y **C** en la fila central del editor, entre el control Tone y el control Bias.
3. Haga clic en **A**, **B** o **C** para seleccionar un carácter de tubo. El botón seleccionado se vuelve ámbar. Solo un modelo puede estar activo a la vez.
4. Observe la curva de transferencia: la forma de la curva se actualiza inmediatamente para reflejar el carácter seleccionado. La bola de entrada en vivo continúa recorriendo la nueva curva.

## Función de cada control

| Control | Valor predeterminado | Valores válidos |
|---------|---------------------|-----------------|
| **A**   | Seleccionado (activo) | Seleccionado / no seleccionado |
| **B**   | No seleccionado | Seleccionado / no seleccionado |
| **C**   | No seleccionado | Seleccionado / no seleccionado |
| RN2     | Alternancia solo TX (oculto en modo RX). Habilita el eliminador de ruido neuronal RNNoise en la entrada del micrófono antes de la cadena DSP. Suprime el ruido de fondo antes de que llegue al compuerta/compresor/saturador. | Se encuentra en el StripTubePanel flotante, debajo del medidor de nivel de salida, solo en el lado TX. Solo modos de voz; los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten esta etapa. La configuración se conserva mediante AudioEngine. |

A, B y C son mutuamente excluyentes. Seleccionar uno deselecciona los demás. La misma clave de configuración (`ClientTubeTxModel` para TX, `ClientTubeRxModel` para RX) almacena la elección para su respectivo lado; las selecciones de TX y RX son completamente independientes.

## Comportamiento de atenuación al puentear

Cuando la etapa de tubo está puenteada, el mosaico de la aplicación acoplada se muestra con opacidad reducida (aproximadamente 55 %). Esto coincide con el efecto de atenuación utilizado en la curva EQ en otras partes de la cadena. El mosaico vuelve a la opacidad completa tan pronto como se rehabilita la etapa. La atenuación se aplica a todo el mosaico, incluida la curva de transferencia y todos los controles. Es solo un indicador visual y no afecta las configuraciones guardadas.

## Edición de valor en línea de los controles

Todos los controles de perilla en el editor flotante de Aetherial Tube admiten la edición de valor en línea. Haga clic en el texto del valor mostrado de una perilla para abrir un pequeño campo de entrada de texto superpuesto en el control. Escriba un valor numérico y presione Enter, o haga clic en otro lugar, para aplicar el valor. El valor ingresado se limita al rango válido de la perilla. Presione Escape para cancelar la edición y volver al valor anterior.

Cuando el campo de entrada de texto está enfocado, muestra un fondo oscuro con un borde cian para indicar el modo de edición. Cuando no está enfocado, aparece idéntico al texto del valor pintado.

## Consejos

- La visualización de la curva de transferencia se actualiza en tiempo real al cambiar de modelo. Úsela junto con la bola de entrada en vivo para ver cómo sus configuraciones actuales de Drive y Bias están curvando el nuevo modelo antes de confirmarlo.
- Los lados TX y RX mantienen selecciones de modelo independientes. Cambiar el modelo en "Aetherial Tube — TX" no tiene ningún efecto en "Aetherial Tube — RX" y viceversa.
- Después de cambiar de modelo, la mezcla armónica puede cambiar notablemente con configuraciones altas de Drive o Bias. Si el nivel cambia, ajuste el control Output para compensarlo.
- Utilice la edición de valor en línea para una entrada numérica precisa en lugar de arrastrar las perillas. Esto es especialmente útil para establecer valores exactos para los parámetros Bias, Drive, Output y Envelope.
- Si el mosaico acoplado aparece atenuado, la etapa de tubo está actualmente puenteada. Rehabilítela antes de evaluar cómo suena un cambio de modelo.

## Relacionados

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Ajuste Drive hasta que la curva comience a doblarse (calidez en TX o moldeado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Desplace Bias para ajustar el equilibrio armónico](shift-bias-to-tweak-the-harmonic-balance.md)
- [Compense los cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Puente el tubo desde cualquier cadena](bypass-the-tube-from-either-chain.md)
