# Seleccione un carácter de tubo (Modelo A, B o C) para cambiar el matiz armónico

El selector de carácter de tubo elige entre tres curvas de saturación distintas que utiliza la etapa de tubo, moldeando directamente el contenido armónico añadido a su audio de TX o RX. Cambie de modelo para comparar matices sin modificar ningún otro parámetro.

## Antes de comenzar

- La etapa de tubo debe estar habilitada en el lado que desea ajustar (TX o RX). Si la etapa está puenteada, la selección del modelo persistirá pero no notará ninguna diferencia hasta que la habilite. Cuando la etapa está puenteada, el mosaico completo de la applet acoplada se atenúa aproximadamente al 55 % de opacidad como indicador visual; vuelve a la opacidad completa cuando la etapa se vuelve a habilitar.
- Abra el editor flotante para el lado correspondiente: haga doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX para abrir el editor "Aetherial Tube — TX" o "Aetherial Tube — RX". El selector de modelo solo está disponible en el editor flotante, no en el mosaico de la applet acoplada.

## Pasos

1. Haga doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX. Se abre el editor sin marco titulado "Aetherial Tube — TX" o "Aetherial Tube — RX".
2. Localice los tres botones de alternancia etiquetados como **A**, **B** y **C** en la fila central del editor, entre el mando de Tone y el mando de Bias.
3. Haga clic en **A**, **B** o **C** para seleccionar un carácter de tubo. El botón seleccionado se vuelve ámbar. Solo puede haber un modelo activo a la vez.
4. Observe la curva de transferencia: la forma de la curva se actualiza inmediatamente para reflejar el carácter seleccionado. La bola de entrada en vivo continúa recorriendo la nueva curva.

## Qué hace cada control

| Control       | Valor predeterminado                                                                                                                                                               | Valores válidos                                                                                                                                                                                               |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **A**         | Marcado (activo)                                                                                                                                                                   | Seleccionado / no seleccionado                                                                                                                                                                                |
| **B**         | Sin marcar                                                                                                                                                                         | Seleccionado / no seleccionado                                                                                                                                                                                |
| **C**         | Sin marcar                                                                                                                                                                         | Seleccionado / no seleccionado                                                                                                                                                                                |
| **Drive**     | 0.00 dB                                                                                                                                                                            | 0.0 a 24.0 dB                                                                                                                                                                                                 |
| **Tone**      | 0.00                                                                                                                                                                               | -1.0 a 1.0                                                                                                                                                                                                    |
| **Bias**      | 0 %                                                                                                                                                                                | 0.0 a 1.0                                                                                                                                                                                                     |
| **Output**    | 0.00 dB                                                                                                                                                                            | -24.0 a 12.0 dB                                                                                                                                                                                               |
| **Dry/Wet**   | 100 %                                                                                                                                                                              | 0.0 a 1.0                                                                                                                                                                                                     |
| **Envelope**  | 0 %                                                                                                                                                                                | -1.0 a 1.0                                                                                                                                                                                                    |
| **Attack**    | 5.00 ms                                                                                                                                                                            | 0.1 a 30.0 ms                                                                                                                                                                                                 |
| **Release**   | 35.00 ms                                                                                                                                                                           | 10.0 a 500.0 ms                                                                                                                                                                                               |
| **RN2**       | Alternancia solo para TX (oculta en modo RX). Habilita el eliminador de ruido neuronal RNNoise en la entrada del micrófono antes de la cadena DSP. Suprime el ruido de fondo antes de que llegue al puerta/compresor/saturador. | Ubicado en el StripTubePanel flotante debajo del medidor de nivel de salida, solo en el lado TX. Solo modos de voz: los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten esta etapa. La configuración se conserva mediante AudioEngine. |
| RN2           | Alternancia solo para TX (oculta en modo RX). Habilita el eliminador de ruido neuronal RNNoise en la entrada del micrófono antes de la cadena DSP. Suprime el ruido de fondo antes de que llegue al puerta/compresor/saturador. | Ubicado en el StripTubePanel flotante debajo del medidor de nivel de salida, solo en el lado TX. Solo modos de voz: los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten esta etapa. La configuración se conserva mediante AudioEngine. |

A, B y C son mutuamente excluyentes. Seleccionar uno deselecciona los demás. La misma clave de configuración (`ClientTubeTxModel` para TX, `ClientTubeRxModel` para RX) almacena la selección para su lado respectivo; las selecciones de TX y RX son completamente independientes.

