# Seleccione un carácter de tubo (Modelo A, B o C) para cambiar el perfil armónico

El selector de carácter de tubo elige cuál de las tres curvas de saturación distintas utiliza la etapa de tubo, dando forma directamente al contenido armónico añadido al audio de TX o RX. Cambie de modelo para comparar perfiles sin modificar ningún otro parámetro.

## Antes de comenzar

- La etapa de tubo debe estar habilitada en el lado que desee ajustar (TX o RX). Si la etapa está omitida (bypass), la selección de modelo se conserva, pero no se escuchará diferencia hasta que la habilite.
- Abra el editor flotante del lado correspondiente: haga doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX para abrir el editor "Aetherial Tube — TX" o "Aetherial Tube — RX". El selector de modelo solo está disponible en el editor flotante, no en el mosaico del applet anclado.

## Pasos

1. Haga doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX. Se abre el editor sin marco titulado "Aetherial Tube — TX" o "Aetherial Tube — RX".
2. Localice los tres botones de selección etiquetados como **A**, **B** y **C** en la fila central del editor, entre el control Tone y el control Bias.
3. Haga clic en **A**, **B** o **C** para seleccionar un carácter de tubo. El botón seleccionado se ilumina en ámbar. Solo puede estar activo un modelo a la vez.
4. Observe la curva de transferencia: la forma de la curva se actualiza de inmediato para reflejar el carácter seleccionado. El indicador de entrada en tiempo real continúa siguiendo la nueva curva.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Ajuste persistente |
|---------|----------------------|-----------------|--------------------|
| **A** | Activado | Seleccionado / no seleccionado | `ClientTubeTxModel` / `ClientTubeRxModel` (almacenado como entero: 0) |
| **B** | Desactivado | Seleccionado / no seleccionado | `ClientTubeTxModel` / `ClientTubeRxModel` (almacenado como entero: 1) |
| **C** | Desactivado | Seleccionado / no seleccionado | `ClientTubeTxModel` / `ClientTubeRxModel` (almacenado como entero: 2) |

A, B y C son mutuamente excluyentes. Al seleccionar uno, los demás se deseleccionan. La misma clave de ajuste (`ClientTubeTxModel` para TX, `ClientTubeRxModel` para RX) almacena la elección para su lado respectivo; las selecciones de TX y RX son completamente independientes.

## Consejos

- La visualización de la curva de transferencia se actualiza en tiempo real al cambiar de modelo. Úsela junto con el indicador de entrada en tiempo real para ver en qué medida los ajustes actuales de Drive y Bias están curvando la nueva curva antes de confirmar el cambio.
- Los lados TX y RX mantienen selecciones de modelo independientes. Cambiar el modelo en "Aetherial Tube — TX" no tiene efecto sobre "Aetherial Tube — RX" y viceversa.
- Tras cambiar de modelo, la mezcla armónica puede variar notablemente con ajustes altos de Drive o Bias. Si el nivel cambia, ajuste el control Output para compensar.

## Relacionados

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Ajuste el Drive hasta que la curva comience a curvarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Ajuste el Bias para modificar el balance armónico](shift-bias-to-tweak-the-harmonic-balance.md)
- [Compense los cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Omita el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md)
