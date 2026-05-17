# Seleccionar un carácter de válvula (Modelo A, B o C) para cambiar el sello armónico

El selector de carácter de válvula elige entre tres curvas de saturación distintas que la etapa de válvula utiliza, moldeando directamente el contenido armónico que se agrega a su audio de TX o RX. Cambie de modelo para comparar sellos sin modificar ningún otro parámetro.

## Antes de empezar

- La etapa de válvula debe estar habilitada en el lado que desea ajustar (TX o RX). Si la etapa está en bypass, la selección del modelo se mantiene, pero no notará una diferencia hasta que la habilite. Cuando la etapa está en bypass, el mosaico completo del applet acoplado se atenúa aproximadamente al 55 % de opacidad como indicador visual; vuelve a la opacidad completa cuando se rehabilita la etapa.
- Abra el editor flotante del lado correspondiente: haga doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX para abrir el editor "Aetherial Tube — TX" o "Aetherial Tube — RX". El selector de modelo solo está disponible en el editor flotante, no en el mosaico del applet acoplado.

## Pasos

1. Haga doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX. Se abre el editor sin bordes titulado "Aetherial Tube — TX" o "Aetherial Tube — RX".
2. Localice los tres botones de alternancia etiquetados como **A**, **B** y **C** en la fila central del editor, entre el control Tone y el control Bias.
3. Haga clic en **A**, **B** o **C** para seleccionar un carácter de válvula. El botón seleccionado se vuelve ámbar. Solo un modelo puede estar activo a la vez.
4. Observe la curva de transferencia: la forma de la curva se actualiza inmediatamente para reflejar el carácter seleccionado. La bola de entrada en vivo continúa recorriendo la nueva curva.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Configuración persistente |
|---------|---------------------|-----------------|---------------------------|
| **A**   | Marcado (activo)    | Seleccionado / no seleccionado | `ClientTubeTxModel` / `ClientTubeRxModel` (almacenado como entero: 0) |
| **B**   | Sin marcar          | Seleccionado / no seleccionado | `ClientTubeTxModel` / `ClientTubeRxModel` (almacenado como entero: 1) |
| **C**   | Sin marcar          | Seleccionado / no seleccionado | `ClientTubeTxModel` / `ClientTubeRxModel` (almacenado como entero: 2) |

A, B y C son mutuamente excluyentes. Seleccionar uno deselecciona los otros. La misma clave de configuración (`ClientTubeTxModel` para TX, `ClientTubeRxModel` para RX) almacena la elección para su respectivo lado; las selecciones de TX y RX son completamente independientes.

## Comportamiento de atenuación en bypass

Cuando la etapa de válvula está en bypass, el mosaico del applet acoplado se renderiza con opacidad reducida (aproximadamente al 55 %). Esto coincide con el efecto de atenuación utilizado en la curva EQ en otras partes de la cadena. El mosaico vuelve a la opacidad completa tan pronto como se rehabilita la etapa. La atenuación se aplica a todo el mosaico, incluida la curva de transferencia y todos los controles. Es solo un indicador visual y no afecta las configuraciones persistentes.

## Edición inline del valor de los controles

Todos los controles de tipo perilla en el editor flotante Aetherial Tube admiten edición inline del valor. Haga clic en el texto del valor mostrado de un control para abrir un pequeño campo de entrada de texto superpuesto sobre el control. Escriba un valor numérico y presione Enter, o haga clic en otro lugar, para confirmar el valor. El valor ingresado se limita al rango válido del control. Presione Escape para cancelar la edición y revertir al valor anterior.

Cuando el campo de entrada de texto está enfocado, muestra un fondo oscuro con un borde cian para indicar el modo de edición. Cuando no está enfocado, aparece idéntico al texto del valor pintado.

## Consejos

- La visualización de la curva de transferencia se actualiza en tiempo real al cambiar de modelo. Úsela junto con la bola de entrada en vivo para ver cómo sus ajustes actuales de Drive y Bias están curvando el nuevo modelo antes de confirmarlo.
- Los lados TX y RX mantienen selecciones de modelo independientes. Cambiar el modelo en "Aetherial Tube — TX" no tiene efecto en "Aetherial Tube — RX" y viceversa.
- Después de cambiar de modelo, la mezcla armónica puede cambiar notablemente con ajustes altos de Drive o Bias. Si el nivel cambia, ajuste el control Output para compensar.
- Use la edición inline de valores para una entrada numérica precisa en lugar de arrastrar los controles. Esto es especialmente útil para establecer valores exactos para los parámetros Bias, Drive, Output y Envelope.
- Si el mosaico acoplado aparece atenuado, la etapa de válvula está actualmente en bypass. Vuelva a habilitarla antes de evaluar cómo suena un cambio de modelo.

## Relacionados

- [Vista general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Ajuste Drive hasta que la curva empiece a doblarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Desplace Bias para ajustar el equilibrio armónico](shift-bias-to-tweak-the-harmonic-balance.md)
- [Compense cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Ponga la válvula en bypass desde cualquier cadena](bypass-the-tube-from-either-chain.md)
