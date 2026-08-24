# Configurar el controlador de hardware AetherControl / FlexControl

Configure una rueda FlexControl física o la rueda virtual AetherControl para sintonización y acciones de botones. El diálogo le permite gestionar la conexión, el comportamiento de la rueda y las asignaciones de botones para controladores físicos y virtuales.

## Antes de comenzar

- Un FlexControl físico conectado por USB (para uso con hardware)
- Solo para uso virtual, no se necesita hardware

## Pasos

1. Abra **Settings > AetherControl...**
2. Para conectar un FlexControl físico, haga clic en **Detect** en la sección Physical. El diálogo escanea los puertos serie y se conecta automáticamente. Si la detección falla, haga clic en **Close** e intente nuevamente.
3. Para usar la rueda virtual, haga doble clic y arrastre alrededor del indicador Wheel para sintonizar el slice activo. Haga doble clic nuevamente para liberar la captura, o presione Escape.
4. Ajuste el control deslizante **Wheel Tightness** para establecer la resistencia de inercia (0 = firme, 100 = suelto). Valor predeterminado: 45.
5. Ajuste el control deslizante **Mouse Sensitivity** para escalar el movimiento del puntero capturado (0 = menos, 100 = más). Valor predeterminado: 50.
6. Active **Compact** para ocultar los botones auxiliares y mostrar solo la rueda y la lectura de frecuencia.
7. Active **External Spin** para habilitar la sintonización de rueda giratoria iniciada al arrastrar en el panadapter.
8. Active **Reverse** para invertir la dirección de sintonización de la rueda.
9. Configure la acción de pulsación de la rueda: seleccione una acción del cuadro combinado **Push**.
10. Configure la acción de doble toque de la rueda: seleccione una acción del cuadro combinado **Double-tap**.
11. Para configurar los botones auxiliares, haga clic en un botón auxiliar (marcado con puntos). Luego seleccione acciones de los cuadros combinados **Aux single-tap combo** y **Aux double-tap combo** que aparecen.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---------|---------|-------------|-------------|----------|
| Wheel | — | — | — | Rueda virtual: haga doble clic para capturar, luego gire con el mouse/táctil para sintonizar el slice activo. Haga doble clic nuevamente o presione Escape para liberar. Muestra la lectura de frecuencia y modo. |
| Physical | — | — | `FlexControlPort`, `FlexControlOpen`, `FlexControlAutoDetect` | Muestra el estado de conexión y el nombre del puerto del FlexControl físico. Los botones Detect/Close gestionan el dispositivo. Restaura automáticamente el estado de los LED después de un reinicio del dispositivo. |
| Compact | — | — | `FlexControlCompactMode` | Oculta los botones auxiliares; muestra solo la rueda y la frecuencia. |
| External Spin | — | — | `FlexControlVirtualExternalSpin` | Habilita la sintonización de rueda giratoria activada al arrastrar en el panadapter. |
| Reverse | — | — | `FlexControlInvertDir` | Invierte la dirección de sintonización de la rueda. |
| Push | — | — | `FlexControlButtonAction_*` | Acción asignada al toque único de la rueda. |
| Double-tap | — | — | almacenado por botón | Acción asignada al doble toque de la rueda. |
| Wheel Tightness | 45 | 0–100 | `FlexControlVirtualWheel` (campo de resistencia) | Ajusta la resistencia de inercia de la rueda virtual. 0 = firme (detención rápida), 100 = suelto (inercia larga). |
| Mouse Sensitivity | 50 | 0–100 | `FlexControlVirtualWheel` (campo de sensibilidad) | Escala el movimiento del puntero capturado. 50 = escala 1.0x. El anti-temblor limita los deltas de puntero de eventos individuales a 15°. Re-anclaje perezoso: cuando el puntero cruza la zona muerta central, el siguiente movimiento re-ancla sin calcular un delta. |
| Aux buttons (1–5) | — | 5 botones | — | Haga clic para seleccionar; luego configure las acciones de toque único y doble toque. |
| Aux single-tap combo | — | — | `FlexControlBtn1Action0`–`FlexControlBtn4Action0` | Acción para el toque único del botón auxiliar seleccionado. |
| Aux double-tap combo | — | — | `FlexControlBtn1Action1`–`FlexControlBtn4Action1` | Acción para el doble toque del botón auxiliar seleccionado. |

## Consejos

