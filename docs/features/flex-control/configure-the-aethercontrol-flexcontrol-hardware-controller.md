# Configurar el controlador hardware AetherControl / FlexControl

Configure una rueda FlexControl física o la rueda virtual AetherControl para sintonización y acciones de botones. El diálogo le permite gestionar la conexión, el comportamiento de la rueda y las asignaciones de botones tanto para controladores físicos como virtuales.

## Antes de empezar

- Un FlexControl físico conectado por USB (para uso con hardware)
- Para uso solo virtual, no se necesita hardware

## Pasos

1. Abra **Settings > AetherControl...**
2. Para conectar un FlexControl físico, haga clic en **Detect** en la sección Physical. El diálogo escanea los puertos serie y se conecta automáticamente. Si falla la detección, haga clic en **Close** e intente de nuevo.
3. Para usar la rueda virtual, haga clic y arrastre alrededor del indicador Wheel para sintonizar el slice activo.
4. Ajuste el control deslizante **Wheel Tightness** para configurar el arrastre por inercia (0 = apretado, 100 = suelto). Valor predeterminado: 45.
5. Ajuste el control deslizante **Mouse Sensitivity** para escalar el movimiento del puntero capturado (0 = menos, 100 = más). Valor predeterminado: 50.
6. Alterne **Compact** para ocultar los botones auxiliares y mostrar solo la rueda y la lectura de frecuencia.
7. Alterne **External Spin** para habilitar la sintonización por giro iniciada al arrastrar en el panadapter.
8. Alterne **Reverse** para invertir la dirección de sintonización de la rueda.
9. Configure la acción de presionar la rueda: seleccione una acción del cuadro combinado **Push**.
10. Configure la acción de doble toque en la rueda: seleccione una acción del cuadro combinado **Double-tap**.
11. Para configurar los botones auxiliares, haga clic en un botón auxiliar (etiquetado con puntos). Luego seleccione acciones de los cuadros combinados **Aux single-tap combo** y **Aux double-tap combo** que aparecen.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---------|----------------|--------------|------------------------|----------------|
| Wheel | — | — | — | Rueda virtual: gire con el ratón/toque para sintonizar el slice activo. Muestra la frecuencia y el modo. |
| Physical | — | — | `FlexControlPort`, `FlexControlOpen`, `FlexControlAutoDetect` | Muestra el estado de conexión del FlexControl físico y el nombre del puerto. Los botones Detect/Close gestionan el dispositivo. |
| Compact | — | — | `FlexControlCompactMode` | Oculta los botones auxiliares; solo muestra la rueda y la frecuencia. |
| External Spin | — | — | `FlexControlVirtualExternalSpin` | Habilita la sintonización por giro al arrastrar en el panadapter. |
| Reverse | — | — | `FlexControlInvertDir` | Invierte la dirección de sintonización de la rueda. |
| Push | — | — | `FlexControlButtonAction_*` | Acción asignada al toque simple en la rueda. |
| Double-tap | — | — | almacenado por botón | Acción asignada al doble toque en la rueda. |
| Wheel Tightness | 45 | 0–100 | `FlexControlVirtualWheel` (campo de soltura) | Ajusta el arrastre por inercia de la rueda virtual. 0 = apretado (parada rápida), 100 = suelto (arrastre largo). |
| Mouse Sensitivity | 50 | 0–100 | `FlexControlVirtualWheel` (campo de sensibilidad) | Escala el movimiento del puntero capturado. 50 = escala 1.0x. |
| Botones auxiliares (1–5) | — | 5 botones | — | Haga clic para seleccionar; luego configure las acciones de toque simple y doble toque. |
| Aux single-tap combo | — | — | `FlexControlBtn1Action0`–`FlexControlBtn4Action0` | Acción para el toque simple en el botón auxiliar seleccionado. |
| Aux double-tap combo | — | — | `FlexControlBtn1Action1`–`FlexControlBtn4Action1` | Acción para el doble toque en el botón auxiliar seleccionado. |

## Consejos

- Los controles deslizantes **Wheel Tightness** y **Mouse Sensitivity** solo afectan a la rueda virtual (uso con trackpad/ratón), no a un FlexControl físico.
- Los ID de acción predefinidos incluyen: `Tune Slice`, `Band Zoom`, `Segment Zoom`, `RIT`, `XIT`, `Master Volume`, `Headphone Volume`, `AGCT`, `APF`, `Clear RIT`, `Clear XIT`, `Toggle APF`, `Change Active Slice`, `Split Active Slice`, `MOX`, `RF Power`, `CW Speed`, `Step Up`, `Step Down`, `Toggle Tune`, `Toggle Mute`, `Toggle Lock`, `Previous Slice`, `Toggle AGC`, `Slice AF Up`, `Slice AF Down`, `None` y macros CWX 1–12.
- La configuración se guarda automáticamente al ajustar los controles en este diálogo.

## Solución de problemas

- **FlexControl físico no detectado** — Asegúrese de que el dispositivo esté conectado a un puerto USB. Haga clic en **Detect** de nuevo. Si aún no se encuentra, pruebe con un cable o puerto USB diferente.
- **La rueda virtual se siente lenta** — Aumente **Mouse Sensitivity** y disminuya **Wheel Tightness** para una respuesta más rápida.

## Relacionados

- [AetherControl / FlexControl overview](overview.md)
- [Use the virtual wheel to tune the active slice](use-the-virtual-wheel-to-tune-the-active-slice.md)
- [Configure single- and double-tap actions for the PUSH button](configure-single-and-double-tap-actions-for-the-push-button.md)
- [Set up aux buttons with single- and double-tap actions](set-up-aux-buttons-with-single-and-double-tap-actions.md)
- [Adjust wheel tightness (coasting feel)](adjust-wheel-tightness-coasting-feel.md)
- [Adjust mouse sensitivity for the virtual wheel](adjust-mouse-sensitivity-for-the-virtual-wheel.md)
- [Toggle compact mode for a minimal controller UI](toggle-compact-mode-for-a-minimal-controller-ui.md)
- [Toggle Auto Spin for external frequency change animation](toggle-auto-spin-for-external-frequency-change-animation.md)
- [Toggle Reverse to invert tuning direction](toggle-reverse-to-invert-tuning-direction.md)
- [Map push-button and double-tap actions to the wheel](map-push-button-and-double-tap-actions-to-the-wheel.md)
