# Configurar el controlador hardware AetherControl / FlexControl

Configure un FlexControl físico o la rueda virtual AetherControl para sintonización y acciones de botones. El diálogo le permite gestionar la conexión, el comportamiento de la rueda y las asignaciones de botones tanto para controladores físicos como virtuales.

## Antes de empezar

- Un FlexControl físico conectado por USB (para uso con hardware)
- Para uso solo virtual, no se necesita hardware

## Pasos

1. Abra **Settings > AetherControl...**
2. Para conectar un FlexControl físico, haga clic en **Detect** en la sección Physical. El diálogo escanea los puertos serie y se conecta automáticamente. Si la detección falla, haga clic en **Close** e intente de nuevo.
3. Para usar la rueda virtual, haga doble clic y arrastre alrededor del indicador Wheel para sintonizar el slice activo. Vuelva a hacer doble clic para liberar la captura, o presione Escape.
4. Ajuste el deslizador **Wheel Tightness** para configurar el arrastre por inercia (0 = ajustado, 100 = suelto). Valor predeterminado: 45.
5. Ajuste el deslizador **Mouse Sensitivity** para escalar el movimiento del puntero capturado (0 = menos, 100 = más). Valor predeterminado: 50.
6. Active **Compact** para ocultar los botones auxiliares y mostrar solo la rueda y la lectura de frecuencia.
7. Active **External Spin** para habilitar la sintonización por giro iniciada arrastrando el panadapter.
8. Active **Reverse** para invertir la dirección de sintonización de la rueda.
9. Configure la acción de pulsación de la rueda: seleccione una acción del cuadro combinado **Push**.
10. Configure la acción de doble toque de la rueda: seleccione una acción del cuadro combinado **Double-tap**.
11. Para configurar los botones auxiliares, haga clic en un botón aux (marcado con puntos). Luego seleccione acciones de los cuadros combinados **Aux single-tap combo** y **Aux double-tap combo** que aparecen.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de ajuste | Comportamiento |
|---------|---------------------|--------------|-----------------|----------------|
| Wheel | — | — | — | Rueda virtual: haga doble clic para capturar, luego gire con el ratón/táctil para sintonizar el slice activo. Vuelva a hacer doble clic o presione Escape para liberar. Muestra frecuencia y modo. |
| Physical | — | — | `FlexControlPort`, `FlexControlOpen`, `FlexControlAutoDetect` | Muestra el estado de conexión del FlexControl físico y el nombre del puerto. Los botones Detect/Close gestionan el dispositivo. Restaura automáticamente el estado de los LED después de un reinicio del dispositivo. |
| Compact | — | — | `FlexControlCompactMode` | Oculta los botones auxiliares; muestra solo la rueda y la frecuencia. |
| External Spin | — | — | `FlexControlVirtualExternalSpin` | Habilita la sintonización por giro iniciada arrastrando el panadapter. |
| Reverse | — | — | `FlexControlInvertDir` | Invierte la dirección de sintonización de la rueda. |
| Push | — | — | `FlexControlButtonAction_*` | Acción asignada al pulsar la rueda una vez. |
| Double-tap | — | — | almacenado por botón | Acción asignada al pulsar la rueda dos veces. |
| Wheel Tightness | 45 | 0–100 | `FlexControlVirtualWheel` (campo de soltura) | Ajusta el arrastre por inercia de la rueda virtual. 0 = ajustado (parada rápida), 100 = suelto (inercia larga). |
| Mouse Sensitivity | 50 | 0–100 | `FlexControlVirtualWheel` (campo de sensibilidad) | Escala el movimiento del puntero capturado. 50 = escala 1.0x. El antirrebote limita los deltas de puntero de eventos individuales a 15°. Reanclaje diferido: cuando el puntero cruza la zona muerta central, el siguiente movimiento reancla sin calcular un delta. |
| Botones aux (1–5) | — | 5 botones | — | Haga clic para seleccionar; luego configure acciones de uno y dos toques. |
| Aux single-tap combo | — | — | `FlexControlBtn1Action0`–`FlexControlBtn4Action0` | Acción para un solo toque en el botón aux seleccionado. |
| Aux double-tap combo | — | — | `FlexControlBtn1Action1`–`FlexControlBtn4Action1` | Acción para dos toques en el botón aux seleccionado. |

## Consejos

- Los deslizadores **Wheel Tightness** y **Mouse Sensitivity** solo afectan a la rueda virtual (uso con trackpad/ratón), no a un FlexControl físico.
- Los IDs de acción predefinidos incluyen: `Tune Slice`, `Band Zoom`, `Segment Zoom`, `RIT`, `XIT`, `Master Volume`, `Slice Audio Volume`, `Headphone Volume`, `AGCT`, `APF`, `Clear RIT`, `Clear XIT`, `Toggle APF`, `Change Active Slice`, `Split Active Slice`, `MOX`, `RF Power`, `CW Speed`, `Step Up`, `Step Down`, `Toggle Tune`, `Toggle Mute`, `Toggle Lock`, `Previous Slice`, `Toggle AGC`, `Slice AF Up`, `Slice AF Down`, `None` y las macros CWX 1–12.
- Los ajustes se guardan automáticamente al ajustar los controles en este diálogo.
- La rueda virtual ahora usa doble clic para capturar y liberar, proporcionando una experiencia más intuitiva que el modelo anterior de clic para capturar / Escape para liberar. Escape sigue funcionando como ruta de liberación secundaria.
- El diálogo FlexControl restaura automáticamente el estado de los LED en el dispositivo físico cuando recibe un comando de reinicio de hardware, asegurando que los LED auxiliares coincidan con el modo de botón de rueda activo de la aplicación.

## Solución de problemas

- **FlexControl físico no detectado** — Asegúrese de que el dispositivo esté conectado a un puerto USB. Haga clic en **Detect** de nuevo. Si aún no se encuentra, pruebe con un cable o puerto USB diferente.
- **La sintonización de la rueda virtual se siente lenta** — Aumente **Mouse Sensitivity** y disminuya **Wheel Tightness** para una respuesta más rápida.
- **Los LED auxiliares del FlexControl físico no coinciden** — Esto ahora se maneja automáticamente. El diálogo restaura el estado de los LED después de los reinicios del dispositivo, corrigiendo cualquier desajuste que pudiera ocurrir durante las secuencias de encendido.

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