- Los controles deslizantes **Wheel Tightness** y **Mouse Sensitivity** solo afectan la rueda virtual (uso con trackpad/puntero), no un FlexControl físico.
- Los ID de acciones predefinidos incluyen: `Tune Slice`, `Band Zoom`, `Segment Zoom`, `RIT`, `XIT`, `Master Volume`, `Slice Audio Volume`, `Headphone Volume`, `AGCT`, `APF`, `Clear RIT`, `Clear XIT`, `Toggle APF`, `Change Active Slice`, `Split Active Slice`, `MOX`, `RF Power`, `CW Speed`, `Step Up`, `Step Down`, `Toggle Tune`, `Toggle Mute`, `Toggle Lock`, `Previous Slice`, `Toggle AGC`, `Slice AF Up`, `Slice AF Down`, `None` y macros CWX 1–12.
- Los ajustes se guardan automáticamente cuando ajusta los controles en este diálogo.
- La rueda virtual ahora usa doble clic para capturar y liberar, lo que proporciona una experiencia más intuitiva que el modelo anterior de clic para capturar / Escape para liberar. Escape sigue funcionando como una vía secundaria de liberación.
- El diálogo FlexControl restaura automáticamente el estado de los LED en el dispositivo físico cuando recibe un comando de reinicio de hardware, lo que garantiza que los LED auxiliares coincidan con el botón de modo de rueda activo de la aplicación.
- El diálogo ahora usa un área de desplazamiento para su contenido. Cuando el controlador completo excede la altura disponible de la pantalla, el contenido se desplaza verticalmente y el desplazamiento horizontal está deshabilitado. Esto garantiza que el diálogo nunca se abra más alto que el espacio de trabajo de su pantalla, incluso en pantallas cortas o con escala DPI. El tamaño mínimo de ventana no compacta es de 610 px de alto por 430 px de ancho, con el ancho mínimo coincidiendo con el ancho intrínseco del contenido.
- La conexión del FlexControl físico ahora se recupera automáticamente de conexiones de puerto serie interrumpidas. Si el dispositivo se desconecta y se vuelve a conectar (o una re-enumeración USB asigna un puerto COM diferente), el controlador vuelve a detectar el puerto y se reconecta automáticamente, con intervalos de reintento que aumentan de 2 segundos hasta un máximo de 30 segundos.

## Solución de problemas

- **FlexControl físico no detectado** — Asegúrese de que el dispositivo esté conectado a un puerto USB. Haga clic en **Detect** nuevamente. Si aún no se encuentra, pruebe con otro cable o puerto USB.
- **La conexión del FlexControl físico se cae y no se recupera** — El controlador ahora maneja esto automáticamente. Si el dispositivo se desconecta, reintenta la reconexión cada 2 segundos inicialmente, aumentando hasta 30 segundos para fallas persistentes. Vuelva a conectar el dispositivo; debería reconectarse automáticamente.
- **La sintonización de la rueda virtual se siente lenta** — Aumente **Mouse Sensitivity** y disminuya **Wheel Tightness** para una respuesta más rápida.
- **Los LED auxiliares en el FlexControl físico no coinciden** — Esto ahora se maneja automáticamente. El diálogo restaura el estado de los LED después de los reinicios del dispositivo, corrigiendo cualquier discrepancia que pueda ocurrir durante las secuencias de encendido.
- **El diálogo aparece recortado o demasiado alto** — El diálogo limita automáticamente su altura para ajustarse al espacio de trabajo de su pantalla y agrega una barra de desplazamiento vertical si el contenido es más alto que el espacio disponible. Redimensione la ventana verticalmente si prefiere el desplazamiento.

## Relacionados

- [Descripción general de AetherControl / FlexControl](overview.md)
- [Usar la rueda virtual para sintonizar el slice activo](use-the-virtual-wheel-to-tune-the-active-slice.md)
- [Configurar acciones de toque único y doble toque para el botón PUSH](configure-single-and-double-tap-actions-for-the-push-button.md)
- [Configurar botones auxiliares con acciones de toque único y doble toque](set-up-aux-buttons-with-single-and-double-tap-actions.md)
- [Ajustar la resistencia de la rueda (sensación de inercia)](adjust-wheel-tightness-coasting-feel.md)
- [Ajustar la sensibilidad del mouse para la rueda virtual](adjust-mouse-sensitivity-for-the-virtual-wheel.md)
- [Activar el modo compacto para una interfaz de controlador minimalista](toggle-compact-mode-for-a-minimal-controller-ui.md)
- [Activar Auto Spin para la animación de cambio de frecuencia externa](toggle-auto-spin-for-external-frequency-change-animation.md)
- [Activar Reverse para invertir la dirección de sintonización](toggle-reverse-to-invert-tuning-direction.md)
- [Asignar acciones de botón de pulsación y doble toque a la rueda](map-push-button-and-double-tap-actions-to-the-wheel.md)