## Indicadores

| Indicador           | Propósito                                                                                                                                                                                       |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Curva de transferencia | ClientTubeCurveWidget en modo compacto. Dibuja la curva de transferencia del tubo configurada actualmente con una bola en vivo en la entrada. Los colores reconocen el tema mediante las claves de color de ThemeManager. |
| Bola de entrada en vivo | El punto se mueve a lo largo de la curva de transferencia al nivel de entrada actual, visualizando el régimen de saturación. El resplandor de la bola usa `color.accent.warning`, el centro usa `color.text.primary`. |
| Medidor de nivel de salida | Widget ClientLevelMeter (extremo derecho del editor) que muestra el nivel máximo posterior a la saturación con balística de ataque rápido / liberación lenta. Etiquetado como 'OUT'. Solo visible en el editor flotante, no en el mosaico de la applet acoplada. Zonas de color: verde (-60 a -12 dB), lima (-12 a -6 dB), ámbar (-6 a -3 dB), rojo (por encima de -3 dB). |

## Comportamiento de atenuación por puenteo

Cuando la etapa de tubo está puenteada, el mosaico de la applet acoplada se renderiza con opacidad reducida (aproximadamente 55 %). Esto coincide con el efecto de atenuación utilizado en la curva EQ en otras partes de la cadena. El mosaico vuelve a la opacidad completa tan pronto como se vuelve a habilitar la etapa. La atenuación se aplica a todo el mosaico, incluida la curva de transferencia y todos los mandos. Es solo un indicador visual y no afecta las configuraciones conservadas.

## Edición de valor en línea del mando

Todos los controles de mando en el editor flotante de Aetherial Tube admiten edición de valor en línea. Haga clic en el texto del valor mostrado de un mando para abrir un pequeño campo de entrada de texto superpuesto al control. Escriba un valor numérico y presione Enter, o haga clic en otro lugar, para confirmar el valor. El valor ingresado se ajusta al rango válido del mando. Presione Escape para cancelar la edición y volver al valor anterior.

Cuando el campo de entrada de texto está enfocado, muestra un fondo oscuro con un borde cian para indicar el modo de edición. Cuando no está enfocado, aparece idéntico al texto del valor pintado.

## Colores de mando que reconocen el tema

Todos los componentes del mando (anillo de fondo, arco de valor, puntero, etiqueta y texto del valor) ahora leen del espacio de nombres `color.knob.*` dedicado de ThemeManager. La anulación por contenedor de applet (por ejemplo, `applet/tube`) permite que los mandos del tubo respeten el tema actual. El texto de la etiqueta del mando usa `color.text.secondary`, el texto del valor usa `color.text.primary`.

## Consejos

- La visualización de la curva de transferencia se actualiza en tiempo real al cambiar de modelo. Úsela junto con la bola de entrada en vivo para ver qué tan intensamente sus configuraciones actuales de Drive y Bias están deformando la nueva curva antes de confirmar.
- Los lados TX y RX mantienen selecciones de modelo independientes. Cambiar el modelo en "Aetherial Tube — TX" no tiene efecto en "Aetherial Tube — RX" y viceversa.
- Después de cambiar de modelo, la mezcla armónica puede cambiar notablemente con configuraciones altas de Drive o Bias. Si el nivel cambia, ajuste el mando Output para compensar.
- Use la edición de valor en línea para una entrada numérica precisa en lugar de arrastrar los mandos. Esto es especialmente útil para establecer valores exactos para los parámetros Bias, Drive, Output y Envelope.
- Si el mosaico acoplado aparece atenuado, la etapa de tubo está actualmente puenteada. Vuelva a habilitarla antes de evaluar cómo suena un cambio de modelo.
- Los colores del widget de curva de tubo reconocen completamente el tema: el fondo usa `color.background.0`, el marco usa `color.background.1`, la curva usa `color.accent.dim`.

## Relacionados

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Ajuste Drive hasta que la curva comience a deformarse (calidez de TX o modelado de tono de RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Desplace Bias para ajustar el equilibrio armónico](shift-bias-to-tweak-the-harmonic-balance.md)
- [Compense los cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Puentee el tubo desde cualquier cadena](bypass-the-tube-from-either-chain.md)
