# Selección de un carácter de válvula (Modelo A, B o C) para cambiar la coloración armónica

El selector de carácter de válvula elige entre tres curvas de saturación distintas que utiliza la etapa de válvula, moldeando directamente el contenido armónico añadido a su audio de TX o RX. Cambie de modelo para comparar coloraciones sin modificar ningún otro parámetro.

## Antes de comenzar

- La etapa de válvula debe estar habilitada en el lado que desea ajustar (TX o RX). Si la etapa está puenteada, la selección del modelo persiste, pero no escuchará una diferencia hasta que la habilite. Cuando la etapa está puenteada, todo el mosaico acoplado del applet se atenúa aproximadamente al 55 % de opacidad como indicador visual; vuelve a la opacidad completa cuando la etapa se rehabilita.
- Abra el editor flotante del lado correspondiente: haga doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX para abrir el editor "Aetherial Tube — TX" o "Aetherial Tube — RX". El selector de modelo solo está disponible en el editor flotante, no en el mosaico acoplado del applet.

## Pasos

1. Haga doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX. Se abre el editor sin marco titulado "Aetherial Tube — TX" o "Aetherial Tube — RX".
2. Localice los tres botones de alternancia etiquetados como **A**, **B** y **C** en la fila central del editor, entre el mando de Tone y el mando de Bias.
3. Haga clic en **A**, **B** o **C** para seleccionar un carácter de válvula. El botón seleccionado se vuelve ámbar. Solo un modelo puede estar activo a la vez.
4. Observe la curva de transferencia: la forma de la curva se actualiza inmediatamente para reflejar el carácter seleccionado. La bola de entrada en vivo continúa recorriendo la nueva curva.

## Función de cada control

| Control   | Valor predeterminado                                                                                                                            | Valores válidos                                                                      |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| **A**     | Seleccionado (activo)                                                                                                                           | Seleccionado / no seleccionado                                                       |
| **B**     | No seleccionado                                                                                                                                 | Seleccionado / no seleccionado                                                       |
| **C**     | No seleccionado                                                                                                                                 | Seleccionado / no seleccionado                                                       |
| **Drive** | 0.00 dB                                                                                                                                         | 0.0 a 24.0 dB                                                                       |
| **Tone**  | 0.00                                                                                                                                            | -1.0 a 1.0                                                                          |
| **Bias**  | 0 %                                                                                                                                             | 0.0 a 1.0                                                                           |
| **Output** | 0.00 dB                                                                                                                                        | -24.0 a 12.0 dB                                                                     |
| **Dry/Wet** | 100 %                                                                                                                                          | 0.0 a 1.0                                                                           |
| **Envelope** | 0 %                                                                                                                                            | -1.0 a 1.0                                                                          |
| **Attack**  | 5.00 ms                                                                                                                                        | 0.1 a 30.0 ms                                                                       |
| **Release** | 35.00 ms                                                                                                                                       | 10.0 a 500.0 ms                                                                     |
| **RN2**     | Alternancia solo para TX (oculta en modo RX). Habilita el eliminador de ruido neuronal RNNoise en la entrada de micrófono antes de la cadena DSP. Suprime el ruido de fondo antes de que llegue al puerta/compresor/saturador. | Ubicado en el StripTubePanel flotante debajo del medidor de nivel de salida, solo lado TX. Modos de voz únicamente: los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten esta etapa. La configuración se conserva mediante AudioEngine. |

A, B y C son mutuamente excluyentes. Seleccionar uno deselecciona los demás. La misma clave de configuración (`ClientTubeTxModel` para TX, `ClientTubeRxModel` para RX) almacena la elección para su lado respectivo; las selecciones de TX y RX son completamente independientes.

## Indicadores

