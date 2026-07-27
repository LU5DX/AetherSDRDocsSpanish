# Configurar botones auxiliares con acciones de pulsación simple y doble

Configure los cinco botones auxiliares del diálogo AetherControl / FlexControl para que cada botón pueda activar una acción diferente con una pulsación simple o con una pulsación doble.

## Antes de comenzar

- Abra el diálogo AetherControl: `Settings > AetherControl...`
- Familiarícese con la [descripción general](overview.md) del controlador

## Pasos

1. Haga clic en uno de los cinco botones auxiliares numerados para seleccionarlo. El botón seleccionado se resalta en verde.
2. En el cuadro combinado de pulsación simple debajo de los botones auxiliares, seleccione una acción para una pulsación simple.
3. En el cuadro combinado de pulsación doble debajo de los botones auxiliares, seleccione una acción para una pulsación doble.
4. Repita para cada botón auxiliar que desee configurar.

## Qué hace cada control

| Control | Descripción | Claves de configuración |
|---|---|---|
| Wheel | Rueda virtual de FlexControl: gírela con el ratón o el panel táctil para sintonizar el slice activo. Muestra la frecuencia y el modo. Haga doble clic para capturar la sintonización circular; haga doble clic nuevamente para liberarla. Presione Escape como vía de liberación secundaria. | None |
| Physical | Muestra el estado de conexión del FlexControl físico y el nombre del puerto. Botones Detect/Close para gestionar el dispositivo físico. | None |
| Compact | Alterna el modo compacto: oculta los botones auxiliares y muestra solo la rueda y la frecuencia para una interfaz mínima. El área de contenido se desplaza si la altura del diálogo supera el espacio de trabajo disponible en la pantalla. | None |
| External Spin | Habilita la sintonización con rueda externa: arrastrar sobre el panadapter activa gestos de sintonización con rueda. | None |
| Reverse | Invierte la dirección de sintonización de la rueda. | None |
| Push (action) | Asigna una acción al presionar la rueda (pulsación simple). Las opciones incluyen ciclo de modo, zoom por paso, restablecer zoom, banda arriba/abajo y más. | `FlexControlButtonAction_*` |
| Double-tap (action) | Asigna una acción a la pulsación doble de la rueda. | None |
| Wheel Tightness | Ajusta el arrastre de la rueda virtual; 0 = ajustada (parada rápida), 100 = suelta (arrastre largo). Principalmente para paneles táctiles; no afecta al FlexControl físico. Se almacena como parte de un objeto JSON anidado bajo `FlexControlVirtualWheel`. | `FlexControlVirtualWheel` (JSON anidado, campo looseness) |
| Mouse Sensitivity | Ajusta cuánto movimiento capturado del ratón o panel táctil gira la rueda virtual. El punto medio (50) produce una escala de 1.0x. Principalmente para paneles táctiles; no afecta al FlexControl físico. La eliminación de vibraciones limita los deltas de un solo evento del puntero a 15° (π/12). Reanclaje diferido: cuando el puntero cruza la zona muerta central, se suelta el anclaje; el siguiente movimiento reancla sin calcular un delta. | `FlexControlVirtualWheel` (JSON anidado, campo sensitivity) |
| Aux buttons (1–5) | Seleccione un botón auxiliar para configurar. El botón activo se muestra con un punto verde. | None |
| Aux single-tap combo | Asigna una acción a una pulsación simple del botón auxiliar seleccionado. | `FlexControlBtn1Action0` – `FlexControlBtn4Action0` |
| Aux double-tap combo | Asigna una acción a una pulsación doble del botón auxiliar seleccionado. | `FlexControlBtn1Action1` – `FlexControlBtn4Action1` |

Las acciones disponibles son:

Tune Slice, Band Zoom, Segment Zoom, RIT, XIT, Master Volume, **Slice Audio Volume**, Headphone Volume, AGCT, APF, Clear RIT, Clear XIT, Toggle APF, Change Active Slice, Split Active Slice, MOX, RF Power, CW Speed, CWX Macro 1–12, Step Up, Step Down, Toggle Tune, Toggle Mute, Toggle Lock, Previous Slice, Toggle AGC, Slice AF Up, Slice AF Down, None.

## Consejos

- Una pulsación doble debe completarse en menos de 230 ms desde la primera pulsación. Si pulsa demasiado lentamente, la acción se dispara como dos pulsaciones simples.
- Las acciones que son controles continuos (Tune Slice, Master Volume, etc.) enganchan el botón auxiliar en un modo de sintonización. Las acciones de un solo disparo (Step Up, Toggle MOX, macros) se ejecutan inmediatamente y no se enganchan.
- La rueda virtual ahora usa doble clic para capturar y liberar el modo de sintonización circular. Un solo clic no cambia el estado de captura. Esto reemplaza la asimetría anterior donde solo Escape podía liberar la captura.
- Cuando un dispositivo FlexControl físico envía un comando de inicio/restablecimiento (por ejemplo, `F0304;`), el diálogo reemite automáticamente el estado de los LED para garantizar que el hardware coincida con el modo de rueda activo de la aplicación. Esto resuelve condiciones de competencia donde el restablecimiento de encendido del dispositivo podría borrar el estado del LED después de que la aplicación ya lo hubiera establecido.
- Slice Audio Volume le permite ajustar el volumen de audio del slice activo de forma independiente usando la rueda, sin afectar el volumen maestro ni otros slices.
- El diálogo ahora usa un área de desplazamiento para el modo no compacto. Si la altura de su pantalla es limitada o utiliza una escala DPI alta, el contenido se desplaza verticalmente para que el controlador completo permanezca accesible. La ventana no puede redimensionarse a una altura mayor que el espacio de trabajo de pantalla disponible.

## Relacionado

- [Configurar acciones de pulsación simple y doble para el botón PUSH](configure-single-and-double-tap-actions-for-the-push-button.md)
- [Asignar acciones de pulsación de botón y doble pulsación a la rueda](map-push-button-and-double-tap-actions-to-the-wheel.md)
- [Usar la rueda virtual para sintonizar el slice activo](use-the-virtual-wheel-to-tune-the-active-slice.md)
