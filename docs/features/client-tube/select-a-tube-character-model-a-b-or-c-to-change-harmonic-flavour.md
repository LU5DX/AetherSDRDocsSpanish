# Seleccionar un carácter de tubo (Modelo A, B o C) para cambiar el matiz armónico

El selector de carácter de tubo permite elegir cuál de las tres curvas de saturación distintas utiliza la etapa de tubo, moldeando directamente el contenido armónico añadido al audio de TX o RX. Cambie de modelo para comparar matices sin modificar ningún otro parámetro.

## Antes de comenzar

- La etapa de tubo debe estar habilitada en el lado que desea ajustar (TX o RX). Si la etapa está omitida, la selección del modelo persiste, pero no notará diferencia hasta que la habilite. Cuando la etapa está omitida, la totalidad del mosaico acoplado del applet se atenúa aproximadamente al 55 % de opacidad como indicador visual; vuelve a la opacidad completa al re-habilitar la etapa.
- Abra el editor flotante del lado correspondiente: haga doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX para abrir el editor "Aetherial Tube — TX" o "Aetherial Tube — RX". El selector de modelo solo está disponible en el editor flotante, no en el mosaico acoplado del applet.

## Pasos

1. Haga doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX. Se abre el editor sin bordes titulado "Aetherial Tube — TX" o "Aetherial Tube — RX".
2. Localice los tres botones de alternancia etiquetados como **A**, **B** y **C** en la fila central del editor, entre el mando Tone y el mando Bias.
3. Haga clic en **A**, **B** o **C** para seleccionar un carácter de tubo. El botón seleccionado cambia a color ámbar. Solo un modelo puede estar activo a la vez.
4. Observe la curva de transferencia: la forma de la curva se actualiza inmediatamente para reflejar el carácter seleccionado. La bola de entrada en vivo continúa recorriendo la nueva curva.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Ajuste persistente |
|---------|-----------------------|-----------------|-------------------|
| **A** | Seleccionado (activo) | Seleccionado / no seleccionado | `ClientTubeTxModel` / `ClientTubeRxModel` (almacenado como entero: 0) |
| **B** | No seleccionado | Seleccionado / no seleccionado | `ClientTubeTxModel` / `ClientTubeRxModel` (almacenado como entero: 1) |
| **C** | No seleccionado | Seleccionado / no seleccionado | `ClientTubeTxModel` / `ClientTubeRxModel` (almacenado como entero: 2) |

A, B y C son mutuamente excluyentes. Seleccionar uno deselecciona los demás. La misma clave de ajuste (`ClientTubeTxModel` para TX, `ClientTubeRxModel` para RX) almacena la elección para su respectivo lado; las selecciones de TX y RX son completamente independientes.

## Comportamiento de atenuación al omitir

Cuando la etapa de tubo está omitida, el mosaico acoplado del applet se renderiza con opacidad reducida (aproximadamente 55 %). Esto coincide con el efecto de atenuación utilizado en la curva EQ en otras partes de la cadena. El mosaico vuelve a la opacidad completa tan pronto como se re-habilita la etapa. La atenuación se aplica a todo el mosaico, incluyendo la curva de transferencia y todos los mandos. Es solo un indicador visual y no afecta los ajustes persistentes.

## Consejos

- La visualización de la curva de transferencia se actualiza en tiempo real al cambiar de modelo. Úsela junto con la bola de entrada en vivo para ver cuánto están curvando el nuevo modelo sus ajustes actuales de Drive y Bias antes de decidirse.
- Los lados TX y RX mantienen selecciones de modelo independientes. Cambiar el modelo en "Aetherial Tube — TX" no tiene efecto en "Aetherial Tube — RX" y viceversa.
- Después de cambiar de modelo, la mezcla armónica puede cambiar notablemente con ajustes altos de Drive o Bias. Si el nivel cambia, ajuste el mando Output para compensar.
- Si el mosaico acoplado aparece atenuado, la etapa de tubo está actualmente omitida. Re-habilitela antes de evaluar cómo suena un cambio de modelo.

## Relacionados

- [Visión general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Ajuste Drive hasta que la curva comience a doblarse (calidez en TX o moldeado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Desplace Bias para ajustar el equilibrio armónico](shift-bias-to-tweak-the-harmonic-balance.md)
- [Compense cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Omita el tubo desde cualquier cadena](bypass-the-tube-from-either-chain.md)
