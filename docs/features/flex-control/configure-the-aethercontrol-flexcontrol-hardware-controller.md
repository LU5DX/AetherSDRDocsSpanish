# Configure el controlador de hardware AetherControl / FlexControl

Configure un FlexControl físico o la rueda virtual AetherControl para sintonización y acciones de botones. El diálogo permite gestionar la conexión, el comportamiento de la rueda y las asignaciones de botones tanto para controladores físicos como virtuales.

## Antes de comenzar

- Un FlexControl físico conectado por USB (para uso con hardware)
- Para uso solo virtual, no se necesita hardware

## Pasos

1. Abra **Settings > AetherControl...**
2. Para conectar un FlexControl físico, haga clic en **Detect** en la sección Physical. El diálogo escanea los puertos serie y se conecta automáticamente. Si la detección falla, haga clic en **Close** e intente nuevamente.
3. Para usar la rueda virtual, haga doble clic y arrastre alrededor del indicador Wheel para sintonizar la slice activa. Vuelva a hacer doble clic para liberar la captura, o presione Escape.
4. Ajuste el deslizador **Wheel Tightness** para configurar la fricción de deslizamiento (0 = ajustado, 100 = suelto). Valor predeterminado: 45.
5. Ajuste el deslizador **Mouse Sensitivity** para escalar el movimiento del puntero capturado (0 = menos, 100 = más). Valor predeterminado: 50.
6. Active **Compact** para ocultar los botones auxiliares y mostrar solo la rueda y la lectura de frecuencia.
7. Active **External Spin** para habilitar la sintonización por giro iniciada al arrastrar en el panadapter.
8. Active **Reverse** para invertir la dirección de sintonización de la rueda.
9. Configure la acción de pulsación de la rueda: seleccione una acción del cuadro combinado **Push**.
10. Configure la acción de doble toque de la rueda: seleccione una acción del cuadro combinado **Double-tap**.
11. Para configurar los botones auxiliares, haga clic en un botón aux (marcado con puntos). Luego seleccione acciones de los cuadros combinados **Aux single-tap combo** y **Aux double-tap combo** que aparecen.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---------|---------|-------------|-------------|----------|
| Wheel | — | — | — | Rueda virtual: haga doble clic para capturar, luego gire con el ratón/táctil para sintonizar la slice activa. Vuelva a hacer doble clic o presione Escape para liberar. Muestra la lectura de frecuencia y modo. |
| Physical | — | — | `FlexControlPort`, `FlexControlOpen`, `FlexControlAutoDetect` | Muestra el estado de conexión del FlexControl físico y el nombre del puerto. Los botones Detect/Close gestionan el dispositivo. Restaura automáticamente el estado del LED después de un reinicio del dispositivo. |
| Compact | — | — | `FlexControlCompactMode` | Oculta los botones auxiliares; muestra solo la rueda y la frecuencia. |
| External Spin | — | — | `FlexControlVirtualExternalSpin` | Habilita la sintonización por giro iniciada al arrastrar en el panadapter. |
| Reverse | — | — | `FlexControlInvertDir` | Invierte la dirección de sintonización de la rueda. |
| Push | — | — | `FlexControlButtonAction_*` | Acción asignada a la pulsación simple de la rueda. |
| Double-tap | — | — | almacenado por botón | Acción asignada al doble toque de la rueda. |
| Wheel Tightness | 45 | 0–100 | `FlexControlVirtualWheel` (campo looseness) | Ajusta la fricción de deslizamiento de la rueda virtual. 0 = ajustado (parada rápida), 100 = suelto (deslizamiento largo). |
| Mouse Sensitivity | 50 | 0–100 | `FlexControlVirtualWheel` (campo sensitivity) | Escala el movimiento del puntero capturado. 50 = escala 1.0x. El anti-temblor limita los deltas del puntero de un solo evento a 15°. Reanclaje diferido: cuando el puntero cruza la zona muerta central, el siguiente movimiento se reancla sin calcular un delta. |
| Botones aux (1–5) | — | 5 botones | — | Haga clic para seleccionar; luego configure las acciones de toque simple y doble toque. |
| Aux single-tap combo | — | — | `FlexControlBtn1Action0`–`FlexControlBtn4Action0` | Acción para la pulsación simple del botón aux seleccionado. |
| Aux double-tap combo | — | — | `FlexControlBtn1Action1`–`FlexControlBtn4Action1` | Acción para el doble toque del botón aux seleccionado. |

## Consejos

- Los deslizadores **Wheel Tightness** y **Mouse Sensitivity** solo afectan a la rueda virtual (uso con trackpad/puntero), no a un FlexControl físico.
- Los ID de acción predefinidos incluyen: `Tune Slice`, `Band Zoom`, `Segment Zoom`, `RIT`, `XIT`, `Master Volume`, `Slice Audio Volume`, `Headphone Volume`, `AGCT`, `APF`, `Clear RIT`, `Clear XIT`, `Toggle APF`, `Change Active Slice`, `Split Active Slice`, `MOX`, `RF Power`, `CW Speed`, `Step Up`, `Step Down`, `Toggle Tune`, `Toggle Mute`, `Toggle Lock`, `Previous Slice`, `Toggle AGC`, `Slice AF Up`, `Slice AF Down`, `None`, y macros CWX 1–12.
- La configuración se guarda automáticamente al ajustar los controles en este diálogo.
- La rueda virtual ahora utiliza doble clic para capturar y liberar, proporcionando una experiencia más intuitiva que el modelo anterior de clic para capturar / Escape para liberar. Escape sigue funcionando como ruta secundaria de liberación.
- El diálogo FlexControl restaura automáticamente el estado del LED en el dispositivo físico cuando recibe un comando de reinicio de hardware, asegurando que los LED auxiliares coincidan con el botón de modo de rueda activo de la aplicación.
- El diálogo ahora usa un área de desplazamiento para su contenido. Cuando el controlador completo excede la altura disponible de la pantalla, el contenido se desplaza verticalmente y el desplazamiento horizontal está desactivado. Esto asegura que el diálogo nunca se abra más alto que el espacio de trabajo de su pantalla, incluso en pantallas de baja altura o con escalado DPI. El tamaño mínimo de la ventana no compacta es de 610 píxeles de alto por 430 píxeles de ancho, y el ancho mínimo coincide con el ancho intrínseco del contenido.

## Solución de problemas

- **FlexControl físico no detectado** — Asegúrese de que el dispositivo esté conectado a un puerto USB. Haga clic en **Detect** nuevamente. Si aún no se encuentra, pruebe con un cable o puerto USB diferente.
- **La sintonización de la rueda virtual se siente lenta** — Aumente **Mouse Sensitivity** y disminuya **Wheel Tightness** para una respuesta más rápida.
- **Los LED auxiliares del FlexControl físico no coinciden** — Esto ahora se maneja automáticamente. El diálogo restaura el estado del LED después de los reinicios del dispositivo, corrigiendo cualquier discrepancia que pudiera ocurrir durante las secuencias de encendido.
- **El diálogo aparece recortado o demasiado alto** — El diálogo limita automáticamente su altura para ajustarse al espacio de trabajo de su pantalla y agrega una barra de desplazamiento vertical si el contenido es más alto que el espacio disponible. Redimensione la ventana verticalmente si prefiere el desplazamiento.

## Relacionado

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