| Indicador          | Propósito                                                                                                                                                                                                                                  |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Curva de transferencia | ClientTubeCurveWidget en modo compacto. Dibuja la curva de transferencia de la válvula configurada actualmente con una bola en vivo en la entrada. Los colores se adaptan al tema mediante las claves de color de ThemeManager. |
| Bola de entrada en vivo | Un punto se mueve a lo largo de la curva de transferencia al nivel de entrada actual, visualizando el régimen de saturación. El resplandor de la bola usa `color.accent.warning`, el núcleo usa `color.text.primary`.                          |
| Medidor de nivel de salida | Widget ClientLevelMeter (extremo derecho del editor) que muestra el nivel pico posterior a la saturación con balística de ataque rápido / liberación lenta. Etiquetado 'OUT'. Solo visible en el editor flotante, no en el mosaico acoplado del applet. Zonas de color: verde (-60 a -12 dB), lima (-12 a -6 dB), ámbar (-6 a -3 dB), rojo (por encima de -3 dB). |

## Comportamiento de atenuación al puentear

Cuando la etapa de válvula está puenteada, el mosaico acoplado del applet se renderiza con opacidad reducida (aproximadamente 55 %). Esto coincide con el efecto de atenuación utilizado en la curva de ecualización en otras partes de la cadena. El mosaico vuelve a la opacidad completa tan pronto como la etapa se rehabilita. La atenuación se aplica a todo el mosaico, incluida la curva de transferencia y todos los mandos. Es solo un indicador visual y no afecta la configuración persistente.

## Edición de valores en línea de los mandos

Todos los controles de mandos en el editor flotante de Aetherial Tube admiten la edición de valores en línea. Haga clic en el valor mostrado de un mando para abrir un pequeño campo de entrada de texto superpuesto sobre el control. Escriba un valor numérico y presione Enter, o haga clic en otro lugar, para confirmar el valor. El valor ingresado se limita al rango válido del mando. Presione Escape para cancelar la edición y volver al valor anterior.

Cuando el campo de entrada de texto está enfocado, muestra un fondo oscuro con un borde cian para indicar el modo de edición. Cuando no está enfocado, aparece idéntico al texto del valor pintado.

## Colores de mandos adaptables al tema

Todos los componentes del mando (anillo de fondo, arco de valor, puntero, etiqueta y texto de valor) ahora leen del espacio de nombres dedicado `color.knob.*` de ThemeManager. La anulación del contenedor por applet (por ejemplo, `applet/tube`) permite que los mandos de la válvula respeten el tema actual. El texto de la etiqueta del mando usa `color.text.secondary`, el texto del valor usa `color.text.primary`.

## Consejos

- La visualización de la curva de transferencia se actualiza en tiempo real al cambiar de modelo. Úsela junto con la bola de entrada en vivo para ver qué tan intensamente sus ajustes actuales de Drive y Bias están deformando la nueva curva antes de decidirse.
- Los lados TX y RX mantienen selecciones de modelo independientes. Cambiar el modelo en "Aetherial Tube — TX" no tiene efecto en "Aetherial Tube — RX" y viceversa.
- Después de cambiar de modelo, la mezcla armónica puede cambiar notablemente con ajustes altos de Drive o Bias. Si el nivel cambia, ajuste el mando de Output para compensarlo.
- Use la edición de valores en línea para ingresar números precisos en lugar de arrastrar mandos. Esto es especialmente útil para establecer valores exactos en los parámetros Bias, Drive, Output y Envelope.
- Si el mosaico acoplado aparece atenuado, la etapa de válvula está actualmente puenteada. Habilítela de nuevo antes de evaluar cómo suena un cambio de modelo.
- Los colores del widget de curva de válvula se adaptan completamente al tema: el fondo usa `color.background.0`, el marco usa `color.background.1`, la curva usa `color.accent.dim`.

## Relacionados

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Ajuste Drive hasta que la curva comience a deformarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Desplace Bias para ajustar el equilibrio armónico](shift-bias-to-tweak-the-harmonic-balance.md)
- [Compense los cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Puentee la válvula desde cualquier cadena](bypass-the-tube-from-either-chain.md)
